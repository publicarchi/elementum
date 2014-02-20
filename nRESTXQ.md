---
title: Note RESTXQ
filename: nRESTXQ.md
author: Emmanuel Château
date: 2014-02-19
version: 0.1
---

Note RESTXQ
===========


Approche
-------------

Alors que XQuery est depuis longtemps identifié comme un bon langage pour produire du XHTML et du HTML à partir de requêtes complexes, il ignore jusqu'à présent presque complètement le Web. En effet, XQuery ne fournit aucune fonctionnalités natives soit pour formuler des requêtes web, soit comme langage de script côté serveur pour traiter des requêtes Web. En décrivant l'alignement des requêtes REST en code XQuery exécutable, RESTXQ propose une standardisation de la manière dont XQuery peut être invoqué dans un contexte Web pour développer des applications. On renseigne de manière déclarative les capacités HTTP d'une fonction XQuery en utilisant des annotations. Par l'intermédiaire de ce mécanisme, XQuery peut être employé comme un langage de traitement côté serveur pour le web.


Contexte
-------------

XML Query Language (XQuery) est une recommandation du W3C pour rédiger des requêtes d'après la structure logique de documents XML (modèle de données XPath et XML Data Model (XDM)). XQuery est un langage de programmation fonctionnel Turing-complet centré sur des expressions FLWOR (For Let Where Order-by Return) qui utilisent des expressions de chemin pour adresser le modèle de données XML. Le code XQuery peut être groupé dans des fonctions et des modules, desquels il y a toujours un module principal par lequel le traitement débute.

XQuery 3.0 introduit plusieurs fonctionnalités nouvelles dont les annotations. Les annotations permettent de déclarer les propriétés de fonctions ou de variables, zéro ou plusieurs annotations peuvnet être ajoutées à la déclaration d'une fonction ou d'une variable. Ces annotations débutent par `%` et consistent d'un nom qualifié étendu et une valeur optionnelle, cette valeur étant une séquence de litéraux.

REST pour Representational State Transfer est un style architectural de programmation théorisé par Roy Fielding dans sa thèse de doctorat pour décrire de manière abstraite les principes de conception architecturaux développés par le Web. "REST est défini par quatre contraintes d'interface : l'identification des ressources ; la manipulation des ressources au travers de leurs représentations ; l'utilisation de messages auto-descriptifs ; et de l'hypermédia comme moteur de l'application d'état." On qualifie les applications correspondant à cette description de RESTful.

Le Web utilise l'Hyper-Text Transfer Protocol (HTTP) comme protocole d'application et l'Uniform Resource Identifier (URI) comme mécanisme d'adressage. Les services web dits RESTful implémentés avec HTTP utilisent l'étendue des méthodes définies par le protocole (GET, PUT, POST, DELETE, OPTIONS, etc.) et la négociation de contenu pour retrouver et stocker des représentations au travers d'URI d'espaces de nom richement descriptives.


Fonctions ressource (_Resource Functions_)
-------------

Une fonction ressource (_resource functions_) est une fonction XQuery marquée avec des annotations RESTXQ. Ces annotations indiquent à un processeur que lorsqu'elle est présentée par une requête d'un service web REST avec les contraintes correspondantes à celles indiquées par les annotations, la fonction doit être invoquée et le résultat retourné comme le résultat de la requête du service.

Il y a deux types d'annotations de fonction ressource déscrites dans RESTXQ :

- Contraints() les contraintes
- Parameters() les paramètres


### Contraintes des fonctions ressource (_Resource Function Constraints_)

Des contraintes restreignent le service de requêtes qu'une fonction ressource peut traiter.


#### Annotation de chemin et Motifs (_Path Annotation and Templates_)

Une _annotation de chemin_ (_Path Annotation_) fait correspondre l'URI d'un service REST à une fonction ressouce. Une fonction ressource doit contenir une seule annotation de chemin. Des annotations supplémentaires peuvent être également utilisées pour contraindre la fonction ressource.

L'annotation de chemin est nommée `%rest:path` et prend une unique chaîne de caractère obligatoire qui décrit l'URI du chemin du service. Cet URI de chemin est relatif à un URI de base défini par l'implémentation.

L'URI de chemin peut contenir zéro ou plusieurs motifs d'URI dénotant les segments du chemin qui doivent correspondre à des paramètres de fonction. Un motif d'URI présente la syntaxe `{$fn-param-name}`, où `fn-param-name` est le nom d'un paramètre de la fonction annotée dont la valeur doit être prise pour le chemin.

Les paramètres adressés par un motif d'URI doivent remplir les contraintes suivantes :

- La cardinalité n'autorise qu'une valeur atomique, sinon une erreur sera produite par l'implémentation
- Un type hérité de xs:anyAtomicType, sinon une erreur sera produite par l'implémentation. La conversion dans le type requis intervient au moment de l'exécution, si la conversion est impossible, une erreur doit être produite.

### Méthodes HTTP (_HTTP Methods_)

Les fonctions ressource peuvent être contraintes à zéro ou plusieurs méthodes HTTP au moyen d'annotation de méthode. Si la fonction ressource n'est pas contrainte par une annotation de méthode l'annotation de chemin d'une fonction ressource applique toutes les méthodes HTTP.

Les annotations sont définies pour toutes les méthodes HTTP 1.1 à l'exception de TRACE et CONNECT. Toutes les méthodes doivent retourner des ressources à l'exception de HEAD, qui doit seulement retourner un élément `rest:response`.

Les annotations de méthode POST et PUT peuvent prendre un litéral optionnel qui fait correspondre le corps de la requête HTTP au nom d'un paramètre de fonction[??]. La même syntaxe  que celle utilisée pour les motifs d'URI est appliquée, par exemple `%rest:POST("{$request-body")` injectera le corps de la requête dans la fonction à travers le paramètre de la fonction nommé `request-body`. Le paramètre de la fonction pour le corps de la requête doit correspondre aux contraintes suivantes :

- Une cardinalité qui autorise un ou plusieurs items du type.
- Un type compatible avec le coprs de la requête. Celui-ci est déterminé par l'en-tête de type de contenu de HTTP

### Capacités de type de média (_Media-Type Capabilities_)

### Paramètres de fonction ressource (_Resource Function Parameters_)

### Paramètre de chaîne de requête (_Query String Parameters_)

### Paramètres de champ de formulaire (_Form Field Parameters_)

### Paramètres d'entête HTTP (_HTTP Header Parameters_)

### Paramètres de Cookies (_Cookies Parameters_)

### Sérialisation de fonction ressource (_Resource Function Serialization_)

### Format de réponse REST (_REST Response Format_)

### Module de fonction REST (_REST Function Module_)



Références
-----------

- [Adam Retter, "RESTful XQuery. Standardised XQuery 3.0 Annotations for REST", _XML Prague 2012_, janvier 2012.](http://www.adamretter.org.uk/papers/restful-xquery_january-2012.pdf)
- [Adam Retter, _RESTXQ 1.0: RESTful Annotations for XQuery 3.0, Unofficial Draft_, 17 septembre 2012.](http://exquery.github.io/exquery/exquery-restxq-specification/restxq-1.0-specification.html)
