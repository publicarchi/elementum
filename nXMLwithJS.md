# XML alternatif

L’utilisation du langage de balisage XML et des technologies associées sont depuis quelques années en perte de vitesse. Alors que la technologie et ses langages associés ont connu des évolutions significatives ces dernières années, hormis les personnes acquises à la cause qui travaillent en environnement Java avec des outils dédiés, peu d’utilisateurs emploient ces dernières versions en l’absence de processeur dans d’autres environnements plus communs. Le portage récent de XSLT en C++ effectué par Michael Kay n’a pas suffit à renouveler l’intérêt pour ce langage. Aussi, peut-on sérieusement s’interroger sur l’avenir de ces technologies alors même qu’elles répondent particulièrement bien à un cas spécifique qui est celui de l’encodage du texte.

Ce nouveau contexte, avec le vieillissement des personnes qui ont largement été les protagonistes de la révolution XML, nécessite de réfléchir à des alternatives ou de nouvelles solutions pour travailler des textes balisés.

## Utiliser JavaScript pour manipuler du XML

Si XSLT et XQuery sont tous deux des langages particulièrement puissants et bien adaptés pour manipuler des données XML, de moins en moins d’informaticiens connaissent et apprécient ces langages. Dès lors, dans certains projets, envisager la manipulation des fichiers XML par le langage JavaScript peut s’avérer pertinente. JavaScript est devenu un des langages les plus employés et il est devenu de plus en plus puissant ces dernières années.

Travailler sur le DOM, avec XML Dom.

Parser du XML avec JavaScript

- https://andrew.stwrt.ca/posts/js-xml-parsing/ avec seulement Lodash comme dépendance, mais ne traite pas les contenus mixtes
- https://github.com/danmactough/node-feedparser mais dépendance absente dans le browser

Exemple de manipulation de XML-TEI dans le browser avec JavaScript

https://github.com/TEIC/CETEIcean

Angular et XML

[Angular-XML](https://github.com/johngeorgewright/angular-xml)

http://rabidgadfly.com/2013/02/angular-and-xml-no-problem/

http://plnkr.co/edit/QmwPeGI6s2TKHsksSLiC?p=info

http://www.amitavroy.com/justread/content/articles/working-xml-angular-js/



## Baliser sans XML

XML est avant tout un langage de balisage qui permet de produire des documents structurés. Son modèle de contenu qui permet de décrire des structures séquentielles est particulièrement bien adapté pour traiter le texte qui peut être modéliser comme un modèle de contenu hiérarchiquement ordonné.

Alors que le W3C avait imposé la syntaxe XML pour le HTML au milieu des années 2000, l’offensive conduite par l’industrie pour renoncer à cette syntaxe et l’adoption de HTML5 ont en grande partie marqué la défaite de XML. Toutefois, le W3C a produit récemment une spécification pour des documents polyglottes qui pourrait faire revenir XML. 

Dans le même temps, les limites de HTML5 pour le balisage des textes sont patentes, et d’une certaine manière le travail conduit autour des Web components consiste à réinventer XML.

Les Web components introduisent dans HTML5 une API permettant de définir ses propres éléments en les spécifiant de manière déclarative (*custom elements*). Le *Shadow DOM* permet d’encapsuler les éléments personnalisés dans la hiérarchie. Les *Templates* permettait de stocker les données dans un document HTML sans être interprétés. Enfin HTML Imports permettait d’importer d’autres documents HTML dans le document courant.

En revanche, il ne semble pas qu’aucune technologie de schema pour contrôler la consistance ait été implémentée.

https://github.com/alexmilowski/duckpond

## Sources

Critiques récentes de XML :

- https://norman.walsh.name/2016/05/28/non-standard
- http://www.milowski.com/journal/entry/2016-06-17T16:54:00-08:00/

az

