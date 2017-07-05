---
author: emchateau
since: 2017-07-01
tags: javascript, ajax
---

# Ajax avec Javascript

## Ajax

La programmation dite asynchrone a révolutionné le développement d’application web. L’architecture informatique dite Ajax pour *Asynchronous Javascript and Xml* a permis de construire des applications web et des sites web dynamiques interactifs fonctionnant côté client en utilisant les technologies disponibles dans les navigateurs (CSS, JSON, XML, le DOM et XMLHttpRequest). Cette terminologie a été introduite dans un article publié sur *Adaptive Path* par Jesse James Garrett le 18 février 2005.

## Une manière moderne

Pendant longtemps, il était nécessaire d’écouter pour `readystatechange`, mais la plupart des navigateurs modernes supportent aujourd’hui les événements `load`, `abort`, `progress` et `error` pour `XMLHttpRequest`. De même, la plupart des tutoriaux proposaient des traitements spécifiques pour Internet Explorer 10 (window.ActiveXObject), celui-ci n’étant presque plus utilisé, ils s’avèrent inutiles.

On peut remplacer le nombre magique 4 par XMLHttpRequest.DONE

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
    'Content-Type': 'text/html'
  })
})
  .then(status)
  .then(json)
  .then(function(data) {
    console.log('Request succeeded with JSON response', data);
  })
  .catch(function(error) {
  console.log('Request failed', error);
});
```

## Bibliothèques

### Microajax

Tiny AJAX library

[Microajax](https://code.google.com/archive/p/microajax/)

### Reqwest

browser asynchronous http requests

[Reqwest](https://github.com/ded/Reqwest)





## Ressources

- http://ajaxpatterns.org (dead)
- ​

