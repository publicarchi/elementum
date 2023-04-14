---
title: Note sur l’Océrisation
since: 2016-11
---

# Océrisation

OCR Optical Character Recognition, en français reconnaissance optique des caractères.

L’océrisation est opération technique consistant à traiter une image en faisant intervenir un logiciel de reconnaissance de caractères. Au cours de cette procédure, à partir d’une acquisition numérique de l’image, le logiciel identifie les formes et les traduit en un flux textuel. Certains dispositifs associent des techniques d’apprentissage ou emploient des dictionnaires terminologiques pour améliorer la qualité de reconnaissance. Parfois la reconnaissance de caractère est associée à des techniques de structuration de document.

Ce procédé permet de convertir de grands ensembles documentaires numérisés en données textuelles par exemple pour offrir une recherche plein-texte. Elle s’applique de manière préférentielle aux textes imprimés même si de nets progrès commencent à être réalisés dans le domaine de l’écriture manuscrite.

La qualité d’une océrisation se mesure en fonction du taux de reconnaissance effectif. Il subsiste toujours un taux d’erreur qui, même minime, peut considérablement altérer la qualité du texte acquis. En 2016, un laboratoire de recherche de Microsoft a déclaré être parvenu à un taux de reconnaissance comparable à une transcription humaine. Toutefois, parcequ’elle est en partie basée sur des dictionnaires terminologiques, la qualité des résultats de l’OCR peut varier en fonction de la nature des textes (spécialisés, techniques, anciens, etc.) et de la nature de l’impression (caractères typographiques, mise en page, notes, formules mathématiques, etc.). La plupart des logiciels du marché ayant été en effet d’abord développés pour les langues contemporaines et l’impression mécanique actuelle.

## Processus

### Prétraitement

Un logiciel d’océrisation applique généralement plusieurs phases de prétraitement avant de tenter la reconnaissance du texte contenu dans une image proprement dit. Ces pré-traitements peuvent être :

- légère rotation de l’image
- suppression du bruit
- conversion en noir et blanc ou niveaux de gris
- analyse de l’agencement du contenu (layout analysis)
- détection des lignes et des mots
- reconnaissance de l’écriture
- isolation des caractères
- normalisation du ratio et de l’échelle

### Reconnaissance

Deux grands types d’algorithmes de reconnaissance de caractères s’appliquent généralement qui génèrent une liste qualifiée de caractères candidats.

La matrice de correspondance (_matrix matching_) implique la comparaison d’une image avec des glyphes stockées sur une base pixel par pixel, aussi connue comme une "pattern matching" ou une "pattern recognition", ou "image correlation". Cette méthode implique que les glyphes soient correctement isolés du reste de l’image et que les glyphes stockées soient stockés dans des échelles comparables. Cette technique fonctionne mieux avec du texte tapuscrits et fonctionne mal lorsque de nouvelles polices de caractères sont rencontrées. Ce fut la première technique qui fut implémentée.

L’extraction de propriété (_feature extraction_) décompose les glyphes en propriétés comme des lignes, des boucles, des directions et des intersections. Ces propriétés sont comparées avec une représentation vectorielle abstraite du caractère qui peut se réduire à un ou plusieurs prototypes de glyphes. Les techniques générales de détection de propriétés en vision computationnelle sont applicables à ce type d’OCR. La classification des voisins utilise des algorithmes comme le k-nearest neighbors pour comparer les propriétés de l’images et celle stockées et choisir la correspondance.

Certains logiciels comme Tesseract utilisent une approche basée sur deux passes. La seconde passe est appelée une reconnaissance adaptative (_adaptative recognition_ ) et utilise la forme des lettres pour identifier avec une grande certitude les identifications produites par la première passe. Ce qui est avantageux pour les polices de caractères inhabituelles ou les scans de faible qualité où les caractères sont distordus, flous, ou altérés.

## Service

- En France, HumaNum offre un service d’océrisation avec Abby fine reader
- [Tesseract](https://github.com/tesseract-ocr/tesseract) (open source) est un programme développé en C et en C++ disponible sous licence Apache v 2.0. Développé à partir de 1985 comme logiciel propriétaire par la société Hewlett-Packard, son code a été publié sous la forme de logiciel libre et open source en 2005, son développement est désormais sponsorisé par Google.
  https://github.com/tesseract-ocr
- [Aletheia](http://www.primaresearch.org/tools) (avec Tesseract intégré)
- [Ocropy](https://github.com/tmbdev/ocropy) est un projet open-source développé en Python et soutenu par Google qui utilisait initialement Tesseract comme moteur de reconnaissance mais qui a ensuite développé son propre outil.
- [Kraken](https://kraken.re) kraken is a turn-key OCR system optimized for historical and non-Latin script material.
- Projet https://www.ocr4all.org/

## Outils

https://www.pdflabs.com/docs/pdftk-cli-examples/

https://stackoverflow.com/questions/6349984/shell-script-to-change-pdf-files-to-png-mac-os-10-3

https://ademcan.net/blog/2013/04/10/how-to-convert-pdf-to-png-from-the-command-line-on-a-mac/

http://www.cs.cmu.edu/~benhdj/Mac/unix.html#splitPDF

```
for i in *pdf; do sips -s format png $i --out `basename $i .pdf`.png; done
for i in *; do sips -s format png $i --out $i.png; done
```

https://stackoverflow.com/questions/6349984/shell-script-to-change-pdf-files-to-png-mac-os-10-3

```
# diviser un pdf en plusieurs pages
pdftk ledoux1804txt.pdf burst
```

```
convert ledoux1804txt.pdf ledoux-%04d.jpg
```



### OpenConvert

Text conversion tool (from e.g. Word, HTML, txt) to corpus formats TEI or FoLiA) <http://openconvert.clarin.inl.nl/>

https://github.com/INL/OpenConvert

## Calamari

https://github.com/Calamari-OCR/calamari

[Calamari](https://github.com/Calamari-OCR/calamari) is built on [TensorFlow](https://www.tensorflow.org/tutorials/), an open-source machine learning library, which allows Calamari to take  advantage of TensorFlow's neural network capacity. It's relatively  straightforward to use, but it comes with some tricky dependencies.  Because Calamari only does text recognition, you have to use another  engine (they recommend OCRopus) to increase contrast, deskew, and  segment the images you want to read. OCRopus requires Python 2, and  Calamari is written in Python 3 — not an insurmountable obstacle but one to be alert to.

http://techsoupforlibraries.org/blog/the-best-ocr-tools-to-digitize-text-compared

### Kraken

http://kraken.re

Installation https://github.com/mittagessen/kraken/blob/master/.travis.yml#L12-L27

Documentation https://github.com/mittagessen/kraken/blob/master/docs/training.rst

https://github.com/lascivaroma/lexical/tree/master/ocr-training/anthologia-latina

Initial ground truth was generated through Tesseract then converted using an ad-hoc [XSL converting hOCR to Kraken correction environment](https://gist.github.com/PonteIneptique/c866c3387f7a5709dbd17b86123b37c5).

Install Kraken

```
ketos extract pages/*.html -o extract -u NFD -s
```

Characters count

```
awk '{for (i=1;i<=NF;i++) a[$i]++} END{for (c in a) print c,a[c]}' FS="" extract/*.txt > characters.with_case.txt
sed 's/\(.\)/\1\n/g' extract/*.txt | sort | uniq -ic | sort -k 2 > characters.txt
```

http://kraken.re/training.html

2019-10 : il est possible d’entraîner la segmentation.

### Guides

http://hdw.artsci.wustl.edu/articles/154

http://www.cis.uni-muenchen.de/ocrworkshop/program.html

https://drive.google.com/drive/u/0/folders/0B7l10Bj_LprhQnpSRkpGMGV2eE0

https://github.com/tmbdev/ocropy/wiki

## Grobid dictionnaries

http://cloud.science-miner.com/grobid/

https://github.com/kermitt2/grobid

## Handwritten Text Recognition (HTR)

### Transkribus

https://transkribus.eu/Transkribus/

Modèle basé sur IA

Création de modèles langagiers. Modèle de développement où READ utilise les données utilisateurs pour mettre au point des modèles langagiers qui feront par la suite l’objet d’une commercialisation.

Possibilités d’export de document aux format TEI.

Qualité des images : une bonne résolution d’image n’est pas nécessaire (1 Mega suffisant). Les développeurs du logiciel disent que 30 pixels par caractère suffit pour la reconnaissance.

Le logiciel permet le partage de collections. Les documents analysés avec la reconnaissance de manuscrit sont interrogeables avec un moteur de recherche interne (SolR). Les documents sont balisés avec un sous-ensemble de la Text Encoding Initiative (TEI) qui peut servir à gérer les documents. Toutefois, pour certains traitement fins, il vaut sans doute mieux travailler certaines métadonnées à l’extérieur du logiciel. Par ailleurs, certains types de balisage ne sont pas forcément nécessaire pour l’entraînement d’un modèle. L’ensemble des données sont accessibles par l’intermédiaire d’une API. Afin de travailler de manière collaborative dans l’interface il peut être nécessaire de développer des règles de nommage ou bien de construire un outil basé sur des requêtes de l’API.

Les modèles langagiers sont générés par Transkribus. Les utilisateurs sont propriétaires de leurs données mais Transkribus contrôle la création de modèle. Se pose la question du statut des modèle produits.

Plusieurs manières de procéder. Si une écriture régulière et grand nombre de pages. Peut-être intéressant de procéder avec un modèle spécifique. Il est également possible de travailler avec un modèle générique ou un modèle générique et des sous-modèles.

Option P2PaLA letter analysis

L’année dernière le développeur principal du projet pensait passer à un modèle payant en 2019. Modèle économique qui vise à desservir les centres d’archives pour la transcription de grosses masses de documentation.

## Formats

Abby FineReader XML <https://abbyy.technology/en:features:ocr:xml>

https://abbyy.technology/en:features:ocr:xml

ALTO  <https://www.loc.gov/standards/alto/>

https://github.com/altoxml/documentation/wiki/Software

Page <http://www.primaresearch.org/schema/PAGE/gts/pagecontent/2017-07-15/pagecontent.xsd>

hOCR <https://en.wikipedia.org/wiki/HOCR>

Conversions

- http://james.blushingbunny.net/omnipage2TEI/
- https://github.com/dariok/page2tei
- https://github.com/cneud/ocr-conversion-scripts
- https://github.com/INL/OpenConvert

voir ce que fait Syd Bauman http://tei-l.970651.n3.nabble.com/OCRed-XML-samples-td4031040.html

## Segmentation

FineReader et CITLab dans Transkribus

FineReader

- très bon pour la détection des zones, le typage et l’ordonnancement
- segmentation et transcription indissociables ; pas de HTR

CITLab

- adaptation au type de document ; entraînable
- moins bon que FineReader (même pour le ms car typage et ordonnancement moindre qualité pour les documents complexes, dans le cas de la presse)

Dans TimeUs pour écriture fin XIXe, HTR 5,2% erreur

Presse, et monographies Kraken. Création propre modèle.

Transcription pas toujours entièrement obtimisable. Scripts de transformation de textes brut ou d’interaction avec Kraken. Modélisation de la structure de chaque ensemble, en rendre compte dans les formats de fichiers.

Régularisation des graphies pour les détecter rapidement. Les développer pour ressembler à du langage naturel (HTR). Résoudre les césures.

Développement module de correction automatiques en travaillant sur des contextes.

Structuration 

## Redressement image

ScanTailor pour redressement images

## Rdv Alix Chagué, 8 octobre 2020

Laboratoire Almanach

Travail en cours sur le Minutier central, projet Lectorep. Se dégage actuellement de l’ANR TimeUs.

Lectorep dans le cadre d’une convention cadre entre l’INRIA et le MCC. Troisième itération, prolongée d’un an.

Technique

Entraînement des modèles de Kraken présentée en ligne est obsolète. Deux manières d’entraîner, avec html mais pas d’entraînement de la segmentation. Dans eScriptorium, possible de faire de la segmentation sémantique qui permet d’aider à faire un export TEI. Actuellement Kraken ne fait pas d’export TEI. Besoin d’une XSLT mais une réflexion en cours. Laurent Romary participe au Lectorep donc très TEI, idée de pouvoir proposer une sortie TEI qui sera modifiée. Mais plus de projet, plus possible de créer un scénario.

Dessiner les bases lignes, puis bleu pour dessiner des polygones autour de la ligne.

A créé un truc pour syphonner les données entraînées par Transkribus. Possible d’également importer des transcriptions XML Alto ou transcription XML Page. Transkribus Alto 2 mais eScriptorium Alto 4. Alix a fait un script pour convertir les fichiers. Possible de pouvoir partager des modèles.

Une interface graphique mais présent sur Herokuapp.

Entraîner la segmentation « line and regions ». Alors créée des groupes de ligne comme pour les paragraphes. Notre modèle ne sait pas faire.

L’idée avec eScriptorium être une interface. 

Discussion Kraken, Transkribus. Stockel qui gère le projet Scripta dans lequel développé eScriptorium. Lien avec le développeur principal de Kraken.

Plusieurs modes pour voir l’ordre des lignes. Mode zones.

Sélectionner toutes les images > Train segmenter ou recogniser.

Donner un nom, entraîner from scratch ou finetuner un modèle.

Une fois qu’il est entraîné, disponible dans une liste.

- Fichier entraînement partageable.
- Ground fact, images et transcriptions

Les ground facts sont des images et des fichiers Alto. Les fichiers Alto et Pages sont les fichiers pivots de Kraken.

https://gitlab.inria.fr/scripta/escriptorium  pour faire des tickets

également une API pour escriptorim

https://gitlab.inria.fr/scripta/escriptorium 

http://traces6.paris.inria.fr/api/

eScriptorium développé avec Kraken par Daniel Stoekl EPHE dans le cadre de Scripta. Approché Benjamin? sans doute car travail sur des écritures non-latines ou avec sens de lecture différent.

Daniel Stoekl travaillait avec Laurent Romary dans le cadre de l’équipe ALMAnaCH. Plus le cas aujourd’hui.

Lectaurep est un projet de l’équipe ALMAnaCH. De même que Time Us et DAHN.

Autour de Scripta Vietnamica et Tikoum Sofrim (hébreux).

Lectraurep est un projet mené de front avec le DMC des Archives nationales. Marie-Françoise Limon Bonnet et Aurélia Rostaing (Minutier central).

Phase 1 (2018), stage du M2 TNAH pour explorer la possibilité d’utiliser Transkribus ou explorer autre chose. Finalement décidé eScriptorium.

DMOASI Département de la maîtrise œuvre et ouvrage et service informatique aux Archives nationales : Gaetano Piraino (ancien TNAH, vision plus maîtrise ouvrage) et Frédéric Zamareno.

Le projet Lectaurep à 80% anciens AP ou TNAH. 

SCRIPTA développe l’interface. ALMAnaCH qui travaille sur les modèles et cas d’usage français.

Laurent Romary qui est le boss.

Benoît Sago chef d’équipe. Laurent Romary qui fait les sujets DHs.

DAHN Carmen Brando. Partenariat de Laurent EHESS INRIA. Anne Baillot.

Atelier 21 octobre. Demandera si gens OK pour contribuer doc. Et mettre en contact des gens.

Contrat jusqu’en novembre 21. En profiter pour avoir un an d’ici la fin de mon contrat de réfléchir à une thèse. Veut travailler sur le HTR. Pas encore de perspectives de financement. 



École du Louvre

- Françoise Zalek (documentation)
- Christophe Leclerc (HA numérique)
- Alix Chagué typologie numérique

ajouter de la technique dans la formation.

https://lectaurep.hypotheses.org/equipe-projet

## HTR-United sur Github pour partager Ground truth

https://github.com/HTR-United/htr-united

## eScriptorium

https://gitlab.inria.fr/scripta/escriptorium

https://escripta.hypotheses.org

## Services commerciaux

https://www.digitisation.eu

**Word Pro** , Pondicherry

saisie de textes multilingue de haute précision

11, Canteen Street, 

1st Floor, East Wing

Pondicherry 605001

INDIA

tel: 00 91 413 2223034

cel: 00 91 94422 94226

[www.wordpro-pondicherry.com](http://www.wordpro-pondicherry.com/)

## Prakrit texts

Projet de OCR de milliers de livres avec Kraken

https://github.com/aso2101/prakrit_texts

## Formats

### PageXML

https://ocr-d.de/en/gt-guidelines/trans/trPage.html

https://github.com/omni-us/pagexml

Library in C++ and a python wrapper for dealing with Page XML files



   .............................

## Références

- [Techniques et formats de conversion en mode texte. Bnf, pages professionnels](http://www.bnf.fr/fr/professionnels/numerisation_boite_outils/a.num_conversion_mode_texte.html)
- http://www.generation-nt.com/comparatif-logiciel-ocr-roc-abbyy-omnipage-nuance-readiris-finereader-paperport-irislink-article-975981-1.html
- http://www.er-tim.fr/sites/default/files/memoire_m2_Lecailliez_final_v1.00.pdf
- https://www.digitisation.eu
- Benchmark https://github.com/factful/ocr_testing
- http://techsoupforlibraries.org/blog/the-best-ocr-tools-to-digitize-text-compared
- https://ocr-d.github.io/
- https://ocr-d.github.io/core/
- Chagué, Alix. 2021. « Comment faire lire des gribouillis à mon ordinateur ? par Alix Chagué ». *MATE-SHS*. 11 mars. https://mate-shs.cnrs.fr/actions/tutomate/tuto31-lire-des-gribouillis-chague/.

## À voir

https://ocr-d.github.io

https://github.com/OCR-D/





https://github.com/INL/OpenConvert

https://github.com/opf/text-extractor
