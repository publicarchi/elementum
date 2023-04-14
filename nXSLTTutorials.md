---
since: 2020-05-19
tags: xslt, guides
---

# Guide XSLT

## Qu’est-ce que XSLT ?

[librement adapté de la spécification]

Une transformation est exprimée sous la forme d’une feuile de style (stylesheet). Une feuille de style est constituée d’un ou plusieurs doucments XML bien formés ses conformant à la spécification sur les espaces de noms.

Une feuille de style, inclue généralement un mélange d’élémenst définis par XSLT placés dans l’espace de nom de XSLT `http://www.w3.org/1999/XSL/Transform` et un mélange d’autres éléments.

Le terme feuille de style reflète le fait que XSLT est destiné à ajouter des informations de stylage à des documents sources XML en les transformant en un document consistant de XSL formating objects (XSL-FO) ou dans un autre format de présentation comme HTML, XHTML, ou SVG. Cependant XSLT est également employé pour toutes sortes de tâche de transformation, et pas seulement dans des buts de formattage ou d’applications de présentation.

Une transformation exprimée en XSLT décrit des règles pour transformer les données en entrée en données de sortie. Ces données sseront toute des instances du XDM data model. Dans le cas le plus simple et le plus commun, l’entrée est un document XML désigné arbre source (source tree), la sortie est un document XML appelé abre résultat (result tree). Il est également possible de traiter plusieurs documents sources ou de générer plusieurs documents résultats et de traiter d’autres formats que XML.

La transformation est réalisée au moyen d’un ensemble de **règles modèles (template rules)**. Un règle modèle associe un **motif (pattern)** qui correspond typiquement à des nœuds dans le document sources, avec un **constructeur de séquence (sequence constructor)**. Dans la plupart des cas, le constructeur de séquence provoquera la cosnrtuction de nouveaux nœuds qui peuvent faire partie d’un **arbre résultat (result tree)**. La structure de l’arbre résulatt peut être complètement différente de la structure des arbres sources. Lors de la construction d’un abre résultat, les nœuds des arbres sources peuvent être filtrés et réordonnés, et des structures arbritraires peuvent être ajoutées. Ce mécanisme permet à une feuille de style d’être applicable à une large classe de documents qui présentent des structures sources similaires.

Les **feuilles de style (stylesheets)** on une structure modulaire ; elles peuvent contenir plusierus package développés indépendamment les uns des autres, et chaque package peut cosntitué en plusieurs modules de feuilles de style.

- [Definition: un **motif (pattern)** spécifie un ensemble de conditions sur un item. Un item qui satisfie les conditions matche le motif ; un item qui ne satisfait pas les conditions ne matche pas.]
  Il existe deux types de motifs :
  - Un **motif de prédicat (predicate pattern)** est écrit sous la forme d’un point `.` suivi par un ou plusieurs prédicats entre crochets et matche n’importe quel item pour lesquels chaque prédicat est évalué vrai `true`.
    Cette construction peut être employée pour matcher des items de n’importe quel type (nœud, valeur atomique, ou un item de fonction).
  - un **motif de sélection (selection pattern)** utilise un sous-ensemble de la syntaxe des expressions de chemin (path expressions), et il est défini pour matcher un nœud dans l’expression de chemin correspondante qui sélectionne le nœud. Les motifs de sélection peuvent aussi être formés en combinaison d’autres motifs utilisant l’union, l’intersection et différents opérateurs.
- [Definition: un **constructeur de séquence (sequence constructor)** est une séquence de zéro ou plusieurs nœuds adjascents dans la feuille de style qui peuvent être évalués pour retourenr une séquence de nœuds, des valeurs atomiques, ou des items de fonction.

## Nouveautés de XSLT 3.0

- Streaming

  - `xsl:source-document`
  - mode
  - `xsl:iterate`
  - `xsl:merge`
  - `xsl:fork`
  - accumulators

- une instruction `xsl:evaluate` instruction qui permet l’expression d’expressions XPath qui sont construites de manière dynamique ou lue depuis un document source ;

- des améliorations de la syntaxe des motifs qui permettent notamment les valeurs atomiques comme les nœuds ;

- une instruction `xsl:try` qui permet de retrouver des erreurs dynamiquement ;

- l’élément `xsl:global-context-item` pour la délcation les attendus d’une feuille de style

- une nouvelle instruction `xsl:assert` pour assister les dévelopeurs dans la production de code robuste.

- XSLT 3.0 apporte également les améliorations instroduites dans le langage XPath et la librairie de fonctions standard.

  - variables peuvent être liées dans une expression XPath avec la clause `let`
  - les fonctions sont des citoyens de première classe, elle peuvent être passées comme arguments d’autres fonctions
  - de nombreuses nouvelles fonctions sont disponibles dont `parse-xml` et `serialise` pour convertir des représentations lexicales et des arbres.
  - support des maps.

  cf. https://www.w3.org/TR/xslt-30/#changes-since-2.0

# Tutoriaux XSLT 2.0

David J. Birnbaum http://dh.obdurodon.org  

http://ebeshero.github.io 

Walmsley, Priscilla. 2010. « Getting the Most out of XSLT 2.0 ». XML Summer School. http://www.datypic.com/services/xslt/getting-most-out-of-xslt2.pdf. 

—. s. d. « Exploring the New Features of XSLT 2.0 ». http://www.datypic.com/services/xslt/xslt-new-in-2.0.pdf. 

Walmsley, Priscilla. 2012. « Adding Structure to Content Using XSLT 2.0 ». présenté à XML summer school. http://www.datypic.com/services/xslt/adding-semantics2.pdf. 

Tennison, Jeni. 2003. « What’s New In XSLT 2.0 ». https://www.jenitennison.com/xmleurope/WhatsNewInXSLT2.0.ppt 

DuCharme, Bob. 2003. « Regular Expression Matching in XSLT 2 ». XML.com (blog). 4 juin 2003. https://www.xml.com/pub/a/2003/06/04/tr.html. 

DuCharme, Bob. 2005. « The XPath 2.0 Data Model ». XML.com (blog). 2 février 2005. https://www.xml.com/pub/a/2005/02/02/xpath2.html. 

DuCharme, Bob. 2003. « Regular Expression Matching in XSLT 2 ». *XML.com* (blog). 4 juin 2003. https://www.xml.com/pub/a/2003/06/04/tr.html.

DuCharme, Bob. 2002. « Splitting and Manipulating Strings ». *XML.com* (blog). 1 mai 2002. https://www.xml.com/pub/a/2002/05/01/xslt-string.html.

Gregorio, Joe. 2003. « Regex-able Xml ». *BitWorking* (blog). 25 février 2003. https://bitworking.org/news/2003/02/40.

Walmsley, Priscilla. 2011. « Adding Structure and Semantics with XSLT 2.0 - Transforming Unstructured Narrative Content to Structured, Feature-Rich XML », 16. http://www.datypic.com/services/xslt/xslt-article1.html.

—. 2012. « Adding Structure to Content Using XSLT 2.0 ». présenté à XML summer school. http://www.datypic.com/services/xslt/adding-semantics2.pdf.

Wilmott, Sam. s. d. « Regular Expressions in XSLT 2.0, XQuery 1.0 and XPath 2.0 ». Mulberry. http://www.mulberrytech.com/quickref/regex.pdf.

## Tutoriaux XSLT 3.0

> declarative (functional) tree transformation language with referential transparency and implicit dispatch

- Quin, Liam. s. d. « Exciting new features in XSLT 3 for book publishers ». *BookNet Canada*. Consulté le 4 novembre 2019. https://www.booknetcanada.ca/blog/2019/1/9/exciting-new-features-in-xslt-3-for-book-publishers.
- Liam Quin. XSLT 3: Clearer, faster, wider, stronger, https://youtu.be/p8087hIYX2M
- https://archive.xmlprague.cz/2017/files/presentations/prague-w3c.pdf
- http://www.datypic.com/services/xslt/whatsnew3.html
- Kosek, Jirka. 2019. « XSLT 3.0 for Daily Coding ». présenté à XML SummerSchool, Oxford. https://www.kosek.cz/xml/2019xmlss/Kosek_XSLT4DailyCoding.pdf.
- Walmsley, Priscilla. 2015. *XQuery: Search across a Variety of XML Data*. Second edition. Sebastopol, CA : O’Reilly Media.

## Tutoriaux XQuery

- XQuery for the humanist, https://github.com/CliffordAnderson/XQuery4Humanists 
- Adam Rester. XQuery is the Plumber's Toolkit! https://youtu.be/dUtyE50igbA