---
author: emchateau
since: 2017-07-01
tags: javascript, ajax, histoire de l’internet
---

# Ajax avec Javascript

## Court historique

La programmation dite *asynchrone* a révolutionné le développement des applications web. En effet, l’architecture informatique dite Ajax pour *Asynchronous JavaScript + XML* a permis de construire des sites web dynamiques interactifs fonctionnant côté-client en utilisant les technologies disponibles dans les navigateurs (CSS, JSON, XML, le DOM et XMLHttpRequest). Cette terminologie a été introduite dans un article publié sur *Adaptive Path* par Jesse James Garrett le 18 février 2005 (2005). En 2006, Jesse James reçu le Rave Award for Technology du *Wired Magazine*, son rôle important dans le domaine a été souligné dans plusieurs publications comme *The New York Times*, *The Wall Street Journal* et *BusinessWeek*. Toutefois, comme le faisait remarquer Jesse en 2005, Ajax ne désigne pas une technologie en tant que telle mais plutôt la réunion d’un ensemble de technologies dont la convergence représentait un tournant dans ce qu’il était désormais possible de proposer aux utilisateurs sur le web. Les nombreuses interactions côté clients proposées par Google Suggest ou Google Map étaient alors caractéristiques de ce que l’on désignait alors comme des applications internet riches (*Rich Internet Applications*).

Ainsi, Ajax (Asynchronous JavaScript + XML) implique

- l’utilisation de présentation basées sur les standards avec XHTML et CSS
- la présentation dynamique et interactive des contenus avec le Document Object Model
- l’échange de données et leur manipulation avec XML et XSLT (à l’époque avec LibXML)
- la réception de données asynchrone en utilisant XMLHttpRequest
- et l’emploi de JavaScript pour lier l’ensemble

La généralisation de la bibliothèque JQuery créée en 2006 par John Resig va faciliter l’adoption de ces techniques de développement web. Depuis quelques années, on tend de plus en plus à parler de XHR, abréviation de la fonction JavaScript dédiée `XMLHttpRequest`. Cette fonctionnalité est prise en charge par la plupart des frameworks JavaScript et réside au cœur de la conception des *Single page applications*. La nouvelle fonction `fetch()` de JavaScript a rendu l’utilisation de ces requêtes asynchrones plus aisées mais en renonçant au parsing de XML. Des fonctionnalités comme le *streaming* se sont depuis ajouter à ces techniques.

## Une manière moderne

Pendant longtemps, il était nécessaire d’écouter pour `readystatechange`, mais la plupart des navigateurs modernes supportent aujourd’hui les événements `load`, `abort`, `progress` et `error` pour `XMLHttpRequest`. De même, la plupart des tutoriaux proposaient des traitements spécifiques pour Internet Explorer 10 (window.ActiveXObject), celui-ci n’étant presque plus utilisé, ils s’avèrent inutiles.

On peut remplacer le nombre magique 4 par XMLHttpRequest.DONE

[XMLHttpRequest, Living Standard — Last Updated 15 June 2017](https://xhr.spec.whatwg.org/#xmlhttprequestresponsetype)

## En utilisant seulement ES6/ES2015

```javascript
function get(url) {
  // Return a new promise.
  return new Promise(function(resolve, reject) {
    // Do the usual XHR stuff
    var req = new XMLHttpRequest();
    req.open('GET', url);
    req.onload = function() {
      // This is called even on 404 etc
      // so check the status
      if (req.status == 200) {
        // Resolve the promise with the response text
        resolve(req.response);
      }
      else {
        // Otherwise reject with the status text
        // which will hopefully be a meaningful error
        reject(Error(req.statusText));
      }
    };
    // Handle network errors
    req.onerror = function() {
      reject(Error("Network Error"));
    };
    // Make the request
    req.send();
  });
}
```

Cette fonction retourne une `promise`. Voici un exemple d’utilisation de la fonction et de sa réponse.

```javascript
get('story.json').then(function(response) {
  console.log("Success!", response);
}, function(error) {
  console.error("Failed!", error);
})
```

Pour charger un fichier JSON, il est possible d’employer la fonction `JSON.parse()` pour convertir les données téléchargées en un objet JavaScript. On pourrait aussi intégrer la `req.responseType='json'` dans la fonction, mais cela n’est malheureusement pas supporté par IE.

voir https://developers.google.com/web/fundamentals/getting-started/primers/promises

voir https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

avec `async` et `wait` (EcmaScript 2017) https://stackoverflow.com/questions/14220321/how-do-i-return-the-response-from-an-asynchronous-call/16825593#16825593

## Utilisation de la méthode `fetch()`

Les nouveaux navigateurs supportent nativement la méthode `fetch()` qui présente une API plus commode. Toutefois la méthode n’est pas supportée par Internet Explorer. Elle ne l’est que récemment par beaucoup de navigateurs (à date, juillet 2017).

Plusieurs contournements sont cependant possibles :

-  utiliser le Polyfill [A window.fetch JavaScript polyfill](https://github.github.io/fetch/) en pointant vers le script `<script src="https://cdn.rawgit.com/github/fetch/master/fetch.js"></‌script>`

```javascript
var opts = {
  method: 'GET',
  body: 'json',
  headers: {}
};
fetch('/get-data', opts).then(function (response) {
  return response.json();
})
.then(function (body) {
  //doSomething with body;
});
```

cf. https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch

https://github.com/mdn/fetch-examples/

https://davidwalsh.name/fetch

<https://caniuse.com/#search=fetch()>

```javascript
// Chaining for more "advanced" handling
fetch('http://localhost:8984/gdp/bibliography/items/sauval1724', {
	method: 'get',
  	redirect: 'follow',
	headers: new Headers({
		'Content-Type': 'text/html'
	}
}).then(function(response) {
	return response.json(); // pour récupérer du json
}).then(function(returnedValue) {
	// Yay, `j` is a JavaScript object
	console.log(returnedValue); 
}).catch(function(err) {
	// Error :(
    console.log(err);
});
```



```javascript
/**
 * Fetch JSON API
 * @return an asynchrous request with Promise
 * @rmq [Fetch API polyfill](https://github.com/github/fetch) for IE
 * @see https://developers.google.com/web/updates/2015/03/introduction-to-fetch
 */

function status(response) {  
  if (response.status >= 200 && response.status < 300) {  
    return Promise.resolve(response)  
  } else {  
    return Promise.reject(new Error(response.statusText))  
  }  
}

function json(response) {  
  return response.json()  
}

fetch('http://localhost:8984/gdp/bibliography/items/sauval1724', {
  method: 'get',
  redirect: 'follow',
  headers: new Headers({
    'Content-Type': 'text/json'
  })
})
  .then(status)
  .then(json)
  .then(function(data) {
    console.log('Request succeeded with JSON response', data);
  })
  .catch(function(Error) {
  console.log('Request failed', Error);
});
```



Il n’existe pas de parseur natif pour XML avec `fetch()`, on peut alors utiliser un outil tiers ou bien le DOMParser natif (IE>9). 

ou bien méthode load de l’objet XMLDocument

L’absence de support de XML avec fetch() plaide en partie pour l’utilisation d’un templating avec JSON.

```javascript
function getCurrentCity(location) {
	const lat = location.coords.latitude;
	const lon = location.coords.longitude;
	return fetch(apis.currentWeather.url(lat, lon))
    	.then(response => response.text())
	    .then(str => (new window.DOMParser()).parseFromString(str, "text/xml"))
    	.then(data => console.log(data))
 }
```
}

## Utilisation de l’API history

cf. https://css-tricks.com/rethinking-dynamic-page-replacing-content/

```javascript
history.pushState(stateObject, "title", URL);
```

## Datalist

https://dzone.com/articles/example-dynamic-html5-datalist

https://developer.mozilla.org/en-US/docs/Introduction_to_using_XPath_in_JavaScript

## Bibliothèques JavaScript

http://youmightnotneedjquery.com

### Classe minimale

https://github.com/jakecyr/Slim-Http-JavaScript-Object

### Axios

Dépendance mais minimale et centrée sur AJAX. Axios s’inspire directement du service \$http d’Angular. Côté serveur et navigateur, promise API, pas de stream.

387KB

https://github.com/mzabriskie/axios

https://www.npmjs.com/package/axios

### Got

> Simplified HTTP requests

côté serveur, compatible avec électron

245KB, cf. comparatif avec Axios

https://github.com/sindresorhus/got

### SuperAgent

> Ajax with less suck - (and node.js HTTP client to match)

http://visionmedia.github.io/superagent/

### MicroJS

2011-2017

http://microjs.com/#ajax

### fetchival.js

https://github.com/typicode/fetchival

### Microajax

Tiny AJAX library

[Microajax](https://code.google.com/archive/p/microajax/)

### Nanoajax

> An ajax library you need a microscope to see

https://github.com/yanatan16/nanoajax

### MajaX

> majaX stands for micro asynchronous javascript and X

http://cdn.simon.waldherr.eu/projects/majaX/

### Ajax

Standalone AJAX library inspired by jQuery/zepto [https://component.jit.su/ForbesLindes…](https://component.jit.su/ForbesLindesay/ajax)

https://github.com/ForbesLindesay/ajax

### Reqwest

> browser asynchronous http requests

https://github.com/ded/Reqwest

### Zeptojs

> **Zepto** is a minimalist **JavaScript library for modern browsers** with a largely **jQuery-compatible API**. *If you use jQuery, you already know how to use Zepto.*

http://zeptojs.com

## Frameworks

### Mithril

> Mithril is a modern client-side Javascript framework for building Single Page Applications. It's small (< 8kb gzip), fast and provides routing and XHR utilities out of the box.

https://mithril.js.org

https://scrimba.com/c/cast-1746

### Riot.js

Simple and elegant component-based UI library

http://riotjs.com

### VueJs

https://forum.vuejs.org/t/vue-2-0-and-ajax-calls/75/17

Nota vue-ressource est le plugin qui fournit les services pour les XMLHttpRequest sur JSONP

https://github.com/pagekit/vue-resource/blob/HEAD/docs/api.md, https://www.npmjs.com/package/vue-resource

cf. https://stackoverflow.com/questions/50833398/how-to-import-a-local-stored-xml-file-in-vue-and-edit-it

### Cycle.js

> A functional and reactive JavaScript framework for predictable code

https://cycle.js.org

### Redux

http://redux.js.org

## Ressources

- http://ajaxpatterns.org (dead)
- https://css-tricks.com/rethinking-dynamic-page-replacing-content/
- https://es5.github.io

## Bibliographie

- Garret, James (2005). Ajax: A New Approach to Web Applications. Adaptive path, 18 février 2005. <http://adaptivepath.org/ideas/ajax-new-approach-web-applications/>