# Bonnes pratiques XQuery

En XQuery comme avec tout autre langage, l’adoption d’un certain nombre de principes simples peut permettre à la fois d’augmenter la lisibilité du code que vous produisez, sa maintenabilité et sa portabilité.


## Être explicite

Lorsque l’on passe du code en revue, on a besoin de pouvoir rapidement identifier :
- les dépendances
- les arguments attendus par une fonction
- le type de résultat d’une fonction
- comprendre l’intention de l’auteur

XQuery est un langage fortement typé. La signature des fonction XQuery facilite le débugage et permet de la documenter. En plus de ce typage, l’utilisation de [xqDoc](http://xqdoc.org) permet de rendre votre code encore plus explicite.

Lorsque vous écrivez du code, toujours il est bon de toujours veiller à :
- déclarer les modules importés et les espaces de nom
- déclarer les types et la cardinalité des arguments des fonctions
- déclarer le type et la cardinalité du résultat
- Utiliser xqDoc pour documenter ses fonctions


### Expliciter les types et les cardinalités

- Facilite la refactorisation (erreurs statiques vs erreurs dynamiques)
- Fournit des éléments de documentation
- Permet d’inférer des intentions
- Facilite l’écriture de tests unitaires


### Utilisation de xqDoc

Le temps consacré à la documentation de votre code peut vous faire gagner énormément de temps lorsque vous aurez à vous relire par la suite.

En prenant le temps de signer vos fonctions, la documentation du code avec xqDoc consiste pour l’essentiel à renseigner les paramètres et la sortie.

Au début du document, vous pouvez préciser l’auteur et la version de votre code avec les étiquettes @author, @version.

Une documentation xqDoc comprend d’abord une description générale de la fonctions. Suivent avec les étiquettes @param et @return la description des paramètres et des sorties. @since permet d’indiquer la date d’introduction de la fonction, @see un renvoi vers de la documentation.

Personnellement, j’utilise des marqueurs spécifiques comme @todo pour les choses à faire, @issue pour les bugs et @source pour des sources.

Tout en essayant d’être le plus succint possible, définissez des règles de rédaction pour ces descriptions (temps, forme verbale des phrases, etc.)

Avec ces simples éléments et des signatures des fonctions, il sera possible de générer une documentation complète à la volée avec un processeur xqDoc. BaseX propose un support natif de xqDoc qui permet de générer une documentation XML à la volée avec le [module d’inspection](http://docs.basex.org/wiki/Inspection_Module#inspect:xqdoc).


## Portabilité

### Déclaration de version et portabilité

```xquery
  xquery version '3.0' ;
```

Choisir une version standardisée du language (au moins la version 1.0).

En utilisant une version standardisée de XQuery, vous devez importer les modules propriétaires utilisés.

Par exemple, pour une application BaseX, c’est une bonne pratique d’importer les modules explicitement :

```xquery
  xquery version "3.0" ;
  import module namespace db = "http://basex.org/modules/db" ;
  import module namespace restxq = "http://exquery.org/ns/restxq";
  import module namespace file = "http://expath.org/ns/file" ;

  declare namespace db = "http://basex.org/modules/db" ;
  declare namespace restxq = "http://exquery.org/ns/restxq" ;
  declare namespace file = "http://expath.org/ns/file" ;
  (: etc. :)
```

### Déclaration des fonctions

Plutôt que :

```xquery
  xquery version "1.0" ;

  declare function process() {
    <something/>
  };

  process()
```

Il est préférable de déclarer explicitement le préfixe de la fonction :

```xquery
  xquery version "1.0" ;

  declare function local:process() {
    <something/>
  };

  local:process()
```

### Utilisation d’un constructeur d’espace de nom

```xquery
  xquery version "3.0";

  declare function local:create-example($entity as element()) as element() {
    element { fn:node-name($entity) } {
      $entity/@*,
      fn:in-scope-prefixes($entity) !
        namespace {.} {fn:namespace-uri-for-prefix(., $entity)},
      element other {
        text { "something" }
      }
    }
};
```


## Présentation du code

Comme pour tout langage informatique, la consistance dans la présentation de votre code facilitera sa lecture et sa compréhension.

### indentation

Même s’il n’existe pas de règles standard pour l’indentation du code XQuery, fixez-vous des règles de présentation et appliquez les rigoureusement.

- indentez votre code toujours de la même manière
- veillez à l’indentation du code en XML
- définissez des règles d’indentation pour les expressions incluses, les tests, etc.


### Utilisation des espaces

En XQuery, les espaces ne sont généralement pas significatifs. Leur emploi peut augmenter la lisibilité des fonctions incluses ou des expressions XPath complexes.


```xquery

```


## Simplification du code


### Éviter la répétition des mêmes expressions

Dnas bien des cas, il est possible de simplifier le code en évitant la répétition de la même expression soit au niveau de l’expression sur laquelle on itère, soit en utilisant la clause let.

@todo exemples



### Déclaration des namespaces

- ne pas déclarer les namespaces en ligne
- réduit le risque d’erreur

```xquery
  declare function local:get-metadata() as element(m:metadata) {
    <metadata xmlns="http://sub.corp.dom.com/ns/proj/module">
      ...
    </metadata>
  };

  <metadata-container xmlns="http://sub.corp.dom.com/ns/proj/module">
    { local:get-metadata() }
  </metadata-container>
```

```
  declare namespace m = "http://sub.corp.dom.com/ns/proj/module";

  declare function local:get-metadata() as element(m:metadata) {
    <m:metadata>
      ...
    </m:metadata>
  };

  <m:metadata-container>
    { local:get-metadata() }
  </m:metadata-container>
```


### Emploi des Simple map operators

En XQuery 3.0, l’emploi des Simple map operators peut parfois faciliter la lecture du code.

```xquery
  xquery version "1.0" ;

  for $animal in $animals/animal
  return
    element { $animal/type } { $animal/name }
```

```xquery
  xquery version "3.0";

  $animals/animal ! element { type } { name }
```

### factorisation des fonctions

... see Adam Retter


### Affectation des Regex en variables


## Écrire des tests



## Sources

- Adam Retter, XQuery from the trenches, http://slides.com/adamretter/xquery-from-the-trenches
