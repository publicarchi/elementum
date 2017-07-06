---
since: 2017-07-07
author: emchateau
@tags: xquery
---

# Introduction XQuery

## Les types définis par le XML Data Model (XDM)

```xquery
'string' (: chaîne de caractères :)
```

```xquery
1 (: entier :)
```

```xquery
1 + 1 + 1 (: somme :)
```

```xquery
<p/> (: constructeur direct :)
```

```xquery
1, 2, 3 (: séquence :)
```

Concaténations et conversions

```xquery
1 || 2 || 3
```

## Structures FLOWR

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

Utilisation d’une boucle for

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

Appels d’une fonction

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

création d’une base de données

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

