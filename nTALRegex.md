# TAL avec des expressions régulières

On utilisera très souvent pour du traitement de texte et la recherche simple des expressions régulières.

Une **expression régulière (ER)** est une façon simple de caractériser un ensemble de chaînes de caractères, de façon compacte.

- ex. toutes chaînes de caractères correspondant à un montant en argent

C’est un formalisme utile pour faire de l’extraction d’information (simple) dans des données textuelles.

- l’outil Unix `grep -E` retourne toutes les lignes contenant une ER
- l’outil Unix `perl -p -e` permet d’appliquer des remplacements
- la plupart des langages de programmation généralistes prennent en charge les expressions régulières

L’expression régulière la plus simple consiste à préciser une seule chaîne de caractères

- une **correspondance** (match) est obtenue pour chaque sous-chaîne trouvée
- la casse (minuscule ou majuscule) est respectée

NB : en Perl les expressions régulières sont encadrées par des `/` (dans le livre sont seulement soulignées les premières occurence des correspondances)

#### Disjonction, négation, répétition

Les opérations de disjonction, négation, répétition, vont nous permettre de manipuler du texte de manière plus approfondie avec des expressions régulières.

##### Dijonction

Pour correspondre à plus d’une chaîne, on peut utiliser des disjonctions de caractères à l’aides des crochets `[`et `]`.

- `[wW]` *w* ou *W*
- `[abc]` *a* ou *b*, ou *c*

L’utilisation d’**intervalles** est aussi permise pour faire des dijonctions

- `[A-Z]` l’ensemble des majuscules
- `[0-9]` un chiffre de 0 à 9

##### Négation

Le symbole `^` permet de formuler une **négation**. Il doit être à l’intérieur de crochets et être le premier symbole.

- `[^A-Z]` tout sauf une majuscule
- `[^Ss]` ni *S* ni *s*
- `[^\.]` pas un point

Le signe circonflexe peut toutefois être utile s’il n’est pas placé au début d’une expression

- `[e^]`soit *e* ou *^*
- `a^b` le motif *a^b*

S’il se trouve au début de l’ER, il correspond à un début de ligne (`$` fin de ligne).

##### Caractère optionnel, répétitions

Le symbole `?` permet d’identifier un caractère qui est **facultativement** présent. Le caractère optionnel est celui qui précède le `?`

- `woodchucks?` *woodchuck* ou *woodchucks*
- `colou?r` *color* ou *colour*

Les symboles `*` et `+` permettent d’exprimer un nombre arbitraire (possiblement 0 pour `*`) de **répétitions**.

- `a*` correspond à *a*, *aa*, *aaa*, etc. ainsi que la chaîne vide
- pour ne pas inclure la chaîne vide : `aa*` ou `a+`

##### Disjonctions de chaînes

Les crochets permettent des disjonctions de caractères individuels. Pour faire une disjonction sur des chaînes de caractères, on utilise le symbole `|`.

- `cat|dog` correspond avec la présence du mot *cat* ou du mot *dog*

On peut appliquer à une sous-chaîne de l’ER, à l’aide de parenthèses.

- `gupp(y|ies)` correspond à *guppy* et *guppies*

#### Combinaison d’opérations

Il est ensuite possible de combiner ces opérations. Pour ce faire il existe des priorités entre ces opérations. Les voici par ordre descendant :

- Parenthesis	`()`
- Couters `*` `+` `{}`
- Sequences and anchors `the ^my end$`
- Dijunction `|`

ex. pour une entête de tableau comme *Column 1 Column 2*, etc.

`(Column [0-9]+ +)+`

#### Correspondance vorace

Si la priorité des opérations règles les ambiguïtés d’interprétation. Mais une expression régulière peut encore être ambigüe d’une autre manière.

- `[a-z]+` correspond à un mot en minuscule et tous ses préfixes

Pour résoudre ce genre d’ambiguïtés, on a recours à la correspondance la plus longue possible à chaque fois, de **façon vorace**. On la continue jusqu’à ce que ne puisse plus faire de correspondance puis répète.

#### Caractères spéciaux

Certains caractères servent d’opérateurs (`*`, `[`, etc.), d’autres ont une signification spéciale comme le `.` pour tout caractère.

Une barre oblique inverse est utilisée pour faire référence à ces caractères plutôt qu’aux opérateurs.

- `\*` une astérisque
- `\.` un point
- `\?` un point d’interrogation
- `\n` une nouvelle ligne
- `\t` une tabulation

#### Alias

Certains **alias** existent afin de faire facilement référence à des ensembles communs de caractères.

- `\d` [0-9] n’importe quel chiffre
- `\D` [\^0-9] n’importe quel caractère non chiffre
- `\w` [a-zA-Z0-9_] n’importe quel caractère alphanumérique ou underscore
- `\W` [\^\w] un caractère non-alphanumérique
- `\s` [ \r\t\n\f] n’importe quel espace (espace, fabulation, etc.)
- `\S` [\^\s] non espace

#### Symboles de répétitions

Il existe d’autres façons de définir des répétitions en dehors de `*`, `+`, `?` pour spécifier plus précisément un nombre de répétitions.

- `*` zéro ou plusieurs occurrences de l’expression ou du caractère précédent
- `+` une ou plusieurs occurrences de l’expression ou du caractère précédent
- `?` exactement zéro ou plusieurs occurrences de l’expression ou du caractère précédent

- `{n}` *n* occurrences du caractère précédent ou de l’expression précédente
- `{n,m} de `m` à ` *n* occurrences du caractère précédent ou de l’expression précédente
- `{n,}` au moins *n* occurrences du caractère précédent ou de l’expression précédente

#### Substitutions

Une des utilisations possibles des expressions régulières consiste à faire des substituons dans le texte.

L’outil Unix `perl ` avec les paramètres `-p` et `-e` permet d’appliquer des **substitutions** avec des ER.

```perl
cat *.txt | perl -p -e "s/coulour/color/g"
```

Le `s` au début spécifie qu’une substitution est appliquée

Le `g` à la fin spécifie qu’une substitution est appliquée à chaque correspondance trouvée (pas seulement la première).

Les correspondances sont trouvées de façon vorace, sans chevauchement.

@todo continuer



## Ressources

- [Regex Cross­word](http://www.regexcrossword.com/). *Welcome to the fantastic world of nerdy regex fun! Start playing by selecting one of the puzzle challenges below. There are a wide range of difficulties from beginner to expert.*
- [Regular Expression Test Page for Perl](http://www.regexplanet.com/advanced/perl/index.html)
- [Quick start regex for analysis](http://www.coppelia.io/quick-start-regex-for-analysts-part-i/)
- [Introduction aux expressions régulières de Perl 5 et PCRE](http://youtu.be/QTvi77m0pco?a) ([slides ici ](http://maddingue.free.fr/conferences/fpw-2014/regexp/))

http://perl.linguistes.free.fr