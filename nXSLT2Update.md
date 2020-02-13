---
author: Emmanuel Château-Dutier
since: 2019-11-16
---
# Nouveautés introduites dans XSLT 2.0

## Le modèle de données 2.0

Travail conjoint sur XSLT 2.0 et XQuery 1.0. Élaboration du XQuery 1.0 et du XPath 2.0 Data Model. Utilisation du même modèle de données.

Au moment de la publication de la [recommandation XML](http://www.w3.org/TR/REC-xml ) en février 1998, plusieurs personnes jugèrent que l’on n’était pas parvenu à décrire un modèle de donné rigoureux (DuCharme 2005). Ce fut pour y remédier que le W3C publia en octobre 2001 la recommandation [XML Information Set](http://www.w3.org/TR/xml-infoset), également connue sous la désignation *Infoset*. Celle-ci décrivait de manière plus formelle et moins ambiguë le contenu d’un document XML.

La recommandation XSLT 1.0 incluait une section sur le [Data Model](http://www.w3.org/TR/1999/REC-xslt-19991116#data-model) qui décrivait les dépendances avec le modèle de données de XPath, avant d’introduire plusieurs détails sur la représentation des nœuds d’un document XML envisagé comme un arbre. En effet, il existe d’autres manières de modéliser un document XML comme le DOM ou un arbre de structures d’entités, etc.

Le nouveau modèle de données adopté avec le *XQuery 1.0 and XPath 2.0 Data model* est un document important dont près de la moitié récapitule dans des appendices l’état des spécifications précédentes. L’introduction explique que ce modèle de données est basé sur l’infoset avec deux additions pour supporter les types issus de XML Schéma types et la représentation de collections de documents et de valeurs complexes.

- toute instance du modèle de données est une séquence
- une séquence est une collection ordonnées de zéro ou plus items
- tous les items sont soit des valeurs atomiques (comme un nombre entier, ou une chaîne) ou un nœud ou encore l’un des septs types suivants : *element node*, *attribute node*, *text node*, etc.

## XPath 2.0

- nouveautés et améliorations des expressions de chemins (*Path expressions*)
- nouveaux opérateurs
- expressions conditionnelles (*if*-*then*-*else*) et boucles (*for*)

## XSLT 2.0

Notion de constructeur de séquence

http://www.w3.org/TR/2004/WD-xslt20-20041105/#dt-sequence-constructor

### Améliorations apportées aux templates et au traitement des feuilles de style

Result Tree Fragments

- Arbres temporaires (*temporary trees*)
- Modes multiples (*Multiple modes*)
- *Next best match*
- *Tunnel parameters*

### Définition de fonctions (*Function definition*)

[XQuery 1.0 and XPath 2.0 Functions and Operators](http://www.w3.org/TR/xpath-functions)

- Fonctions prédéfinies dans le langage (*Built-in XPath 2.0 functions*)
- Fonctions définies par l’utilisateur (*User-defined functions*)

### Entrées et sorties (*Inputs and outputs*)

- Ouverture de documents : les fonctions `document()`, `doc() et `collection()`
- Parsing de documents non-XML
- Création de documents résultats multiples

### Manipulation de chaînes (*String manipulation*)

- Expressions régulières en XSLT 2.0
- Les fonctions de chaînes de XPath 2.0
- Parser des chaînes de caractères avec `xsl:analyze-string`

### Grouping

Avec XSLT 1.0, utilisation de la méthode Muenchienne (keys).

XSLT 2.0 offre l’instruction `for-each-group` don’t l’attribut `@select` identifie les items qui doivent être groupés. Il est possible de les grouper par des clefs de valeurs calculées avec `@group-by` pour tous les items, ou `@group-adjacent`.

- groupement par valeur
- groupement par position

### Result Documents

- multiple Res

### XSLT et W3C Schema Types

http://www.w3.org/TR/xmlschema-1/ 

- Using namespaces in XSLT 2.0
- The XSLT 2.0 type system in more detail
- Declaring types for variables and parameters
- Using schemas with XSLT 2.0

### Considerations for upgrading stylesheets

- Backward compatibility concerns
- Removing extension functions
- Ten easy simplifications
- Performance considerations

## Remarques générales sur le langage

> Although XSLT is based on functional programming ideas, it is not as yet a full functional programming language, as it lacks the ability to treat functions as a first-class data type.

- @bib Kay, Michael. 2001. « What Kind of Language Is XSLT? » IMB Developer. 1 février 2001. http://www.ibm.com/developerworks/library/x-xslt/index.html.

Noter toutefois l’existence d’une librairie développée par Dimitre Novatchev pour la programmation fonctionnelle avec XSLT.

Cette question est par ailleurs résolue avec la version 3.0 du langage qui introduit un usage large des fonctions ainsi que des fonctions d’ordre supérieur.

- @bib Novatchev, Dimitre. 2003. « Functional programming in XSLT using the FXSL library ». Dans *Proceedings of Extreme Markup Languages*. Montreal. http://conferences.idealliance.org/extreme/html/2003/Novatchev01/EML2003Novatchev01.html.

## Bibliographie

- Tennison, Jeni. 2003. « What’s New In XSLT 2.0 ». https://www.jenitennison.com/xmleurope/WhatsNewInXSLT2.0.ppt
- Kay, Michael. 2008. *XSLT 2.0 and XPath 2.0: programmer’s reference*. 4th ed. Wrox programmer’s references. Indianapolis, IN : Wiley Pub.
- DuCharme, Bob. 2005. « The XPath 2.0 Data Model ». *XML.com* (blog). 2 février 2005. https://www.xml.com/pub/a/2005/02/02/xpath2.html.
- DuCharme, Bob. 2003a. « XSLT 2 and Delimited Lists ». *XML.com* (blog). 7 mai 2003. https://www.xml.com/pub/a/2003/05/07/tr.html.—. 2003b. « Regular Expression Matching in XSLT 2 ». *XML.com* (blog). 4 juin 2003. https://www.xml.com/pub/a/2003/06/04/tr.html.
- DuCharme, Bob. 2003c. « Transclusion with XSLT 2.0 ». *XML.com* (blog). 9 juillet 2003. https://www.xml.com/pub/a/2003/07/09/xslt.html.
- DuCharme, Bob. 2003d. « Writing Your Own Functions in XSLT 2.0 ». *XML.com* (blog). 3 septembre 2003. https://www.xml.com/pub/a/2003/09/03/trxml.html.
- DuCharme, Bob. 2003e. « Datatype Checking With XSLT 2.0 ». *XML.com* (blog). 1 octobre 2003. https://www.xml.com/pub/a/2003/10/01/tr.html.
- DuCharme, Bob. 2003f. « Grouping With XSLT 2.0 ». *XML.com* (blog). 5 novembre 2003. https://www.xml.com/pub/a/2003/11/05/tr.html.
- Toro, Max. 2015. « Deep-Skip in XSLT 2.0 - Maxtoroq ». 6 novembre 2015. https://maxtoroq.github.io/2015/11/deep-skip-in-xslt-2.html.

## Références

- https://www.w3.org/TR/xpath-datamodel