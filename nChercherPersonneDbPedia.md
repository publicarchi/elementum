---
title: Chercher une personne dans DBpeda
fileName:nChercherPersonneDbPedia.md
date: 2014-02-01
author: emchateau
version: 0.1
tags: dbpedia
---

# Chercher une personne dans DBPedia

Lancé à l’initiative de ?? et d’Alexandre Monin, le projet [Semanticpedia](http://www.semanticpedia.org) a été conçu dans le cadre d’un partenariat entre l’association Wikipédia France, le Ministère de la Culture et de la Communication et l’INRIA, est un projet d’exposition des données de l’Encyclopédie collaborative francophone dans le Linked Open Data. Ce projet est l’équivalent francophone d’un projet allemand conduit à partir des pages anglophones de Wikipédia.

http://fr.wikipedia.org/wiki/DBpedia

L’intérêt principal d’un tel projet c’est qu’il permet d’accéder à un certain nombre d’informations structurées contenues dans l’Encyclopédie en ligne collaborative Wikipédia exprimées dans les formats du web sémantique. En d’autres termes, cela signie que l’information structurée comprise par exemple dans les infobox de l’encyclopédie, les sources de la notice encyclopédique, ses catégories, ou ses renvois sont exprimés sur le web sous forme de triplets RDF. Or, dès lors que le projet met à disposition un point d’accès (ou SparQL endpoint) ces jeux de données sont accessibles à l’aide du langage de requête SparQL.

SparQL est en quelque sorte le langage SQL du web sémantique. À l’aide de requête très simples, on peut par exemple extraire de DBpedia le résumé d’une notice Wikipédia, les dates et lieux de naissance ou de mort d’une personne pour les afficher dans sa propre page web. On sent bien ici tout l’intérêt des technologies sémantiques pour leur capacité à extraire et requêter de l’information à travers différentes applications tierces afin de produire avec elles des compendium (ou mashups).


## Exploration du graphe d’un auteur

La ressource [Henri Sauval](http://fr.dbpedia.org/page/Henri_Sauval) sur DBpedia présente un certain nombre d’informations extraites de la page Wikipédia.

- la propriété (aussi appelée prédicat) `rdfs:label` fournit le nom sous forme de chaîne de caractère. Autrement dit : l’URI http://fr.dbpedia.org/page/Henri_Sauval a pour intitulé (label) la chaîne de caractères `Henri Sauval`.

- la propriété `dbpedia-owl:abstact` comporte le résumé tiré de la page Wikipédia.

- les propriétés `dbpedia-owl:birthDate` et `dppedia-owl:birthPlace` renseignent les dates et lieux de naissance. On remarque que la date est typée avec le XML schema (`xsd:date`).

- la propriété `dcterms:subject` renseigne les catégories de la page sur Wikipédia.


## Quelques exemples de requêtes

Récupérer le nom d’une personne néée quelque part

```sparql
    prefix db-owl: <http://dbpedia.org/ontology/>
    select * where {
        ?nom rdf:type db-owl:Person.
        ?nom db-owl:birthPlace ?lieuNaissance.
    }
```

Afficher les 1 000 premiers objets de la page "catégorie" intitulés "Œuvre conservée au Musée d’Orsay" dans DbPedia (exemple rapport ModRef)

```sparql
  select * where {
    ?categorie rdfs:label "Œuvre conservée au Musée d’Orsay"@fr .
    ?oeuvre <http://dbpedia.org/ontology/wikiPageWikiLink> ?categorie
    }
  LIMIT 1000
```

## Recherches dans Open street map

https://wiki.openstreetmap.org/wiki/SPARQL_examples

## Sources

- http://www.informatheque.fr/articles/enrichir-son-catalogue-avec-dbpedia-0
- http://www.informatheque.fr/articles/enrichir-son-catalogue-avec-dbpedia-comment


## Références
- http://www.w3.org/TR/rdf-primer/


URL du Sparql end-point de dbpedia
http://dbpedia.org/sparql

```sparql
  PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> PREFIX dcterms: <http://purl.org/dc/terms/>
  PREFIX skos: <http://www.w3.org/2004/02/skos/core#> PREFIX dbo: <http://dbpedia.org/ontology/>
  SELECT DISTINCT ?s ?p FROM <http://dbpedia.org> WHERE {
    ?s rdf:type dbo:FictionalCharacter . ?s dbo:portrayer ?p .
    ?p rdf:type dbo:Person .
    ?p dcterms:subject/skos:broader*
    <http://dbpedia.org/resource/Category:Academy_Award_winners> . }
    ORDER BY ?p
```
