---
since: 2017-07-07

author: emchateau
---

# Why XML Rules !

Lorsque l’on vient du monde XML et que l’on passe à JavaScript on peut être surpris par le défaut de prise en charge de la représentation du texte. Chacun sait à quel point le DOM offre une représentation bien moins expressive que le XML Data Model d’une structure hiérarchique. Chose étonnante pour un langage dont l’application principale concerne normalement la présentation du texte sur le web dans le navigateur. Plus étonnant encore, c’est l’absence de prise en charge de fonctionnalités communes dans le monde XML telles que certains types courants comme les dates, ou les séquences, et une intégration pour le moins médiocre d’Unicode (absence de collation par exemple).

D’aucun diront qu’on peut suppléer à tout cela par l’emploi de librairies dédiées. Le problème c’est que rarement on atteint la qualité d’implémentation actuellement offerte par exemple par XQuery ou XSLT avec XPath.

## Expressivité des Objets

comparée au maps

## Absence des séquences

## Échappement des fragments balisés dans les objets

Obligation d’échapper certains caractères dans les valeurs des propriétés des objets. Ennuyeux lorsque l’on travail sur des contenus HTML. Aberrant lorsqu’il s’agit simplement de balader une URL ou une URI !

## Types XML

Dates, raisonnement sur les dates

URL, id, langues, etc.

## Collation Unicode

Absence de collation Unicode. On ne peut pas choisir l’ordre de tri des caractères ceux-ci étant seulement renvoyés dans leur ordre de point. Ainsi `a` > `A`...

## Le DOM vs XPath

Pas d’accès aux attributs

Pas d’évaluation ensembliste

etc.

## Une syntaxe absconde

Pas de distinction claire des variables

boucles for dégueulasses, ES2017 pour régler ça...

## Et c’est sans même évoquer

Tout cela sans évoquer les problèmes d’implémentation que rencontre le langage. À bien des égards, on pourrait dire que la standardisation de JavaScript reflète pour l’essentiel les dictats des éditeurs de navigateurs. Et face à ces défauts, on pourrait se prendre à rêver de voir un jour remplacer JavaScript par un langage conçu sur des bases plus cohérentes et plus élégantes.