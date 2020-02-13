---
title: Templating
author: Emmanuel Château-Dutier
since: 2014-06-27
tags: basex, xquery, templating
---

# Templating

Un moteur de templating est une solution pour les développeurs pour interpoler des chaînes de caractères de manière efficace. L’utilisation d’un moteur de templating économise beaucoup de temps aux développeurs front-end JavaScript. Il existe un grand nombre de solutions disponibles actuellement.

## Note sur le templating avec BaseX

Diverses solutions peuvent être envisagées pour le templating avec BaseX :
- utilisation d’un map
- XRC comme template
- XQMVC
- Mustache.xq
- AngularJS

### Utilisation d’un map

https://gist.github.com/micheee/e053068a41eb35e727bb

### XQMVC

MVC (Model View Controller) est un modèle de conception qui promeut l’organisation du code et de la structure de fichiers en séparant la présentation de la partie logique. XQMVC est une proposition de cadre de travail pour produire des applications XQuery organisées d'après le modèle MVC.
https://code.google.com/p/xqmvc/

### Mustache

Une implémentation de Mustache en XQuery avec BaseX
https://github.com/dirkk/mustache.xq


Liens:

- [XQuery templating engines and TXQ](http://cubeb.blogspot.fr/2012/11/xquery-templating-engines-and-txq.html)

- [Discussion sur la liste eXist](http://exist.2174344.n4.nabble.com/eXist-MVC-and-separating-XHTML-templates-from-XQuery-code-td3460892.html#a3500028)

- [HTML Templating Module](http://exist-db.org/exist/apps/doc/templating.xml)

- [XQuery/Generating Skeleton Typeswitch Transformation Modules](http://en.wikibooks.org/wiki/XQuery/Generating_Skeleton_Typeswitch_Transformation_Modules)

## Templating avec Javascript

### Template-Engine-Chooser!

https://garann.github.io/template-chooser/

### JSX

JSX, une syntaxe déclarative comme XML qui fonctionne au sein de JavaScript

Utilisée par React mais aussi Vue (mais pas sa 1er)

https://reactjs.org/docs/introducing-jsx.html

### elm

https://elm-lang.org/

### Svelte

https://svelte.technology

https://ractive.js.org/

### Liquid

> Safe, customer-facing template language for flexible web apps.

Templating utilisé sur Jekyll

https://shopify.github.io/liquid/

### Hogan.js

> JavaScript templating from Twitter

http://twitter.github.io/hogan.js/

### HandlebarsJS

> Handlebars provides the power necessary to let you build semantic templates effectively with no frustration.

actif en 2017, basé sur Mustache

http://handlebarsjs.com

https://github.com/wycats/handlebars.js

### EJS

> Embedded JavaScript templating.

L’un des derniers moteurs de templating.

http://ejs.co

### Vue.js

https://fr.vuejs.org/v2/guide/syntax.html

### doT

> The fastest + concise javascript template engine for nodejs and browsers. Partials, custom delimiters and more. 
>

https://github.com/olado/doT

### KnockoutJs

> Knockout makes it easier to create rich, responsive UIs with JavaScript
>

(actif 2017)

- Pure JavaScript — works with any web framework
- Small & lightweight — 59kb minified

http://knockoutjs.com

### Pug (Jade)

> Pug – robust, elegant, feature rich template engine for Node.js 

https://pugjs.org

https://github.com/pugjs/pug

actif 2017, révision de Jade

### Jade

http://jade-lang.com

### UnderscoreJs

http://underscorejs.org

### JavaScript Templates

> 1KB lightweight, fast & powerful JavaScript templating engine with zero dependencies. Compatible with server-side environments like node.js, module loaders like RequireJS and all web browsers. [https://blueimp.github.io/JavaScript-…](https://blueimp.github.io/JavaScript-Templates/)

actif en 2017

https://github.com/blueimp/JavaScript-Templates

### Pure

https://beebole.com/pure/

https://github.com/pure/pure

### dustjs

> Asynchronous Javascript templating for the browser and server http://dustjs.com
>

https://github.com/linkedin/dustjs/

### ejs

http://ejs.co

### Embeddedjs

http://www.embeddedjs.com remplacé par https://donejs.com

### John Resig Micro-Templating

https://johnresig.com/blog/javascript-micro-templating/

### JST

http://blog.markturansky.com/BetterJavascriptTemplates.html

### Moon

https://kbrsh.github.io/moon/

### Liste

https://github.com/nje/jquery/wiki/jquery-templates-proposal

## Templating Python

https://wiki.python.org/moin/Templating

- string.Template
- mustache
- ctemplate-python

https://www.fullstackpython.com/template-engines.html

à comparer avec XSLT

## Nouveau ++

Svelte https://svelte.dev/

Sapper https://sapper.svelte.dev/

https://infernojs.org/

https://stenciljs.com/

https://preactjs.com/

## Sources

- https://en.wikipedia.org/wiki/JavaScript_templating

- https://sylvainpv.developpez.com/tutoriels/javascript/guide-templating-client/

- https://jonsuh.com/blog/javascript-templating-without-a-library/
