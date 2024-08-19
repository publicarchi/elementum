---
author: emchateau
tags: nlp
---

# Traitement automatique de la langue (TAL)

Natural language processing (NLP)

Larochelle, Hugo. s. d. *Traitement automatique des langues*. Consulté le 9 avril 2020. https://www.youtube.com/watch?v=waTZl_IbDdo&list=PL6Xpj9I5qXYHMDt3aBiI2KVff8c5Cwlfe.

Il existe plusieurs approches du traitement automatique de la langue. La plus fréquemment employée est une approche statistique, c’est-à-dire que l’on va utiliser des données pour essayer de fournir les connaissance linguistiques au système que l’on cherchera à développer. Cette « connaissance » sera donc obtenue de manière empirique. « You shall know a word by the company it keeps » (1957). C’est par le contexte observé des mots que pourra extraire une compréhension de la syntaxe des mots et de leur sémantique. Cette approche a permis d’attaquer des problèmes hors de portée des techniques précédentes.

Auparavant, des approches à base de règles ont été beaucoup développées. Ces approches s’avèrent moins efficace face à des problèmes complexes. Au cours des années 1960-1985, le domaine était dominé par l’approche du rationalisme. Pour un aperçu sur l’histoire de ces approches, cf. :

- Manning, Christopher D. et Hinrich Schütze. 1999. *Foundations of statistical natural language processing*. Cambridge, Mass : MIT Press. Chapitre 1
- Jurafsky, Dan et James H Martin. 2008. *Speech and Language Processing: An Introduction to Natural Language Processing, Computational Linguistics, and Speech Recognition*. 2e édition. Delhi : Pearson Education. Chapitres 1.5 et 1.6

### Pourquoi le traitement automatique de la langue est-il difficile ?

Interpréter une phrase correctement est une tâche difficile. Plusieurs difficultés doivent être surmontées.

- Ambiguïté : il n’est pas rare qu’une phrase puisse être interprétée de plusieurs manières. ex. Pour une même phrase, plusieurs arbres syntaxiques sont possibles. *Our company is training workers* (Manning & Schütz)
- Métaphores. Utilisation des mots qui rend une approche à base de règles prédéfinies ardue.
- Variation dans le sens dans le temps et de nouveaux mots peuvent être introduits dans la langue.

### Pourquoi l’approche statistique est-elle intéressante ?

Dans l’approche statistique on va commencer par définir des modèles probabilistes du langage. Et estimer de manière automatisées, les paramètres du modèle probabiliste à partir de données. Les probabilités permettent de gérer l’incertitude sur l’interprétation (ambiguïté). L’exploitation de données permet d’adapter automatiquement les modèles (métaphore, variation dans le temps, etc.).

### Propriétés statistiques de données textuelles

Le point de départ du TAL statistique ce sont les données. On parle donc de **corpus** qui constituent des collections de textes ou de documents. Il s’agit de l’ensemble de nos données. Il existe certaines structures ou propriétés qui sont typiques de données textuelles et facilement observables.

#### Fréquence

Exemple de statistiques des mots du roman *Tom Sawyer* (Manning & Schütz). Classement des mots par **fréquence** : peu de mots fréquents, beaucoup de mots rares. Les mots différents sont nombreux et gérer le fait qu’il y a des mots pour lesquels on a peu d’observation, la **parcimonie** (*sparsity*) est un problème en TAL.

#### Classe fermée

Les mots les plus fréquents dans les corpus appartiennent le plus souvent à des classes syntaxiques que l’on va dire fermées. Les **classes fermées** sont les classes pour lesquelles des mots ne sont jamais invités. Ils n’ont quasiment pas variés depuis deux ans ans dans la langue.

- déterminants : un, le, son, etc.
- pronoms : je, tu, il, etc.
- conjonctions: mais, ou, et, donc, etc.
- prépositions : pour, de, etc.

ex. statistique des mots du roman *Tom Sawyer* (Manning & Schütz)

#### Loi de Zipf

Une propriété que l’on observe presque toujours dans les données textuelles a été caractérisée par George Kingsley Zipf (1902-1950). 

D’après la loi de Zipf : la fréquence *f* d’un mot est (approximativement) inversement proportionnelle à son rang *r*.

```f x 1/r ou f x r = k```

La fréquence est inversement proportionnelle à son rang r. Ou la fréquence multipliée par le rang d’un mot est égale à une constante *k* inconnue.

Le rang du mot est la place du mot dans leur ordonnancement par ordre croissant de fréquence. Plus regarde loin dans la liste ordonnées des mots, plus la fréquence va diminuer selon un taux de 1/r. Ce qui implique que si on passe du rang 1 à 2, la fréquence va beaucoup diminuer alors que si l’on passe d’un mot qui a le rang 4000 à 40001, la fréquence diminuera peu. 

On aura donc beaucoup de mots qui auront des fréquences presque égales mais très basses mais très peu de mots qui auront des fréquences très élevées.

ex. *Tom Sawyer* (Manning & Schütz). Souvent un produit qui est autour de 8 ou 9. 

ex. Autre illustration sur une échelle logarithmique (distribution au prend la forme d’une droite descendante)

```
f x r = k => log f + log r = log k => log f = -log r + log k
```

#### Collocations

Autre exemple bien connu, celui des collocations. Les collocations sont des phrases courts dont le sens va « au-delà » de la combinaison des sens de ses mots. 

- Celles-ci pourraient être inclues dans un dictionnaire. 
- Si un mot apparaît dans une collocation, il pourrait être traduit différemment

Exemples : *disk drive*, *make up*, *printemps érable*

ex. New York Times (Manning & Schütz). Sélections des paires nom-nom et adjectif-nom les plus fréquentes (motif de partie du discours). Souvent, parmi les paires les plus fréquentes des associations que l’on pourrait inclure comme des collocations.

Une collocation de mot sera une combinaison de deux ou plusieurs mots dont l’utilisation sera différente. Cette méthode par fréquence est une manière simple de détecter les collocations, mais il existe d’autres méthodes statistiques pour identifier des utilisations différentes de ces mots que si les observaient isolément.

### Manipulation de textes

Avant d’appliquer une méthode statistique, on doit définir la forme que doivent prendre les données.

- la forme désirée devra souvent varier selon l’application
- le choix de la forme peut avoir un impact significatif sur les résultats

Parfois des aller-retours.

Transformer les données sous la forme désirée nécessitera de définir certaines règles de transformations (pas forcément statistiques). Souvent des règles qui sont inspirées par des connaissances linguistiques pour faciliter le travail et les performances.

#### Document

Il existe plusieurs outils et algorithmes de base qui sont utiles pour manipuler du texte et le transformer. On suppose le plus souvent que les documents sont déjà dans un format électronique purement textuel (UTF-8, ASCII).

- un document sera donc une longue chaîne de caractères
- à cette étape, on suppose que les balises aient été élevées, même si elles peuvent parfois être utiles pour l’analyse (localise phrases, paragraphes, parties, etc.)

#### Les expressions régulières

On utilisera très souvent pour du traitement de texte et la recherche simple des expressions régulières.

Une **expression régulière (ER)** est une façon simple de caractériser un ensemble de chaînes de caractères, de façon compacte.

- ex. toutes chaînes de caractères correspondant à un montant en argent

C’est un formalisme utile pour faire de l’extraction d’information (simple) dans des données textuelles.

- l’outil Unix `grep -E` retourne toutes les lignes contenant une ER
- l’outil Unix `perl -p -e` permet d’appliquer des remplacements

L’expression régulière la plus simple consiste à préciser une seule chaîne de caractères

- une **correspondance** (match) est obtenue pour chaque sous-chaîne trouvée
- la casse (minuscule ou majuscule) est respectée

NB : en Perl les expressions régulières sont encadrées par des `/` (dans le livre sont seulement soulignées les premières occurence des correspondances)

#### Disjonction, négation, répétition

Les opérations de disjonction, négation, répétition, vont nous permettre de manipuler du texte de manière plus approfondie avec des expressions régulières.

#### Dijonction

Pour correspondre à plus d’une chaîne, on peut utiliser des disjonctions de caractères à l’aides des crochets `[`et `]`.

- `[wW]` *w* ou *W*
- `[abc]` *a* ou *b*, ou *c*

L’utilisation d’**intervalles** est aussi permise pour faire des dijonctions

- `[A-Z]` l’ensemble des majuscules
- `[0-9]` un chiffre de 0 à 9

#### Négation

Le symbole `^` permet de formuler une **négation**. Il doit être à l’intérieur de crochets et être le premier symbole.

- `[^A-Z]` tout sauf une majuscule
- `[^Ss]` ni *S* ni *s*
- `[^\.]` pas un point

Le signe circonflexe peut toutefois être utile s’il n’est pas placé au début d’une expression

- `[e^]`soit *e* ou *^*
- `a^b` le motif *a^b*

S’il se trouve au début de l’ER, il correspond à un début de ligne (`$` fin de ligne).

#### Caractère optionnel, répétitions

Le symbole `?` permet d’identifier un caractère qui est **facultativement** présent. Le caractère optionnel est celui qui précède le `?`

- `woodchucks?` *woodchuck* ou *woodchucks*
- `colou?r` *color* ou *colour*

Les symboles `*` et `+` permettent d’exprimer un nombre arbitraire (possiblement 0 pour `*`) de **répétitions**.

- `a*` correspond à *a*, *aa*, *aaa*, etc. ainsi que la chaîne vide
- pour ne pas inclure la chaîne vide : `aa*` ou `a+`

#### Disjonctions de chaînes

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

(continuer)

## Textométrie

Selon M. Tournier, la lexicometrie aussi appelée : logométrie, analyse automatique,

« **statistique linguistique** (Guiraud, 1959, 1960), **statistique lexicale** ou **linguistique quantitative** (Muller, 1964, 1967, 1973, 1979), **statistique textuelle** (Salem 1987, 1994), voire **analyse des données en linguistique** (Benzecri 1981), **la lexicométrie**  (Tournier 1975, Lafon 1984) n’est pas une théorie mais une méthodologie  d’étude du discours, qui se veut exhaustive, systématique est  automatisée. » Tournier M., 2002, p. 342-343.

Michel Pêcheux 1969, Analyse automatique du discours (AAD) à partir d’une approche syntaxique à la suite de Z. Harris. Mais son approche nécessitait une préparation importante du corpus. L’usage d’une codification thématique mobilisant déjà une analyse et un jugement (Achard 1991). —> Volonté de travailler sur la langue naturelle, sans préparation particulière du texte.

G. Herdan (1964) considère la linguistique statistique comme « une branche de la linguistique structurale, avec pour principale fonction la description statistique du fonctionnement (dans des corpus de textes) des unités définies par le linguiste aux différents niveaux de l’analyse linguistique (phonologique, lexical, phrastique) » cf. Lebart L., Salem A., 1994, p.16.

D. Mayaffre historien discours politiques

Mayaffre D., 2000, p.749. explique que ses connaissances linguistiques ne lui suffisent pas pour nourrir le débat épistémologique sur le lien entre Histoire et Linguistique dans l’analyse du discours

 ni à la méthode binomiale ni le modèle hypergéométrique en statistique lexicale

fait du mot un “objet réticulaire” pour Mayaffre

Traitement lexicographique qui consiste à traiter le texte sans lemmatisation (pour lemmatiser le vocabulaire d’un texte écrit en français, on ramène en général les formes verbales à l’infinitif, les substantifs au singulier, les adjectifs au masculin singulier, les formes élidées à la forme sans élision). Les formes apparaissent donc telles qu’elles ont été saisies : une forme au singulier et au pluriel comptant pour deux formes différentes, de même qu’un adjectif féminin ou masculin, ou encore un verbe sous ses différentes formes conjuguées.

Le corpus est distribué en plusieurs parties dans l’édition avant l’opération de segmentation. On y introduit différentes clés qui correspondent à des variables dont on dispose par ailleurs et qui peuvent permettent, par exemple, d’identifier des locuteurs puis de les regrouper par âge, sexe, niveau d’étude, etc.

Les traitements lexicométriques reposent sur une segmentation automatique du texte en occurrences de formes graphiques à partir de la définition d’un sous-ensemble de caractères délimiter. Les autres caractères étant considérés comme non délimiter. Chaque suite de caractères bornée à ses deux extrémités par des caractères délimiter est considérée comme une occurence. Et deux suites de caractères non délimiter indentifiques constituent deux occurrences d’une même forme. « La forme est un archétype correspondant à une ensemble d’occurrences identiques. L’ensemble des formes d’un texte constitue son vocabulaire. » (Leimdorfer et Salem 1995)

Cette segmentation en formes graphiques permet ensuite de considérer le texte comme une suite d’occurrences séparées entre elles par un ou plusieurs caractères délimiter. « On regroupe sous le terme de lexicométrie toute une série de méthodes qui permettent d’opérer, à partir d’une segmentation, des réorganisations formelles de la séquence textuelle et des analyses statistiques portant sur le vocabulaire. » (Leimdorfer et Salem 1995)

- méthodes documentaires qui opèrent une simple réorganisation de la surface textuelle
- méthodes qui opèrent, pour chaque texte pris isolément, des comptages et des calculs d’indices statistiques
- les méthodes statistiques contrastives qui produisent des résultats portant sur le vocabulaire de chacun des textes par rapport à l’ensemble des textes réunis dans un même corpus à des fins de comparaisons.

Logiciels qui fournissent après la segmentation série de documents permettant de mieux appréhender le vocabulaire du corpus

- L’*index alphabétique* permet de vérifier la saisie du texte, de rapprocher les utilisations du singulier et du pluriel d’un même substantif, les différentes flexions d’un verbe, etc.
- L’*index hiérarchique*, dans lesquels les formes sont classées par fréquence décroissante, permet d’examiner les formes les plus utilisées
- Les *concordances* permettent, pour chaque forme, de rassembler l’ensemble des contextes dans lesquels la forme apparaît
- Les *inventaires de segments répétés* permettent de repérer les séquences de formes qui apparaissent à plusieurs endroits du texte
- le *calcul de spécificités* permet de dégager les formes et les segments qui se trouvent être particulièrement employés (ou, au contraire, particulièrement sous-employés) dans chacune des parties du corpus.

[...]

L’outil lexicométrique s’avère, du point de vue de l’analyse de discours, d’un très grand intérêt, dans trois directions principales :

- par les données quantitatives fournies, les comparaisons et les vérifications qu’il permet ;
- comme outil de repérage de pistes de recherche, et comme premier bilan d’un corpus ;
- comme outil heuristique puissant, entraînant à des allers-retours fructueux entre le texte analysé et les données produites. Il incite à une définition plus fine des données et à des comparaisons vers d’autres corpus. Il oblige également à une réflexion sur le statut du « quantitatif » dans le discours à l’écrit et à l’oral.

D’un point de vue pratique, il est particulièrement utile si **plusieurs éléments se trouvent réunis** :

- si le corpus est relativement important, difficilement maîtrisable par une analyse fine de fragments ; mais des informations intéressantes se dégagent avec des corpus de quelques dizaines de pages seulement ;
- si la saisie sous traitement de texte peut être faite sans difficultés particulières, et de manière économique (en temps de travail notamment) ;
- si le corpus est suffisamment connu, déjà analysé pour que les indications statistiques données puissent prendre sens et orienter la recherche ; lorsque cette connaissance de l’« l’intérieur » n’existe pas, les données fournies par le calcul indiquent autant de pistes possibles, mais qu’il est difficile d’examiner exhaustivement. Par contre, lorsque le corpus a déjà été analysé en partie ou que l’on dispose de pistes de recherche identifiées, l’outil lexicométrique devient un « multiplicateur » de recherche remarquable, par les allers-retours continuels qu’il permet entre l’analyse de fragments, les données statistiques et les nouvelles demande de tri que l’on peut formuler.

(Leimdorfer, François et André Salem. 1995. « Usages de la lexicométrie en analyse de discours ». *Cahiers de Sciences humaines* 31 (1) : 131-143. décrivent ensuite l’exemple de thèses)



## Ressources pédagogiques

- Informatique et Linguistique de Jean Véronis (nous contacter pour y accéder)
- [Introduction au TALN et à l'ingénierie linguistique](http://www.lattice.cnrs.fr/sites/itellier/poly_info_ling/index.html) de Isabelle Tellier
- [Instruments et ressources électroniques pour le français](http://www.amazon.fr/Instruments-ressources-électroniques-pour-français/dp/2708011197) de Benoît Habert
- [*Python NLTK Demos for Natural Language Text Processing*](http://text-processing.com/demo/)
- [Machine Translation](https://mitpress.mit.edu/books/machine-translation-0), Thierry Poibeau, MIT Press, 2017
- [Natural Language Processing](https://github.com/jacobeisenstein/gt-nlp-class/blob/master/notes/eisenstein-nlp-notes.pdf), Jacon Eisenstein, 2018
- [Speech and Language Processing](https://web.stanford.edu/~jurafsky/slp3/) (3rd ed. draft), Dan Jurafsky and James H. Martin, 2018 
- [Foundations of Statistical Natural Language Processing](https://nlp.stanford.edu/fsnlp/), Chris Manning and Hinrich Schütze, 1999

## Expressions régulières

- [Regex Cross­word](http://www.regexcrossword.com/). *Welcome to the fantastic world of nerdy regex fun! Start playing by selecting one of the puzzle challenges below. There are a wide range of difficulties from beginner to expert.*
- [Regular Expression Test Page for Perl](http://www.regexplanet.com/advanced/perl/index.html)
- [Quick start regex for analysis](http://www.coppelia.io/quick-start-regex-for-analysts-part-i/)
- [Introduction aux expressions régulières de Perl 5 et PCRE](http://youtu.be/QTvi77m0pco?a) ([slides ici ](http://maddingue.free.fr/conferences/fpw-2014/regexp/))

http://perl.linguistes.free.fr

## Statistiques

- [La Statistique en clair](http://www.editions-ellipses.fr/product_info.php?manufacturers_id=358&products_id=7900) de François Grosjean, Jean-Yves Dommergues et Gilles Macagno
- [**Ludovic Lebart, André Salem** (1994) **Statistique Textuelle**](http://lexicometrica.univ-paris3.fr/livre/st94/st94-tdm.html), Dunod.
- [**Stat Trek**](http://stattrek.com/) Teach yourself statistics

## Linguistique générale

- Nouveau dictionnaire encyclopédique des sciences du langage, Ducrot Oswald, Schaeffer Jean-Marie, Seuil, 1995.
- Introduction à la linguistique, 3 volumes, Milicevic Jasmina, Mel'cuk Igor, Hermann, 2014.
- Un blog de linguistique "pour tout le monde" : https://bling.hypotheses.org/

## Lectures classiques

- Cours de linguistique générale, Ferdinand de Saussure, 1916, réédité chez Payot.
- Langage, Leonard Bloomfield, 1933, traduction française.
- Structures syntaxiques, Noam Chomsky, 1957, traduction française au Seuil.
- Eléments de syntaxe structurale, Lucien Tesnière, 1959, Klincksieck.
- Eléments de linguistique générale, André Martinet; 1970, Armand Colin.
- Problèmes de linguistique générale, Emile Benveniste, 1966, Gallimard.

## Signets

### Lexicometrica

ISSN 1773-0570

http://lexicometrica.univ-paris3.fr

La revue LEXICOMETRICA s'adresse aux chercheurs, aux étudiants, aux professionnels de la communication et de la fouille de données textuelles... intéressés par les travaux théoriques et pratiques menés dans les domaines suivants : Lexicométrie / statistique textuelle, linguistiques de corpus, extraction d'informations à partir de corpus de texte, acquisition de connaissances...

### Revue Corpus

https://journals.openedition.org/corpus/397

### Semen, revue de sémio-linguistique des textes et discours

https://journals.openedition.org/semen

### Revue Texto, Textes & Cultures

http://www.revue-texto.net/****

### Google Ngram Viewer (2013)

https://books.google.com/ngrams

### Atelier Cahier 2019

Exploiter les corpus d’auteur – Atelier de formation annuel du consortium Cahier – Poitiers – 18-20 juin 2019 – ouverture des inscriptions

https://cahier.hypotheses.org/4662

Vos formateurs pour 2019 seront : Dr.[Peter Stockes](http://www.peterstokes.org/cv/index.html) (École Pratique des Hautes Études), Directeur d’Etudes à l’EPHE [Raphaël Céré](http://igd.unil.ch/rcere/) (Université de Lausanne), Doctorant à l’Université de Lausanne Dr. [Aris Xanthos](https://www.unil.ch/sli/fr/home/menuinst/collaborateurs/xanthos-aris.html) (Université de Lausanne), Maître d’enseignement et de recherche à l’Université de Lausanne. 

https://github.com/pastokes/python_tei

http://textable.io/cahier/

Revue en ligne *Kairos*

http://kairos.technorhetoric.net/archive.html

### RECITAL

https://aclanthology.org/venues/jeptalnrecital/