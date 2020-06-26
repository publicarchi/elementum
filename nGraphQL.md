---
since: 2020-04-16
tags: graphql, rest, javascript, xquery
---

# GraphQL

GraphQL est à la fois un langage de requêtes et un environnement d’exécution pour des interfaces programmables (APIs). Développé par FaceBook depuis 2012, le langage a été rendu public en 2015 (React.js Conf 2015) puis mis à disposition sous Licence OWFa-1.0 (Open Web Foundation) en 2017. Il est depuis maintenu par une large communauté. 

GraphQL est compatible avec diverses plateformes de développement comme Python Django, Ruby on Rails, ou JavaScript Node.js. Ce cadre de développement est notamment employé par FaceBook, Twitter, GitHub et Shopify, pour leurs APIs.

GraphQL permet d’aller chercher des données de manière déclarative (*declarative data fetching*). Un un client peut directement spécifier les données dont il a besoin à une API. Au lieu de présenter une multitude de points d’accès qui retournent des structures de données fixes (comme dans l’architecture REST), un serveur GraphQL expose seulement un point d’entrée unique qui répond avec les données spécifiquement demandées par le client.

GraphQL repose sur trois composantes : un langage de requêtes, un système de schémas ou de typage, et un environnement d’exécution.

- le langage de requête (*query language*) facilite l’accès à l’API par sa flexibilité tant en termes de requêtes pouvant être formulées que de préparation des données. Il est également possible de formuler des requêtes en écriture et en lecture.
- le système de schéma offre la possibilité de définir des structures de données. Ces schémas permettent de valider les requêtes.
- l’environnement d’exécution permet l’analyse syntaxique des requêtes, leur validation, ainsi que la stérilisation des réponses.

GraphQL se caractérise par la simplicité de son langage de requête. Le format des données est très proche du format JSON ([JavaScript Object Notation](https://www.json.org/json-fr.html)). Découle de ce modèle une structure hiérarchisée, un typage fort et une grande flexibilité. Des propriétés partagées avec XML, toutefois JSON n’est pas bien adapté pour prendre en charge des contenus mixtes souvent rencontrés avec le texte structuré.

Si GraphQL utilise HTTP, il ignore généralement les propriétés du protocole. Son utilisation se distingue donc fortement d’une architecture REST qui impose une description fine des ressources et permet la négociation de contenu. Le déploiement de GraphQL peut poser des difficultés en matière de scalabilité ou de gestion de caches.

## Exemple

Exemple de création d’une application GraphQL développée en JavaScript avec le cadre de développement web [Express](https://expressjs.com).

Créer un répertoire

```bash
mk dir testGraphql
cd testGraphql
```

En supposant que [Node.js](https://nodejs.org/) est déjà installé, utilisez la commande `npm init` pour créer un fichier `package.json` pour l’application. La commande vous invite à renseigner plusieurs informations sur votre application.

Avec npm

```bash
npm init
```

Installer les dépendances ([express](https://expressjs.com/fr/starter/installing.html), graphql, et expres-graphql)

```bash
npm install --save express
```

```bash
npm install --save graphql
```

```bash
npm install --save express-graphql
```

Avec Yarn

```bash
yarn init -y
```

```bash
yarn add graphql
```

```bash
$ yarn add express-graphql
```



Créer dans le répertoire un fichier `serve.js` avec le contenu suivant

```javascript
const express = require('express')
const graphqlHTTP = require('express-graphql')
const app = express()

app.use('/graphql', graphqlHTTP({
  graphiql: true
}))

app. listen(4000)
console.log('Listening...')
```

Lancer

## REST vs GraphQL

REST est un style architectural, l’autre un langage et un framework. Tous deux peuvent être utilisés à travers plusieurs protocoles.

REST in peace, Rest, mais rappelle commentaire sur SOAP. Cf. REST is the ne SOAP... Sans doute une nouvelle itération.

Un style architectural est un un ensemble de contraintes qui impliquent un système qui dispose de certaines propriétés (cf. Fielding).

> Architectural style is a set of constraints that imply system with certain properties.
>
> Zdenek, Goodapi, 2018

- Découplé (*decoupled*) implique que le client et le serveur peuvent évoluer différemment
- Sans état (*stateless*), le fait qu’il n’y ait pas d’état permet fiabilité et scalabilité
- Interface uniforme (*uniform interface*) peut impliquer dégradation de l’efficience car construit une interface intermédiaire, en même temps implique simplicité et régularité.

Un architecte de système doit connaître ces différents styles architecturaux et raisonnés en fonction de leurs avantages et inconvénients pour une tâche donnée.

Il y a plusieurs genres d’API

- Web API (REST)
- Query API (GraphQL)
- Streaming APIs
- Flat File
- RPC APIs

Première vague dans les années 2000, API spécifiques pour des clients. Seconde vague 2010, API générique. Troisième vague 2020 où les APIs pourraient être autonomes et communiquer les unes avec les autres.

SOAP, EDI, FTP toujours en application, pas en REST ou en GraphQL.

Contraintes

- contraintes d’affaire (*business contraints*) : liées au client, au besoins du secteur, aux fonctionnalités du produit
- contraintes de complexité : implications en terme de complexité pour un système distribué, qualités d’évolution
- contraintes de domaine : limitations-spécifiques, régulation, environnement
- contraintes culturelles : loi de Conway, savoir, ressources humaines, pression par les pairs, mode

Ces contraintes impliquent des propriétés pour le système que construit.

Propriétés

- performance : réseau, efficience, perçue
- scalibilité : taille
- simplicité : interface uniforme, perçue par utilisateur, en fonction des structures de tâches, prédictibilité, algorithmique, chaotic
- modifiabilité : évolution, extensibilité, personnalisation, configurabilité, réutilisation
- visibilité : monitoring, sécurité, caching
- portabilité : environnements, code et données
- fiabilité : susceptibilité d’erreurs, récupération
- découvrabilité : design-time, runtime-time
- sécurité
- facilité développement
- efficience

Communauté, documentation, etc. qui influent plus globalement sur le choix.

REST, difficile d’entrer, difficile à maîtriser. Implémentations de qualité difficiles à trouver en dehors du www. Mais scalabilité sans comparaison, évolvabilité et découvrabilité si bien implanté.

Contraintes de REST

1. Client-Server
2. Stateless
3. Cacheable
4. Layered System
5. Code on Demand (optional)
6. Uniform interface
   1. Identification of Resources
   2. Resource Representation
   3. Self-descriptive Messages
   4. HATEOAS

Contraintes qui amène propriétés. Si suit ces contraintes amène un certain nombre de propriétés.

Induced properties of REST

1. Performance
2. Scalability
3. Simplicity
4. Modifiability
5. Visibility
6. Portability
7. Reliability

Bénéfices de REST

- Scale indéfiniment
- Hautes performance (spécialement avec HTTP2)
- Fait ses preuve depuis longtemps
- Fonctionne avec n’importe quelle représentation ou type de média
- Affordance-centric (design maturity)
- Server-driven application state (le serveur dit ce que peut appeler et quand)
- Découplage complet du client et du serveur permet évolution indépendante
- Liens entre les APIs

Couts de REST

- forte barrière entrée en matière de formation et d’apprentissage, que peu d’utilisateurs parviennent à surmonter
- gros changement de paradigme par rapport à SOAP qui implique un changement d’état d’esprit
- exige que le client fonctionne séparément, = discipline des deux côtés
- Peu d’outils ou pauvres pour les clients
- Limite la description des formats
- Challenge pour conserver consistance et gouvernance.

so-called-REST APIs

Le plus commun aujourd’hui. Suivent contraintes HTTP mais pas toujours (séparation des concerts, cf. Amundsen & Richardson maturity models).

Exigent bonne connaissance de HTTP côté client et serveur.

Évolutions indépendantes impossibles, ou difficiles.

Bénéficient de l’infrastructure de l’internet et de sa scalabilité.

Contraintes de so-called-REST

1. Client-Server
2. Stateless
3. Cacheable
4. Layered System
5. Code on Demand (optional)
6. Uniform interface
   1. Identification of Resources
   2. Resource Representation
   3. ~~Self-descriptive Messages~~
   4. ~~HATEOAS~~

Contraintes qui amène propriétés. Si suit ces contraintes amène un certain nombre de propriétés.

Induced properties of so-called-REST

1. Performance
2. Scalability
3. ~~Simplicity~~
4. ~~Modifiability~~
5. Visibility
6. Portability
7. Reliability

Pour autant reste plutôt performant. Scale bien quand suit HTTP. Haute performance. Bien établi. Fonctionne avec nombreuses représentations. Des outils relativement mûrs. Mais coût barrière entrée. Difficulté à évoluer. Challenge de gouvernance. Type et sécurité.

GraphQL APIs, plus spécifique que REST. 

Facile à accéder essentiellement remote data access, simplifié par rapport SQL, agnostique vendeur. Ignore infrastructure du web (POST tunneling). Pour authentification, négociation de contenu, pagination, etc. se débrouiller soi-même. Problèmes de scalabilité (pas d’infrastructure de cache). Tight coupling des clients avec les serveurs (structure de données).

Bénéfices fournis par GraphQL

- facile à démarrer
- time to market for servers and clients
- expérience de développement étonnante
- contract-driven by nature
- built-in introspection
- facile à garder consistant ou gouverner
- plus proche de WS/SQL qui rend le changement de paradigme plus simple que REST
- conception qui peut intervenir en aval

Mais cela a un coût

- néglige le problème du système distribués
- serveur et client couplés at the client programming time, état de l’application pas gérés par le serveur
- optimisation des requêts
- freins (négociation de contenu, erreurs réseau, cache, authentification)
- scaling (cache serveur et client seulement, pas possible d’utiliser cache existant)
- jette par dessus bord tout ce qu’a essayé d’établir HTTP
- support de médias limités
- peu de vendeurs dans l’éco-système

Pour conclure : utiliser REST pour un système qui doit durer, faire de al négociation de contenu, gérer des authentifications, ou lier des APIs entre elles, utiliser des contenus divers, scalabilité.

GraphQL si parle à soi-même (front-end et backend), à la place de so-called-REST, pour des projets à court terme, des cas d’utilisation incertains, juste pour accéder à des données sans besoin de cache, expérience de développement étonnante avec peu d’effort.

Arrêter so-called-APIs !

Source : REST vs GraphQL: Critical Look. This is a session given by Zdenek “Z” Nemec at Nordic APIs 2018 Platform Summit on October 23rd, in Stockholm, Sweden.  https://youtu.be/yLf0rIaRtRc

## Remarques

Fondamentalement, GraphQL n’offre guère plus que les technologies de bases de données XML natives. Il existe dans l’environnement XML plusieurs langages de schémas et des outils de validation standardisés. XQuery constitue un langage de requête et de manipulation de données typé et turing complet probablement plus expressif que GraphQL. Les technologies XML offrent en outre une meilleure prise en charge du texte structuré avec les contenus mixtes. XQuery Full-text, une extension de XQuery, permet de formuler des requêtes plein-texte. Les bases de données XML permettent de développer des applications REST avec RESTXQ mais il est également possible de requêter la base de données directement depuis un point d’accès unique comme avec GraphQL. Les requêtes sont alors envoyées au serveur par l’intermédiaire d’une simple requête GET. L’utilisation d’une base de données XML permet de bénéficier des performances de l’indexation, mais il est également possible de requêter des fichiers à plats en ligne de commande. 

Il n’existe malheureusement pas de framework ou de client qui facilite l’utilisation de XQuery dans le cadre de l’écriture de JavaScript.

La pluspart des outils XML et des applications XQuery fonctionnent en environnement Java.

Il manque le concept de subscriptions dans XQuery.

## Sources

- How to GraphQL https://www.howtographql.com/basics/0-introduction/
- REST vs GraphQL: Critical Look. This is a session given by Zdenek “Z” Nemec at Nordic APIs 2018 Platform Summit on October 23rd, in Stockholm, Sweden.  https://youtu.be/yLf0rIaRtRc

