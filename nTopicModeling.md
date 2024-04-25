# Topic Modeling

> Topic modelling is an NLP task where, given a corpus of documents, the objective is to find the underlying meaningful *clusters* of docu- ments (or *topics*) that are thematically coherent (use consistent and related vocabulary) and assign each document to one or more of these topics. As a text mining technique, it allows the analysis of big volumes of textual documents through clus- tering them into coherent sets addressing similar subjects (or topics), and labeling them using key- words that are understandable by the end-user. It has the advantage of not relying on any labeled data to achieve good results, as the training of topic models is done in an unsupervised matter. 
>
> https://aclanthology.org/2021.ranlp-1.55.pdf

*Proceedings of Recent Advances in Natural Language Processing*

https://aclanthology.org/volumes/R15-1/

méthode utilisée en exploration

## Outils

- Mallet
- Linkage
- BERT Topic

Python (textblob, spacy)

## Textblob

https://textblob.readthedocs.io/en/dev/

> *TextBlob* is a Python (2 and 3) library for processing textual data. It provides a simple API for diving into common natural language processing (NLP) tasks such as part-of-speech tagging, noun phrase extraction, sentiment analysis, classification, translation, and more.

#### Features

- Noun phrase extraction
- Part-of-speech tagging
- Sentiment analysis
- Classification (Naive Bayes, Decision Tree)
- Language translation and detection powered by Google Translate
- Tokenization (splitting text into words and sentences)
- Word and phrase frequencies
- Parsing
- `n`-grams
- Word inflection (pluralization and singularization) and lemmatization
- Spelling correction
- Add new models or languages through extensions
- WordNet integration

## Spacy

https://spacy.io

> spaCy is designed to help you do real work — to build real products, or gather real insights. The library respects your time, and tries to avoid wasting it. It's easy to install, and its API is simple and productive. We like to think of spaCy as the Ruby on Rails of Natural Language Processing.

## Word vectors

An R package for building and exploring word embedding models.

https://github.com/bmschmidt/wordVectors

cf. tutoriaux 

- https://github.com/NEU-DSG/wwp-public-code-share/tree/master/WordVectors
- https://jmclawson.net/blog/posts/word-vector-utilities/
- https://github.com/NEU-DSG/wwp-public-code-share/blob/master/WordVectors/introduction_word2vec.Rmd
- https://github.com/NEU-DSG/wwp-public-code-share/blob/master/WordVectors/template_word2vec.Rmd

## Topic Modeling avec Julia

### TextAnalysis.jl

https://github.com/JuliaText/TextAnalysis.jl

Julia's leading NLP library

Latent Dirichlet Allocation (LDA), but Latent Semantic Analysis (LSA) is also available 

### TopicModels.jl

Latent Dirichlet Allocation (LDA, Blei et al. 2003)

https://juliapackages.com/p/topicmodels

### QuranTree.jl

https://docs.juliahub.com/QuranTree/Ze2JD/0.1.0/man/nlp/topic_modeling/

Tutoriaux

### TopicModelsVB.jl

https://github.com/ericproffitt/TopicModelsVB.jl

