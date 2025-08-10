---
author: emchateau
tags: nlp
---

# Traitement automatique de la langue (TAL)

Le traitement automatique de la langue (TAL) ou *Natural language processing* (NLP) en anglais, désigne un ensemble de méthodes utilisées pour rendre accessible la langue aux ordinateurs. Ces méthodes se sont forgées à la croisée de plusieurs domaines de recherche :

- la linguistique
- l’apprentissage machine
- l’intelligence artificielle
- et l’informatique

Le traitement automatique de la langue concerne également les interractions homme-machine, et soulève également des enjeux éthiques et d’équité.

L’objet de la linguistique est de comprendre comment fonctionne le langage. Elle peut s’intéresser aux grandes familles de langue et leurs relations, aux principes qui déterminent la correction grammaticale des phrases, aux évolutions de la langue ou encore à leur apprentissage.

L’apprentissage machine permet de construire des programmes informatiques complexes à partir d’exemples. En raison de leur complexité, l’apprentissage machine est souvent nécessaire pour traiter les langues. Les systèmes de traduction automatique sont par exemple construits grâce à ces approches plutôt que simplement des règles ou l’utilisation de dictionnaires.

L’intelligence artificielle désigne un champ de recherche qui s’intéresse à l’autimatisation des capacités mentales. Or, le langage occupe une place fondamentale dans l’intelligence humaine.

Le traitement automatique de la langue s’appuie enfin sur plusieurs aspects de l’informatique. D’une part, la modélisation formelle qui repose sur des outils théoriques comme ceux employés pour l’analyse des langages de programmation ; d’autre part, sur des données et des algorithmes qui permettent de les analyser ou de les implémenter.

Le traitement automatique de la langue pose différents enjeux éthiques. Cela concerne l’accès et les utilisateurs, les biais qui peuvent être renforcés ou répliqués, ou enfin des questions de respect de liberté d’expression et de surveillance.

cf. Larochelle, Hugo. s. d. *Traitement automatique des langues*. Consulté le 9 avril 2020. https://www.youtube.com/watch?v=waTZl_IbDdo&list=PL6Xpj9I5qXYHMDt3aBiI2KVff8c5Cwlfe.

## Plusieurs approches du Traitement automatique de la langue

Il existe plusieurs approches du traitement automatique de la langue. La plus fréquemment employée est une approche statistique, c’est-à-dire que l’on va utiliser des données pour essayer de fournir les connaissance linguistiques au système que l’on cherchera à développer. Cette « connaissance » sera donc obtenue de manière empirique. « You shall know a word by the company it keeps » (1957). C’est par le contexte observé des mots que pourra extraire une compréhension de la syntaxe des mots et de leur sémantique. Cette approche a permis d’attaquer des problèmes hors de portée des techniques précédentes.

Auparavant, des approches à base de règles ont été beaucoup développées. Ces approches s’avèrent moins efficace face à des problèmes complexes. Au cours des années 1960-1985, le domaine était dominé par l’approche du rationalisme. Pour un aperçu sur l’histoire de ces approches, cf. :

- Manning, Christopher D. et Hinrich Schütze. 1999. *Foundations of statistical natural language processing*. Cambridge, Mass : MIT Press. Chapitre 1
- Jurafsky, Dan et James H Martin. 2008. *Speech and Language Processing: An Introduction to Natural Language Processing, Computational Linguistics, and Speech Recognition*. 2e édition. Delhi : Pearson Education. Chapitres 1.5 et 1.6

## Pourquoi le traitement automatique de la langue est-il difficile ?

Interpréter une phrase correctement est une tâche difficile. Plusieurs difficultés doivent être surmontées.

- Ambiguïté : il n’est pas rare qu’une phrase puisse être interprétée de plusieurs manières. 
  ex. Pour une même phrase, plusieurs arbres syntaxiques sont possibles. *Our company is training workers* (Manning & Schütz)
- Métaphores. Utilisation des mots qui rend une approche à base de règles prédéfinies ardue.
- Variation dans le sens dans le temps et de nouveaux mots peuvent être introduits dans la langue.

## Pourquoi l’approche statistique est-elle intéressante ?

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

La fréquence est inversement proportionnelle à son rang `r, ou la fréquence multipliée par le rang d’un mot est égale à une constante *k* inconnue.

Le rang du mot est la place du mot dans leur ordonnancement par ordre croissant de fréquence. Plus on regarde loin dans la liste ordonnées des mots, plus la fréquence va diminuer selon un taux de 1/r. Ce qui implique que si on passe du rang 1 à 2, la fréquence va beaucoup diminuer alors que si l’on passe d’un mot qui a le rang 4 000 à 40 001, la fréquence diminuera peu. 

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

Des allers-retours sont parfois nécessaires selon les tâches à effectuer. Transformer les données sous la forme désirée nécessitera de définir certaines règles de transformations (pas forcément statistiques). Souvent, on emploie des règles qui sont inspirées par des connaissances linguistiques pour faciliter le travail et les performances.

#### Document

Il existe plusieurs outils et algorithmes de base qui sont utiles pour manipuler du texte et le transformer. On suppose le plus souvent que les documents sont déjà dans un format électronique purement textuel qui utilise un encodage UTF-8 ou ASCII.

- un document sera donc une longue chaîne de caractères
- à cette étape, on suppose que les balises aient été énlevées, même si elles peuvent parfois être utiles pour l’analyse (pour localiser des phrases, des paragraphes, des parties, etc.)

## Autres notes

[nTALRegex.md](nTALRegex.md)

[nTextometrie.md](nTextometrie.md)

[nNLP](nNLP.md)

[nRessourcesLexicalesFr.md](nRessourcesLexicalesFr.md)

[nJuliaNLP.md](nJuliaNLP.md)

[nTopicModeling.md](nTopicModeling.md)

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