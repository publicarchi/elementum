---
title: Qu’est-ce que REST ?
author: Emmanuel Chateau
filename: nREST.md
date: 2014-02-18
version: 0.4
---


# Qu’est-ce que REST ?

L’architecture du web définit un ensemble de contraintes qui peuvent être modélisées en identifiant les propriétés qu’elles induisent. À partir d’une telle modélisation, Roy Thomas Fielding a théorisé, dans sa thèse de doctorat, un paradigme de développement d’applications web qu’il nomme REST, pour Resource State Transfer.

## Les contraintes du modèle
---------------

REST se compose d’un ensemble de contraintes architecturales qui induisent des propriétés sur les architectures logicielles.

1° Une **architecture client-serveur** qui sépare les problématiques d’interface utilisateur de celle du stockage de données.

Cette contrainte améliore la portabilité de l’interface utilisateur sur les diverses plate-formes en permettant à ces deux composants d’évoluer indépendamment.

2° Une **communication dite sans état**, c’est-à-dire dans laquelle chaque requête du client vers le serveur doit contenir toutes les informations nécessaires pour qu’elle puisse être comprise. Ainsi, cette requête ne peut utiliser aucun contexte stocké sur le serveur. L’état de la session est entièrement détenu par le client.

Cette contrainte facilite la visibilité de la requête, la fiabilité est améliorée car il est plus simple de faire face à des échecs. Enfin, il est plus facile de monter en charge car l’absence de stockage d’état entre les requêtes permet aux composants du serveur de libérer rapidement les ressources et la mise en œuvre est facilitée. L’inconvénient de cette contrainte est qu’elle peut diminuer les performances en nécessitant des interactions supplémentaires puisque l’information ne peut être conservée sur le serveur dans un contexte partagé. La gestion de l’état, côté client, réduit en outre le contrôle du serveur sur le comportement de l’application.

3° **Utilisation d’un cache** pour améliorer les performances réseau. Cela impose que les données d’une réponse à une requête soient implicitement, ou explicitement, marquées comme pouvant être, ou non, mises en cache. Lorsqu’une réponse est mise en cache, le cache du client a la possibilité de réutiliser ces données pour les demandes ultérieures équivalentes.

Cette contrainte a l’avantage d’offir la possibilité d’éliminer certaines interactions et d’améliorer l’efficacité et la performance.

4° Une **interface uniforme** entre les composants est mise en place. Celle-ci implique quatre contraintes : l’identification des ressources, la manipulation des ressources par des représentations, des messages auto-descriptifs et l’hypermédia comme moteur de l’application.

Cette contrainte simplifie l’architecture globale du système et la visibilité des interactions. La mise en œuvre est découplée des services fournis ce qui favorise leur indépendance et les évolutions. Cependant, cela pénalise l’efficacité puisque l’information doit être transmise sous une forme normalisée plutôt que de manière spécifique aux besoins d’une application.

5° Un **système en couches** pour le déploiement d’une architecture à grande échelle comme le web. Le système est composé de couches hiérarchiques qui contraignent le comportement des composants puisque chaque composant ne peut pas voir au-delà de la couche intermédiaire avec laquelle il interagit.

Cette contrainte limite la complexité du système global et favorise l’indépendance des couches. Toutefois, l’utilisation d’intermédiaires ajoutent une latence supplémentaire et un surcoût dans le traitement des données.

6° Un modèle de **code à la demande** où le téléchargement et l’exécution de code sous forme d’applet ou de script permet l’extension des fonctionnalités d’un client.

Cette contrainte facultative simplifie les clients en réduisant le nombre de fonctionnalités qu’ils doivent mettre en œuvre par défaut. Elle améliore l’extensibilité du système.


## Les éléments architecturaux de REST

"Le modèle REST (Representation State Transfer) est une abstraction des éléments architecturaux d’un système réparti d’hypermédias." De ce fait, il est indépendant des détails de mise en œuvre de ces composants et de la syntaxe de protocole. Il se concentre sur le rôle des composants, les contraintes, sur leurs interactions, et leur interprétation des données. "Il englobe les contraintes fondamentales sur les composants, les connecteurs et les données qui définissent la base de l’architecture du Web, et ainsi l’essence de leur comportement en tant qu’application réseau."


### Les éléments de données

En tant qu’hypermédia distribué, lorsque l’on choisit un lien, l’information doit être déplacée depuis l’endroit où elle est stockée jusqu’à l’endroit où elle sera utilisée.

"Les composants REST communiquent en transférant une représentation d’une ressource dans un format appartenant à un ensemble évolutif de types de données standard." Le format de représentation de la ressource est choisi dynamiquement en fonction des possibilités ou des souhaits du destinataire et de la nature de la ressource.

Les éléments d’informations sont les suivants :

éléments d’information | exemples
Ressource | la cible conceptuelle d’une référence hypertexte
Identifiant de la ressource | URI, URL
Représentation | Document HTML, image JPEG
métadonnées de la représentation | type de média, date de dernière modification
métadonnées de la ressource | lien sur la source, liens alternatifs, variation
Données de contrôle | if-modified-since, cache-control

#### Ressources et identifiants de ressource

"L’abstraction principale de l’information dans REST est la ressource. **Toute information pouvant être nommée peut être une ressource** : un document ou une image, un service temporel (par exemple «le temps d’aujourd’hui à Marseille»), une collection d’autres ressources, un objet réel (par exemple une personne), etc. En d’autres termes, tout concept pouvant être la cible d’une référence hypertexte d’un auteur doit entrer dans la définition d’une ressource. C’est une correspondance conceptuelle à un ensemble d’entités et ce n’est pas l’entité correspondant à cette association à un moment particulier dans le temps."

Une telle définition permet de généraliser de nombreuses sources d’information sans les distinguer ni par leur type ni par leur mise en œuvre. Ensuite elle permet de lier tardivement la référence et sa représentation. Enfin, elle permet de mettre en exergue un concept plutôt qu’une représentation donnée à ce concept.

Cela implique de donner un identifiant pour identifier des ressources impliquées dans une interaction entre composants. C’est l’autorité responsable de l’assignation d’un identifiant à la ressource qui est responsable du maintien de sa validité. C’est en ce sens que REST s’appuie plutôt sur les auteurs.

#### Les représentations

"Les composant REST effectue des actions sur une ressource en utilisant une représentation pour capturer l’état courant ou prévu de cette ressource et en transférant cette représentation entre composants." Une représentation se compose de données et de métadonnées qui les décrivent. Le format de données d’une représentation est connu comme étant un type de média.

### Les connecteurs

Les connecteurs offrent une interface abstraite pour la communication entre les composants. Une interface prend des paramètre en entrée et fournit des paramètres en sortie.

Plusieurs types de connecteurs :
- client et serveur
- connecteur de cache
- résolveurs de liens
- tunnel

### Les composants

Un **Agent utilisateur** utilise un connecteur client pour initier une requêet et devient destinaire final de la réponse. L’exemple le plus commun est un navigateur web qui permet d’accéder aux services d’information.

Le **Serveur d’origine** utiliser un connecteur serveur pour régir l’espace de nom pour une ressource demandée. C’est la source définitive de représentattion de ses ressources, il doit être destinataire final de toute requête prévoyant de modifier la valeur de ses ressources.

Les **composants intermédiaires** agissent en tant que client et serveur afin de faire suivre, avec une traduction éventuelle, des requêtes et des réponses. Un composant mandataire est un intermédiaire choisi par un client. Un composant passerelle est un intermédiaire imposé par le réseau ou le serveur d’origine.


## Les vues

Vue processus
Vue connecteur
Vue orientée données


## REST vs SOAP

Description | SOAP | REST
(Perceived) complexity | High | Low
HTTP as an application protocol | No, abused as transport protocol | Yes
Web-friendly (direct support of caches, proxies, etc.) | No | Yes
Stateless | No (most of the time) | Yes
Addressable resource | No | Yes
Data handling | Automatic mapping to objects (O/X) | No automatism
Date security | WS-Security, ... | HTTPS


## Références

- Traduction Française du Chapitre 5 de la thèse de Roy T. Fielding http://opikanoba.org/tr/fielding/rest/

- Roy T. Fielding, _Architectural Styles and the Design of Network-based Software Architectures_, doctoral dissertation, University of California, Irvine, 2000.
