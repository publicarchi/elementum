---
author: emchateau
tags: python, networks, outils
---

# Network analysis with Python

Artur Krochin. [Network Analysis in Python: Getting Started](https://app.pluralsight.com/courses/d4fc1424-3e22-42a6-96c2-ea904e3efe66/table-of-contents)

Science des réseau vs graph theory

Qu’est-ce que NetworkX

Manipulation de réseau avec NetworkX

Théorie des graphes avec NetworkX

Accéder et modifier des nœuds

## Science des réseau vs graph theory

## Qu’est-ce que NetworkX

## Manipulation de réseau avec NetworkX

## Théorie des graphes avec NetworkX

## Accéder et modifier des nœuds



## Quelques conseils

https://www.slideshare.net/LaurentBeauguitte/analyse-de-rseaux-en-sciences-sociales

- visualiser autrement (distribution des degrés, matrice bloquée)
- zoomer sur les lieux denses
- passer du graphe à l’égo-network
- visualisation mixte graphe-matrice (logiciel Node Trix)

## Remarques générales sur le projet eXperts

Sans doute un réseau social du point de vue de la carrière et des liens familiaux. Malheureusement les sources ne permettent pas toujours de renseigner les relations entre experts. Nous avons en fait surtout une communauté d’acteurs qui peut interagir dans le cadre de sa pratique. C’est la raison pour laquelle de ce point de vue les affaires traitées sont importantes. Les experts sont en liens avec des affaires qui peuvent être caractérisées et typologies, et ces affaires constituent en quelque sorte le liens des experts entre eux.

Même si toute forme de vie sociale peut être considérée comme un réseau, caractériser de manière évidente les deux populations d’experts et d’architectes ne sera pas possible au seul moyen de l’analyse de réseau. Toutefois, cette méthodologie peut offrir un regard complémentaire et particulièrement utile pour caractériser la structuration du secteurs.

pertinence de la démarche

choix des indicateurs

formattage des données.

> Trois grands obstacles sont fréquemment évoqués par les chercheurs en histoire débutant en analyse de réseau : l’incomplétude des données ; la nature non réticulaire du phénomène observé (avec l’argument d’autorité 􏰀 Ceci n’est pas un vrai réseau 􏰁) et enfin la complexité propre à l’analyse de réseau. (Beauguitte 2016, p. 20-21)

--> « Il est pourtant possible de considérer l’analyse de réseaux comme une boîte à outils méthodologiques susceptible d’éclairer de nombreuses thématiques de recherche, que celles-ci portent ou non sur de 􏰀 vrais réseaux. »

C’est donc en complémentarité que nous envisageons son emploi.

Quantitatif, mais aussi **formalisation**.

Rôle de la visualisation qui joue sans doute un rôle non négligeable dans la popularité qu’a connue ce type d’analyse. Si la visualisation de réseau sous la forme de projection dans un plan des liens et des sommets présente un intérêt non négligeable du point de vue de l’exploration ou de la communication, il nous semble que notre approche requiert plutôt de privilégier le recours à des mesures quantitatives. Les phénomènes que l’on cherche à observer (@todo les lister) se prêtent relativement mal à la visualisation.

--> distinguer visualisation exploratoire et communicationnelle. Choix de travailler des légendes

--> privilégier quanti et mesures pour l’étude du phénomène étudié à l’instar des physiciens qui utilisent d’autres types de graphiques a􏰄fin de révéler les propriétés des réseaux étudiés comme la distribution des degrés en en traçant la courbe pour déterminer si le réseau est ou non sans échelle, etc.

> Un réseau sans échelle se caractérise par une très forte hiérarchie de degré des sommets : quelques sommets ont un degré très élevé, la très grande majorité a un degré très faible. Le degré moyen n’a donc pas de sens pour un tel réseau, d’où l’appellation de réseau sans échelle (scale-free).



## Références

On trouvera un rappel utile des limites liées au recueil des données en analyse des réseaux sociaux dans M. HENNIG, U. BRANDES, J. PFEFFER et I. MERGEL, Studying Social Networks. A Guide to Empirical Research, Campus Verlag, 2012 ainsi que la présentation des moyens utilisés pour limiter les biais dans C. BIDART, A. DEGENNE et M. GROSSETTI, La vie en réseaux. Dynamique des relations sociales, Paris, PUF, 2011.

J. BERTIN, 1967, Sémiologie graphique. Les diagrammes - Les réseaux - Les cartes, Paris, Éditions Gauthier-Villar, 1967.

\40. E.R. TUFTE, The Visual Display of Quantitative Information, Cheschire, Graphics Press, 1983

> l'excellence graphique est une présentation bien conçue des don- nées d'intérêt [...], [elle] vise à communiquer des idées complexes avec clarté, précision et e􏰆cacité ; [elle] est ce qui donne au lecteur le plus grand nombre d'idées dans le temps le plus court, tout en utilisant le moins d'encre sur un minimum d’espace. (Tufte, p. 51)