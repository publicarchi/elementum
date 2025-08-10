# Spacy

https://spacy.io

- Produit de la société [explosion.ai](https://explosion.ai) fondée par : Matthew Honnibal ([@honnibal](https://twitter.com/honnibal)) et Ines Montani ([@_inesmontani](https://twitter.com/_inesmontani))
- Licence MIT (Open Source) pour le code
- Licences ouvertes diverses pour les modèles
- Projet démarré en 2015, v1.0.0 en octobre 2016, v3.3.0 ([github](https://github.com/explosion/spaCy))

## Fonctionnalités

Chaîne de traitements de TAL

- tokenisation (*tokenizer*)
- étiquetage POS (*tagger*)
- analyse syntaxique (*parser*)
- détection d'entités nommées (*ner*)
- lemmatisation
- (catégorisation de texte
- word embedding)

Usage de modèles statistiques (méthodes neuronales)

Intégration possible de modèles tiers (PyTorch ou TensorFlow)

## Avantages / inconvénients

Outil destiné à être utilisé en production :

- rapide
- stable
- qualité du code (tests, documentation, packaging)

Mais pas de choix de la méthode ou de l'algorithme utilisé. D’autre logciels peuvent être pertinents dans certains cas d’usage, par exemple NLTK ou Stanza.

Relativement simple à prendre en main. Très bien documenté.



## Modèles

- 4 modèles pour le français
  - [fr_core_news_sm](https://spacy.io/models/fr#fr_core_news_sm) (tagger, morphologizer, lemmatizer, parser, ner) 15 Mo
  - [fr_core_news_md](https://spacy.io/models/fr#fr_core_news_md) (tagger, morphologizer, lemmatizer, parser, ner, vectors) 43 Mo
  - [fr_core_news_lg](https://spacy.io/models/fr#fr_core_news_lg) (tagger, morphologizer, lemmatizer, parser, ner, vectors) 545 Mo
  - [fr_dep_news_trf](https://spacy.io/models/fr#fr_dep_news_trf) (tagger, morphologizer, lemmatizer, parser) 382 Mo
- modèles `fr` appris sur les corpus [Sequoia](https://deep-sequoia.inria.fr/fr/) et [WikiNer](https://figshare.com/articles/Learning_multilingual_named_entity_recognition_from_Wikipedia/5462500)
- sauf le modèle `trf` qui est issu de camembert-base distribué par [Hugging Face](https://huggingface.co/camembert-base), entraîné sur [Oscar](https://oscar-corpus.com/)

## Tutoriaux

https://course.spacy.io