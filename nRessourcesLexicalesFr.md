---
author: Emmanuel Château-Dutier
since: 2017-01-18
tags: nlp
---

# Ressources utiles pour le traitement automatique de la langue française

voir 

Habert, Benoît. 2005. *Instruments et ressources électroniques pour le français*. Collection l’essentiel français. Gap : Ophrys.

## Ressources pour le TAL du Français

### OpenNLP

[OpenNLP](https://sites.google.com/site/nicolashernandez/resources/opennlp) propose des modèles pour le traitement automatique du français.

Licence Apache.

Découpage de phrases, tokeniser, étiquetage des parties du discours, analyse morphologique.

## LGeRM

[LGeRM](http://www.atilf.fr/LGeRM/) est un lemmatiseur du français moyen utilisable sur des corpus du français moderne.

voir l’article https://halshs.archives-ouvertes.fr/halshs-00396452/document

ainsi que https://books.google.ca/books?id=Ca6dCgAAQBAJ&pg=PA461&lpg=PA461

voir également http://lexicometrica.univ-paris3.fr/jadt/jadt2000/pdf/89/89.pdf

## Étiquetage des rôles grammaticaux et morphosyntaxique

- cf. https://www.coralcorpuslab.com/tools-and-taggers
- Charpentier, Lucas, Yannis Haralambous, et Achraf El Masdouri. 2020. « Etude des performances de POS-taggers appliqués à la langue française ». Collection des rapports de recherche d’IMT Atlantique. IMT Atlantique. https://doi.org/10.13140/RG.2.2.17313.35689.

Corpus de référence pour le français : French TreeBank

### TreeTagger

- Url: https://www.cis.uni-muenchen.de/~schmid/tools/TreeTagger/
- Licence: custom
- Language: ?
- Étiquettes : 

[TreeTagger](https://www.cis.uni-muenchen.de/~schmid/tools/TreeTagger/) est un outil pour l’annotation de textes avec des informations de partie du discours et de lemme développé par Helmut Schmid dans le cadre du TC project à l’Institute for Computational Linguistics de l’Université de Stuttgart. 

> The TreeTagger is a Markov Model tagger which makes use of a decision tree to get more reliable estimates for contextual parameters.

Il est utilisé avec succès sur de nombreuses langues comme le français.

### Stanford CoreNLP

- Url: https://stanfordnlp.github.io/CoreNLP/
- Licence: GNU GPL v2+
- Language: Java
- Étiquettes : custom

> CoreNLP is your one stop shop for natural language processing in Java! CoreNLP enables users to derive linguistic annotations for text, including token and sentence boundaries, parts of speech, named entities, numeric and time values, dependency and constituency parses, coreference, sentiment, quote attributions, and relations. CoreNLP currently supports 8 languages: Arabic, Chinese, English, French, German, Hungarian, Italian, and Spanish.

### Spacy

- Language: Python
- Étiquettes : Universal Dependencies

### Talismane

- Url: https://github.com/joliciel-informatique/talismane
- Licence: [AGPL open-source license](http://www.gnu.org/licenses/agpl.html)
- Language: Java
- Étiquettes : Universal Dependencies
- Traits

Traitement Automatique des Langues par Inférence Statistique Moyennant l'Annotation de Nombreux Exemples

> Talismane is a natural language processing framework with sentence detector, tokeniser, pos-tagger and dependency syntax parser. Current available language packs include French (standard and [Universal Dependencies](https://github.com/joliciel-informatique/talismane/wiki/Analysing-French-Universal-Dependencies)) and English.

## Lefff, lexique des formes fléchies du français
livresse des mots

https://www.labri.fr/perso/clement/lefff/

## Morphalou, *Lexique morphologique ouvert du français*

Morphalou3 comprend 159 271 lemmes et 954 690 formes fléchies, du français moderne. Ce document présente toutes les informations concernant Morphalou3 : composition, formats, données, jeu d'étiquettes et statistiques.

La version 3 de Morphalou a été obtenue par la fusion de cinq lexiques : 

- [Morphalou 2](https://repository.ortolang.fr/api/content/morphalou/2/LISEZ_MOI.html#morphalou2) (version de décembre 2013)
- [DELA](https://repository.ortolang.fr/api/content/morphalou/2/LISEZ_MOI.html#dela) (version de décembre 2011)
- [Dicollecte](https://repository.ortolang.fr/api/content/morphalou/2/LISEZ_MOI.html#dicollecte) (version 4.3)
- [LGLex et LGLexLefff](https://repository.ortolang.fr/api/content/morphalou/2/LISEZ_MOI.html#lglex) (version 3.4)
- [Lefff](https://repository.ortolang.fr/api/content/morphalou/2/LISEZ_MOI.html#lefff) (version 2.1 avril 2006)

Cette fusion a permis d'augmenter et corriger le contenu de près de 70 000 lemmes et plus de 500 000 formes fléchies. Elle a également permis de redéfinir [le jeu d'étiquettes, décrit en détail dans un chapitre dédié](https://repository.ortolang.fr/api/content/morphalou/2/LISEZ_MOI.html#jeu_etiquettes). 

https://repository.ortolang.fr/api/content/morphalou/2/LISEZ_MOI.html

## FNS SERMO

Neufchâtel projet linguistique sur des corpus de sermons de la réforme. Travail sur des imprimés.

https://libra.unine.ch/Projets/Projets-en-cours/29276

http://www.atilf.fr/LGeRM/

Outils Presto université de ENS Lyon

## WOLF (Wordnet Libre du Français)

Le WOLF (Wordnet Libre du Français) est une ressource lexicale sémantique (wordnet) libre pour le français

<http://alpage.inria.fr/~sagot/wolf.html>

http://blog.onyme.com/etude-de-lontologie-wordnet-libre-du-francais-wolf/

http://www.aclweb.org/anthology/W14-6704

http://www.cnrtl.fr/outils/

http://dragonfly.hypotheses.org/648

Stanford CoreNLP for French texts

voir aussi http://www.nltk.org/api/nltk.stem.html#module-nltk.stem.snowball qui prend en charge le français

## « Les verbes français » de Jean Dubois et Françoise Dubois-Charlier (Version LVF+1)

http://rali.iro.umontreal.ca/rali/?q=fr/node/1237

## Hunspell

https://github.com/hunspell/hunspell

## Dictionnaire Électronique des Mots — DEM, par Jean Dubois et Françoise Dubois-Charlier

http://rali.iro.umontreal.ca/rali/dem/

## French LEFFF Lemmatizer

https://github.com/ClaudeCoulombe/FrenchLefffLemmatizer

http://pauillac.inria.fr/~sagot/index.html#lefff

https://team.inria.fr/almanach/

## Alix

http://obvil.lip6.fr/alix/

https://github.com/oeuvres/Alix

Maybe with TreeTagger ? I haven't try but this app can work in french
[http://www.cis.uni-muenchen.de/~schmid/tools/TreeTagger/](http://www.cis.uni-muenchen.de/~schmid/tools/TreeTagger/)
[http://txm.sourceforge.net/installtreetagger_fr.html](http://txm.sourceforge.net/installtreetagger_fr.html)

## Lexique

http://lexique.org/telLexique.php

The Historical Lexicon of French is focused on the 17th century, late Renaissance French. It is an intermediate period between Middle French (covered by LGeRM data – see [http://www.atilf.fr/dmf/LGeRM/](http://www.atilf.fr/dmf/LGeRM/)) and Modern French (covered by Morphalou data – see [http://www.cnrtl.fr/lexiques/morphalou/](http://www.cnrtl.fr/lexiques/morphalou/)).The current lexicon consists of 27,508 lemmata, 115,201 word forms and 141,152 lemma/word forms combinations.

## Tapor

http://tapor.ca@

## DériF (Dérivation en Français)

- Last updated: 2013-01-29
- Site: [http://www.cnrtl.fr/outils/DeriF/](http://www.cnrtl.fr/outils/DeriF/)

DériF (Dérivation en Français) is a free, web based morphological analyzer for French. It lemmatizes a text and labels each lemma, out of context, with a grammatical category (noun, verb, adjective, etc.).

## dictionnaire LVF (Les Verbes Français) de J. Dubois et F. Dubois-Charlier

https://papyrus.bib.umontreal.ca/xmlui/handle/1866/10432

## Corpus écrits

http://explorationdecorpus.corpusecrits.huma-num.fr

## Outils divers

https://github.com/brightmart/text_classification?utm_content=buffer8d897&utm_medium=social&utm_source=twitter.com&utm_campaign=buffer

https://www.digitisation.eu/tools-resources/tools-for-text-digitisation/

https://github.com/statsmaths/cleanNLP

https://nlp.stanford.edu/projects/glove/

## ELEXIS – European Lexicographic Infrastructure

voir http://www.elex.is 

## Clarin, The research infrastructure for language as social and cultural data

https://www.clarin.eu

## DARIAH Topic Explorer

https://dariah-de.github.io/TopicsExplorer/

## Outils pour le français ancien et moderne

### Graphist : Logiciel de lemmatisation indexation et modernisation automatique de textes anciens

Laurent Catach

Graphiste est un programme informatique pour la lemmatisation, l’indexation et la modernisation des documents écrits en français de la Renaissance, de l’époque classique ou moderne. Le programme développé par l’équipe du CNRS Histoire et Structure de l’Orthographe (HESO).

>Le projet a donc bénéficié d'un environnement particulièrement riche en compétences, et constitue d'une certaine façon une synthèse de nombreux travaux linguistiques menés à HESO depuis plus de 20 ans par Nina Catach et son équipe, en matière de lexicologie, de morphologie et d'histoire de l'orthographe ([N. Catach 1985](https://www.digitalstudies.org/articles/10.16995/dscn.215/print/#catach_n)).

Utilisation du DAC qui contient la première édition du *Dictionnaire de l’Académie française* 1694

Décès prématuré de Nina Catach en 1998

https://www.digitalstudies.org/articles/10.16995/dscn.215/print/

https://homes.chass.utoronto.ca/~wulfric/siehlda/clermont/cat_bib.htm

http://projects.chass.utoronto.ca/chwp/catach_l/index.html

**Catach**, L. (1994). "GRAPHIST: logiciel de lemmatisation, indexation et modernisation automatique de textes anciens", *Early Dictionary Databases* (éd. I. Lancashire & T.R. Wooldridge) = *CCH Working Papers*, 4, 183-196 et *Informatique et dictionnaires anciens* (éd. T.R. Wooldridge) = *Dictionnairique et lexicographie*, 3 (1995), 183-196; rééd. in [*CH Working Papers*, B.25](http://www.chass.utoronto.ca:8080/epc/chwp/) (1996).

**Catach**, N. & L. **Catach** (1994). "Le projet GRAPHIST et la recherche en industries de la langue", Congrés ALLC-ACH (Paris, avril).

<https://projects.chass.utoronto.ca/chwp/catach_l/index.html>

https://projects.chass.utoronto.ca/chwp/index.html

*Les Listes orthographiques de base du français (LOB) : les mots les plus fréquents et leurs formes fléchies les plus fréquentes*, avec la collab. de Fabrice Jejcic et l'équipe H.E.S.O., collection Nathan Recherche, Paris, Nathan, 1984 ([ISBN 2-09-190505-1](https://fr.wikipedia.org/wiki/Sp%C3%A9cial:Ouvrages_de_r%C3%A9f%C3%A9rence/2-09-190505-1)) édité erroné (notice [BnF](https://fr.wikipedia.org/wiki/Biblioth%C3%A8que_nationale_de_France) no [FRBNF34777112](http://catalogue.bnf.fr/ark:/12148/cb34777112j.public))

*Pour une théorie de la langue écrite : actes de la table ronde internationale C.N.R.S.-H.E.S.O., Paris, 23-24 octobre 1986*, éd. par Nina Catach, Paris, Éd. du Centre national de la recherche scientifique, 1988  ([ISBN](https://fr.wikipedia.org/wiki/International_Standard_Book_Number) [2-222-04220-8](https://fr.wikipedia.org/wiki/Sp%C3%A9cial:Ouvrages_de_r%C3%A9f%C3%A9rence/2-222-04220-8))

Nina Catach, de Mireille Huchon et d’André Tournon

opération d’évaluation de ces analyseurs organisée conjointement par l’Aupelf-Uref et le CNRS, en recensent plus d’une vingtaine cf. http://www.etudes-francaises.net/colloque/demonet.htm voir aussi numéro 38 du *Médiéviste et l’ordinateur*

tagger TAL, élaboré par la société IBM. Cet outil a participé à
l’évaluation Grace (action d’évaluation INaLF-CNRS qui s’est déroulée de 1996 à 1998).

ANTONI Marie-Hélène, DEMONET Marie-Luce, « Informatisation et lemmatisation du corpus rabelaisien », *Le Médiéviste et l’ordinateur*, n° 38, février 2000.

Antoni M.-H. (1997). TAL et le projet Grace. Rapport technique interne IBM.

El-Bèze M. (1993) Les modèles de langage probabilistes: quelques domaines d’application.

Thèse HDR. LIPN (Paris XIII).

http://lexicometrica.univ-paris3.fr/jadt/jadt2000/pdf/89/89.pdf

gestion des hétérographes

#### TreeTagger et Flemm

TreeTagger (Stein et Schmid 1995) et Flemm (Namer 2000). TreeTagger, on l’a dit, est un outil permettant d’assigner automatiquement des annotations morpho-syntaxiques. Flemm est un ensemble de modules Perl permettant d’analyser la flexion du français moderne dans des corpus préalablement étiquetés par le TreeTagger.

www.ling.uqam.ca/forum/satoman/images/jadt2010_submission_54-1.doc

https://www.cis.uni-muenchen.de/~schmid/tools/TreeTagger/

### Open Corpus Workbench

https://www.ims.uni-stuttgart.de/forschung/projekte/corpus-workbench/

http://cwb.sourceforge.net/

> The IMS Open Corpus Workbench (CWB) is a collection of **open-source** tools for managing and querying **large text corpora** (up to 2 billion words) with **linguistic annotations**. Its central component is the flexible and efficient query processor **CQP**.

Doit travailler en format VRT

CQP en ligne de commande qui fonctionne le mieux

http://cwb.sourceforge.net/files/CQP_Tutorial.pdf

http://fedora.clarin-d.uni-saarland.de/teaching/Corpus_Linguistics/Tutorial_CQP_I.html

CQP Web (difficile à installer)

https://corpora.clarin-d.uni-saarland.de/cqpweb/

TXM

### Étienne Brunet

Université de Nice, lemmatiseur du français moderne

### ATLIF

Souvay lemmatiseur sur Dictionnaire français moyen

### Français contemporain

Analyseur syntaxique FRMG développé à INRIA

http://alpage.inria.fr/frmgwiki/frmg_main/frmg_server

> Pour une phrase donnée, l'analyseur essaie de retourner la meilleure structure grammaticale. L'analyseur FRMG résulte de la compilation de la [grammaire FRMG](http://alpage.inria.fr/frmgwiki/node/4305)dans l'environnement DyaLog. C'est un analyseur robuste et à large couverture du français. Il est utilisé pour le [traitement de très gros corpus](http://alpage.inria.fr/frmgwiki/wiki/quelques-applications-de-frmg), a participé aux campagnes d'évaluation EASy et Passage, et peut se [comparer](http://alpage.inria.fr/frmgwiki/wiki/performances-de-frmg) aux analyseurs statistiques sur leur corpus d'entraînement tout en restant stable hors domaine.
>
> FRMG peut analyser une chaîne de mots et plus généralement un treillis de mots reflétant des ambiguïtés sur les mots et leur segmentation. Il calcule l'ensemble de toutes les analyses possibles, en s'appuyant sur des techniques d'[analyse par charte](http://en.wikipedia.org/wiki/Chart_parser) ([programmation dynamiqu](http://fr.wikipedia.org/wiki/Programmation_dynamique)e). Une phase de désambiguïsation permet ensuite de sélectionner la meilleure analyse parmi l'ensemble généralement très grand de toutes les analyses. Cette phase de désambiguïsation peut faire appel à un modèle statistique appris sur un corpus annoté (*treebank*) pour de meilleures [performances](http://alpage.inria.fr/frmgwiki/node/6325).
>
> Pour la version de l'analyseur utilisable en ligne sur ce site, il est à noter qu'elle n'utilise pas un tel modèle statistique de désambiguïsation pour des raisons de temps de latence (le temps de chargement des modèles de quelques secondes est trop couteux pour une simple phrase et ne se justifie que lors du traitement de corpus). D'autre part, divers réglages (sur la segmentation en phrases/mots, sur la détection des entités nommées, sur l'utilisation de restrictions de sélection, ...) peuvent influer sur les performances et expliquer certaines différences entre la version en ligne et les résultats sur corpus.
>
> FRMG ainsi que l'ensemble de la chaîne de traitement ALPAGE sont librement disponibles. Mais n'hésitez pas à nous contacter pour plus d'informations et de conseils si vous souhaitez utiliser nos outils pour vos applications, commerciales ou non.

## CamemBERT

https://camembert-model.fr/

## Le Dictionnaire électronique des synonymes · DES

http://crisco.unicaen.fr/dictionnaire-electronique-des-synonymes/actualites-des/

## Liste de mots vides dans différentes langues

https://github.com/Alir3z4/stop-words/

http://snowball.tartarus.org/algorithms/french/stop.txt
