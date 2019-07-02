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
- [Aletheia](http://www.primaresearch.org/tools) (avec Tesseract intégré)
- [Ocropy](https://github.com/tmbdev/ocropy) est un projet open-source développé en Python et soutenu par Google qui utilisait initialement Tesseract comme moteur de reconnaissance mais qui a ensuite développé son propre outil.

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



### Guides

http://hdw.artsci.wustl.edu/articles/154

http://www.cis.uni-muenchen.de/ocrworkshop/program.html

https://drive.google.com/drive/u/0/folders/0B7l10Bj_LprhQnpSRkpGMGV2eE0

http://www.cis.uni-muenchen.de/ocrworkshop/program.html

https://github.com/tmbdev/ocropy/wiki

## Transkribus

https://transkribus.eu/Transkribus/

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

   .............................

## Références

- [Techniques et formats de conversion en mode texte. Bnf, pages professionnels](http://www.bnf.fr/fr/professionnels/numerisation_boite_outils/a.num_conversion_mode_texte.html)
- http://www.generation-nt.com/comparatif-logiciel-ocr-roc-abbyy-omnipage-nuance-readiris-finereader-paperport-irislink-article-975981-1.html
- http://www.er-tim.fr/sites/default/files/memoire_m2_Lecailliez_final_v1.00.pdf
- https://www.digitisation.eu

## À voir

https://ocr-d.github.io