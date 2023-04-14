---
author: Emmanuel Château-Dutier
since: 2017-02-11
---

# Feed Back sur les Spécifications XSLT et XQuery 3 par Michael Kay

Près de 10 ans après XSLT 2, Michael Kay a offert à XMLPrague 2017 un point d’information sur l’état des différents langages dans leur version 3. Au cours de cette présentation, il a notamment cherché à dégager les aspects de cette nouvelle version du langage qui constituent de véritables nouveautés. Deux changements sont stratégiques pour XQuery et XSLT : les fonctions de haut-niveau pour leur capacité à prendre en compte la variété et le changement, et le support de JSON car toutes les données ne sont pas en XML.

## Fonctions d’ordre supérieur

L’introduction de fonction d’ordre supérieur peut être appréciée du point de vue de leur élégance en terme de programmation. Mais cette nouveauté apporte également des fonctionnalités importantes car elle donne la possibilité de traiter les choses de manière dynamique. Ces fonctions de haut-niveau offrent la capacité de prendre en charge la variété et le changement. Au sein du langage XSLT, le mécanisme du *templating* offrait déjà des réponses à ces questions.

On peut passer un paramètre à une requête de sorte que l’action peut être effectuée de manière différente. Aussi, il ne s’agit pas seulement d’une manière élégante de programmer mais de quelques chose qui présente le potentiel de pouvoir rendre les applications qui montent mieux en charge.

## Support de JSON

Une des nouveautés importantes de cette version concerne l’introduction du support de JSON. MK ne croit pas que XQuery ou XSLT seront un jour largement utilisés sur le web pour traiter du JSON, cela pour plusieurs raisons : d’abord pour une raison culturelle, au sens où les langages proviennent d’un terrain distinct. Cependant ce support de JSON était nécessaire pour des raisons stratégiques car les personnes qui utilisent XML n’utilisent pas seulement du XML, et il est très important que leurs outils rencontrent tous les besoins de ces utilisateurs. Il s’agit donc d’étendre la portée du langage.

Il est désormais possible de parser des fichiers JSON en XSLT ou en XQuery. Un nouvel objet *map* a été introduit dans le langage qui est plus expressif que les simples objets JSON. Par ailleurs un nouvel objet *array* a également été introduit.

## Streaming et Packaging

Le streaming et le packaging sont deux choses qui présentent des enjeux pour la monté en charge de XSLT. Le Streaming permet de prendre en charge de larges sources de documents, et le packaging est utile pour la production de grandes applications très stratégiques en terme de maintenance.

- `xsl:stream`
- `xsl:source-document` et `xsl:iterate`
- `xsl:where-populated` `xsl:on-empty`, `xsl:on-non-empty`

## Sérialisation HTML5 et JSON

Il est désormais possible de générer du HTML5 en XSLT.

## Bénéfices

Plusieurs bénéfices en termes de productivité ont été introduits dans le langage.

### La possibilité de passer et sérialisme au sein du langage

Nombreuses personnes cherchent à tirer parti du parse/serialisation au sein du langage. Possibilités de contrôler le pipeline. Mais aussi possibilité d’inclure du XML.

### Maps et arrays

Les *maps* et *arrays* sont en partie là pour le support de JSON mais dès que l’on commence à les utiliser, on réalise à quel point on en avait besoin. Pour la première fois un typage et des structures de données correctes qui permet de configurer les applications, là où XML n’était pas très adapté. Par exemple lorsque la valeur d’un attribut ne peut pas être une liste de nombre, mais seulement une chaîne. Augmente donc la faisabilité de certaines applications en XQuery et XSLT.

### Standardisation des Collations UCA

La standardisation des collations UCA est importante car on a parfois besoin de comparer des collations internationales. Un ensemble de collations standardisées par des URI que l’on peut employer de différentes manières, sans doute un réel bénéfice pour traiter des données internationales.

### Grouping en XQuery

Grouping en XQuery qui augmente interopérabilité entre les deux langages.

### Collections généralisées

Collections généralisées, possibilité d’utiliser des URIs. Aujourd’hui bien plus puissantes, peut avoir des collections de n’importe quoi, de texte, de JSON, de contenus hybrides, cela fournit une abstraction très puissante entre les applications XQuery et XSLT et le monde extérieur.

### Entrées et sorties non-hiérarchiques

Entrée et sortie non-hiérarchiques, importantes pour XSLT.

## Petites choses

Petites choses qui donnent le sourire et améliorent l’expérience.

### Nouveaux opérateurs

Nouveaux opérateurs : `!`, `||`, `?`, `=>` (`||` provient de sequel)

Possibilité de faire des chaînage de fonctions, au lieu de dire string before, etc. possibilité de mettre le résultat d’une fonction dans la suivante.

### Text Value Template

*Text Value template* en XSLT très appréciable évidemment.

> XSLT 3.0 has Text Value Templates https://www.w3.org/TR/xslt-30/#text-value-templates that allow the use of curly braces in text nodes, as a shorter alternative to `xsl:value-of`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
    xmlns:xs="http://www.w3.org/2001/XMLSchema"
    exclude-result-prefixes="xs"
    expand-text="yes"
    version="3.0">
	  <xsl:param name="seq" as="xs:string*" select="'c', 'a', 'b', 'z'"/>
    <xsl:template name="xsl:initial-template">
        This is a test {sort($seq)}
    </xsl:template>
</xsl:stylesheet>
```

[exemple de Liam Quin où donne un nombre de chaussettes avec xsl:message]

Il est possible de l’activer ou le désactiver en ajoutant l’attribut `expand-text="yes"` ou `expand-text="no"` à n’importe quel élément XSLT, y compris `xsl:stylesheet`.

Il est également possible d’utiliser l’élément `xsl:expand-text` pour un constructeur d’élément direct ou un élément d’extension. 

### Union Types

Union Types possible maintenant d’écrire des fonctions qui opèrent sur une date ou une heure, au lieu d’écrire deux fonctions distinctes.

`tokenize()` et `contains-token()` qui 

## État du projet

Nous avons terminé et pense qu’avons été successfull du point de vue des implémentations fonctionnelles, du déploiement dans des applications critiques. Une masse d’utilisateurs. Qualité de la spécification du langage. Portée de l’application, et intérêt de la communauté.

## Conclusions

Michael Kay explique qu’il est désormais content de pouvoir disposer des journées que consacrait à ce groupe libres. Après vingt ans de travail, content de pouvoir dire que va pouvoir s’occuper d’autre chose.

Quelques diapositives de spéculations sur le futur. En tous les cas plusieurs choses peuvent intervenir, depuis quelques années réouvre les boîtes de plusieurs standards. Plusieurs choses que j’espère qu’interviennent, de nouvelles générations de langages de requêtes ou de tranformation qui produiront les choses encore mieux qu’on a pu les penser avec les technologies XML. Ne croit pas qu’avons là le dernier langage de transformation. Attend le moment où d’autres produiront un langage qui rendra obsolète ce que nous avons fait au cours des vingt dernières années.

## Détails

### Expressions XPath 3.0 et 3.1

- Mapping operator (`!`)
- String concatenation operator (`||`)
- Arrow operator (`==>`)
- EQNames
- Clause `let`

### Nouvelles fonctions pré-définies

- Sorting
- Analyzing strings
- Parsing and serializing XML
- Math and trigonometry

### Fonctions de haut-niveau

- Cas d’usage
- Named function references
- Inline function expressions
- Partial function application
- Built-in higher-order functions

### Arrays, maps et JSON

- Arrays
- Maps
- Conversion depuis et vers JSON

### Améliorations apportées aux templates et au traitement des feuilles de style

- Text value templates
- Matching on atomic values
- Declaring the context item (`xsl:context-item`)
- Mode declarations (`xsl:mode`)
- Dynamic evaluation of XPath (`xsl:evaluate`)
- Try/catch(`xsl:try`, `xsl:catch`)
- Assertions (`xsl:assert`)

### Packages

- Package definitions (`xsl:package`)
- Versions of a package
- Package dependencies
- Named components in packages
- Overriding template rules from a package
- Declarations local to a package

### Streaming

- Streaming source documents
- Streaming modes
- Iterating (`xsl:iterate`)
- Merging (`xsl:merge`)
- Forking (`xsl:fork`)
- Accumulators (`xsl:accumulator`)

## Divers

### XSD 1.1

Standardisation terminée en avril 2012. Bien reçu par les utilisateurs mais seulement 3 implémentations.

### XQuery 3.0

La seconde version du langage en 14 ans.

Investissement actif des implémenteurs.

Tourne le langage en un langage fonctionnel complet.

Nombreuses améliorations facilement adoptables par les utilisateurs (`group by`, `try/catch`, `switch`)

### Fonction de haut-niveau

```xquery
declare function sort(
	$input as item()*, 
	$key as (function(item()) as xs:anyAtomicValue)) {
	for $item in $inputorder by $key($item)
	return $item
};

sort(//employee, 
	function($e){current-date() - $e/joining-date})
```

```xquery
function sort(
	$input as item()*, 
	$key as (function(item()) as xs:anyAtomicValue)) {
	for $item in $inputorder by $key($item)
	return $item
};

sort(//employee, 
	function($e){current-date() - $e/joining-date})
```

- Fonctions anonymes
- Utilisation de `?`

### XPath 3.0

Clef pour XSLT 3.0 et XQuery 3.0

Largement utilisé mais arrêté à la version 1.0 (DOM, Selenium, etc.)

Peut d’intérêt en dehors de XSLT et XQuery.

Production de la version 3.1 rapide car la plupart du travail fait avec la version 3.0. Focalisation sur les maps et les arrays. Tensions face à JSON.

> Tension: is JSON something that exists in the big bad world outside XQuery, or does it have equal status to XML?

### Maps et Arrays

Représentation sans perte des données JSON

Riches structures de données pour travailler

Immutable (comme les séquences)

Pas d’identité

Initié avec XSLT 3.0 pour les applications de streaming, migré vers XPath 3.1

### XSLT 3.0

Getting closer: 2nd Last Call in October 2014●A big and complex spec, getting the bugs out is challenging●WG is stretched for resources●2 declared implementors (Saxon and Exselt)●selected features also in Altova

### Reste à faire

- XQuery Update 3.1
- Full Text 3.1

## BestFeature in XSLT 3.0

Cf. discussion XSL-l 7 octobre 2019

https://www.biglist.com/lists/lists.mulberrytech.com/xsl-list/archives/201910/threads.html

- maps et arrays
- opérateurs `!`, `=>` et `||`
- text value templates
- json

### Nouveaux opérateurs XPath

#### Simple map operator (`!`)

Pas de restriction sur les opérandes qui peuvent être des nœuds ou n’importe quel type de séquence. Cet opérateur est comparable à l’opérateur `/` mais ce dernier est plus restrictif, il ne peut évaluer que des nœuds à gauche. Ses résultats suppriment toutes les redondances parmi les résultats, pas dans le cas du `!`, ensuite les résultats apparaissent dans l’ordre des nœuds du documents depuis lesquels sont produits alors que les résultats de l’opérateur simple map ne sont pas ordonnés, ils apparaissent dans l’ordre où l’expression est évaluée.

##### Exemple 01

```xquery
('a', 'b', 'c') ! upper-case(.)
```

Résultat

```xquery
'A', 'B', 'C'
```

##### Exemple 02

```xquery
(1 to 10) ! (. mod 2 eq 0)
```

Résultats

```xquery
false, true, false, true, false, true, false, true, false, true
```

##### Exemple 03

```xquery
$person ! (@first, @middle, @last)
```

Résultats

Chacun des attributs pour chaque employé dans l’ordre spécifié. Nota : l’utilisation de l’opérateur `/` rend les résultats dans l’ordre du document mais l’ordre des attributs n’est pas prescrit et dépend de l’implémentation.

##### Exemple 04

```xquery
avg(//employee/salary ! translate(., '$', '') ! number(.))
```

Résultats

Moyenne des salaires de tous les employés. On peut remplacer le premier opérateur par le `/` mais pas le second car son opérande de gauche est une valeur atomique.

##### Exemple 05

```xquery
/*/num ! ..
```

Résultats n fois l’élément document. Avec l’opérateur `/`, on aurait seulement eu un seul nœud en raison de la dé-duplication appliquée par ce dernier opérateur sur les résultats.

#### Exemple 06

```xquery
/*/num ! (., 'Is even', . mod 2 eq 0)
```

On ne peut pas remplacer l’opérateur simple map par `/` car produirait une séquence mixte comme résultat ce qui est interdit pour cet opérateur.

#### Arrow operator (`=>`)

L’opérateur fléché prend le résultat de l’expression de gauche comme premier argument de la foction de droite.

```xquery
'hello' => upper-case()
```

Résultat

```xquer
'HELLO'
```

Le simple map operator fonctionne sur chaque item dans la séquence à son tour, un peu à la manière des prédicats `[]` tandis que l’opérateur flêché `=>` fonctionne sur le résultat dans son ensemble.

```xquery
string-to-codepoints("Henri") ! count(.)
```

A pour résultat `(1 1 1)`, tandis que :

```xquery
string-to-codepoints("Henri") => count(.)
```

A pour résultat `5`.

#### String concaténation (`||`)

```xquery
'a' || 'b' || 'c'
```

Résultat

```xquery
'abc'
```

### Améliorations pour la lisibilité des templates

#### Text value templates

En XSLT 2.0, on peut s’occuper d’un nœud texte de la manière suivante :

```xml
<element><xsl:value-of select="node"/></element>
```

```xml
<element id="{generate-id()}"><xsl:value-of select="node"/></element>
```

En XSLT 3.0, les expressions entre accolades peuvent être utilisées pour produire des nœuds textes en utilisant la déclaration `expand-text="yes"`

```xml
<xsl:stylesheet ... expand-text="yes">
  <element id="{generate-id()}">{node}</element>
</xsl:stylesheet...expand-text>
```

Il est possible d’activer/désactiver cette propriété sur n’importe quel élément avec `xsl:expand-text="no"` ou `xsl:expand-text="yes »` pour disposer d’éléments littéraux, par exemple pour rendre du contenu CSS.

```xml
<style type="text/css"xsl:expand-text="no">
  h1 { color: blue; }
</style>
```

Exercices

- Réécrire une feuille de transformation XSLT pour la rendre plus concise en utilisant les text value templates.
- Veiller que l’utilisation des accolades permet de bien prendre en charge les blocs en JavaScript et CSS.
- Essayer de rendre la feuille de style encore plus concise.

#### Constructions conditionnelles avec `xsl:where-populated`

Dans certaines transformations, l’élément englobant doit seulement être rendu lorsqu’il y a du contenu.

```xml
<xsl:if test="item">
  <ul>
    <xsl:for-each select="item">
      <li>...</li>
    </xsl:for-each>
  </ul>
</xsl:if>
```

Cette approche est relativement verbeuse et ne permet pas le streaming. C’est la raison pour laquelle une nouvelle instruction `xsl:where-populated` a été introduite. Le contenu de cette instruction n’est sorti que lorsqu’il y a des nœuds petits-fils.

```xml
<xsl:where-populated>
  <ul>
    <xsl:for-each select="item">
      <li>...</li>
    </xsl:for-each>
  </ul>
</xsl:where-populated>
```

#### Constructions conditionnelles avec `xsl:on-empty` et `xsl:on-non-empty`

Le contenu d’une instruction `xsl:on-empty` n’est sorti que lorsque les éléments adjacents précédents ne produisent rien.

```xml
<xsl:sequence>
  <xsl:for-each select="item">
    <!-- do something --->
  </xsl:for-each>
  <xsl:on-empty>
    <p>no items to process</p>
  </xsl:on-empty>
</xsl:sequence>
```

- Cette instruction ne peut être employée qu’une fois dans un constructeur de séquence. 
- Il doit apparaître à la fin du constructeur de séquence.

De même le contenu de l’instruction `xsl-on-non-empty` n’est sorti que lorsque les nœuds adjacents (autre que `xsl:on-empty` ou `xsl:on-non-empty`) produisent quelque chose.

Les mêmes restrictions s’appliquent à son utilisation que pour `xsl:on-empty`.

### Facilitation du paramétrage des feuilles de style

#### Évaluation dynamique

L’instruction `xsl:evalate` accepte des chaînes de caractères et les évalue comme des expressions  XPath.

```xml
<xsl:sort>
  <xsl:evaluate xpath="$key" context-item="."/>
</xsl:sort>
```

Attention aux implications du point de vue de la sécurité.

#### Shadow attributes

Pour des raisons de rétrocompatibilité, tous les attributs ne peuvent pas utiliser des valeurs d’attributs.

Légal

```xml
<xsl:sort order="{$order}"/>
```

Illégal

```xml
<xsl:sort select="{$key}"/>
```

l’attribut `@select` n’est pas AVT, il doit directement contenir une expression. Sinon, tous les temps seront évaluer en utilisant la même clef.

Les noms de shadow attributes débutent par `_` et remplacent les valeurs des attributs normaux. Seules des expressions statiques peuvent être employées comme valeur.

Placer un `_` devant un nom d’attribut, le tranforme en `attribute value template` qui sera évalué au moment de la compilation pour fournir la valeur de l’attribut. Tous les paramètres ou les variables auxquelles on se réfère doivent être déclarés avec `static="yes"`. 

Ce mécanisme peut être utilisé pour paramétriser, par exemple, la sortie d’un doctype dans un document.

`xsl:evaluate` peut être utilisé si les expressions statiques s’avèrent trop contraignantes.

### Autres nouveautés utiles

#### Fonction `random-number-generator()`

L’expression `random-number-generator()?number` retourne un nombre aléatoire entre 0 et 1

L’expression `random-number-generator()?permute(sequence)` retourne une séquence dans un ordre aléatoire.

#### Template initial

Un template nommé `xsl:initial-template` sera invoqué en premier.

```xml
<xsl:template name="xsl:initial-template">
  <!-- do something -->
</xsl:template>
```

C’est en particulier utile lorsque l’entrée n’est pas du XML ou quand une feuille de style génère seulement une sortie.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
  xmlns:xs="http://www.w3.org/2001/XMLSchema"
  exclude-result-prefixes="xs"
  version="3.1">
  <xsl:param name="seq" as="xs:string*" select="'c', 'a', 'b', 'z'"/>
  <xsl:template name="xsl:initial-template">
    This is a test <xsl:value-of select="sort($seq)"/>
  </xsl:template>
</xsl:stylesheet>
```

En ligne de commande, avec Saxon 9.xx, passer un paramètre `-it` avec la valeur `Q{http://www.w3.org/1999/XSL/Transform}initial-template`. Si le nom du template est omis, la valeur par défaut est `xsl:initial-template`.

Dans Oxygen, sélectionner le processeur Saxon 9.xx et dans les paramètres avancés du processeur renseigner la valeur du paramètre `-it` avec `Q{http://www.w3.org/1999/XSL/Transform}initial-template`

#### Manipulations de JSON

XSLT 3.0 offre deux manières de traiter du JSON.

Les fonctions `json-to-xml()` et `xml-to-json()` permettent de transformer du JSON en XML et vice-et-versa

- Les mapping sont génériques et universels mais pas toujours concis ou intuitifs
- Une fois qu’un contenu JSON est converti en XML il peut être traité et accédé avec XPath.

Les fonctions `parse-json()` et `json-doc()` transforment du JSON en maps et en arrays.

- Leur utilisation est pus naturelle et plus proche de JSON.
- L’opérateur lookup (`?`) offre une navigation facilité

```xquery
(:~ 
 : JavaScript :
 : $json.result[0].geometry.location.lat 
 :)
$json?results(1)?geometry?location?lat
```

Rappel : l’index des arrays en XPath n’est pas 0.

La fonction `array:flatten()` permet de convertir des array en séquence.

Ces fonctions sont placées dans un espace de nom différent : `http://www.w3.org/2005/xpath-functions/array`.

#### Nouvelle solution pour la recopie à l’identique

Par défaut en XSLT, une transformation vide copie seulement les nœuds texte.

Pour une copie à l’identique du fichier, on utilise classiquement la règle de recopie à l’identique suivante (*identity transform*) :

```xml
<xsl:template match="node()">
  <xsl:copy>
    <xsl:copy-of select="@*" />
    <xsl:apply-templates />
  </xsl:copy>
</xsl:template>
```

On peut dorénavant utiliser l’instruction `xsl:mode` pour modifier ce comportement par défaut.

```xml
<xsl:mode on-no-match="shallow-copy"/>
```

- `deep-copy` l’arbre est copié en une fois
- `shallow-copy` l’arbre est copié, nœud à sud (dès lors il est possible de personnaliser le traitement de nœuds individuels par des templates)
- `deep-skip` l’arbre entier est passé
- `shallow-skip` l’bare est passé nœud par nœud
- `text-only-copy` seuls les nœuds texte sont copiés (règle par défault)
- `fail` la transformation échoue si il n’y pas de templates pour certains nœuds.

D’après Michael Kay, l’instruction `xsl:mode on-no-match="..."` fut initialement introduite parce que la forme conventionnelle d’identification des templates n’était pas streamable. Mais l’analyse de la streamability s’est améliorée et cette justification a largement disparu. Mais cette instruction devient un raccourci commode. Note : L’opérateur d’union  dans select="node() | @* » présente toujours des difficultés pour le streaming -- voir la note dans 19.8.8.4. Mais il est possible de l’écrire sous la forme <xsl:apply-templates select="@* »/> <xsl:apply-templates select="node() »/>.

#### `contains-token()`

La fonction `contains-token()` facilite la sélection de classes HTML ou DITA

```xml
<div class="theme navbar cols-2">
  ...
</div>
<xsl:template match="*[contains-token(@class, 'navbar')]">
  <!-- do something -->
</xsl:template>
```

#### Fonctions trigonométriques et exponentielles

À l’exception de `math:pi`, toutes ces fonctions sont spécifiées en référence à la norme IEEE 754-2008 où elles apparaissent comme des opérations recommandées (section 9).

https://www.w3.org/TR/xpath-functions-31/#trigonometry

| Fonction                                                     | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`math:pi`](https://www.w3.org/TR/xpath-functions-31/#func-math-pi) | Renvoie une approximation à la constante mathématique *π*.   |
| [`math:exp`](https://www.w3.org/TR/xpath-functions-31/#func-math-exp) | Renvoie la valeur de l’ex.                                   |
| [`math:exp10`](https://www.w3.org/TR/xpath-functions-31/#func-math-exp10) | Renvoie la valeur puissance 10.                              |
| [`math:log`](https://www.w3.org/TR/xpath-functions-31/#func-math-log) | Renvoie le logarithme naturel de l’argument.                 |
| [`math:log10`](https://www.w3.org/TR/xpath-functions-31/#func-math-log10) | Renvoie le logarithme en base 10 de l’argument.              |
| [`math:pow`](https://www.w3.org/TR/xpath-functions-31/#func-math-pow) | Renvoie le résultat de l’élévation du premier argument à la puissance du second. |
| [`math:sqrt`](https://www.w3.org/TR/xpath-functions-31/#func-math-sqrt) | Renvoie la racine carrée non négative de l’argument.         |
| [`math:sin`](https://www.w3.org/TR/xpath-functions-31/#func-math-sin) | Renvoie le sinus de l’argument. L’argument est un angle en radians. |
| [`math:cos`](https://www.w3.org/TR/xpath-functions-31/#func-math-cos) | Renvoie le cosinus de l’argument. L’argument est un angle en radians. |
| [`math:tan`](https://www.w3.org/TR/xpath-functions-31/#func-math-tan) | Renvoie la tangente de l’argument. L’argument est un angle en radians. |
| [`math:asin`](https://www.w3.org/TR/xpath-functions-31/#func-math-asin) | Renvoie l’arc sinusoïdal de l’argument.                      |
| [`math:acos`](https://www.w3.org/TR/xpath-functions-31/#func-math-acos) | Renvoie l’arc cosinus de l’argument.                         |
| [`math:atan`](https://www.w3.org/TR/xpath-functions-31/#func-math-atan) | Renvoie l’arc tangent de l’argument.                         |
| [`math:atan2`](https://www.w3.org/TR/xpath-functions-31/#func-math-atan2) | Renvoie l’angle en radians sous-tendu à l’origine par le point sur un plan de coordonnées (x, y) et l’axe des x positif. |

Voir aussi les Opérateurs arithmétiques sur les valeurs numériques https://www.w3.org/TR/xpath-functions-31/#op.numeric

### Fonction `unparsed-text-lines()`

La fonction `unparsed-text-lines()` lit une ressource externe (par exemple un fichier) et retourne son contenu comme une séquence de chaînes de caractères, ligne par ligne du contenu de la ressource.



### La fonction `transform()`

La fonction `transform()` est une fonction XPath qui invoque une feuille de style XSLT, exécute la transformation et retourne le résultat.

```xml
<xsl:sequence select="fn:transform(..., .)" />
```

- traitement de plusieurs fichiers sans redemarrer Java (test suite)
- pipeline comme avec XProc
- simplifier les stylesheets en remplaçant les modes
- replacer ANT ou d’autres systèmes de construction.

### L’instruction `xsl:iterate`

Une amélioration syntaxique qui offre la simplicité de `xsl:for-each` combinée avec le passage de paramètres. Elle garantie une tail-recursion (efficacité en mémoire). Mais elle ne peut cependant pas toujours être utilisée.

```xml
<xsl:iterate select="sequence">
  <!- paramètres passés à chaque itération -->
  <xsl:param name="a" value="initial value"/>
  <xsl:on-completion>
    <!-- contenu retourné lorsque l’itération a lieu -->
  </xsl:on-completion>
  <xsl:if test="premature">
    <xsl:break/>
  </xsl:if>
  <xsl:next-iteration>
    <xsl:with-param name="a" select="new value"/>
  </xsl:next-iteration>
</xsl:iterate>
```

- Un attribut `select` obligatoire comme  `xsl:for-each` 
- Possibilité d’utiliser `xsl:break` pour terminer l’itération
- Possibilité d’utiliser `xsl:next-iteration` avec de nouveaux paramètres, n’importe quand, mais seulement lors de la dernière instruction dans le corps d’un if, d’une itération, d’une clause when ou otherwise ou try ou catch.

### L’instruction `xsl:where-populated`

Créer une enveloppe si l’élément n’est pas vide.

```xml
<xsl:where-populated>
  <fn-wrap>
    <xsl:apply-templates select="fn"/>
  </fn-wrap>
</xsl:where-populated>
```

De même `xsl:on-empty` et `xsl:on-non-empty` utilisés en streaming car on ne peut pas regarder en avant mais utiles en dehors.

### Les instructions `xsl:try` et `xsl:catch`

Les instructions `xsl:try` et `xsl:catch` sont utilisées pour évaluer des expressions qui peuvent générer des erreurs, afin de réaliser une action à partir de cette erreur.

- par exemple pour convertif un attribut date en entier
- ouvrir un fichier qui peut ne pas êrte bien formé

### Divers

- `head()` et `tail()` facilitent le traitement récursif des séquences
- `parse-xml()`et `serialize()`facilitent la sérialisation et le parsing des chaînes
- `load-xquery-module()` permet d’accéder à des fonctions et des variables depuis des modules XQuery
- `transform()` invoque des feuilles de style chargées  dynamiquement 
- `path()` retourne le XPath des nœuds sélectionnés
- `analyze-string()`fonction qui matche du texte contre des expressions régulières et retourne le résultat sous la forme d’une structure XML

* L’attribut `@select` sur `xsl:when` et `xsl:otherwise` (et parfois `xsl:if`) comme alternative à une instruction xsl:séquence contenue.
* L’attribut `@as` sur `xsl:mode` pour définir le type de retour de toutes les règles modèles dans ce mode (bon pour la documentation, bon pour le contrôle de type de xsl:apply-templates)

> I think it's useful to distinguish (a) features that appeal immediately to existing users because they make it easier to do the things that you do a lot, and (b) features that are more strategic in nature, making it possible to do new things that you weren't doing before, or to get significant benefits (in say productivity, performance, or maintainability) but which may be difficult to adopt immediately because it needs a whole different approach.
>
> expand-text, new operators, and things like contains-token() and xsl:iterate definitely fall in the first category.
>
> Streaming and packages definitely fall into the second.
>
> Maps, JSON, fn:transform, fn:serialize, xsl:evaluate, and accumulators etc are perhaps intermediate. You probably won't change your existing code to take advantage of them, and you probably won't use them until the next time you write a new stylesheet that's a bit more challenging than the ones you've written before. As John Lumley noted, we couldn't have written an XSLT compiler in XSLT without these features - but we managed to get by without streaming and packages. In fact, we only realised after doing it quite how much packages could have made the job easier.
>
> Michael Kay, Saxonica

## Standards

- https://www.w3.org/TR/xslt-30
- https://www.w3.org/TR/xpath-functions-31
- https://www.w3.org/TR/xpath-31

## Sources

- https://archive.xmlprague.cz/2017/files/presentations/prague-w3c.pdf
- http://www.datypic.com/services/xslt/whatsnew3.html
- Kosek, Jirka. 2019. « XSLT 3.0 for Daily Coding ». présenté à XML SummerSchool, Oxford. https://www.kosek.cz/xml/2019xmlss/Kosek_XSLT4DailyCoding.pdf.
- Walmsley, Priscilla. 2015. *XQuery: Search across a Variety of XML Data*. Second edition. Sebastopol, CA : O’Reilly Media.

## XSLT 3 overview

Un langage moderne plus fonctionnel.

- Construit à partir de XSLT 2 avec `xsl:sequence` et des types.
- Ajoute le streaming, le packaging, de nouveaux types de données et de nouvelles manières de travailler et de combiner des feuilles de styles
- XPath s’est renforcé

XSLT 3 est plus orthogonal, plus d’instructions peuvent avoir des attributs `select` et il est possible d’utiliser self:foo pour les match patterns 

Les endroits où les chaînes de caractères constant ne pouvaient être transformées en expression peuvent aujourd’hui prendre des `shadow attributes` qui sont computé au moment de la compilation.

- Nouveaux opérateurs `!` et `=>`
- Nouveaux types `map` et `array` avec des fonctions pour manipuler des fichiers JSON
- Nouvelles fonctions pour le streaming, la manipulation des maps et des arrays, les fonctions sur les fonctions (`apply()` et `fold-left()`), la collation et les tris, la sérialisation, les variables d’environnement ou les fonctions mathématiques.
- Ne pas oublier les extensions [Expath](http://expath.org) pour la manipulation de fichiers binaires, l’écriture ou la lecture de fichiers, l’utilisation d’archive zip ou exécuter des requêtes REST
