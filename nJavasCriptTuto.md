---
author: emchateau
tags: javascript
---

## Usage de JavaScript

historique

destination

## Définition d’une variable

```js
var exemple = 'emmanuel';
console.log(exemple);
```

Var déprécié, utiliser `let`

```js
let exemple = 'emmanuel';
console.log(exemple);
```

Constance

```js
const exemple = 'emmanuel';
console.log(exemple);
```

## Type de données

Définition d’une chaîne

```js
let firstname = "Emmanuel";
let surname = "Chateau";
console.log(exemple);
```

Concaténation

```js
let firstname = "Emmanuel";
let surname = "Chateau";
console.log(firstname + surname);
```

Possibilité de concatenner les chaînes avec les accolades

```js
let firstname = "Emmanuel";
let surname = "Chateau";
console.log(`${firstName} €{surname}`);
```

## Méthodes sur les chaînes

Une méthode est une fonction, un ensemble d’instructions. Les chaînes de JavaScript viennent avec un ensemble de méthodes qui détermine ce que va pouvoir faire avec.

Propriété de chine `length`

```js
let firstname = "Emmanuel";
let surname = "Chateau";
console.log(`     ${firstName} €{surname}`.length);
```

Propriété `trim`()

```js
let firstname = "Emmanuel";
let surname = "Chateau";
console.log(`     ${firstName} €{surname}`.trim().length);
```

Propriété `toUpperCase()`, `toLowerCase()`

```js
let firstname = "Emmanuel";
let surname = "Chateau";
console.log(`${firstName} €{surname}`.toUpperCase());
```

Propriété `split()`, le résultat est un array

Sur les espaces

```js
let firstname = "Emmanuel";
let surname = "Chateau";
console.log(`${firstName} €{surname}`.split(' '));
```

Sur tous les caractères

```js
let firstname = "Emmanuel";
let surname = "Chateau";
console.log(`${firstName} €{surname}`.split(''));
```

## Travail avec les nombres

On définit un nombre directement.

```js
var exemple = 7;
console.log(exemple);
```

Il n’y a qu’un type de nombre en javascript

```js
var exemple = 7.77;
console.log(typeof exemple);
```

Récupérer valeur entière

```js
var exemple = 7.77;
console.log(parseInt(exemple));
```

Transformer une chaîne en float

```js
var exemple = '7.77';
console.log(parseFloat(exemple));
```

Arrondir à n décimal

```js
var exemple = 7.77;
console.log(exemple.toFixed(2));
```

### Comportements spécifiques

```js
let exemple1 = parseInt('test 33 World 22');
let exemple2 = parseInt('33 World 22');
let exemple3 = parseFloat('44 Dylan 22');
let exemple4 = 55.3333.toFixed(0);
let exemple5 = 200.0.toFixed(2);

console.log(exemple1);
console.log(exemple2);
console.log(exemple3);
console.log(exemple4);
console.log(exemple5);
```

Résultats

- null
- 33
- 44
- 55
- 200.00

Types avec typeof

- number
- numbr
- string
- string

## Booléens

```js
let exemple1 = true;
let exemple2 = false;
console.log(Boolean(exemple1));
```

```js
let exemple1 = false;
let exemple2 = true;
let exemple3 = null;
let exemple4 = undefined;
let exemple4 = '';
let exemple4 = NaN;
let exemple4 = -5;
let exemple4 = 0;

console.log(Boolean(exemple1));
```

- false
- true
- false
- false
- false
- false
- true
- false

## Arrays

Instantiation

```js
let exemple1 = [5, 5, 6];
console.log(exemple1.length)
```

Arrays start on 0

```js
let exemple1 = [5, 5, 6];
console.log(exemple1[2])
```

20aine de méthodes disponibles sur les arrays

Ajouter une valeur avec la méthode `push()`

```js
let exemple1 = [5, 5, 6];
exemple1.push(3);
console.log(exemple1);
```

```js
let exemple1 = [5, 5, 6];
exemple1.push(3, 2, 4);
console.log(exemple1);
```

Retirer la dernière valeur avec `pop()`

```js
let exemple1 = [5, 5, 6];
exemple1.pop();
console.log(exemple1);
```

Mettre à jour une valeur d’index

```js
let exemple1 = [5, 5, 6];
exemple1.push(3, 2, 4);
exemple1[0] = 1;
console.log(exemple1);
```

Itérer sur les éléments de l’array avec `foreach()`

```js
let exemple1 = [5, 5, 6];
exemple1.forEach((element) => {
    console.log(element)
});
```

### Challenge

```js
let exemple1 = ['Dylan', 5, true];
let exemple2 = exemple1;
exemple2.push(11);
console.log(exemple1);
console.log(exemple2);
```

Les deux valeurs sont identiques mêmes si seulement ajouté à l’exemple2. Quand travaille avec des arrays, on travaille avec des références.

pour créer un nouvel array, spread operator

```js
let exemple1 = ['Dylan', 5, true];
let exemple2 = [...exemple1];
exemple2.push(11);
console.log(exemple1);
console.log(exemple2);
```

Méthode `map()` qui créer nouvel array

```js
let exemple1 = ['Dylan', 5, true];
let exemple2 = exemple1.map((element) => {
    return element;
});
exemple2.push(11);
console.log(exemple1);
console.log(exemple2);
```

## Objets

Les objets sont définis avec les accolades. Il peuvent prendre des propriétés.

```js
let exemple1 = {
    firstname: 'Emmanuel',
    lastname: 'Chateau'
};
console.log(exemple1.firstname);
```

Imbrication

```js
let exemple1 = {
    firstname: 'Emmanuel',
    lastname: 'Chateau',
    address: {
        city: 'Paris',
        state: 'France'
    }
};
console.log(exemple1.adress.city);
```

Mettre à jour des valeurs dans un objet

```js
let exemple1 = {
    firstname: 'Emmanuel',
    lastname: 'Chateau',
    address: {
        city: 'Paris',
        state: 'France'
    },
    age: 42,
    cats: ['Milo', 'Tito']
};
console.log(exemple1.age);
```

Mettre à jour des valeurs

```js
let exemple1 = {
    firstname: 'Emmanuel',
    lastname: 'Chateau',
    address: {
        city: 'Paris',
        state: 'France'
    },
    age: 42,
    cats: ['Milo', 'Tito']
};
exemple1.age = 31;
console.log(exemple1.age);
```

Afficher toutes les clefs

```js
let exemple1 = {
    firstname: 'Emmanuel',
    lastname: 'Chateau',
    address: {
        city: 'Paris',
        state: 'France'
    }
    age: 42,
    cats: ['Milo', 'Tito']
};
console.log(Object.keys(exemple1));
```

Afficher toutes les valeurs

```js
let exemple1 = {
    firstname: 'Emmanuel',
    lastname: 'Chateau',
    address: {
        city: 'Paris',
        state: 'France'
    }
    age: 42,
    cats: ['Milo', 'Tito']
};
console.log(Object.values(exemple1));
```

Voir si une propriété ou clef existe

```js
let exemple1 = {
    firstname: 'Emmanuel',
    lastname: 'Chateau',
    address: {
        city: 'Paris',
        state: 'France'
    }
    age: 42,
    cats: ['Milo', 'Tito']
};
console.log(Object.hasOwnProperty('firstname2'));
```

### Challenge

Passe par référence également comme les arrays

```js
let exemple1 = {
    firstname: 'Emamnuel'
};
let exemple1 = exmple1;
let exemple2.lastname = 'Chateau';

console.log(exemple1);
console.log(exemple2);
```

Pour créer nouvel objet, utiliser la méthode Objet (sinon classe)

Objet a la méthode assign()

```js
let exemple1 = {
    firstname: 'Emamnuel'
};
let exemple1 = exmple1;
let exemple2 = Object.assign({}, exemple1);

console.log(exemple1);
console.log(exemple2);
```



