---
tags: authentification, sites statiques
---

# Authentification légère

La mise en place d’une authentification est souvent problématique pour les sites statiques. GitHub Pages ne supporte pas de logique serveur, ce qui impose de gérer l’accès contrôlé autrement.

Une architecture légère peut consister à proposer une redirection vers un fournisseur d’authentification déléguée (OAuth via GitHub, Google, etc.) qui retourne un token, une fonction edge pour vérifier l’identité et valider la liste d’accès. Un token de session côté client pour débloquer le contenu dans le site statique.



Redirection OAuth dans svelte

```js
// src/lib/auth.js
const CLIENT_ID = 'your-client_id_github_ou_google';
const REDIRECT_URI = 'https://worker.your-compte.workers.dev/callback';

export function login() {
  const url = `https://github.com/login/oauth/authorize?client_id=${CLIENT_ID}&redirect_uri=${REDIRECT_URI}&scope=user:email`;
  window.location.href = url;
}
```

Une fonction edge avec Cloudflare Workers, ou Netlify Edge qui reçoit le callback OAuth, échange le code contre un token, récupère l’identité et vérifie la liste d’accès

```js
// worker.js (Cloudflare Workers)
export default {
  async fetch(request, env) {
    const url = new URL(request.url);

    if (url.pathname === '/callback') {
      const code = url.searchParams.get('code');

      // Échange du code OAuth contre un access token
      const tokenRes = await fetch('https://github.com/login/oauth/access_token', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json', Accept: 'application/json' },
        body: JSON.stringify({ client_id: env.CLIENT_ID, client_secret: env.CLIENT_SECRET, code }),
      });
      const { access_token } = await tokenRes.json();

      // Récupération de l'email de l'utilisateur
      const userRes = await fetch('https://api.github.com/user/emails', {
        headers: { Authorization: `Bearer ${access_token}` },
      });
      const emails = await userRes.json();
      const primaryEmail = emails.find(e => e.primary)?.email;

      // Vérification contre la liste d'accès
      const allowlist = env.ALLOWLIST.split(','); // variable d'environnement
      if (!allowlist.includes(primaryEmail)) {
        return new Response('Accès refusé', { status: 403 });
      }

      // Création d'un JWT signé
      const jwt = await createJWT({ email: primaryEmail }, env.JWT_SECRET);

      // Redirection vers le site avec le token
      return Response.redirect(`https://ton-site.github.io/#token=${jwt}`, 302);
    }
  }
};

```

Liste d’accès

```js
const allowedDomains = ['tonentreprise.com', 'partenaire.fr'];
const domain = primaryEmail.split('@')[1];
const allowed = allowedDomains.includes(domain);
```

Vérification du JWT côté Svelte

```svelte
<!-- src/routes/+layout.svelte -->
<script>
  import { onMount } from 'svelte';
  import { writable } from 'svelte/store';

  export const user = writable(null);

  onMount(async () => {
    // Récupération depuis l'URL hash ou localStorage
    const hash = new URLSearchParams(window.location.hash.slice(1));
    const token = hash.get('token') ?? localStorage.getItem('session_token');

    if (token) {
      const payload = await verifyJWT(token, PUBLIC_KEY);
      if (payload) {
        user.set(payload);
        localStorage.setItem('session_token', token);
        // Nettoie l'URL
        history.replaceState(null, '', window.location.pathname);
      }
    }
  });
</script>
```

Protection des routes

```js
// src/hooks.client.js
import { redirect } from '@sveltejs/kit';
import { get } from 'svelte/store';
import { user } from '$lib/stores/auth';

export async function handle({ event, resolve }) {
  const protectedPaths = ['/dashboard', '/contenu'];
  const isProtected = protectedPaths.some(p => event.url.pathname.startsWith(p));

  if (isProtected && !get(user)) {
    throw redirect(302, '/login');
  }

  return resolve(event);
}
```

Configuration Svelte pour GitHub Pages

```js
// svelte.config.js
import adapter from '@sveltejs/adapter-static';

export default {
  kit: {
    adapter: adapter({
      pages: 'build',
      fallback: '404.html', // SPA mode : toutes les routes → index
    }),
    paths: {
      base: process.env.NODE_ENV === 'production' ? '/nom-du-repo' : '',
    },
  },
};
```

Le contenu reste visible dans le Bundle, cette solution n’est donc pas approprié pour des données hautement confidentielles.

---

## Utilisation des équipes GitHub

Lorsque l’on dispose d’une organisation GitHub, on peut l’utiliser comme annuaire.

Voici l'implémentation complète de la solution A — organisation GitHub comme annuaire, PKCE, zéro serveur.

### Structure du projet

```
src/
├── lib/
│   └── auth.js          ← tout le mécanisme OAuth + vérification org
├── routes/
│   ├── +layout.svelte   ← guard global
│   ├── +page.svelte     ← page publique / login
│   ├── callback/
│   │   └── +page.svelte ← réception du token GitHub
│   └── dashboard/
│       └── +page.svelte ← contenu protégé
└── app.html
```

------

### `src/lib/auth.js`

js

```js
const CLIENT_ID  = import.meta.env.VITE_GITHUB_CLIENT_ID;
const ORG        = import.meta.env.VITE_GITHUB_ORG;
const TEAM       = import.meta.env.VITE_GITHUB_TEAM; // optionnel
const ORIGIN     = typeof window !== 'undefined' ? window.location.origin : '';

// ── PKCE ───────────────────

async function generatePKCE() {
  const verifier = crypto.randomUUID() + crypto.randomUUID();
  const digest   = await crypto.subtle.digest(
    'SHA-256',
    new TextEncoder().encode(verifier)
  );
  const challenge = btoa(String.fromCharCode(...new Uint8Array(digest)))
    .replace(/\+/g, '-').replace(/\//g, '_').replace(/=/g, '');
  return { verifier, challenge };
}

// ── Login ──────────────────

export async function login() {
  const { verifier, challenge } = await generatePKCE();
  sessionStorage.setItem('pkce_verifier', verifier);

  const params = new URLSearchParams({
    client_id:             CLIENT_ID,
    redirect_uri:          `${ORIGIN}/callback`,
    scope:                 'read:org user:email',  // read:org pour vérifier l'appartenance
    code_challenge:        challenge,
    code_challenge_method: 'S256',
  });

  window.location.href = `https://github.com/login/oauth/authorize?${params}`;
}

// ── Callback ───────────────

export async function handleCallback() {
  const code     = new URLSearchParams(window.location.search).get('code');
  const verifier = sessionStorage.getItem('pkce_verifier');
  if (!code || !verifier) return { error: 'missing_params' };

  // Échange du code contre un access token (PKCE — pas de secret)
  const tokenRes = await fetch('https://github.com/login/oauth/access_token', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json', Accept: 'application/json' },
    body: JSON.stringify({
      client_id:     CLIENT_ID,
      code,
      redirect_uri:  `${ORIGIN}/callback`,
      code_verifier: verifier,
    }),
  });

  const { access_token, error } = await tokenRes.json();
  if (error || !access_token) return { error: error ?? 'no_token' };

  sessionStorage.removeItem('pkce_verifier');

  // Identité GitHub de l'utilisateur
  const userRes  = await fetch('https://api.github.com/user', {
    headers: { Authorization: `Bearer ${access_token}` },
  });
  const { login: username, name, avatar_url } = await userRes.json();

  // Vérification de l'appartenance à l'org (ou à l'équipe)
  const allowed = TEAM
    ? await checkTeam(access_token, username)
    : await checkOrg(access_token, username);

  if (!allowed) return { error: 'not_in_org', username };

  // Persistance de la session
  const session = { username, name, avatar_url, token: access_token };
  sessionStorage.setItem('session', JSON.stringify(session));
  return { ok: true, session };
}

async function checkOrg(token, username) {
  const res = await fetch(
    `https://api.github.com/orgs/${ORG}/members/${username}`,
    { headers: { Authorization: `Bearer ${token}` } }
  );
  return res.status === 204;
}

async function checkTeam(token, username) {
  const res = await fetch(
    `https://api.github.com/orgs/${ORG}/teams/${TEAM}/memberships/${username}`,
    { headers: { Authorization: `Bearer ${token}` } }
  );
  if (res.status !== 200) return false;
  const { state } = await res.json();
  return state === 'active';
}

// ── Session ────────────────

export function getSession() {
  if (typeof window === 'undefined') return null;
  const raw = sessionStorage.getItem('session');
  return raw ? JSON.parse(raw) : null;
}

export function logout() {
  sessionStorage.removeItem('session');
}
```

### `.env`

```bash
VITE_GITHUB_CLIENT_ID=Ov23liXXXXXXXXXXXXXX
VITE_GITHUB_ORG=mon-organisation

# Optionnel — restreint à une équipe dans l'org :
# VITE_GITHUB_TEAM=mon-equipe
```

### `src/routes/+page.svelte` — page publique

```svelte
<script>
  import { login, getSession } from '$lib/auth';
  import { onMount } from 'svelte';
  import { goto } from '$app/navigation';

  onMount(() => {
    if (getSession()) goto('/dashboard');
  });
</script>

<main>
  <h1>Accès restreint</h1>
  <p>Connectez-vous avec votre compte GitHub membre de l'organisation.</p>
  <button on:click={login}>Se connecter avec GitHub</button>
</main>
```

### `src/routes/callback/+page.svelte`

```svelte
<script>
  import { onMount } from 'svelte';
  import { goto } from '$app/navigation';
  import { handleCallback } from '$lib/auth';

  let message = 'Vérification en cours…';

  onMount(async () => {
    const result = await handleCallback();

    if (result.ok) {
      goto('/dashboard');
      return;
    }

    message = {
      not_in_org:    `@${result.username} n'appartient pas à l'organisation.`,
      missing_params: 'Paramètres manquants. Recommencez la connexion.',
      no_token:       'Impossible d'obtenir un token GitHub.',
    }[result.error] ?? 'Erreur inconnue.';
  });
</script>

<p>{message}</p>
{#if message !== 'Vérification en cours…'}
  <a href="/">Retour</a>
{/if}
```

------

### `src/routes/dashboard/+layout.svelte` — guard

svelte

```svelte
<script>
  import { onMount } from 'svelte';
  import { goto } from '$app/navigation';
  import { getSession, logout } from '$lib/auth';

  let session = null;

  onMount(() => {
    session = getSession();
    if (!session) goto('/');
  });
</script>

{#if session}
  <nav>
    <img src={session.avatar_url} alt={session.username} width="32" height="32" />
    <span>@{session.username}</span>
    <button on:click={() => { logout(); goto('/'); }}>Déconnexion</button>
  </nav>
  <slot />
{/if}
```

------

### `svelte.config.js`

js

```js
import adapter from '@sveltejs/adapter-static';

export default {
  kit: {
    adapter: adapter({
      pages:    'build',
      fallback: '404.html',  // SPA — toutes les routes → gérées côté client
    }),
    paths: {
      base: process.env.NODE_ENV === 'production' ? '/nom-du-repo' : '',
    },
  },
};
```

------

### GitHub Actions

yaml

```yaml
# .github/workflows/deploy.yml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20

      - run: npm ci
      - run: npm run build
        env:
          VITE_GITHUB_CLIENT_ID: ${{ secrets.VITE_GITHUB_CLIENT_ID }}
          VITE_GITHUB_ORG:       ${{ secrets.VITE_GITHUB_ORG }}
          VITE_GITHUB_TEAM:      ${{ secrets.VITE_GITHUB_TEAM }}

      - uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir:  ./build
```

### Configuration OAuth dans GitHub

Dans **Settings → Developer settings → OAuth Apps → New OAuth App** de votre compte ou organisation :

```
Application name : Mon site
Homepage URL     : https://votre-org.github.io/nom-du-repo
Callback URL     : https://votre-org.github.io/nom-du-repo/callback
```

> L'activation de PKCE se fait côté client uniquement — pas de case à cocher dans GitHub, c'est automatique dès que vous envoyez `code_challenge` dans la requête.

### Ce que vous obtenez

L'annuaire est votre organisation GitHub. Pour donner accès à quelqu'un : `Settings → Members → Invite`. Pour révoquer : retirer le membre. Au prochain login, l'appel à `checkOrg` (ou `checkTeam`) retournera 404 et l'accès sera refusé — sans toucher au code ni déclencher un rebuild.

---

## Avec AuthO

Voici l'implémentation complète et autonome — Auth0 + vérification d'une liste d'emails, SvelteKit statique sur GitHub Pages.

------

## Structure du projet

```
src/
├── lib/
│   ├── auth.js            ← PKCE + Auth0 + vérification liste
│   └── allowlist.json     ← la liste de vos étudiants
├── routes/
│   ├── +layout.svelte     ← injecte la session dans toute l'app
│   ├── +page.svelte       ← page publique / bouton login
│   ├── callback/
│   │   └── +page.svelte   ← réception du token
│   └── dashboard/
│       ├── +layout.svelte ← guard : redirige si non connecté
│       └── +page.svelte   ← contenu protégé
svelte.config.js
.env
```

------

## `src/lib/allowlist.json`

```json
{
  "emails": [
    "alice.durand@etu.univ.fr",
    "bob.martin@etu.univ.fr",
    "carol.petit@etu.univ.fr"
  ]
}
```

Vous modifiez ce fichier et committez — GitHub Actions redéploie automatiquement.

------

## `.env`

```bash
VITE_AUTH0_DOMAIN=mon-app.eu.auth0.com
VITE_AUTH0_CLIENT_ID=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

------

## `src/lib/auth.js`

```js
import allowlist from '$lib/allowlist.json';

const DOMAIN       = import.meta.env.VITE_AUTH0_DOMAIN;
const CLIENT_ID    = import.meta.env.VITE_AUTH0_CLIENT_ID;
const REDIRECT_URI = typeof window !== 'undefined'
  ? `${window.location.origin}/callback`
  : '';

// ── PKCE ──────────────────────────────────────────────────────────────────────

async function generatePKCE() {
  const verifier  = crypto.randomUUID() + crypto.randomUUID();
  const digest    = await crypto.subtle.digest('SHA-256', new TextEncoder().encode(verifier));
  const challenge = btoa(String.fromCharCode(...new Uint8Array(digest)))
    .replace(/\+/g, '-').replace(/\//g, '_').replace(/=/g, '');
  return { verifier, challenge };
}

// ── Login ─────────────────────────────────────────────────────────────────────

export async function login() {
  const { verifier, challenge } = await generatePKCE();
  const state = crypto.randomUUID();

  sessionStorage.setItem('pkce_verifier', verifier);
  sessionStorage.setItem('oauth_state',   state);

  const params = new URLSearchParams({
    client_id:             CLIENT_ID,
    redirect_uri:          REDIRECT_URI,
    response_type:         'code',
    scope:                 'openid email profile',
    code_challenge:        challenge,
    code_challenge_method: 'S256',
    state,
    connection:            'windowslive',
  });

  window.location.href = `https://${DOMAIN}/authorize?${params}`;
}

// ── Callback ──────────────────────────────────────────────────────────────────

export async function handleCallback() {
  const params        = new URLSearchParams(window.location.search);
  const code          = params.get('code');
  const returnedState = params.get('state');
  const verifier      = sessionStorage.getItem('pkce_verifier');
  const savedState    = sessionStorage.getItem('oauth_state');

  if (!code || !verifier)           return { error: 'missing_params' };
  if (returnedState !== savedState) return { error: 'invalid_state' };

  sessionStorage.removeItem('pkce_verifier');
  sessionStorage.removeItem('oauth_state');

  const tokenRes = await fetch(`https://${DOMAIN}/oauth/token`, {
    method: 'POST',
    headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
    body: new URLSearchParams({
      client_id:     CLIENT_ID,
      grant_type:    'authorization_code',
      code,
      redirect_uri:  REDIRECT_URI,
      code_verifier: verifier,
    }),
  });

  const tokens = await tokenRes.json();
  if (tokens.error) return { error: tokens.error };

  // Décodage du id_token sans librairie
  const payload = JSON.parse(
    atob(tokens.id_token.split('.')[1].replace(/-/g, '+').replace(/_/g, '/'))
  );

  const email = payload.email?.toLowerCase();
  const name  = payload.name ?? email;

  if (!email) return { error: 'no_email' };

  if (!isAllowed(email)) return { error: 'not_allowed', email };

  const session = { email, name };
  sessionStorage.setItem('session', JSON.stringify(session));
  return { ok: true, session };
}

function isAllowed(email) {
  return allowlist.emails
    .map(e => e.toLowerCase())
    .includes(email);
}

// ── Session ───────────────────────────────────────────────────────────────────

export function getSession() {
  if (typeof window === 'undefined') return null;
  const raw = sessionStorage.getItem('session');
  return raw ? JSON.parse(raw) : null;
}

export function logout() {
  sessionStorage.removeItem('session');
  const params = new URLSearchParams({
    client_id: CLIENT_ID,
    returnTo:  window.location.origin,
  });
  window.location.href = `https://${DOMAIN}/v2/logout?${params}`;
}
```

------

## `src/routes/+layout.svelte`

Injecte la session dans le contexte — accessible depuis toutes les pages via `getContext`.

```svelte
<script>
  import { setContext } from 'svelte';
  import { writable } from 'svelte/store';
  import { getSession } from '$lib/auth';
  import { onMount } from 'svelte';

  const session = writable(null);
  setContext('session', session);

  onMount(() => {
    session.set(getSession());
  });
</script>

<slot />
```

------

## `src/routes/+page.svelte`

```svelte
<script>
  import { getContext, onMount } from 'svelte';
  import { goto } from '$app/navigation';
  import { login } from '$lib/auth';

  const session = getContext('session');

  onMount(() => {
    if ($session) goto('/dashboard');
  });
</script>

<main>
  <h1>Accès cours</h1>
  <p>Connectez-vous avec votre compte universitaire Microsoft.</p>
  <button on:click={login}>Se connecter</button>
</main>
```

------

## `src/routes/callback/+page.svelte`

```svelte
<script>
  import { onMount, getContext } from 'svelte';
  import { goto } from '$app/navigation';
  import { handleCallback } from '$lib/auth';

  const session = getContext('session');

  let message = 'Connexion en cours…';

  const ERRORS = {
    not_allowed:    email => `${email} n'est pas dans la liste d'accès.`,
    invalid_state:  ()    => 'Requête invalide. Recommencez.',
    missing_params: ()    => 'Paramètres manquants.',
    no_email:       ()    => 'Impossible de récupérer votre email.',
  };

  onMount(async () => {
    const result = await handleCallback();

    if (result.ok) {
      session.set(result.session);
      goto('/dashboard');
      return;
    }

    const fn = ERRORS[result.error];
    message = fn ? fn(result.email) : `Erreur : ${result.error}`;
  });
</script>

<p>{message}</p>
{#if message !== 'Connexion en cours…'}
  <a href="/">Retour</a>
{/if}
```

------

## `src/routes/dashboard/+layout.svelte`

```svelte
<script>
  import { getContext, onMount } from 'svelte';
  import { goto } from '$app/navigation';
  import { logout } from '$lib/auth';

  const session = getContext('session');

  onMount(() => {
    if (!$session) goto('/');
  });
</script>

{#if $session}
  <header>
    <span>{$session.name} — {$session.email}</span>
    <button on:click={logout}>Déconnexion</button>
  </header>
  <slot />
{/if}
```

------

## `src/routes/dashboard/+page.svelte`

```svelte
<script>
  import { getContext } from 'svelte';
  const session = getContext('session');
</script>

<h1>Bonjour {$session?.name} !</h1>
<p>Contenu réservé aux étudiants inscrits.</p>
```

------

## `svelte.config.js`

```js
import adapter from '@sveltejs/adapter-static';

export default {
  kit: {
    adapter: adapter({
      pages:    'build',
      fallback: '404.html',
    }),
    paths: {
      base: process.env.NODE_ENV === 'production' ? '/nom-du-repo' : '',
    },
  },
};
```

------

## `.github/workflows/deploy.yml`

```yaml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm ci
      - run: npm run build
        env:
          VITE_AUTH0_DOMAIN:     ${{ secrets.VITE_AUTH0_DOMAIN }}
          VITE_AUTH0_CLIENT_ID:  ${{ secrets.VITE_AUTH0_CLIENT_ID }}
      - uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir:  ./build
```

------

## Ajouter ou retirer un étudiant

Modifier `allowlist.json`, committer sur `main` — le déploiement se déclenche automatiquement. L'historique Git garde la trace de chaque modification.

```json
{
  "emails": [
    "alice.durand@etu.univ.fr",
    "bob.martin@etu.univ.fr",
    "nouvel.etudiant@etu.univ.fr"
  ]
}
```

