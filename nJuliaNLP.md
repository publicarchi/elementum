---
author: emchateau
tags: julia, nlp
---

# Julia NLP

## JuliaText

https://github.com/JuliaText

> JuliaLang Organisation for Natual Language Processing, (textual) Information Retrieval, and Computational Linguistics

### Text Analysis

https://github.com/JuliaText/TextAnalysis.jl

> Julia package for text analysis

### Word Tokenizer

> High performance tokenizers for natural language processing and other related tasks

https://github.com/JuliaText/WordTokenizers.jl

### Embeddings

https://github.com/JuliaText/Embeddings.jl

> Functions and data dependencies for loading various word embeddings (Word2Vec, FastText, GLoVE)

### Languages

https://github.com/JuliaText/Languages.jl

> A package for working with human languages

### Word2Vec

https://github.com/JuliaText/Word2Vec.jl

>Word2Vec takes a text corpus as input and produces the word vectors as output. Training is done using the original C code, other functionalities are pure Julia. See [demo](http://nbviewer.ipython.org/github/JuliaText/Word2Vec.jl/blob/master/examples/demo.ipynb) for more details.



https://github.com/JuliaText/Embeddings.jl

https://word2vec.news-r.org

## WordNet

https://github.com/JuliaText/WordNet.jl

> A Julia package for Princeton's WordNet®.

## Bert like

### Transformers.jl 

> Julia implementation of Transformers models

https://chengchingwen.github.io/Transformers.jl/dev/

### ALBERT

> ALBERT(A Lite BERT for Self-Supervised Learning of Language Representations) implementation in Julia

https://github.com/tejasvaidhyadev/ALBERT.jl

## A voir

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

## Références

- https://youtu.be/4jJD4F40WBA?si=1GEQJbhp2vT20PAa
