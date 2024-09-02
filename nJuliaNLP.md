---
author: emchateau
tags: julia, nlp
---

# Tutoriel Julia NLP

La plupart des applications de l’analyse de texte reposent sur un nombre limité de concepts ou de procédures clefs telles que la concordance, la fréquence des mots, l’annotation ou l’étiquetage, la collocation, la classification de texte, l’analyse des sentiments ou l’extraction d’entité, ou encore les modèles thématiques. Ce tutoriel introduit l’analyse de texte en examinant chancune de ces méthodes dans le contexte des sciences historiques.

Ce tutoriel est basé sur le langage de programmation [Julia](https://julialang.org). Le langage est relativement nouveau par rapport à ses concurrents comme Python ou R. Toutefois, il nous semble qu’il présente plusieurs avantages pour le domaine des humanités nuémriques. Si vous êtes nouvelle ou nouveau dans ce langage ou ne l’avez pas déjà installé, vous pouvez trouver des introductions aux liens suivants.

- Guides pour débuter avec Julia @todo
- Bibliographie de base sur l’analyse de texte @todo

Les paquets nécessaires pour travailler seront indiqués au fur et à mesure de ce tutoriel.

Chaîne de traitements de traitement automatique de la langue possible
- tokenisation (*tokenizer*)
- étiquetage POS (*tagger*)
- analyse syntaxique (*parser*)
- détection d’entités nommées (*ner*)
- lemmatisation
- (catégorisation de texte word embedding)
- Usage de modèles statistiques (méthodes neuronales)
- Intégration possible de modèles tiers (PyTorch ou TensorFlow)

## Explorer les chaînes de caractères avec Julia

Voir le manuel de Julia pour les chaînes de charactères (*Strings*) https://docs.julialang.org/en/v1/manual/strings/

Exemple : travail avec le jeu de données de Spam 

```julia
df = CSV.read("spam_dataset.csv", DataFrames.DataFrame)
first(df, 10) |> pretty
```

[TextAnalysis.jl](https://github.com/JuliaText/TextAnalysis.jl) offre de nombreuses fonctions destinées à travailler avec des chaînes de caractères dans le cadre de l’analyse de textes (voir la documentation). Afin de pouvoir travailler avec cette librairie, il est nécessaire de convertir une chaîne de caractère dans l’un des types suivants :

- `StringDocument`
- `FileDocument`
- `TokenDocument`
- `NGramDocument`

Afin de convertir les données du tableau, on peut utiliser la fonction `transform()`de DataFrames.

```julia
df = @chain df begin
  DataFrames.transform(:Message => ByRow(x -> StringDocument(x)) => :Message2)
end
```

Une fois que les données ont été converties vers un type utilisable par la librairie [TextAnalysis.jl](https://github.com/JuliaText/TextAnalysis.jl) il est désormais possible de leur appliquer des fonctions de cette librairie destinées à normaliser des chaînes de caractères :

- `remove_case!(...)` — pour normaliser une chaîne de caractères en supprimant les majuscules
- `prepare!(..., strip_numbers)` — pour supprimer les chiffres d’une chaîne de caractères
- `prepare!(..., strip_punctuation)` — pour supprimer la ponctuation d’une chaîne de caractères
- `prepare!(..., strip_html_tags)` — pour supprimer le balisage HTML d’une chaîne de caractères

Créer une matrice Tf-idf

Afin de pouvoir créer une matrice Tf-idf, il est nécessaire de créer un corpus afin de représenter la collection de documents

```julia
crps = Corpus(df[:, :Message2])
```

Il est ensuite nécessaire de créer un vocabulaire des données

```julia
update_lexicon!(crps)
```

Pour créer une matrice tf-idf, besoin de wrapper le corpus dans `DocumentTermMatrix(...)` pour appliquer la fonction tf_idf()

```julia
m = DocumentTermMatrix(crps)
tfidf_mat = tf_idf(m)
```

## Concordance

En analyse de texte, la concordance désigne l’extraction des mots de textes donnés. Celle-ci permet d’examiner la fréquence des mots ou des exemples. C’est une étape fondamentale pour des analyses linguistiques plus avancées.

La fonction `lexicon()` permet de lister les mots d’un corpus avec leur fréquence.

```julia
lexicon(crps)
```

Les concordances sont habituellement présentées sous la forme de mot-clef en contexte (*Key Word in Context* KWIC). Cet index permet de montrer les mots dans leur contexte environnant (contexte droit et gauche). C’est un outil qui aide à comprendre comment un terme est employé au sein d’un corpus.



## Étiquetage des rôles grammaticaux

L’étiquettage des rôles grammaticaux est une tâche de pré-traitement récurrente dans le domaine du traitement automatique des langues (TAL). Les corpus étiquettés servent ensuite de supports à des tâches plus complexes ou de plus haut niveau linguistique comme l’extraction terminologique, la recherche d’infromation, de patrons grammaticaux et sémantiques, la détection d’opinions ou la catégorisation des textes, ou de dérivations. L’efficacité de cette tâche est donc déterminante.

NLTK étiquettage seulement pour l’anglais (2012)



## Liste de paquets Julia pour NLP

### JuliaText

https://github.com/JuliaText

> JuliaLang Organisation for Natual Language Processing, (textual) Information Retrieval, and Computational Linguistics

#### Text Analysis

https://github.com/JuliaText/TextAnalysis.jl

Julia package for text analysis

> [TextAnalysis.jl](https://github.com/JuliaText/TextAnalysis.jl) is a comprehensive package for text processing and analysis, offering functionalities like tokenization, stemming, sentiment analysis, and topic modeling. Unlike LLMTextAnalysis.jl, TextAnalysis.jl provides a broader range of traditional NLP tools suitable for various text analysis tasks.

#### Word Tokenizer

> High performance tokenizers for natural language processing and other related tasks

https://github.com/JuliaText/WordTokenizers.jl

#### Embeddings

https://github.com/JuliaText/Embeddings.jl

> Functions and data dependencies for loading various word embeddings (Word2Vec, FastText, GLoVE)

#### Languages

https://github.com/JuliaText/Languages.jl

> A package for working with human languages

#### Word2Vec

https://github.com/JuliaText/Word2Vec.jl

>Word2Vec takes a text corpus as input and produces the word vectors as output. Training is done using the original C code, other functionalities are pure Julia. See [demo](http://nbviewer.ipython.org/github/JuliaText/Word2Vec.jl/blob/master/examples/demo.ipynb) for more details.

https://github.com/JuliaText/Embeddings.jl

https://word2vec.news-r.org

#### WordNet

https://github.com/JuliaText/WordNet.jl

> A Julia package for Princeton's WordNet®.

### Étiquetage des rôles grammaticaux et morphosyntaxique

cf. https://discourse.julialang.org/t/postagger-on-other-languages-than-english/53385/2

https://github.com/JuliaText/TextModels.jl/blob/master/docs/src/tagging.md?plain=1

Spacy state of the art



### Bert like

#### Transformers

https://chengchingwen.github.io/Transformers.jl/dev/

Julia implementation of Transformers models

> [Transformers.jl](https://github.com/chengchingwen/Transformers.jl) provides access to the HuggingFace Transformers library, which offers a wide range of pre-trained state-of-the-art models for NLP tasks. It also allows users to build transformer-based models from scratch on top Flux.jl.

#### ALBERT

> ALBERT(A Lite BERT for Self-Supervised Learning of Language Representations) implementation in Julia

https://github.com/tejasvaidhyadev/ALBERT.jl

### Autres

#### Text Models (obsolète)

> [TextModels.jl](https://github.com/JuliaText/TextModels.jl) enhances the TextAnalysis package with practical natural language models, typically based on neural networks (in Flux.jl)

#### StringAnalysis

> [StringAnalysis.jl](https://github.com/zgornel/StringAnalysis.jl) is a fork of TextAnalytics.jl, which offers a similar set of functionalities as TextAnalysis.jl, but with a slightly different API. It extends the original package with additional features like dimensionality reduction, semantic analysis, and more.

### A voir

https://github.com/oxinabox/DataDeps.jl

https://github.com/tejasvaidhyadev AU MILA

http://tejasvaidhyadev.github.io

## Divers

Avik Sengupta. Natural Language Processing workshop using Julia, JuliaCon 2018. https://youtu.be/f7RNuOLDyM8

Aussi travail Lindoln sur la collection de corpus langagiers.

0-20’ scraping

22-XX

JuliaCon 2018 | DataDeps.jl and other foundational tools for data driven research | Lyndon White https://youtu.be/kSlQpzccRaI

https://github.com/oxinabox/DataDeps.jl

https://github.com/JuliaText/CorpusLoaders.jl

https://github.com/JuliaText/WordNet.jl

JuliaCon 2018 | Julia as a platform for language development | Jamie Brandon https://youtu.be/BBUrQId0HhQ

https://scattered-thoughts.net

Enhanced String handling in Julia | Scott James. JuliaCon 2018 https://youtu.be/kWqFRGLdqc4

JuliaString.org

https://github.com/JuliaML/MLDatasets.jl/



Glob pour requête un disque dur

```julia
using Glob
```

```julia
files = Glob.glob('data/corpus/pdfs/*.pdf')
```

Plusieurs packages, Taro peut lire n’importe quel format

```julia
using Taro
Taro.init()
```

```julia
meta, txtdata = "Taro.extract(files[1])";
```

```julia
meta
```

information stockée comme un Dict

```julia
txtdata
```

données textuelles

```julia
txtdata = replace(txtdata, '\n', ' ')
```

suppression des espaces, car pas pertinents

```julia
using TextAnalysis
using Languages
```

```julia
getTitle(t) = TextAnalysis.sentence_tokenize(Languages.English(), t)[1];
```

```julia
getTitle(txtdata)
```

Extraire première ligne car le titre

```julia
docs = Any[ ]
for i in 1:1000
  try
    meta.txt = Taro.extract(files[i])
    txt = replace(txt, '\n', ' ')
    title = getTitle(txt)
    dm = TextAnalysis.DocumentMetadata(Languages.English(), title, "", meta["Creation-Date"])
    doc = StringDocument(txt, dm)
    
    push!(docs, doc)
    catch e
	    @show e
  end
end
crps = Corpus(docs)
```

```julia
typeof(crps)
```

## TextGraph package

https://juliapackages.com/p/textgraphs

- Semantic embeddings
- Graph embeddings

## SemanticTrajectories

RQA

## TidierText

TidierText.jl is a 100% Julia implementation of the R tidytext package. The purpose of the package is to make it easy analyze text data using DataFrames.

https://docs.juliahub.com/General/TidierText/stable/

## WorldCloud

https://github.com/guo-yong-zhi/WordCloud.jl

## Glove

https://github.com/domluna/Glove.jl

## Topic Models

https://github.com/slycoder/TopicModels.jl

## Text Graph

https://github.com/fargolo/TextGraphs.jl

## Références

- https://youtu.be/4jJD4F40WBA?si=1GEQJbhp2vT20PAa
