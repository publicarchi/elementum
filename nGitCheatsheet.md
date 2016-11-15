# Git cheatsheet

## revenir en arrière

`git reset --soft HEAD^`

Annuler le commit mais laisser tout le reste en place

`git reset HEAD^`

Annuler le commit et tout ce qui a été indexé, en conservant les fichiers intacts

`git reset --hard HEAD^`

Tout annuler en jettant tous les changements non commités et en ramenant tout à l’état précédent (attention la commande peut être dangereuse)


## Annulations et problèmes

`git reset --hard`

Abandonne tout depuis le dernier commit ; cela peut être dangereux.

La commande est utile également pour abandonner un merge qui génère un conflit.

`git reset --hard ORIG_HEAD` ou `git reset --hard origin/master`

Annule le dernier merge réussi et n’importe quel changement intervenu après. Utile pour laisser tomber un merge qui vient d’être fait.

En cas de conflits (merge sans succès), utilisez plutôt `git reset --hard` (ci-dessus)

`git reset --soft HEAD^`

Lorsque l’on a oublié quelque chose lors du dernier commit. Annule le dernier commit mais conserve les changements dans la zone d’indexation pour les éditer.

`git commit --amend`

Relance le dernier commit, y compris les changements indexés entre temps. Permet également d’éditer le message du dernier commit.


## Configurations

`git clone <repo>`
clone le répertoire spécifié par <repo>

`git config -e [--global]` editer le fichier `.git/config` [ou `~/.gitconfig`] dans l’éditeur

`git config --global user.name 'John Doe'`

`git config --global user.email johndoe@example.com`

Configurer les nom d’utilisateur et le courriel pour les messages de commit

`git config branch.autosetupmerge true`

Indique à git-branch et git-checkout de configurer les nouvelles branches de manière à ce que git-pull(1) merge de façon appropriée la branche distante. Cette configuration est recommandée, sans elle il faut ajouter la commadne "--track" aux branches ou merger manuellement les branches distantes avec "fetch" puis "merge".

`git config core.autocrlf true`

Indique de convertir les nouvelles lignes au standard du système lors du check out, et vers LF lors du commit

`git config --list` voir toutes les options

`git config apply.whitespace nowarn` ignorer les espaces

Ajouter "--global" après "git config" à l’une de ces commandes pour les appliquer à tous les répertoires git (écrit dans `~/.gitconfig`).


Ajouter la colorisation au fichier `~/.gitconfig` :

```
[color]
  ui = auto
[color "branch"]
  current = yellow reverse
  local = yellow
  remote = green
[color "diff"]
  meta = yellow bold
  frag = magenta bold
  old = red bold
  new = green bold
[color "status"]
  added = yellow
  changed = green
  untracked = cyan
```

Mettre en évidence les espaces blanc dans les diffs :

```
[color]
  ui = true
[color "diff"]
  whitespace = red reverse
[core]
  whitespace=fix,-indent-with-non-tab,trailing-space,cr-at-eol
```

Ajouter des alias au fichier `~/.gitconfig` :

```
[alias]
  st = status
  ci = commit
  br = branch
  co = checkout
  df = diff
  dc = diff --cached
  lg = log -p
  lol = log --graph --decorate --pretty=oneline --abbrev-commit
  lola = log --graph --decorate --pretty=oneline --abbrev-commit --all
  ls = ls-files

  # Show files ignored by git:
  ign = ls-files -o -i --exclude-standard
```

## Merge sur autre branche

`git fetch . master:gh-pages`

Avec git fetch . master:gh-pages, on indique donc d’envoyer le contenu de `./master` (la branche locale master) vers `./gh-pages` (la branche locale gh-pages).

## Sources

http://cheat.errtheblog.com/s/git
