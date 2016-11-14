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

## Références

[Techniques et formats de conversion en mode texte. Bnf, pages professionnels](http://www.bnf.fr/fr/professionnels/numerisation_boite_outils/a.num_conversion_mode_texte.html)

http://www.generation-nt.com/comparatif-logiciel-ocr-roc-abbyy-omnipage-nuance-readiris-finereader-paperport-irislink-article-975981-1.html

http://www.er-tim.fr/sites/default/files/memoire_m2_Lecailliez_final_v1.00.pdf