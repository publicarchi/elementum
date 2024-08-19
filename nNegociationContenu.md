---
author: emchateau
tags: rest
---

# Négociation de contenu

L’application web des Guides de Paris supporte la négociation de contenu telle qu’elle est définie dans la spécification HTTP/1.1. Elle peut choisir la meilleur représentation d’une ressource en fonction des préférences de l’agent web (par exemple un navigateur) pour ce qui concerne le type de média, les langages, le jeu de caractères et son encodage. Elle doit également implémenter des fonctionnalités pour traiter de manière efficace les requêtes dont les informations de négociation sont incomplètes.

## La négociation de contenu

D’après les standards du web, une **ressource** peut disposer de plusieurs représentations. Une ressource est une entité conceptuelle identifiée par une URI (RFC 2396). Un serveur HTTP Apache propose l’accès à des **représentations** de la ressource à l’intérieur de son espace de nommage. Chaque représentation étant composée d’une séquence d’octets avec la définition d’un type de média, d’un jeu de caractères, d’un encodage, etc. À un instant donné, une ressource peut être associée à zéro, une ou plusieurs représentations. Lorsque plusieurs représentations sont disponibles, la ressource est qualifiée de **négociable** et chacune de ses représentations est nommée **variante**. Les différences entre les variantes disponibles d’une ressource négociable constituent les **dimensions** de la négociation.

Par exemple, une ressource peut être disponible en plusieurs langues, ou pour différents type de média. On peut tout à fait proposer ce choix à l’utilisateur, mais il est souvent plus commode de faire ce choix automatiquement. C’est souvent possible au moyen des informations qu’adresse un client web sur les représentations qu’ils préfèrent dans les en-têtes HTTP de chaque requête.

Un navigateur web peut, par exemple indiquer qu’il préfère recevoir des informations en français, mais sinon en anglais. Alors, il utilisera l’en-tête ’Accept-Language: fr’. Il est également possible de fournir préférences plus complexes en spécifiant des facteurs de qualités. Par exemple :

```
Accept-Language: fr; q=1.0, en; q=0.5
Accept: text/html; q=1.0, text/*; q=0.8, image/gif; q=0.6, image/jpeg; q=0.6, image/*; q=0.5, */*; q=0.1
```

Il s’agit de la négociation de contenu dite « côté serveur » où c’est le serveur qui décide quelle est la meilleure représentation à retourner pour la ressource demandée. Le module RESTXQ de BaseX doit ainsi supporter les en-têtes de requêtes ’Accept’, ’Accept-Language’, ’Accept-Charset’ et ’Accept-Encoding’.

Le module RESTXQ de BaseX doit également supporter la négociation de contenu transparente, qui est un protocole définit dans les RFC 2295 et 2296. (nota, Httpd ne supporte pas les négociation de fonctionnalités (_feature negociation_).

## Manière de négocier une ressource

Afin de négocier une ressource, on doit fournir au serveur des informations à propos de chacune des variantes.
- en utilisant une liste de correspondances (_type-map_) qui nomme explicitement les fichiers contenant les variantes
- en utilisant une recherche « multivue », où le serveur effectue une recherche de correspondance sur un motif de nom de fichier implicite et fait son choix parmi les différents résultats.




## Sources et bibliographie

- http://httpd.apache.org/docs/2.4/fr/content-negotiation.html
