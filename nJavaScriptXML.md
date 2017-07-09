---
since: 2017-07-04
author: emchateau
tags: xml, javascript
---

## Manipuler du XML en JavaScript

Le DOM représente un document XML comme un arbre de nœuds. Le DOM définit plusieurs types de nœuds correspondants aux différentes constructions XML. Par exemple, un éléments XML est un élément nœud (`node`), une valeur d’attribut XML est un nœud attribut, le contenu d’un élément est un nœud texte, etc. Dans le modèle DOM, les nœuds  ont une relation hiérarchique parent/enfant et peuvent être frères (`sibling`). Tous les nœuds dans un modèle DOM sont des enfants directs, ou indirects, du document nœud.

Les interfaces DOM utilisent le concept d’héritage de la programmation orienté-objet. Les différents types de nœuds, tels que les éléments nœuds, les nœuds attributs, les nœuds textes, etc., héritent d’une interface générique appelée `Node`. La structure arborescente du DOM est orientée objet, ce qui signifie que les différents nœuds ne sont pas simplement des structures de données. Chaque nœud est un objet qui contient à la fois des données et des méthodes pour manipuler l’objet. Pour un nœud donné, on peut donc appeler ses méthodes pour obtenir une liste des ses nœuds éléments enfants. D’un élément enfant, on peut également appeler des méthodes pour descendre dans l’arbre du nœud. Il est ainsi possible de traverser l’ensemble du document DOM.

La spécification DOM définit une interface programmable pour ces différents types de nœud et expose leur fonctionnalité. À l’aide de ces interfaces programmables, il est possible de réaliser l’ensemble des traitements nécessaires sur le XML.

Le DOM a été développé en deux niveau, Level 1 et Level 2. Le Level 1 inclut les fonctionnalités de base pour le traitement de document XML

### Utilisation du DOMParser

```javascript
function parseXml(xml) {
   var dom = null;
   if (window.DOMParser) {
      try { 
         dom = (new DOMParser()).parseFromString(xml, "text/xml"); 
      } 
      catch (error) { dom = null; }
   }
   else
      alert("cannot parse xml string!");
   return dom;
}
```

Builder

```javascript
var xml = '<e name="value">text</e>',
    dom = parseXml(xml);
```



http://goessner.net/download/prj/jsonxml/

http://www.xml.com/pub/a/2006/05/31/converting-between-xml-and-json.html

## Références

[DOM for Web Services, Part 1](http://www.xml.com/pub/a/ws/2003/10/14/dom.html)

http://goessner.net/download/prj/jsonxml/

http://www.xml.com/pub/a/2006/05/31/converting-between-xml-and-json.html



[Parsing and serializing XML, MDN](https://developer.mozilla.org/en-US/docs/Web/Guide/Parsing_and_serializing_XML)

https://andrew.stwrt.ca/posts/js-xml-parsing/

http://www.dummies.com/web-design-development/html/how-to-load-xml-with-javascript-on-an-html5-page/

https://davidwalsh.name/convert-xml-json

XMLDocument object

https://visionmedia.github.io/superagent/

https://teamtreehouse.com/community/how-to-pull-data-from-am-xml-file-and-show-it-on-html-table

https://www.w3schools.com/xml/dom_intro.asp

https://github.com/yaronn/xpath.js

https://help.xmatters.com/xPert/xmodwelcome/integrationbuilder/xml-manipulation.htm