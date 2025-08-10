---
author: emchateau
tags: xquery
---

# Introduction XQuery

[XQuery](https://www.w3.org/TR/xquery-31/) est un langage de requêtes applicable à un grand nombre de sources de données qu’elles soient encodées en XML ou représentée en JSON. 

Le langage opère notamment sur le modèle de données XML ([XML Data Model (XDM)](https://www.w3.org/TR/xpath-datamodel-31/)). Là où XSLT est destiné à transformer des données XML, XQuery est principalement destiné à faire des recherche dans des données XML. Il s’utilise habituellement avec une base de données XML capable d’indexer les nœuds d’un document XML. Mais c’est aussi un langage de programmation turing complet qui peut être utilisé dans de nombreuses applications. XQuery est principalement efficace lorsqu’il s’agit de manipuler ou de concilier des données de différents genre.

XQuery est un langage hôte de [XPath](https://www.w3.org/TR/xpath-31/). Ainsi, XPath est généralement un sous-ensemble de XQuery. Autrement dit, toute expression XPath sera une expression XQuery valide. Le langage XQuery apporte toutefois un certain nombre de fonctionnalités pour requêter et manipuler des données XML. La version 3.1 du langage étend XQuery pour travailler sur des données JSON en ajoutant des types *maps* et *arrays* au langage.

Plusieurs extensions de XQuery peuvent s’avérer utiles : XQuery Update est destiné à facilier la mise à jour de documents XML, XQuery Full-text sert à faire des recherches dans des chaînes de caractères, ou faciliter la réalisation de requêtes REST.

## Les types définis par le XML Data Model (XDM)

Dans le [XML Data Model (XDM)](https://www.w3.org/TR/xpath-datamodel-31/), toutes les expressions XPath ramènent une séquence. Une séquence se compose de zéro, un ou plusieurs items. Les items peuvent être des littéraux, des valeurs atomiques ou des fonctions.

### Valeurs atomiques

Voici quelques exemples de création de valeurs atomiques définies par le modèle de données :

Chaîne de charactère (*string*)

```xquery
'string' (: chaîne de caractères :)
```

Entier (*integer*)

```xquery
1 (: entier :)
```

Expression arithmétique

```xquery
1 + 1 + 1 (: somme :)
```

Séquence

```xquery
1, 2, 3 (: séquence :)
```

Concaténations et conversions

```xquery
1 || 2 || 3
```

### Création des nœuds XML

Le XML Data Model définit 7 types de nœuds. En XQuery, il est possible de créer des nœuds en utilisant des constructeurs directs (littéraux) ou bien en les comptant.

Constructeurs directs

```xquery
<p/> (: constructeur direct d’un élément XML p :)
<p xml:id="id01"/> (: constructeur direct d’un élément XML p vide avec un attribut @id qui avec la valeur id01 :)
```

```xquery
element p { '' } (: computation d’un élément XML p vide :)
element p {
	attribute xml:id { 'id01' }
	''
} (: computation d’un élément XML p vide avec un attribut @id qui avec la valeur id01 :)
```

## Structures FLOWR

FLOWR pour For, Let, Order by, Where, Return

Affecter et retourner une variable

```xquery
let $var := 'texte'
return $var
```

```xquery
let $var := 'texte'
return $var || ' encore du texte'
```

Mettre $var dans un élément XML

```xquery
let $var := 'texte'
return 
		<p>{$var}</item>
```

Utilisation d’une boucle `for`

```xquery
let $sequence := (1, 2, 3)
for $item in $sequence
return <item>{$item}</item>
```

Créer un document XML valable

```xquery
<liste>{
	let $sequence := (1, 2, 3)
	for $item in $sequence
	return <item>{$item}</item>
}</liste>
```

```xquery
let $content := 
  let $sequence := (1, 2, 3)
  for $item in $sequence
  return <item>{$item}</item>
return <liste>{$content}</liste>
```

## Les fonctions

Définition d’une fonction

```xquery
declare function nomDeFonction($param) {
	'corps de la fonction'
};
```

Appels de fonction

```xquery
nomDeFonction($param)
```

Typage de la fonction

```xquery
declare function local:toto($param as xs:integer, $param2 as xs:string) as element()* {
  <div>{
    (<p>je suis une fonction</p>,
    <p>{$param}</p>,
    <p>{$param2}</p>,
    $param3)
   }</div>
};
local:toto(1, 'string', <element>element</element>)
```

```xquery
declare function local:toto($param as xs:integer, $param2 as xs:string) as element() {
  <div>
	<p>je suis une fonction ressource </p>
    <p>{$param}</p>
    <p>{$param2}</p>
  </div>
};
local:toto(1, 'string')
```

Travail avec la base de données

création d’une base de données (BaseX v. 9, mettre à jour les fonctions db:open)

```xquery
db:open('gdp')
```

```xquery
db:open('gdp')//*:title
```

```xquery
let $gdp := db:open('gdp')
return $gdp//*:title
```

```xquery
let $gdp := db:open('gdp')
for $titre in $gdp/*:title
return <h1>{$titre}</h1>
```

```xquery
let $gdp := db:open('gdp')
for $titre in $gdp/*:title
return <h1>{$titre/text()}</h1>
```

```xquery
declare function local:titreGdp() {
  let $gdp := db:open('gdp')
  for $title in $gdp//*:title
  return <h1>{$title//text()}</h1>
};
local:titreGdp()
```

```xquery
declare function local:titreGdp( $edition ) {
  let $gdp := db:open('gdp')
  for $title in $gdp//*:title
  return <h1>{$title//text()}</h1>
};
local:titreGdp('gdpBrice1684')
```

## Modules

Créer un module, enregistrer le dans webapp/

```xquery
xquery version "3.0" ;
module namespace local = "local" ;
declare 
  %restxq:path('mapage')
function local:toto($param as xs:integer, $param2 as xs:string, $param3 as element()) as element()* {
  <div>
    (<p>je suis une fonction</p>,
    <p>{$param}</p>,
    <p>{$param2}</p>,
    {$param3})
  </div>
};
```

Aller à localhost:8984

@todo montrer exemple sans param

ajouter les variables

```xquery
xquery version "3.0" ;
module namespace local = "local" ;
declare 
  %restxq:path('mapage')
function local:toto($param as xs:integer, $param2 as xs:string, $param3 as element()) as element()* {
  <div>
    (<p>je suis une fonction</p>,
    <p>{$param}</p>,
    <p>{$param2}</p>,
    {$param3})
  </div>
};
```

```xquery
xquery version "3.0" ;
module namespace local = "local" ;
declare 
  %restxq:path('/mapage/{$param}/{$param1}')
function local:toto($param as xs:string, $param2 as xs:string) {
  <div>
    (<p>je suis une fonction</p>,
    <p>{$param}</p>,
    <p>{$param2}</p>,
    {$param3})
  </div>
};
```

```xquery
xquery version "3.0" ;
module namespace local = "local"; 

declare 
  %restxq:path('unchemin/{$edition}')
  %output:method("html")
  %output:html-version("5.0")
function local:titreGdp($edition as xs:string) {
  let $gdp := db:open('gdp')
  for $titre in $gdp//*:TEI[*:teiHeader/*:fileDesc/*:sourceDesc[@xml:id=$edition]]//*:head
  return <h1>{fn:normalize-space($titre)}</h1>
};
```

