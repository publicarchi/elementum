---
since: 2017-07-07
author: emchateau
tags: cms, wordpress
---

# Wordpress alternatives

Le CMS Wordpress est une solution largement plébicitée pour propulser des sites web. Toutefois, le logiciel comme d’autres concurents tels que Drupal ou Typo3 même s’il est facile d’emploi n’est pas dépourvu d’inconvénients. C’est un logiciel en PHP ce qui contraint certains développements. C’est aussi une solution tout en un qui n’offre pas toujours toute la flexibilité attendue pour certaines applications. De nouvelles solutions propriétaires ou libres ont ainsi émergé pour proposer des alternatives à Wordpress. Dans le domaine du libre, deux logiciels semblent aujourd’hui se démarquer, Ghost et Strapi.

## Ghost

Ghost est un CMS comme Wordpress mais qui se focalise sur le cas d’usage des blogs. Ce CMS propose une structure simplifiée pour la gestion de contenus avec une très belle interface d’édition. C’est une solution moderne développée en node.js qui offre un certain gain de performance.

## Strapi

Strapi est une solution de type headless CMS, il s’agit d’une architecture qui sépare la gestion des contenus de la production du site web. Cette solution permet de distinguer plus clairement les domaines fonctionnels (contenus, versus présentation), et offre une très grande flexibilité. Il s’agit d’une solution développée en node.js.

Strapi est une solution adaptée pour la gestion de sites statitiques de type JamStack.

### Points de vigileance

version libre / version payante. L’internationalisation contextuelle ? Type d’utilisateurs et nombre.

### Changement d’éditeur

https://www.npmjs.com/package/strapi-plugin-editor

### Gratuité pour les projets non-profit

https://strapi.io/blog/announcing-free-strapi-enterprise-editions-for-students-open-source-and-non-profits

SvelteKit

- [How to use JWT with SvelteKit and Strapi](https://youtu.be/WgX87HDrAss)
- https://sveltethemes.dev/article/Sveltekit-Mdsvex-Blog
- https://svelteland.github.io/svelte-kit-blog-demo/create-your-blog/

## Comparatif

|                       | Strapi                              | Strapi Bronze                       | Ghost                                   | Netlify CMS                                     |
| --------------------- | ----------------------------------- | ----------------------------------- | --------------------------------------- | ----------------------------------------------- |
| Locales               | Unlimited                           | Unlimited                           |                                         |                                                 |
| Rôles                 | 3 rôles par défaut                  | Unlimited custom roles              |                                         |                                                 |
| Types de contenus     | Personnalisables                    | Personnalisables                    | Orienté blog                            |                                                 |
|                       |                                     |                                     |                                         |                                                 |
| Thèmes                | Non                                 | Non                                 | Oui                                     | Non                                             |
| API calls             | Unlimited                           | Unlimited                           |                                         |                                                 |
| GraphQL API           | -                                   | -                                   |                                         |                                                 |
| REST API              | Oui                                 | Oui                                 | Oui                                     |                                                 |
| Architecture          | Headless CMS                        | Headless CMS                        | CMS                                     |                                                 |
| Selfhosting           | Oui                                 | Oui                                 | Oui                                     |                                                 |
| Cloud                 | Prochainement, sinon externe Render | Prochainement, sinon externe Render | 9 à 25$ ou 50$/mois                     | Starter gratuit (1 membre), 19$/mois par membre |
| Licence               | MIT Expat License                   | Plan non-profit                     | Libre                                   |                                                 |
| Dépendances           | koa.js (server)                     | koa.js (server)                     | ember.js, Bookshelf.js (client de bdd), |                                                 |
| Bdd                   |                                     |                                     | SQLite3, etc.                           |                                                 |
| Templating            | Au choix                            | Au choix                            | Handlebars.js                           |                                                 |
| Webhooks              | Oui                                 | Oui                                 | Oui                                     | Oui                                             |
| Newsletter            | ?                                   | ?                                   | Oui                                     |                                                 |
| Migration des données | Manuelle                            | Manuelle                            | Oui                                     |                                                 |

## JAMstack

Depuis 2005, plusieurs solutions basées sur la génération de sites statiques à partir de sources en markdown ont connu un véritable succès. Il s’agit d’une nouvelle manière de construire des sites web qui offre de meilleures performances et plus de sécurité. C’est une solution peu couûteuse et simple à mettre en œuvre qui offre une meilleure expérience pour les développeurs en séparant la gestion des contenus du développement du site.

La généralisation des sites web statiques a profondément changé l’architecture des sites web en promouvant des modèles plus distribués. Une architecture parfois qualifiée de JAMstack comme elle est basée sur JavaScript, les APIs et Markdown. Dans le cadre du développement web avec la généralisation des framework JavaScript, les développeurs sont de plus en plus amenés à compiler du code. Depuis quelques années, des acteurs majeurs du web ont dévelopé des modèles basés sur l’utilisation d’API.

- Sites statiques (premier web client-server)
- Sites dynamiques (programme côté serveur)
- LAMP stack (programme côté serveur, base de données)
- CDN et gestion des caches

cf. *The New Front-end Stack. Javascript, APIs and Markup*. Réalisé par Mathias Biilmann. SmashingConf San Francisco 2016, 2016.

![Jamstack](https://d33wubrfki0l68.cloudfront.net/b7d16f7f3654fb8572360301e60d76df254a323e/385ec/img/svg/architecture.svg)



Découpler le front-end et le back-end où le back-end est limité à l’API et site web est construit avec des des technologies modernes.

- découpler construction et hébergement
- découpler le front-end et le back-end
- API plutôt que db
- Pre-baked Markup amélioré avec JS

Utilisation d’outils modernes : Git, Frameworks, APIs, CDN, outils de déploiement

Bénéfices : 

- Simplicité
- Fiabilité
- Sécurité
- Flexibilité
- Possibilité de se connecter à des flux de données

Appelation site statique en réalité trompeuse car les solutions mises en œuvres sont en réalité très dynmaiques.

Exemple d’application pour CIÉCO : connexion avec les RSN, utilisation des données de bibliographie, etc.

### Mise en œuvre

Nombreuses solutions possibles. Souvent basées sur JavaScript et Markdown.

>###  Entire Project on a CDN      
>
>Because Jamstack projects don’t rely on server-side code, they  can be distributed instead of living on a single server. Serving  directly from a CDN unlocks speeds and performance that can’t be beat.  The more of your app you can push to the edge, the better the user  experience.      
>
>### Modern Build Tools      
>
>Take advantage of the world of modern build tools. It can be a  jungle to get oriented in and it’s a fast moving space, but you’ll want  to be able to use tomorrow’s web standards today without waiting for  tomorrow’s browsers. And that currently means Babel, PostCSS, Webpack,  and friends.
>
>### Automated Builds      
>
>Because Jamstack markup is prebuilt, content changes won’t go  live until you run another build. Automating this process will save you  lots of frustration. You can do this yourself with webhooks, or use a  publishing platform that includes the service automatically.
>
>### Atomic Deploys      
>
>As Jamstack projects grow really large, new changes might  require re-deploying hundreds of files. Uploading these one at a time  can cause inconsistent state while the process completes. You can avoid  this with a system that lets you do “atomic deploys,” where no changes  go live until all changed files have been uploaded.
>
>### Instant Cache Invalidation      
>
>When the build-to-deploy cycle becomes a regular occurrence, you need to know that when a deploy goes live, it really goes live.  Eliminate any doubt by making sure your CDN can handle instant cache  purges.
>
>### Everything Lives in Git      
>
>With a Jamstack project, anyone should be able to do a git  clone, install any needed dependencies with a standard procedure (like  npm install), and be ready to run the full project locally. No databases to clone, no complex installs. This reduces contributor friction, and  also simplifies staging and testing workflows.
>
>(https://jamstack.org/best-practices/)

Les approches le plus souvent utilisées reposent sur JavaScript. Toutefois, rien n’interdit de penser développer des solutions basées sur XML pour prendre en charge des contenus plus structurés. L’outillage XML permet en effet de produire des transformation de manière extrèmement efficace. Pour travailler sur la mise à disposition des contenus, il pourrait également être intéressant de penser les choses en termes d’hydratation.

- « Jamstack ». s. d. Jamstack.org. Consulté le 3 octobre 2021. https://jamstack.org/.
- « Ghost on the JAMstack ». 2019. Ghost. 9 janvier 2019. https://ghost.org/changelog/jamstack/.

![image](https://d38xoolefqxt5u.cloudfront.net/original/1X/d7b3c8eb01132dda8f85b28e7123e72fb0d5e9da.png)

Solutions

- [Directus](https://directus.io/open-source/) GNU
- [Tina](https://tina.io/) Apache (pour React, Next.js)
- [Cockpit](https://getcockpit.com/) MIT (modèles de contenus flexible)
- [Webiny](https://www.webiny.com/) MIT (flexible)

https://docs.feathersjs.com/

## Reprise des données

Importation

- « Migrating a WordPress Blog to Strapi ». 2020. *Hash*. 9 février. https://hashinteractive.com/blog/migrating-a-wordpress-blog-to-strapi/.

Exportation

- https://www.npmjs.com/package/strapi-plugin-import-export-content
- https://github.com/EdisonPeM/strapi-plugin-import-export-content
- https://strapi.io/blog/how-to-create-an-import-content-plugin-part-1-4

## Références

- Biseul, Xavier. 2020. « Comparatif : ces CMS headless qui pourraient tuer WordPress et Drupal ». *Le Journal du Net*, 7 décembre 2020. https://www.journaldunet.com/solutions/dsi/1494683-comparatif-ces-cms-headless-qui-pourraient-tuer-wordpress-et-drupal/.
- « Strapi : comprendre ce qu’est un headless CMS Open Source ». s. d. *Notion, Home des Sherpas*. Consulté le 3 octobre 2021. https://www.notion.so.
