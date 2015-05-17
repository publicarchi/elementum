XQuery Update pour les impatients, Une rapide introduction à la fonctionnalité de mise à jour de XQuery
=========

essai de traduction française de

Xavier Franc, XQuery Update for the impatient, A quick introduction to the XQuery Update Facility, http://www.xmlmind.com/tutorials/XQueryUpdate/index.html

CC Attribution-ShareAlike

Table des matières
========

1. Bases
 1.1. Les primitives de mise à jour
    1.2. Comment les primitives de mise à jour se combinent avec le langage de base ?
    1.3. Le modèle de traitement
2. Pour allez plus loin
    2.1. Les opérations avec les primitives revisitées
    2.2. Le problème des mises à jour invisibles
    2.3. Mélanger des expressions de mise à jour avec d'autres expressions
    2.4. Ordre et conflits
3. Conclusion

La fonctionnalité de mise à jour XQuery Update est une relativement petite extension du langage XQuery qui fournit des moyens adaptés pour modifier des documents ou des données XML. Depuis qu’elle est devenue une `recommandation candidate` le 14 mars 2008, la [spécification XQuery Update Facility]() est aujourd’hui plutôt stable.

Pourquoi une fonctionnalité de mise à jour en XML Query ? La réponse peut paraître évidente mais, après tout, le langage XQuery lui-même – ou encore son cousin XSLT2 – est suffisamment puissant pour écrire n’importe quelle transformation d’un arbre XML. Ainsi, une simple fonction `store` ou `put` pourrait sembler suffisante pour réaliser n’importe quelle opération de mise à jour de base de données. Bon, peut-être… En pratique, cela ne serait ni très naturel ou pratique, ni non plus très efficient (une telle approche nécessiterait de stocker tout le document et rendrait l’optimisation très difficile). Ainsi, comme nous allons le voir, la petite complexité ajoutée par XQuery Update semble valoir la peine.

Ce tutoriel essaye de donner une rapide introduction pratique, mais aussi compréhensive, de l’extension XQuery Update, tout en mettant en lumière certaines de ses particularités.

__Pré-requis__ : le lecteur est présumé avoir qeulques accointances avec XML Query et son modèle de données (XDM, la représentation abstraite des données XML qui comporte six types de nœuds : document, element, attribute, text, comment, processing-instruction).


## 1. Bases

### Les primitives de mise à jour

La fonctionnalité de mise à jour de XQuery (_XQuery Update Facility_, abrégée en XQUF ci-après) fournit cinq opérations de base qui agissent sur des nœuds XML :
- __insérer (_insert_)__ un ou plusieurs nœuds dans/après/avant un nœud spécifié ;
- __effacer (_delete_)__ un ou plusieurs nœuds ;
- __remplacer (_replace_)__ un nœud (et tous ses descendants si c’est un élément) par une séquence de nœuds ;
- __remplacer le contenu (_replace the contents_)__ (c’est-à-dire les fils) d’un nœud par une séquence de nœuds, ou la __valeur (_value_)__ d’un nœud avec une valeur de chaîne ;
- __renommer (_rename_)__ un nœud (applicable aux éléments, attributs et instructions de traitements) sans affecter leurs contenus ou attributs.

Ces primitives sont détaillées ci-après.

### 1.2. Comment les primitives de mise à jour se combinent-elles avec le langage ?

Typiquement, on utilise des requêtes pour sélectionner le(s) nœud(s) que l’on souhaite mettre à jour, puis on applique à ce(s) nœud(s) l’opération de mise à jour. Cela est très similaire à l’instruction SQL `UPDATE … WHERE …`.

#### Exemple n°1 :

Dans un document `doc.xml`, renommer en tant que "SECTION_TITLE" tous les éléments fils "TITLE" d’une "SECTION" :

```xquery
    for $title in doc("doc.xml")//SECTION/TITLE  (: sélection :)
    return rename node $title as SECTION_TITLE   (: mise à jour :)
```

#### Exemple n°2 :

Pour tous les éléments "ITEM" qui ont un attribut "Id", remplacer cet attribut par un enfant "NID" en première position :

```xquery
    for $idattr in doc("data.xml")//ITEM/@Id     (: sélection :)
    return (
        delete node $idattr,                     (: mise à jour 1 :)
        insert node <NID>{string($idattr)}</NID> (: mise à jour 2 :)
            as first into $idattr/..
    )
```

Avec ce dernier script, le fragment suivant

```xml
    <ITEM Id="id123">some content</ITEM>
```

serait transformé en :

```xml
    <ITEM><NID>id123</NID>some content</ITEM>
```

__Remarque__ : Dans ce dernier exemple, il est absolument indifférent que l’instruction `delete` soit inscrite avant ou après `insert node`. Cette propriété surprenante de XQUF est expliqué ci-dessous.

Il existe des restrictions dans la manière dont les cinq opérations de mise à jour peuvent être mélangées avec le langage XQuery de base. XQUF fait une distinction entre les `Expressions de mise à jour (_Updating Expression_), lesquelles englobes les primitives de mise à jour, et les `Expressions qui ne mettent pas à jour` (_non-updating expressions_). Les expressions de mise à jour ne peuvent pas apparaître n’importe où. Cette question sera expliquée plus en détail.


### 1.3. Modèles de traitement

Il y a deux manières principales d’utiliser les primitives de mise à jour :

#### 1. par mise à jour directe d’une base de données XML :

Dans les exemples ci-dessus, les nœuds appartenant à une base de données sont sélectionnés puis mis-à-jour.

__Remarque__ : La notion de base de données en XQUF est très générique : elle recouvre n’importe quelle collection de documents ou de fragments XML bien formés.

XQuery Update ne définit pas précisément le protocole au moyen duquel les opérations de mise à jour sont appliquées à une base de données. Les implémentations sont laissées libres. Par exemple, les questions relatives aux transactions et à l’isolation ne sont pas prise en compte par les spécifications.

On suppose simplement que les mises à jour sont appliquées à la base de données quand l’exécution d’un script est terminée. Le langage est conçu de telle manière que la sémantique des opérations de mise à jour `apply-updates` est précisément définie, ainsi toute la latitude nécessaire est laissée pour l’optimisation aux implémentations des bases de données.

Points à noter :
- _Les mises à jour ne sont pas appliquées immédiatement lorsque l’expression s’exécute_. Au contraire, elles sont accumulées dans une liste de mise à jour en attente (_Pending Udate List_). À un certain moment, vers la fin de l’exécution, ces mises à jour en attente sont appliquées toutes en même temps, et la base de données est mise à jour atomiquement.
Une conséquence notable est que les _mises à jour ne sont pas visible pendant l’exécution du script_, mais seulement après. Cela peut être déconcertant pour un développeur. Cela a également une influence évidente sur le style de programmation. Nous verrons plus loin des exemples de cet effet et la manière d’en tenir compte.
- La même expression peut mettre à jour plusieurs document en même temps. Les exemples ci-dessus pourraient être appliqués à n’importe quelle collection de documents au lieu du simple document `doc.xml`.
Exemple :
```xquery
    for $title in collection("/allbooks")//SECTION/TITLE
    return rename node $title as SECTION_TITLE
```

#### 2. par transformation sans effet de bord :

XQUF dispose d’une opération supplémentaire appelée `tranform` qui met à jour la copie d’un nœud existant, sans modifier l’original et retourne l’arbre transformé.

L’exemple suivant produit une version transformée de `doc.xml` sans toucher le document original :

```xquery
    copy $d := doc('doc.xml")
    modify (
        for $t in $d//SECTION/TITLE
        return rename node $t as SECTION_TITLE
    )
    return $d
```

Remarquez qu’_au sein de la clause modify_ XQUF interdit de modifier la _version originale_ des arbres copiés (ici le document `doc.xml` lui-même) : seuls les arbres copiés peuvent être modifiés. L’expression qui suit générerait une erreur :

```xquery
    copy $d := doc("doc.xml")
    modify (
        for $t in doc("doc.xml")//SECTION/TITLE (: **** FAUX **** :)
        return rename node $t as SECTION_TITLE
    )
    return $d
```

## 2. Pour aller plus loin

### 2.1. Les opérations primitives revisitées

#### `delete nodes`

Syntaxe :

```xquery
  delete node location
```

```xquery
  delete nodes location
```

L’expression _location_ représente une séquence de nœuds qui sont markés pour la suppression (le nombre effectif de nœud n’a pas besoin de correspondre au mot-clef `node` ou `node`).

#### `insert nodes`

Syntaxe :

```xquery
  insert (node|nodes) items into location
```

```xquery
  insert (node|nodes) items as first into location
```

```xquery
  insert (node|nodes) items as last into location
```

```xquery
insert (node|nodes) items before location
```

```xquery
insert (node|nodes) items after location
```

L’expression _location_ doit pointer vers un seul nœud cible.

L’expression _items_ doit fournir une séquence d’items à insérer relativement dans le nœud cible.

Remarquez que bien que le mot-clef `node` ou `node` soit employé, les items insérés peuvent être autre chose que des nœuds. En réalité, ce qui arrive c’est que les valeurs de chaînes (_string values_) des items qui ne sont pas de type node() sont concaténés pour former des nœuds textuels.

- Lorsque l’on utilise `into`, alors le nœud cible doit être un élément ou un document. Les items à insérer sont traités exactement comme les contenus d’un élément constructeur (`element constructor`).

Par exemple, si `$target` pointe vers un élément vide `<CONT/>`,

```xquery
  insert nodes (attribute A { 2.1 }, <child1/>, "text", 1 to 3)
  into $target
```

Ramène :

```xml
  <CONT A="2.1"><child1/>text 1 2 3</CONT>
```

Dans ce cas, les même règles que pour les constructeurs s’appliquent : l’ordre des items est préservé, un espace est inséré entre des items consécutifs qui ne sont pas de type nœud, les nœuds insérés sont copiés en premier, les nœuds attributs ne sont pas autorisés après d’autres types d’item, etc.

- Quand les mot-clefs `as first` (et respectivement `as last`) sont employés, les items sont insérés avant (respectivement après) n’importe quel enfant existant de l’élément.

Par exemple, si `$target` pointe vers un élément `<parent><kid/></parent>`,

```xquery
  insert node <elder/> as first into $target
```

Ramène :

```xml
  <parent><elder/><kid/></parent>
```

Lorsque le seul mot-clef `into` est utilisé, la position résultante est dépendante de l’implémentation. Il est seulement garanti que `as first into` et `as last into` aient la priorité sur `into`.

- Si `before` et `after` sont utilisés, n’importe quel type de nœud est autorisé pour le nœud cible.

- Le cas des attributs est un cas spécifique : indépendamment du fait que les mot-clefs `before` et `after` soient utilisés, les attributs sont toujours insérés `into` l’élément parent de la cible. L’ordre des attributs insérés n’est pas spécifié. Les conflits de noms peuvent générer des erreurs.  

#### `replace node`

Syntaxe :

```xquery
  replace node location with items
```

L’expression _location_ doit pointer vers un nœud unique cible.

L’expression _items_ doit ramener une séquence de nœuds qui remplacera le nœud cible.

- Excepté pour les nœud de type attribut et document, le nœud cible peut être remplacé par n’importe quelle séquence d’items. Les items de remplacement sont traités exactement comme les contenus d’un constructeur element ou document.

Par exemple si `$target pointe vers un élément `<P><kid/>some text</P>`,

```xquery
  replace node location $target/kid with "here is"
```

ramène :


```xml
  <P>here is some text</P>
```

- Les attributs sont un cas spécifique : ils peuvent seulement être remplacé par un nœud attribut. Les conflits de nommage peuvent générer des erreurs.

#### `replace value of node`

Syntaxe :

```xquery
  replace value of node location with items
```

Ici, l’identité du nœud cible est préservée. Seule sa valeur ou ses contenus (pour un élément ou un document) est remplacée.

- Si la cible est un nœud élément ou un nœud document, alors tous ses enfants précédents sont retirés et remplacés. Les items de remplacement sont traités exactement comme les contenus d’un constructeur de texte (donc tous les items de nœud sont remplacés par leur valeur-textuelle).

Par exemple si `$target` pointe vers un élément `<P><kid/>some text</P>`,

```xquery
  replace value of node $target with (<text>let's count: </text>, 1 to 3, "...")
```

Ramène :

```xml
  <P>let’s count: 1 2 3 ...</P>
```

Alors, les contenus d’élément sont remplacés par un nœud texte dont la valeur est la concaténation des valeurs textuelles des items de remplacement.

- Si le nœud cible est une feuille (attribut, texte, commentaire, instruction-de-traitement) alors sa valeur de chaîne est remplacée par la concaténation des valeurs de chaînes des items de remplacement.

Par exemple si `$target` pointe ver un élément `<P order="old">some text</P>`,

```xquery
  replace value of node $target/@order with (1 to 3, <ell>...</ell>)
```

Ramène :

```xml
  <P order="1 2 3...">some text</P>
```

#### `rename node`

Syntaxe :

```xquery
  rename node location as name-expression
```

L’expression _location_ doit pointer vers un élément cible, un attribut, ou une instruction de traitement unique.

L’expression _name-expression_ doit ramener un QName ou une chaîne de caractères.

Par exemple, si `$target` pointe vers un élément `<CONT A="a">some texte</CONT>`

```xquery
  rename node $target as qName("some.namespace", "CONTAINER"),
  rename node $target/A as "NEWA"
```

Ramène :

```xml
  <ns1:CONTAINER NEWA="a" xmlns:ns1="some.namespace">some text</ns1:CONTAINER>
```

#### `transform`

Syntaxe :

```xquery
  copy $var := node [, $var2 := node2 ...]
  modify updating-expression
  return expression
```

Chaque expression _node_ est copiée (au moins virtuellement) et liée à une variable.

L’expresion _updating-expression_ contient ou invoque une ou plusieurs primitives de mise à jour. Ces primitives _sont autorisées à agir sur l’arbre résultat_, et pointé par les variables liées. Aussi, l’expression de transformation n’a pas d’effet de bord.

Avant que l’expression _return_ soit évaluée, toutes les mises à jour sont appliquées aux arbres copiés. Typiquement, l’expression _return_ sera liée à une variable, ou un constructeur de nœud engageant les valiables liées, ainsi cela ramène le(s) arbre(s) mis à jour.

Par exemple si `$target` pointe vers un élément :

```xquery
  copy $target := <CONT id="s1">some text</CONT>
  modify (
    rename node $target as "SECTION",
    insert node <TITLE>The title</TITLE> as first into $target
  )
  return element DOC { $target }
```

Retourne :

```xml
  <DOC><SECTION id="s1"><TITLE>The title</TITLE>some text</SECTION></DOC>
```xml

Ramène :

```xml
  <ns1:CONTAINER NEWA="a" xmlns:ns1="some.namespace">some text</ns1:CONTAINER>
```

### 2.2. Le problème des mises à jour invisibles

Le fait que les mises à jour soient appliquées seulement à la fin d’un script d’exécution a deux conséquences en matière de programmation, l’une ennuyeuse, l’autre plaisante :

- La conséquence ennuyeuse est que vous ne pouvez pas voir vos mises à jour avant la fin, et pour cette raison vous ne pouvez pas construire d’autres changements sur vos transformations.

Par exemple, supposez que vous ayez des éléments nommés `PERSON`. Au sein de `PERSON` il peut y avoir une liste d’éléments `BID` (les bids représentatifs réalisés par cette personne), et vous voulez que les éléments `BID` soit entourés par un élément `BIDS`. Mais initialement, `PERSON` n’a pas de fils `BIDS`.

On a initialement :

```xml
  <PERSON id="p0234">
    <NAME>Joe</NAME>
  </PERSON>
```

Nous voulons insérer `<BID id="b0012">data</BID>` pour obtenir :

```xml
  <PERSON id="p0234">
    <NAME>Joe</NAME>
    <BIDS>
      <BID id="b0012">data</BID>
    </BIDS>
  </PERSON>
```

Classiquement, par exemple en utilisant le DOM, nous pourrions procéder en deux étapes :
1. S’il n’y a pas d’élément `BIDS` dans `PERSON`, alors en créer un
2. _puis_ insérer un élément `BID` dans l’élément `BIDS`

Avec XQuery Update, cela serait incorrectement écrit comme suit :
```xquery
  declare updating function insert-bid($person, $bid)
  {
    if(empty($person/BIDS))
      then insert node <BIDS/> into $person
      else (),
    insert node $bid as last into $person/BIDS
  }
```

__N’essayez pas cela, cela ne fonctionne pas !__ Pourquoi ? Parceque l’élément `BIDS` serait uniquement créé à la fin, en conséquence l’instruction `insert … as last into $person/BIDS` ne trouvera aucun nœud avec lesquels correspondant à l’expression `$person/BIDS`, et produit donc une erreur d’exécution.

Alors, quelle est la manière appropriée pour réaliser cette opération ? Nous avons besoin d’une solution autonome dans les deux cas :

```xquery
  declare updating function insert-bid($person, $bid)
  {
  if(empty($person/BIDS))
    then insert node <BIDS>{$bids}</BIDS> into $person
    else insert node $bid as last into $person/BIDS
  }
```

- La conséquence favorable est que le(s) document(s) sur lesquels vous travaillez sont stables durant l’exécution de vos scripts. Vous pouvez être assurés que vous ne sciez pas la branche sur laquelle vous êtes assis. Par exemple, vous pouvez tranquillement écrire :

```xquery
  for $x in collection(...)//X
  return delete node $x
```

Cette expression est parfaitement prévisible et ne s’interrompra pas prématurément. Ou vous pouvez répliquer un élément après lui sans risquer de boucles infinie :

```xquery
  for $x in collection(...)//X
  return insert node $x after $x
```

### 2.3. Mélanger des expressions de mise à jour (_Updating Expression_) et des expressions qui ne mettent pas à jour (_Non-updating Expression_)

Les Expressions XQuery de mise à jour (_Updating Expression_) sont des expressions qui comprennent les cinq primitives de mise à jour.

Il y a des règles concernant la manière de mélanger des expressions de mise à jour et les expressions qui ne mettent pas à jour :

- Tout d’abord, souvenons-nous que les Expressions de mise à jour ne retournent pas de valeur. Elles ajoutent seulement une requête de mise à jour à une liste. Les mises à jour dans la liste sont éventuellement appliquées à la fin de l’exécution d’un script (ou à la fin de la clause `modify` dans le cas de l’expression `transform`).

- De ce fait, les Expressions de mise à jour ne sont pas permises aux endroits où une valeur significative est attendue. Par exemple, la condition d’un `if`, la partie droite d’une affectation `let :=`, la partie `in` d’une claude `for`, etc.

- Mélanger des Expressions de mise à jour et des expressions qui ne mettent pas à jour n’est pas autorisé dans une séquence (la virgule comme séparateur). Même si c’est techniquement faisable, cela ne ferait pas beaucoup de sens de mélanger des expressions qui retournent une valeur et des expressions qui ne le font pas (souvenez-vous que l’opérateur de séquence retourne une concaténation des séquences retournées par leurs composants).

La fonction `fn:error()` et la séquence vide `()` sont spéciaux car il peuvent apparaître à la fois dans des expressions qui mettent à jour ou non.

- De la même manière, les branches d’un `ìf` ou un `typeswitch` doit être consistant : tant pour les expressions de mise à jour ou qui ne mettent pas à jour. Si les deux branches mettent à jour, alors le `if` lui-même est considéré comme mettant à jour, et inversement.

- Si le corps d’une fonction est une expression de mise à jour, alors la fonction doit être déclarée avec le mot-clef `updating`. Par exemple :

```xquery
  declare updating function insert-id($elem, $id-value) {
    insert node attribute id { $id-value } into $elem
  }
```

Un appel à une telle fonction est en lui-même considéré comme une Expression de mise à jour. Logiquement, une fonction de mise à jour retourne aucune valeur, et de ce fait il n’est pas permis de déclarer le type du résultat.

## 2.4. Ordre et conflits

Une autre conséquence du mécanisme de mises à jour en attente est que l’ordre dans lequel les mises à jour sont spécifiées n’est pas important. Dans l’exemple suivant, vous pouvez sans problème supprimer l’attribut `Id` (pointé par `$idattr`), et après utiliser l’expression XPath `$idattr/..` (l’élément parent `ITEM`) pour l’insertion ! Ou bien vous pouvez insérer d’abord et effacer ensuite.

```query
  for $idattr in doc("data.xml")//ITEM/@Id   (: selection :)
  return (               (: updates :)
    delete node $idattr,
    insert node <NID>{string($idattr)}</NID> as first into $idattr/..
  )
```

Mais pour cette raison, des changement conflictuels peuvent produire des résultats imprévisibles. Par exemple, deux renommage du même nœud sont conflictuels, parce qu’on ne sait pas quel ordre doit être appliqué. Autres opérations ambiguës : deux remplacement du même nœud, deux remplacement de valeur (ou de contenu) sur le même nœud.

Les spécifications XQUF prennent soin d’interdire de telles mises à jour ambiguës. Une erreur est générée (au cours de l’étape d'application des mises à jour) lorsqu’un tel conflit est détecté.

Un peu ironiquement, aucune erreur n’est générée pour les conflits sans signification mais non ambigus, par exemple à la fois en renommant et effaçant le même nœud (effacer un nœud a une priorité sur les autres opérations).


## 3. Conclusion

Les fonctionnalités de mise à jour de XQuery constituent une puissante et élégante extension du langage XQuery, en dépit de quelques particularités qui peuvent s’avérer déroutantes pour les programmeurs.

Nous espérons sa large adoption comme langage de choix pour la mise à jour de bases de données XML. Au moment de la rédaction de ce tutoriel, il existe déjà quelques implémentations : Monet DB (CWI), Qizx (XMLmind), Oracle Berkeley DB XML (Oracle), XQilla.

[ndtr : ajoutons aujourd’hui les bases de données XML natives libres et open source telles que BaseX ou eXist.]



We are looking forward to its wide adoption as the language of choice for updating XML databases. At the time this tutorial was written, there were already a few implementations: Monet DB (CWI), Qizx (XMLmind), Oracle Berkeley DB XML (Oracle), XQilla.
