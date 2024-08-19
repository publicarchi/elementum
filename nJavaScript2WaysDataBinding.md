---
since: 2017-07-07
author: emchateau
tags: javascript
---

# Two-way data binding

Le liage bi-directionnel de données consiste à lier une vue et la partie logique d’une application. En d’autres termes des éléments du code HTML sont liés au contrôleur JavaScript.

Avoir un objet JavaScript donné *x* avec une propriété *y* et un élément DOM `<input>` par exemple. Lorsque l’élément DOM change, *x* change et vice-et-versa. En ce sens le lien est bi-directionnel.

![two way data binding](https://i.stack.imgur.com/hu1ps.png)



```javascript
var x = { y : 3};
```

```html
<input type='text' value=''><input>
```

- Comment lier les objets
- Comment écouter les modifications des formulaires

### Une abstraction pour mettre à jour les deux objets

Avoir un DOM qui fait référence à l’élément DOM concerné, et présente une interface qui coordonné les mises à jour avec ses propres données et ses éléments.

`.addEventListener()` offre une belle interface pour faire cela. On peut lui donner un objet qui implémenter l’interface de `eventListener` et il invoquera ses handlers avec cet objets comme valeurs `this`.

### Définir son objet

L’héritage prototype est une manière commode d’implémenter cela, même si elle n’est pas requise. On construit d’abord un constructeur qui reçoit l’élément et des données initiales.

```javascript
function myConstructor(element, data) {}
  this.data = data;
  this.element = element;
  element.value = data;
  element.addEventListener('change', this, false);
```

Ici, le constructeur stocke l’élément et les données dans les propriétés d’un nouvel objet. Il lie également un événement `change` à un élément donné. Chose intéressante, il passe le nouvel objet au lieu d’une fonction comme deuxième argument.

### Implémenter l’interface de `eventListener`

Pour fonctionner, votre objet nécessite encore l’implémentation de l’interface `eventListener`. Pour cela, il est simplement nécessaire de donner à l’objet une méthode `handleEvent()`.

```javascript
myConstructor.prototype.handleEvent = function(event) {
  switch (event.type) {
    case 'change': this.change(this.element.value);
  }
};

myConstructor.prototype.change = function(value) {
  this.data = value;
  this.element.value = value;
}
```

Il y a de multiples manières de structurer cela, mais pour l’exemple, on a ici choisi que la méthode `change()` accepte seulement une valeur et que ce soit `handleEvent` qui lui passe la valeur au lieu de l’objet event. De la sorte, `change()` peut également être invoquée sans un event.

Dès lors qu’un événement `change` intervient, cela met à jour à la fois l’élément et la propriété `.data`. La même chose arrive en appellent `.change()` dans le programme JavaScript.

### Utiliser le code

Pour faire fonctionner cela, il suffit maintenant de créer un nouvel objet et de le laisser faire les mises à jour. Celles ci apparaîtront dans l’élément input et autant des événement change qui seront visibles dans le code JavaScript.

```javascript
var obj = new myConstructor(document.getElementById("foo"), "20");

// simulate some JS based changes.
var i = 0;
setInterval(function() {
    obj.change(parseInt(obj.element.value) + ++i);
}, 3000);
```



## Librairies

https://github.com/remy/bind.js

https://github.com/eddyystop/CrazyGlue (JQuery)

https://www.sellarafaeli.com/jabjs/

https://github.com/gwendall/way.js

## Référence

https://stackoverflow.com/questions/16483560/how-to-implement-dom-data-binding-in-javascript

https://www.sellarafaeli.com/blog/native_javascript_data_binding

https://gist.github.com/austinhyde/4321f22a476e1cbee65f

https://namitamalik.github.io/2-way-data-binding-in-Plain-Vanilla-JavaScript/

