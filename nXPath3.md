---
since: 2020-04-18
tags: xpath
---

# XPath 3.0

Sujets : XDM, nouveaux types XPath 3.0, nouveaux opérateurs XPAth, nouvelles expressions XPath, définitions référence et appel aux fonctions. 

## Sommaire

- Le XPath Data Model (XDM) 3.0
- Les nouveaux types, opérateurs et expressions introduits par XPath 3.0
- Le *data-type function* et le nouveau standard pour les fonctions (12 groupes dont 8 entièrement nouveaux pour XPath)
- Fonctions de haut-niveau (higher-order)
- Création de nouveaux types de données, et de librairies de fonctions

### Le XDM comme fondation de XPath

Rôle du XDM pour XPath 2.0 fondamental pour XPath, évolutions importantes avec la version 3.

- Types de nœuds (rappels)
- Propriétés des nœuds (rappels)
- Nouveaux types ajoutés depuis XDM 2.0, et notamment le *fonction data-type*

### Nouveautés introduites dans XPath 3.0

types, constructs, operators et expressions

- Nouveaux types XPath 3.0
- Nouveaux opérateurs XPath 3.0
- Nouvelles expressions XPath 3.0
- Référencement, définition et appel d’une fonction
- Subtyping relationship entre les fonctions

### Nouvelles fonctions

- Fonctions sur les valeurs numériques
- Fonctions sur les chaînes
- Fonctions sur les nœuds
- Fonctions sur les séquences

- Fonctions sur les entiers, les nombres et les valeurs temporelles
- Fonction donnant accès à de l’information externe
- Fonctions pour parser et sérialiser
- Constructor Functions
- Casting to list / union types

### Fonctions de haut-niveau

- Qu’est-ce qu’une fonction de Haut-niveau
- Commen créer de nouvelles fonctions dynamiquement
  - composition des fonction
  - application partielle
- Closure et environment d’une focntion
- ...

### Outils

Encore peu d’implémentation de la version 3 de XPath.

- BaseX
- EMC/xDB
- SaxonEE 9.5
- XmlPrime 3+
- Zorba 2.9+

Mais encore

- ExistDB
- MarkLogic
- Altova ?

cf. la *QT3 Test Suite Result Summary*. https://dev.w3.org/2011/QT3-test-suite/ReportingResults/

IDEs : [Oxygen](https://www.oxygenxml.com) avec Saxon. [BaseX](http://basex.org).

### Ressources

- Saxon diaries, Michael Kay http://dev.saxonica.com/blog/mike
- XFront, Roger Costello http://www.xfront.com/index.html
- Dimitri Novatchev http://dnovatchev.wordpress.com
- Doc BaseX https://docs.basex.org/wiki/XQuery_3.0
- Pricillia Walmslay. XQuery
- Michael Kay, XSLT 2.0 and XPath 2.0
- Jeni Tennison, XSLT and XPath on the Edge et XPath 2.0
- mailing list XSL-List, Xml-dev

### Standards

3.0 2014, 3.1 en 2017

- [XQuery and XPath Data Model 3.1](http://www.w3.org/TR/xpath-datamodel-31/)
- [XML Path Language (XPath 3.1)](http://www.w3.org/TR/xpath-31/)
- [XPath and XQuery Functions and Operators 3.1](http://www.w3.org/TR/xpath-functions-31/)
- [XSLT and XQuery Serialization 3.1](http://www.w3.org/TR/xslt-xquery-serialization-31/)

## Le XDM comme fondation de XPath

Contenu : Rôle du XDM pour XPath 2.0 fondamental pour XPath, évolutions importantes avec la version 3.

- Types de nœuds (rappels)
- Propriétés des nœuds (rappels)
- Nouveaux types ajoutés depuis XDM 2.0, et notamment le *fonction data-type*

Le XDM sert deux objectifs :

- définit l’entrée (input) pour XSLT et XQuery
- définit toutes les valeurs et expressions permises en XSLT, XQuery et XPath

XDM est fondé sur le [XML Infoset](http://www.w3.org/TR/xml-infoset), il supporte les types définit par XML Schéma (structures et types simples de données). Il définit la représentation de collections de documents et de valeurs complexes. Enfin, il supporte le typage de valeurs atomiques. Le modèle de données définit également des séquences. Dans le modèle de données, toutes valeur est une séquence, même un item est une séquence d’un item.

Une **instance du modèle de données** (*Instance of the Data Model*) est une **séquence** (*Sequence*) d’items.

Une **séquence** (*Sequence*) est une **collection d’items** (*Collection of items*). Une collection n’est pas un ensemble car elle est **ordonnées** (*ordered*), elle peut contenir des doublons. Les séquences sont des collections **hétérogènes** d’objets (*heterogeneous*).

Un **item** (*Item*) est soit un **nœud** (*Node*), soit une **valeur atomique** (*Atomic Value*), soit une **fonction** (*function*). Les fonctions ont été introduites dans la version du modèle de données.

Une **valeur atomique** (*Atomic Value*) est n’importe quelle **valeur de type atomique** (*Value of an atomic type*).

Un **type atomique** (*Atomic type*) est soit un **type primitif simple** (*Primitive Simple Type*) soit **dérivé d’un type atomic** (*Derived from atomic*).

![XPath 3.1 and XQuery 3.1 Type Hierarchy, Part 3: Atomic Types](https://www.w3.org/TR/xpath-datamodel-31/XPathTypeHierarchy-3-anyAtomicTypes-3.1.png)

Voici la hiérarchie complète des type utilisé par le modèle de données XML. *XPath 3.1 and XQuery 3.1 Type Hierarchy, Part 3: Atomic Types.*

Tous les types sont définis par XML Schema, à l’exception de `xs:untypedAtomic`qui est définit par XDM. Notez que `xs:dateTimeStamp` est un nouveau type introduit dans XSD 1.1, il est dérivé par restriction du type `xs:dateTime`déjà existant pour rendre toutes ses facettes de zone obligatoires.

ex. utilisation de  `xs:dateTimeStamp` dans une XSLT

### Types de nœuds

- Document node
- Element node
- Attribute node
- Namespace node
- Processing Instruction node
- Comment node
- Text node

![XQuery 3.0 Type Hierarchy, Part 1: Items](https://www.w3.org/TR/xpath-datamodel-31/XPathTypeHierarchy-1-items-3.1.png)

*XQuery 3.0 Type Hierarchy, Part 1: Items* représente la hiérarchie des types de nœuds. Les boîtes vertes représentent les types dérivés possibles dans un document des nœuds attribut, document et élément. De telles définitions peuvent être fournies avec XML Schema.

Un document XM est un **arbre** (*tree*) formé de **nœuds** (*nodes*). Cet arbre dispose d’un **nœud racine** (*root node*). Un arbre avec un nœud racine qui est un **nœud document** est un **document** (*document*). Un **fragment** (*fragment*) est un arbre dont le **nœud racine** n’est pas le **nœud document** (*document node*).

### Types

XDM définit deux catégories de types

- les **nœuds-types** (*Node-Types*), il s’agit de n’importe quel type de nœud (document, élément, attribut, texte, commentaire, espace de nom, instruction de traitement)
- et les **nœuds-atomiques** (*Atomic-Types*), un types primitif simple ou un type dérivé par restriction d’un autre type atomique

Tout type est représenté par un ***Expanded QName***. Ce *Expanded QName* se compose de trois parties :

- un **Préfixe** (*Prefix*)
- une **URI d’espace de nom** (*Namespace URI*)
- un **nom-local** (*Local-name*)

Le préfixe et l’URI d’espace de nom peuvent être vides.

Les nœuds ont une **identité** (*identity*) tandis que les valeurs atomiques n’ont pas d’identité. 

Identité des nœuds

- node 1 ≡ node 1, chaque nœud est identique à lui-même et seulement à lui-même
- node 1 ≢ node 2, n’importe quel nœud n’est pas identique à n’importe quel autre nœud

Ordre du document

Le concept de l’ordre du document joue un rôle important dans XPath. Formellement, pour tous nœuds dans la stérilisation XML, un nœud précède le second exactement comme la stérilisation du premier nœud précède la stérilisation du second nœud dans la stérilisation du document XML.

**Propriétés des nœuds** (*Node Properties*) dans XDM

- **Nom** (*Name*) :
  Le nom d’un nœud est une séquence de 1 ou plusieurs xs:QName. La valeur de QName peut être tout type de valeur légale XML.
- **Type de nœud** (*Node King*) : 
  Le type de nœud est l’une des sept valeurs possibles de nœuds (*document*, *element*, *attribute*, *comment*, *text*, *namespace*, *processing instruction*)
- **Valeur de chaîne** (*String Value*)
- **Nom de type** (*Type Name*) :
  Le type de nom est un nom dans le type de schéma du nœuds sous la forme d’une séquence de zéro, 1 ou plusieurs xs:QName. Seuls des nœuds *document*, *element*, *attribute* peuvent avoir un nom de type.
- **Valeur typée** (*Types Value*) :
  Est la valeur d’un nœud en prenant en compte son nom de type. Par exemple, la valeur de chaîne d’un attribut est la chaîne. Cependant la valeur typée de cet attribut sera un entier si son type produit par la validation par un schema est xs:integer.

Les nœuds peuvent encore avoir d’autres propriétés.

- Les **enfants** (*Children*)
  Les enfants sont une propriété importantes des nœuds. Il s’agit d’une séquence de zéro ou plusieurs nœuds. Seulement un nœud document et un nœud élément peuvent avoir une séquence non vide d’enfants.

- Le **parent** (*Parent*)
  Il s’agit d’une séquence de zéro ou plusieurs nœuds. Parmi les nœuds d’un document XML, seul le nœud document peut avoir une séquence vide de nœuds parents.

- Attributs (*Attributes*)
  La propriété attribut est une séquence contenant zéro ou plusieurs nœuds attributs. Seul le nœud élément peuvent avoir un ensemble non vide d’attribut. L’ordre des attributs est défini par l’implémentation.

- L’espace de nom (*Namespaces*)

  Les espaces de nom, sont les espaces de noms dans la portée dynamiquement associés à un nœud. C’est une séquence contenant zéro ou plusieurs espaces de nom. De tous les types de nœuds, seul l’élément document peut avoir un ensemble non-vide d’espace de nom. L’ordre des espaces de nœud est défini par l’implémentation.

- Base URI 
  L’URI de base est une séquence contenant zéro ou une URI de référence. Si la séquence est non vide, l’URI qu’elle contient est déterminée par celle du document source, précisément l’entité externe depuis laquelle le document a été chargée.

- Document URI
  L’URI de document est une séquence de zéro ou une URI de référence. Seul le nœud document peut avoir une séquence non vide. Si c’est le cas, l’URI du document est l’URI absolue de la ressource depuis laquelle le document a été construit.

Il reste encore cinq propriétés définies par XDM qui sont moins fréquemment utilisées et qui sont relatives au schéma.

- Is ID
- Is IDREFS
- Nilled
- Unparsed Entity Public ID
- Unparsed Entity System ID

### Changements et nouveautés introduites depuis XDM 2.0

Si les changements sont peu nombreux entre XDM 2.0 et XDM 3.0, cela ne signifient pas que ceux-ci ne soient pas importants.

XDM 2.0 définit des types prédéfinis

- `xs:untyped` qui dénote le type dynamique d’un élément nœud qui n’a pas été validé, ou qui est validé en mode *skip*
- `xs:untypedAtomic` dénote des données atomiques non typées comme du texte qui n’ont pas été assigné à un type spécifique ou un attribut qui est validé en mode *skip*
- `xs:anyAtomicType` est une valeur atomique qui est définit par un type de valeur atomique et aucune valeur qui ne soit pas atomique.
- `xs:dayTimeDuration` est dérivé du type Duration de XML en restreignant sa représentation lexicale pour comprendre seulement ses composants de base heures, minutes, secondes. 
- `xs:yearMonthDuration` est dérivé du type Durationde XML en restreignant sa représentation lexicale pour comprendre seulement ses composants de base année et mois.

Ces trois derniers types ont été rendus officiels par XML Schema 1.1 et inclus dans XDM 3.1. C’est le premier changement dans le système de type.

Plus radicalement, deux nouveaux types de données ont été introduits dans XDM 3.0.

- `xs:dateTimeStamp` trouvé dans XML Schema 1.1 est dérivé par restriction du type existant `xs:dateTime` pour rendre sa zone temporelle explicitement requise. Ce type est totalement ordonné.
- `function` l’introduction de fonction est encore plus radicale.

### Le type fonction

Par définition, une **fonction** est un item qui peut être appelé. 

Il y a plusieurs restrictions au type fonction.

- les fonctions ne peuvent pas avoir d’identité
- aussi, les fonctions ne peuvent pas être comparées, même pour l’égalité
- les fonctions ne peuvent pas être sérialisées

Une fonction dispose d’un certain nombre de **propriétés**

| Nom                                     | Type                | Remarque                                                     |
| --------------------------------------- | ------------------- | ------------------------------------------------------------ |
| nom (*name*)                            | xs:QName            | Même si le nom est utilisé pour identifier les fonctions, le QName peut être absent |
| noms des paramètres (*parameter names*) | xs:QName*           | Noms pour chacun des paramètres                              |
| signature (*signature*)                 | Typed function test | Le type de la fonction. Il y a un SequenceType pour chaque paramètre et pour le résultat |
| implémentation (*implementation*)       |                     | Une expression dans un langage hôte ou définit par l’implémentation |
| *non-local variable bindings*           | xs:QName => item()* | Une valeur pour chacune des variables libres de la fonction  |
| parité (*arity*)                        | xs:integer          | Nombre de paramètres (entier non négatif)                    |

ex. évaluation expression qui contient nouveau type fonction.

```xquery
function-lookup(xs:QName('fn:substing'), 2)
```

La fonction `function-lookup`, prend deux arguments, un `xs:QName` et un entier non négatif. Son résultat est une fonction qui correspond a pour nom le premier argument, et pour arité le second argument, sinon elle renvoie une séquence vide.

- `function-name` renvoie le nom d’une fonction
- `function-arity` renvoie l’arité d’une fonction

```xquery
function-name(function-lookup(xs:QName('fn:substring'), 2)),
function-arity(function-lookup(xs:QName('fn:substring'), 2)),
function($x as xs:double) as xs:double { 
	$x*3 
	} (3)
```

Ici, la troisième fonction est anonyme, elle n’a pas de nom. Elle est appelée avec l’argument 3.

### Résumé

XDM joue un rôle fondamental pour XPath. Le modèle de données définit les types de nœuds, leurs propriétés et les types. De nouveaux types ont été ajoutés depuis XDM 2.0 notamment les types de données fonction.

## Nouveautés introduites dans XPath 3.0

### Contenu

types, constructs, operators et expressions

- Nouveaux types XPath 3.0, ceux adoptés de XML Schema 2.0 et les nouveaux types introduits avec XDM 3.0
- Nouveaux opérateurs XPath 3.0
- Nouvelles expressions XPath 3.0
- Référencement, définition et appel d’une fonction (statiquement ou dynamiquement)
- Subtyping relationship entre les fonctions

### Nouveaux types XPath 3.0

- `xd:dataTimeStamp`
- `function`
- `Generalized atomic type` définit dans un autre document XPath 3.0
  - soit un type atomique
  - soit un Pure union type
- `EQName`
- `xs:error` absent de la recommandation XDM, ne solutionne aucun cas d’usage XPath et pose de nombreuses questions.

Le *Pure Union Type* n’importe quel XML schema union type qui n’est pas dérivé d’autre types d’union par des restrictions non-triviales. Ils ont des list-types comme membres.

ex. définition d’un numérique

```xml
<xs:schema>
  <xs:simpleType name="numeric">
    <xs:union memberTypes="xs:decimal xs:double xs:float"/>
  </xs:simpleType>
</xs:schema>
```

- `3 instance of numeric` true() est une instance de numeric car une instance de integer et decimal
- `'3' instance of numeric` false()
- `7.8E0 instance of numeric` true()
- `'3' castable as numeric` true()

```xml
<xsl:function name="my:add" as="numeric">
  <xsl:param name="pLeft" as="numeric"/>
  <xsl:param name="pRight" as="numeric"/>
  <xsl:sequence select="$pLeft + $pRight"/>
</xsl:function>
```

### Expanded QName

Tout type est représenté par un ***Expanded QName***. Ce *Expanded QName* se compose de trois constituant :

- un **Préfixe** (*Prefix*)
- une **URI d’espace de nom** (*Namespace URI*)
- un **nom-local** (*Local-name*)

Le préfixe et l’URI d’espace de nom peuvent être vides.

Les *Expanded QNames* peuvent être écrits avec la notation `Q{uri}local`, qui permet d’écrire des expressions XPath qui ne dépendent pas d’un contexte d’espace de nom fourni par ailleurs.

Exemples :

- `pi` est un nom local, c’est un lexical QName (*A lexical QName (EQName*)
- `math:pi` c’est une pair de préfixe et de nom local. Lexical QName (*A lexical QName (EQName*). Il est accessible via le préfixe.
- `Q{http://www.w3.org/2005/xpath-functions/math}pi` est un *URI-Qualified name (EQName)*

### xs:error

Pas mentionné dans XDM 3.0. Ce type a probablement été ajouté au dernier moment dans XPath. Nouvellement introduit dans XML Schema 1.1.

Définition : 

- Empty value space
- Not an actual type
- Subtype of all simple types
- Supertype only of itself

xs:error? ≡ ()

xs:error* ≡ ()

Car xs:error ramène toujours une erreur. Ne jamais computer.

### Le type *map*

XPath 3.1 introduit la définition de maps. Un **map** est un nouveau type d’item dans le modèle de données XDM à côté des nœuds et des valeurs atomiques. Un map est une fonction extentionnelle (extensional function). Comment passe d’un ensemble de valeurs à l’autre en listant toutes les entrées. En réalité, un map est une sorte de fonction, on peut le concevoir comme une fonction définie de manière étendue (en tabulant la valeur de la fonction pour tous les arguments possibles) plutôt que de manière intentionnelle (au moyen d’un algorithme). cf. Michael Kay

Un map est un ensemble d’**entrées** (*entry*). Chaque entrée prend la forme d’une **parire clef-valeur** (*key-value pair*). La **clef** (key) est toujours une valeur atomique (*atomic value)*. La **valeur** (*value*) peut prendre n’importe quelle valeurs du modèle XDM : c’est-à-dire une séquence de nœuds, de valeurs atomiques, de fonctions, ou de maps.

Comme les séquences, les maps sont **immuables** (*immutable*). Lorsque l’on ajoute une entrée à un map, on obtient un nouveau map et l’original reste inchangé. De même, comme les séquences, les maps n’ont pas de type intrinsèque propre mais plutôt un type qui peut être déduit de ce qu’elles contiennent. Un map est conforme au type *map(K, V)* si toutes les clefs sont de type *K* et toutes les valeurs sont de type *V*. Par exemple, si les clés sont toutes des chaînes de caractères et les valeurs des éléments, alors le map est conforme au type `map(xs:string, element(employee))`.

Il existe plusieurs manières de créer des *map* :

**Lorsque le nombre d’entrée est connu**, il est possible d’utiliser la syntaxe de constructeur suivant :

```xquery
map { key : value, key : value, ...}
```

Ici, les clefs et les valeurs peuvent être n’importe quelle expression simple (*simple expression*), c’est-à-dire une expression qui ne continent pas une virgule en niveau haut.

Cette expression peut être employée n’importe où une expression XPath peut être employée (en XSL par exemple comme valeur de l’attribut @select d’un `xsl:variable` ).

**La fonction `map:merge()`** prend des maps en entrée et les combines en un seul map dont le nombre d’entrée n’est pas statiquement connu.

Par exemple, `map:merge(for $i in 1 to 10 retourne map{$i : codepoints-to-string($i)})`.

**Un map à une seule entrée peut être construit au moyen de la fonction `map:entry($key, $value)`**.

En XSLT, il est aussi possible de créer des maps en utilisant les fonctions `xsl:map` et `xsl:map-entry`.

Étant donné un map `$M`, la valeur correspondante à une clef donnée `$K` peut être trouvé soit en invoquant le map comme une fonction : `$M($K)`, soit en appelant `map:get($M, $K)`.

La spécification des fonctions dans XPath 3 offre une liste complète de fonctions qui opèrent sur les maps ([Functions Library](https://www.saxonica.com/html/documentation/functions/map)). Ces fonctions sont préfixées `map` et sont représentées dans l’espace de nom `http://www.w3.org/2005/xpath-functions/map`.

- `map:merge($maps as map(*)) as map(*)` : prend une séquence de maps en entrée et les combine en un seul map
- `map:size($map as map(*)) as xs:integer` : retourne le nombre d’entrées (paires clef-valeur) contenues dans un map
- `map:keys($map as map(*)) as xs:anyAtomicType*` : retourne les clefs qui sont présente dans un map, dans un ordre non prédictible
- `map:contains($map as map(*), $key as xs:anyAtomicType) as xs:boolean` : retourne la valeur vrai (*true()*) si la clef est présente dans le map.
- `map:get($map as map(*), $key as xs:anyAtomicType) as item()*` : retourne la valeur associée avec la clef lorsqu’elle est présente, sinon une séquence vide. Équivalent à appeler `$map($key)`
- `map:put($map as map(*), $key as xs:anyAtomicType, $value as item()*) as map(*)` : ajoute une entrée dans un map, qui remplace toute entrée existante ayant la même clef, et retourne un nouveau map
- `map:entry($key as xs:anyAtomicType, $value as item()*)` : créée un *singleton map*. Utile comme argument de `map:merge()`.
- `map:remove($map as map(*), $key as xs:anyAtomicType) as map(*)` : retire une entrée d’une map désignée par une clef (si elle est présente), et retourne un nouveau map. Si la clef n’est pas présente, retourne le map existant inchangé
- `map:for-each($map as map(*), $f as function(xs:anyAtomicType, item()) as item()*) as item()*` : traite toutes les paires clef-valeur d’un map en y appliquant la fonction donnée, retourne le résultat comme une séquence dans un ordre non prédictible.

[Traduit de : Michael Kay https://www.saxonica.com/html/documentation/expressions/xpath30maps.html]

### Le type tableau (*array*)

XPath 3.1 introduit les **tableaux** (*arrays*) comme nouveau type de données. À la différence des maps, les arrays ne sont pas définis pour être utilisés avec XSLT 3.0 à moins que XPath 3.1 soit supporté.

Ce nouveau type a principalement été introduit pour permettre de représenter conformément des structures de données JSON. Cependant, il est possible de profiter des tableaux de nombreuses manières.

Les tableaux (*arrays*) diffèrent des séquences (*sequences*) de plusieurs manières :

- Les tableaux (*arrays*) peuvent être imbriqués (*nested*) : un tableau peut avoir d’autres tableaux comme membres. En fait, les membres d’un tableau peuvent être des valeurs arbitraires de XDM, y compris des nœuds, des valeurs atomiques, des séquences, des fonctions ou des maps. Un membre d’un tableau peut aussi être une séquence vide (*empty sequence*).

- Un tableau est un singleton d’item, il est donc possible d’avoir une séquence de tableaux.

  Attention : comme un tableau est un item unique, `$array[1]` retourne le tableau en entière, et non pas son premier membre. De même `for $x in [1, 2, 3] return $x+1` retourne une erreur de type, car `$x` est lié au tableau dans son ensemble et non pas à chacun de ses membres.

- Pour accéder les *n* membres d’un array, on utilise la syntaxe `$array($n)`. Cela fonctionne car un tableau est une fonction : étant donné un entier *n* comme argument, cette fonction  retourne le membre en position *n*.

- Lorsque l’on connaît statistiquement le membre recherché, on peut également utiliser la syntaxe `$array?1` qui est équivalente à `$array(1)`.

- Les opérateurs et les fonctions conçus pour fonctionner sur des séquences comme `count()`, ou pour des expressions de filtre, `head()`, `tail()`, `remove()`, `insert()`, etc. ne fonctionnent pas sur les tableaux. Celles-ci ne renvoient pas d’erreur car un tableau est une séquence de longueur un, mais elles ne renvoient pas le résultats attendu. Une librairie de fonction spécifique est disponible pour réaliser des opérations similaires sur des tableaux.

  Néanmoins, les opérateurs conçus pour fonctionner sur des séquences de valeurs atomiques peuvent produire des résultats utiles lorsqu’on les applique à des tableaux de valeurs atomiques. Cela s’explique parce que l’atomisation d’un tableau produit la séquence correspondante. Par exemple `sum([1,2,3,4])` retourne 10, de même que `sum([[1,2], [3,4]])`.

Comme toutes les autres valeurs du modèle XDM, les tableaux sont immuables. Lorsque l’on ajoute à la fin (*append*), remplace ou retire un membre d’un tableau, on obtient un nouveau tableau et l’original reste inchangé.

Comme les séquences ou les maps, les arrays n’ont pas un type intrinsèque mais qui doit être inféré de leur contenu. Un tableau est conforme au type `array(T)` si tout ses membres sont de type `T`. Par exemple, si tous les membres d’un tableau sont de type chaîne de caractères, alors le tableau est conforme au type `array(xs:string)`.

Il y a plusieurs manières de créer un tableau :

Lorsque le nombre de membres est connu, vous pouvez utiliser la syntaxe de constructeur suivante :

```xquery
[ value, value, value]
```

Iic les valeurs peuvent être n’importe quelle expression simple (*simple expression*), c’est à dire toute expression qui ne contient pas immédiatement une virgule. 

Si les valeurs sont toutes connues statiquement, on peut écrire :

```xquery
[ 1, 2, "a", "b"]
```

Cette construction peut être utilisée à tous les endroits où une expression XPath peut être employée (en XSL par exemple comme valeur de l’attribut @select d’un `xsl:variable` ).

Les membres n’ont pas besoin d’être des singletons. Par exemple `[(), 1, 2, 5 to 10]` construit un tableau avec quatre membres qui sont respectivement des séquences de longueur 0, 1, 1 et 6.

Le constructeur `[ ]` retourne un tableau vide.

Si lle nombre de membres est inconnu, mais que l’on sait que chaque membre du tableau sera un singleton d’item, il est possible d’utiliser le constructeur `array{ value }` où `value` est n’importe quelle séquence. Par exemple, `array{(), 1, 2, 5 to 10}` construit un tableau avec huit membres qui sont des singleton d’entier (1, 2, 3, 4, 5, 6, 7, 8, 9 et 10).

Il n’y a pas d’instruction XSLT 3 pour créer des tableaux comme pour les maps. Toutefois saxon offre des instructions `saxon:array`, et `saxon:array-member`.

Un ensemble de fonctions qui opèrent sur les tableaux a été introduit par la spécification ([Functions Library](https://www.saxonica.com/html/documentation/functions/array)). Ces fonctions sont préfixées `array` qui représente l’URI d’espace de nom `http://www.w3.org/2005/xpath-functions/array`.

- `array:append` : ajoute un nouveau membre à la fin d’un tableau. 
  Par exemple, `array:append([], 5)` retourne `[5]`.
- `array:filter` : retourne les membres d’un tableau qui satisfont certaines conditions exprimées sous la forme d’une fonction. 
  Par exemple, `array:filter([1 to 5], function($x){$x mod 2 = 1})` retourne `[1, 3, 5]`.
- `array:flatten` : remplace un tableau par une séquence concaténée de ses membres, récursivement. 
  Par exemple, `array:flatten(([1], [2 to 4], [3, [4, 5]]))` retourne (1, 2, 3, 4, 3, 4, 5)`.
- `array:fold-left` : applique une fonction cumulativement aux membres successifs d’un tableau : chaque appel est appliqué avec deux arguments qui sont la valeur et le membre suivant du tableau. 
  Par exemple, `array:fold-left(array{1 to 5}, 0, function($x, $y){$x + $y})` retourne `15`, tandis que `array:fold-left(array{1 to 3}, [], function($x, $y){[$x, $y]})` retourne `[[[[], 1], 2], 3]`.
- `array:fold-right` : applique une fonction cumulativement aux membres successifs d’un tableau. Chaque appel est appliqué à deux arguments qui sont le prochain membre du tableau et le résultat de l’application de la function au reste du tableau.
  Par exemple, `array:fold-right(array{1 to 5}, 0, function($x, $y){$x + $y})` retourne `15`, ands que `array:fold-right(array{1 to 3}, [], function($x, $y){[$x, $y]})` retourne `[1, [2, [3, []]]]`.
- `array:for-each` : applique une fonction à chaque membre d’un tableau, et retourne un tableau qui contient les résultat.
  Par exemple, `array:for-each(array{1 to 5}, function($x){$x + 1})` retourne `[2, 3, 4, 5, 6]`.
- `array:for-each-pair` : applique une fonction à des pairs d’items correspondant dans deux tableaux qui ont été fournis.
  Par exemple, `array:for-each-pair(['x', 'y', 'z'], [1, 2, 3], concat#2)` retourne `['x1', 'y2', 'z3']`.
- `array:get` : retourne les membres à une position donnée (débute à 1).
  Par exemple, `array:get([3, 4, 5], 2)` retourne `4`.
- `array:head` : retourne le premier membre d’un tableau.
  Par exemple, `array:head([1 to 5, 1 to 10])` retourne `(1 to 5)` (une séquence et non pas un tableau).
- `array:insert-before` : insère un nouveau membre à une position donnée.
  Par exemple, `array:insert-before([1, 2, 3, 4], 3, ()]` retourne `[1, 2, (), 3, 4]`.
- `array:join` : joint un nombre de tableau bout-à-bout pour créer un nouveau tableau.
  Par exemple, `array:join(([1], [2 to 4], [3, [4, 5]]))` retourne `[1, (2, 3, 4), 3, [4, 5]]`.
- `array:put` : remplace les membres à une position donnée.
  Par exemple, `array:put([4, 5, 6], 2, 8)` retourne `[4, 8, 6]`.
- `array:remove` : retire le membre à une position données.
  Par exemple, `array:remove([4, 5, 6], 2)` retourne `[4, 6]`.
- `array:reverse` : renverse l’ordre des membres.
  Par exemple, `array:reverse([[1,2], [3,4]])` retourne `[[3,4], [1,2]]`.
- `array:size` : retourne le nombre de membres dans un tableau.
  Par exemple, `array:size([[1,2], [3,4]])` retourne `2`.
- `array:sort` : tri les membres d’un tableau, soit par leur propre valeur atomique, soit par le résultat de l’application d’une fonction pour calculer une clef de tri. Une collation peut également être spécifiée.
  Par exemple, `array:sort([4, 8, 2])` retourne `[2, 4, 8]`.
- `array:subarray` : retourne les memories d’un tableau à partir d’une position spécifiée et jusqu’à la fin du tableau ou à une distance spécifiée.
  Par exemple, `array:subarray([1, 2, 3, 4], 2)` retourne `[2, 3, 4]`, tandis que `array:subarray([1, 2, 3, 4], 2, 2)` retourne `[2, 3]`.
- `array:tail` : retire le premier membre d’un tableau.
  Par exemple, `array:head([1 to 5, 1 to 10]` retourne `[1 to 10]`.

[Traduction de XPath reference. https://www.saxonica.com/html/documentation/expressions/xpath31arrays.html]

### Nouveaux opérateurs XPath 3.0

XPath 3.0 introduit deux nouveaux opérateurs.

- l’opérateur de concaténation (*Concatenation operator*) est dénoté par `||`
- l’opérateur d’affectation simple (*Simple Map operator*) est dénoté par `!`

#### Exemple de concaténation

```xquery
'Con' || 'ca' || 'te' || 'nate'
```

est équivalente à 

```xquery
fn:concat('Con', 'ca', 'te', 'nate')
```

L’expression suivante retourne une chaîne de caractères

```xquery
('$') || 12.5
```

#### Exemple d’utilisation de l’opérateur d’affectation simple

XPath 3.0 a introduit l’**opérateur d’affectation simple** (*simple mapping operator*) `!`.

Une expression d’affectation simple (*simple mapping expression*) est une expression qui peut être définie par une expression de chemin suivie d’une ou plusieurs séquences composée de l’opérateur map et une autre expression de chemin. Il n’y aucune restriction sur la nature de chacune de ces expressions de chemin qui peuvent produire une séquence de nœuds ou d’items.

À première vue, l’opérateur d’affectation simple paraît très proche de l’opérateur `/`. Toutefois, les deux opérateurs présentent des différences notables.

| `E1 / E2`                                                    | `E1 ! E2`                                                  |
| ------------------------------------------------------------ | ---------------------------------------------------------- |
| E1 est une séquence de nœuds                                 | E1 peut contenir n’importe quel item                       |
| Les duplications sont retirées des résultats                 | Pas de suppression des doublons                            |
| Les résultats sont présentés dans l’ordre du document, ou par ordre du document des nœuds de E1 | Pas de réordonancement, simple concaténation des résultats |

L’expression `A!B` évalue l’expression `B`une fois pour chaque item dans le résultat de l’évaluation de  `A`, et concatène les résultats. 

Dans le cas où l’évaluation de  `A` retourne une séquence de nœuds, `A!B` a le même effet que  `A/B` à l’exception que le résultat n’est pas trié dans l’ordre du document et que les duplications ne sont pas éliminées. 

Contrairement à l’opérateur `/` l’opérande de gauche n’a pas besoin d’être une séquence de nœuds.

La sémantique de l’expression `A!B` est précisément équivalente à la construction XSLT `<xsl:for-each select="A"><xsl:sequence select="B"/></xsl:for-each>`.

```xquery
(1 to 7) ! (.*.)
```

Retourne la séquence  `(1, 4, 9, 16, 25, 36, 49)`

```xquery
(1 to 5) ! (. mod 2 eq 0)
```

Retourne : false, true, false, true, false. Ici, l’opérande de gauche renvoie une séquence d’entier, l’opérande de droite  évalue successivement si le modulo de 2 de chacune de ces valeurs est égal à zéro pour déterminer s’il s’agit d’un nombre pair, puis concatène les résultats sous la forme d’une séquence de valeurs booléennes. Noter que l’on n’aurait pas pu ici employer un opérateur `/` car l’opérande de gauche n’est pas un ensemble de nœuds.

```xquery
$emp ! (@first, @middle, @last)
```

Lorsque `$emp` est une variable qui contient une séquence d’éléments décrivant des employés, cette expression renvoie une séquence d’attribut @first, @middle et @last pour chaque employé, exactement dans cet ordre.

Si on remplace ici l’opérateur par le /, l’ordre n’est plus garanti car il dépend de l’ordre du document et que l’ordre des attributs dépend de l’application.

```xquery
avg(//employee/salary ! translate(.,'$', '') ! number(.))
```

Dans cette expression on rencontre une chaîne de deux expressions de répartition simple, le résultat de ces expressions est lui-même évalué par la fonction `avg` pour déterminer la moyenne des salaires des employés. Dans la première expression de répartition simple, l’opérande de gauche ramène une séquence de salaire pour chaque employé, on extrait de chaque valeur la valeur chiffrée, puis chacune de ces valeurs et transformée en entier. Le résultat de cette expression est une séquence qui est évaluée par la fonction moyenne. 

La première occurence aurait pu être remplacée par l’opérateur slash, en revanche la deuxième expression n’aurait pas pu l’être car il s’agit d’une séquence de chaînes de caractères.

```xquery
/*/num ! ..
```

L’opérande de gauche désigne les éléments fils `num` de l’élément racine du document. Le résultat est une séquence de nœuds document dont le nombre d’élément correspond au nombre d’éléments num fils du nœud racine.

Si l’opérateur avait été remplacé par `/` en raison du dédoublonnage, il n’y aurait qu’un seul nœud.

```xml
<nums>
  <num>01</num>
  <num>02</num>
  <num>03</num>
  <num>04</num>
</nums>
```

```xquery
/*/num ! (., 'Is even:', . mod 2 eq 0)
```

Ici l’opérateur map aurait rapporté une erreur car le résultat une séquence mixte composée d’élément et de contenu atomique ce qui est interdit.

### L’expression `let`

https://www.w3.org/TR/xpath-31/#id-let-expressions

L’expression `let` introduite dans XPath 3.0 est similaire de celle déjà introduite dans XQuery.

- une **expression let** (*Let expression*) est une  séquence de **clause let simple** (*Simple Let Clause*) suivie du mot-clef `return` et d’une expression unique (*Single Expression*).
- une **clause let simple** (*Simple Let Clause*) est composée du mot `let` suivi d’une **affectation let simple** (*Simple Let Binding*) et de zéro ou plusieurs `,` suivi d’une expression simple
- une **affectation let simple** (*Simple Let Binding*) est composée d’un `$`suivi du nom de la variable de `:=` puis d’une expression simple

L’expression après `return` s’appelle la **Return expression**, dans les binding, le nom de variable s’appelle aussi **plage de variable** (*Range variable*) et l’opérande de droite la **séquence de liaison** (*Binding sequence*)

*Multiple let binding*, exemples : 

```xquery
let $x := 5, $y := 2
return $x - $y
```

équivalent à :

```xquery
let $ := 5
	return let $y := 2
		return $x - $y
```

### Rappel sur l’expression `for` et les expressions conditionnelles `if` et `else`

XPath 2.0 avait également introduit une expression `for`

```xquery
for $i in (1 to 30) return $i * $i
```

```xquery
for $a in /nuts, $b in ('flour', 'surprise') return $a || ' ' || $b
```

XPath 2.0 permet l’utilisation d’expressions conditionnelles

```xquery
if (//element) then 'yes'
```

### Référencer, appeler et définir une fonction

Nouvellement introduits dans 3.0.

Le référencement d’une fonction (*Runction reference*) peut servir à définir une variable ou un paramètre dont la valeur est un nom de fonction. Cela permet également de passer la fonction comme paramètre, comme appel ou retourner comme résultat d’une fonction une autre fonction.

Fonction définie dans le contexte statique et complètement identifiée par on arité (*Arity*).

```xquery
name#0, substing#2
```

```xquery
let $f := name#1
return (my:fun($f,2), $f(/*))
substring#2("abcd",2)
```

Appel à une fonction

```xquery
name(.)
$f($x)
substing#2('abcd', 2)
```

Avec XPath 3.0, il est possible de définir complètement une fonction.

Exemple de fonction anonyme avec ses paramètres leur type et le type du retour.

```xquery
function($x as xs:double) as xs:double {
	$x * 3 (: corps de la fonction :)
}
```

Dans cette clause let, l’évaluation de `$y` est possible car `$x` est visible depuis son point de définition.

```xquery
let $x := 10, $y := 2 * $x
return $y + $x
```

Exemples de référence d’appels et de définitions de fonctions.

Ici, la variable `$f` est liée à la fonction `name` qui a une arité de 0. L’expression retournée présente un exemple d’appel dynamique de fonction dont le résultat est la valeur d’une variable. Elle fait référence au document courant et produit le nom de son élément racine.

```xquery
let $f := name#0
return /*/$f()
```

L’expression suivante produit une séquence de trois items. La fonction est définit pour produire une valeur double qui est trois fois la valeur de son argument.

```xquery
function-name(function-lookup(xs:QName('fn:substring'), 2)),
function-arity(function-lookup(xs:QName('fn:substring'), 2)),
function($x as xs:double) as xs:double {
	$x * 3
}(3)
```

### Types de fonction

Un test de fonction n’importe quel test qui évalue qu’un item est une fonction ou évalue sa signature.

Voici un test de fonction qui sélectionne n’importe quelle fonction qui est un item

```xquery
function(*)
```

Voici un test de fonction qui sélectionne un item seulement si l’item est une fonction avec une signature donnée, qui est un total d’argument qui serait seulement une séquence d’entier et dont le résultat serait un booléen

```xquery
function(xs:integer*) as xs:boolean
```

Nous sommes maintenant dans la position de pouvoir déterminer si une fonction est un sous-type d’une autre fonction.

Toute fonction est un sous-type de `function(*)`

Les deux fonctions doivent avoir le même nombre d’argument. Le retour d’un sous-type doit avoir les mêmes types d’argument et un sous-type de résultat. Les fonctions sous-types sont des covariants. Les types arguments des contrariant.

Exemple `function(item()) as item()` is-subtype-of `function(*)`

Exemple `function(item()) as xs:double` is-subtype-of `function(item()) as item()`

Exemple `function(item()) as item()` is-subtype-of `function(xs:int) as item()`

cf. article Wikipédia sur la covariance et contra variance (@todo revoir)

La hiérarchie des fonctions est infinie car leur nombre d’arguments est illimité de même que le type de leur résultat.

```xquery
let $f := function($x as item()) as item() { x }
return $f instance of function(*),
let $f := function($x as item()) as xs:double { 2 }
return $f instance of function(item()) as item(),
let $f := function($x as xs:int) as item() { 2 }
return  $f instance of function ( item()) as item(),
let $f := function($x as item()) as item() { 2 }
return $f instance of function(xs:int) as item()
```

## Nouvelles fonctions standard en XPath 3.0

De nombreuses nouvelles fonctions ont été introduites dans XPath 3.

### Fonctions qui opèrent sur les valeurs numériques, sur les chaînes, les nœuds et les séquences

#### Définitions

- Fonctions sur les valeurs numériques
- Fonctions sur les chaînes
- Fonctions sur les nœuds
- Fonctions sur les séquences

Le préfixe `fn: ` est lié à l’espace de nom des fonctions par défaut

Le préfixe `xs:` est lié à l’espace de nom des schémas XML

Le préfixe `math:` est lié à l’espace de nom des fonctions mathématiques

Le préfixe `err:` est lié à l’espace de nom des erreurs

Le préfixe `output:` est lié à l’espace de nom des fonctions de stérilisation

Il n’existe pas de type numérique formellement défini dans le standard, il dérive seulement de `xs:decimal`, `xs:float`, `xs:double` comme un pseudo-type.

Le concept d’*Overloading* désigne l’appel d’une fonction avec un argument supplémentaire. ex. `substing('abcd', 2)` et `substring('abcd', 2, 1)`

La substitution de sous-type `xs:interger` <- `xd:decimal`

Promotion de type.

Le même appel à une fonction avec les mêmes arguments peuvent ramener des résultats en fonction de la portée de l’exécution (*Execution scope*). 

On peut dire que deux valeurs sont identiques quand elles ont le même nombre d’item et que celles-ci sont identiques les uns aux l’autre.

Deux fonctions doivent avoir le même nombre de paramètre de signature et 

- Atomic1 eq Atomic2
- Node1 ≡ Node2
- Name(F1) eq Name(F2) et Signature(F1) eq Signature(F2) et Closure(F1) same as Closure(F2)

Une fonction dépendante de son contexte (*Context-dependent function*) dépend de son contexte statique ou dynamique. Les arguments implicites sont partie du contexte dont dépend la fonction.

Une fonction déterministe (*Deterministic function*) produit des résultats identiques lorsqu’elle est appelée plusieurs fois depuis une seule exécution avec des arguments explicites ou implicites identiques lors de chaque appel.

Les fonctions on par défaut la propriété d’être déterministes et non dépendantes du contexte.

#### Nouvelles fonctions trigonométriques

- `math:pi`

Fonctions définies à partir d’un triangle

- `math:sin`
- `math:cos`
- `math:tan`

Fonctions trigonométriques inverses.

- `math:asin`
- `math:acos`
- `math:atan`
- `math:atan2(y,x)`

#### Groupes de fonctions exponentielles et logarithmiques

Fonctions exponentielles

- `math:exp``
- `math:exp10`
- `math:pow`
- `math:sqrt`

Fonctions logarithmiques

- `math:log`
- `math:log10`

```xquery
math:sin(math:pi() div 2),
for $a in 1 to 10
return math:pow(math:sin($a), 2) + math:pow(math:cow($a), 2)
```

#### Nouvelles fonctions pour les chaînes de caractères

String-join concatène la sequence du premier argument en les séparant par l’argument 2. Si la valeur du deuxième argument est vide, elle les concatène sans délimitateur (*overload*)

- `string-join('$arg1' as xs:string*, $arg2 as xs:string) as xs:string`

XPath 2.0 avait déjà introduit plusieurs fonctions qui fonctionnent utilisent des regex (matches, tokenize et replace).

- `fn:matches($input as xs:string?, $pattern as xs:string, $flags as xs:string) as xs:boolean
  Ramène un `xs:boolean` indiquant si la valeur de `\$input` correspond (*matches*) à l’expression régulière fournie comme `\$pattern` selon l’argument `\$flags` s’il est fourni
- `fn:tokenize($input as xs:string?, $pattern as xs:string) as xs:string*`
  Découpe l’`$input` en une séquence de chaînes de caractères en traitant toute sous-chaîne qui correspond au `$pattern` comme séparateur. Les séparateurs ne sont pas retournés.
- `fn:replace($input as xs:string?, $pattern as xs:string, $replacement, $flags) as xs:string*`
  Retourne la chaîne de caractère obtenue en remplaçant chaque sous-chaine non-overlapping de `$input` qui correspond au `$pattern` avec l’occurence d’une chaîne de remplacement.

XPath 3 introduit une nouvelle fonction pour travailler avec des regex.

- `analyse-string($input as xs:string?, $pattern as xs:string) as element(fn:analyze-string-result)`
- `analyse-string($input as xs:string?, $pattern as xs:string, $flags as xs:string) as element(fn:analyze-string-result)`

La fonction est non-déterministe.

```xquery
analyze-string('The cat sat on the mat.', '\w+')
```

Résultat :

```xml
<fn:analyze-string-result xmlns:fn:"http://www.w3.org/2005/xpath-functions">
	<fn:match>The</fn:match>
  <fn:match>cat</fn:match>
  <fn:match>sat</fn:match>
  <fn:match>on</fn:match>
  <fn:match>the</fn:match>
  <fn:match>mat</fn:match>
  <fn:non-match>.</fn:non-match>
</fn:analyze-string-result>
```



### Autres

- Fonctions sur les entiers, les nombres et les valeurs temporelles
- Fonction donnant accès à de l’information externe
- Fonctions pour parser et sérialiser
- Constructor Functions
- Casting to list / union types

### Fonctions de haut-niveau

Exemples

`(0.9 * 0.2) + (0.3 * 0.8)`

```xquery
sum(for $i in 1 to count($A/col) return number($A/col[$i]) * number($B/col[$i]))
```

```xquery
 sum(for-each-pair($A/col, $B/col, function($a, $b) { $a * $b}))
```



## Sources

- Dimitre Novatchev. The Evolution of XPath: What’s New in XPath 3.0. Pluralsight. https://app.pluralsight.com/course-player?clipId=4e83cced-f061-4172-8316-31089c7e1511
- Michael Kay, Reference XPath Syntax
- Code http://bit.ly/VYWrwh