# WebScraping avec XQuery

Tutoriel avec EXPath

https://gist.github.com/joewiz/2072e9f04838188b2aa6ee4ae0f72a15


## Web-scraping de site web avec XQuery

Cette note concerne la récupération de données web avec XQuery. Elle utilise l’extension EXPath qui est disponible sur la plupart des processeurs XQuery tels que BaseX, eXistDB, etc.

## Questions éthiques

Aspirer des données depuis le web peut poser des questions éthiques et légales. Demandées vous si les données sont sous copyright et l’impact éventuel de votre action sur les serveurs.

Important: vérifier le fichier robots.txt, qui se trouve habituellement à la racine du répertoire. Celui-ci fournit normalement des indications sur les opérations permises pour les robots.

Il est toujours possible de se signaler dans les entêtes de vos requêtes HTTP. Vous pouvez, par exemple, envoyer un message indiquant que vous êtes un chercheur en train d’extraire des informations et proposer de vous contacter immédiatement en cas d’inquiétude en donnant vos coordonnées.

cf. http://robertorocha.info/on-the-ethics-of-web-scraping/

## Étudier la structure du site web

Dans un premier temps, il est nécessaire de prendre le temps de comprendre la structuration du site web dont vous souhaitez récupérer les données. Quelle est la structure des URLs, et quelle est la structure des documents HTML notamment.

En utilisant l’interface et les navigations disponibles, on peut rapidement comprendre la structuration du site en observant la composition des requêtes dans la barre d’adresse.

Préparer l’étendue des années à requêter 

```xquery
let $urlHead := 'http://mysite.xx/articles/list?ay="'
let $urlTail := '&fr"'
let $years := (2014 to 2017) ! ($urlHead || . || $urlTail )
```

## Évaluer les requêtes EXPath

Les langages basés sur XPath comme XQuery disposent de la fonction par défaut `fn:doc()` qui permet d’accéder à des documents. Toutefois, cette fonction ne fonctionne que pour des documents XML bien formés. Or, le plus souvent les documents publiés sur le web ne sont pas des documents XML bien formés.

Ainsi, sur de nombreux sites, l’expression suivante

```xquery
fn:doc('http://url')
```

Ramènera une erreur de ce genre :

> err:FODC0005 exerr:ERROR:
>
> An error occurred while parsing http://url
>
> Open quote is expected for attribute "lang" associated with an element type "html".

La fonction `fn:doc-available()` teste qu’une URI retourne un document XML bien formé en renvoyant une valeur booléenne.

Toutefois, la plupart du temps, cette fonction par défaut ne sera pas suffisante pour faire du web-scraping, dès lors que l’on veut récupérer le HTML même si les documents ne sont pas bien formés. Sans compter, qu’il est souvent nécessaire de récupérer d’autres contenus comme des fichiers textes ou des fichiers binaires.

### Utiliser le client HTTP EXPath

Le [client HTTP EXPath](http://expath.org/modules/http-client/) apporte une solution à ce problème. Il s’agit d’une spécification de module XQuery implémentée par plusieurs processeurs XQuery tels que BaseX, eXistDB, Marklogic et Saxon) pour effectuer des requêtes HTTP.

Le client utile la fonction unique http:send-request()` pour transmettre les requêtes HTTP. Commodément, et à la différence de `fn:doc()`, le client HTTP EXPath convertit automatiquement les documents en documents XML bien formés les rendant de fait accessibles avec XPath et XQuery.

La fonction http:send-request()` permet de préciser les méthodes HTPP utilisées (GET, POST, PUT, DELETE, HEAD, TRACE), de fournir l’URL, et de renseigner des messages d’entête HTTP.

```xquery
xquery version "3.1";

import module namespace http = "http://expath.org/ns/http-client";

let $url := "http://monUrl"
let $request := 
    <http:request href="{$url}" method="GET">
        <http:header name="Connection" value="close"/>    
    </http:request>
return
    http:send-request($request)
```

Cette expression retourne deux items : l’entête de réponse du serveur inclue dans un éléments  `<http:response>` et le corps du message. Les messages d’entêtes renvoyés par le serveur peuvent être intéressants pour identifier des problèmes éventuels.

## Récupérer le résultat

Deux solutions s’offrent à vous pour récupérer le résultat de vos requêtes : soit alimenter directement une base de données, soit stocker les fichiers localement pour d’autres usages.

```xquery
xquery version "3.1";

import module namespace http = "http://expath.org/ns/http-client";

let $path := 'db/path'
let $url := "http://monUrl"
let $request := 
    <http:request href="{$url}" method="GET">
        <http:header name="Connection" value="close"/>    
    </http:request>
let $response := http:send-request($request)
let $record := 
	<record>
		<date>{current-dateTime()}</date>
		{
          $request,
          $response
		}
	</record>
return db:add('database', $record, $path)
```

Ou bien écrire le fichier localement

```xquery
xquery version "3.1";

import module namespace http = "http://expath.org/ns/http-client";

let $path := 'User/path/file.xml'
let $url := "http://monUrl"
let $request := 
    <http:request href="{$url}" method="GET">
        <http:header name="Connection" value="close"/>    
    </http:request>
let $response := http:send-request($request)
let $record := 
	<record>
		<date>{current-dateTime()}</date>
		{
          $request,
          $response
		}
	</record>
return db:add($path, $record)
```

## Récupérer le HTML et les fichiers binaires

@todo

faire une requête head, identifier les type

## Identifier les liens au sein des pages

Dans certains cas, il est possible que toutes les adresses ne soient pas prévisibles. Afin de de rapporter l’ensemble des contenus qui nous intéressent, il peut alors être nécessaire d’identifier à l’intérieur de certaines pages les liens qu’il faut suivre. Comme la requête ramène un document XML qui peut être exploré avec XPath, il est assez aisé de créer une séquence d’URL dont il faudra traiter la récupération groupée à l’aide d’un simple script.

## Références

- [Joewiz. Web Scraping with XQuery](https://gist.github.com/joewiz/2072e9f04838188b2aa6ee4ae0f72a15)
- [Robroc. Scraping websites with BeautifulSoup](https://github.com/robroc/MakeWebNotWar-scraping-with-BeautifulSoup/blob/master/Web%20scraping%20with%20BeautifulSoup.ipynb)
- [Roberto Rocha. On the ethics of web scraping. robertorocha.info](http://robertorocha.info/on-the-ethics-of-web-scraping/)
- [Introduction to web scraping. Data-lessons](https://data-lessons.github.io/library-webscraping/)





