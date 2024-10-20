---
author: emchateau
tags: nlp
---

# NLP Natural Language Processing

Carmelina

Sur les modèles de langues https://twitter.com/deliprao/status/1567280110369214464

Language Models have taken [#NLProc](https://twitter.com/hashtag/NLProc?src=hashtag_click) by storm. Even if you don’t directly work in NLP, you have likely heard and possibly, used language models. But ever wonder who came up with the term “Language Model”? Recently I went on that quest, and I want to take you along with me.

Shannon travaillait sur l’entropy de la langue anglaise, pour développer une théorie de la communication optimale. Shannon dans son article de 1948 ne fait pas mention des "Language Model" ni dans aucun travail successif. https://people.math.harvard.edu/~ctm/home/text/others/shannon/entropy/entropy.pdf

Par la suite c’est en 1958 qu’il est de nouveau fait allusion aux modèles de langues, dans l’article de Chomsky intitulé "three models for the description of language", où il les désigne comme des "Finite State Markov Processes".

> 2. Finite State Markov Processes
>
>    2.1. The most elementary grammars which, with a finite amount of apparatus, will generate an infinite number of sentences, are those based on a familiar conception of language as a particularly simple type of information source, namely, a finite-state Markov process. Specifically, we define a finite-state grammar G as a system with a finite number of states.... 

Par la suite mobilisé par la grammaire et ne poursuivit pas cette conception. Cependant il les désigne comme des Modèles de langue. https://chomsky.info/wp-content/uploads/195609-.pdf

Le Center for Language and Speech Processing at de l’Université Johns Hopkins en 1995 sur l’ajout de syntaxe dans les modèles de langues, “LM95”. Mais l’emploi de la terminologie était alors très opérationnel. Quoiqu’il en soit la désignation apparaît entre 1958 et 1995.

Article de 1976, sans doute le premier à employer le terme “language model” dans la littérature scientifique.

> It is the function of the *language mode (LM)* to provide us with estimates of *P{w}* for all word strings *w*. We will assume that the LM is a Markov source in the sense of Appendix II, i.e., a Markov cahin whose state transitions are associated with word output probability distributions. We will leave to later research the proble of LM construction for natural language corpora, and will simpy assyme here that the LM is given.

Frederick Jelinek. Continuous Speech Recognition by Statistical Methods. Proceedings of the IEEE, vol. 64, n° 4, avril 1976. https://ieeexplore.ieee.org/iel5/5/31240/01454428.pdf

L’article en lui même constitue une étape importante. C’est le premier à décire un engin pré-deep learning ASR. L’architecture qui est décrite est très proche de son déploiement actuel.

Linguistic decoder qui retourne le score de séquences de mots. Attire attention note 17.

https://arxiv.org/abs/0812.4360

Great thread, but I'd argue that Miller & Chomsky "Finitary Models of Language Users" (1963) (section 1 "Stochastic Models") is where it started conceptually.

To add a bit of historical context, the Bakers (who developed Dragon at CMU) would have been working with Jelinek at IBM at this time. Jim Baker's PhD work was Dragon. Both he and Janet Baker were hired by Jelinek's group at IBM around 1974.

I'm not sure if Baker himself ever uses "language model" to describe it, but it was used to describe the general concept in reports comparing language modeling approaches in projects funded by the DARPA SUR program, CMU/Dragon being among them.

Any specific credit for "first" is always going to be murky and depends a lot on which combination of elements you consider to define the contemporary understanding of the concept and in what context. You can certainly make a strong case for the IBM CSR group in the early 1970s.

There was also probably a strong influence from those not directly in the group like John Cocke and Joe Raviv. You could also make a case for basic language models in ASR around 1958 with Denes and Fry. Or even for A. A. Markov in 1906 if you want to get really pedantic about it.

Mel’chuk I. A. “An Intermediary Language Model for Machine Translation” Abstracts of the Conference on Machine Tranlation, may 15-21, 1958, 8.

## Outils de NLP

- [Spacy](http://spacy.io) : python, orienté performance, pas de choix des méthodes et algorithmes
- [NLTK](http://www.nltk.org/) : python, orienté pédagogie, choix des méthodes et algorithmes
- [CoreNLP](https://stanfordnlp.github.io/CoreNLP/) : framework Java de Stanford, orienté recherche, chaîne de TAL très complète pour l’anglais en particulier
- [Stanza](https://stanfordnlp.github.io/stanza/) : python, framework de Stanford, modèles neuronaux entraînés sur les données d'Universal Dependancies.
  [https://github.com/explosion/spacy-stanza](https://github.com/explosion/spacy-stanza) permet d’utiliser les modèles de Stanford avec Spacy
- [TextBlob](https://textblob.readthedocs.io/en/dev/) : python
- [DKPro](https://dkpro.github.io) : java
- [flair](https://github.com/zalandoresearch/flair) : python, le framework de Zalando, très bonnes performances en reconnaissance d’entités nommées

## SVM

SVM désigne un ensemble de méthodes d’apprentissage supervisé développé par Vapnik et ses collègues basé sur le principe de *Structural Risk Minimization* issu de la théorique d’apprentissage statistique.

>As linear classifiers (with linear kernel), SVMs aim to find the hyperplanes that separate data points with the maximal margins between the two decision boundaries. Aiming to minimize the generalization error, SVMs have the advantage of reducing the risk of overfitting. SVMs outperform other text classification methods in a number of comparative evaluations on topic classification tasks (Dumais et al., 1998; Joachims, 1998; Yang and Liu, 1999).

- Vapnik, V. N. (1982). Estimating of Dependencies Based on Empirical Data. New York: Springer. 
- Vapnik, V. N. (1999). The Nature of Statistical Learning Theory. 2nd edn. Berlin: Springer-Verlag.

### Implémentations en Julia

La plupart des implémentations sont des wrapper par dessus [LIBSVM 65](https://www.csie.ntu.edu.tw/~cjlin/libsvm/). MLJ utilise par exemple [LIBSVM.jl 62](https://github.com/mpastell/LIBSVM.jl)).

Il existe un guide pour débuter sur LIBSVM 65 [how to start 62](https://www.csie.ntu.edu.tw/~cjlin/papers/guide/guide.pdf) (normalizing your data, setting the parameters and so forth).

## BERT

> BERT is a neural network-based language mode from Google that is trained to perform natural language processing tasks. It was introduced by google researchers in 2018. 

https://ai.googleblog.com/2018/11/open-sourcing-bert-state-of-art-pre.html

## BART 

> BART is a sequence-to-sequence model that uses a denoising autoencoder to pre-train its encoder and decoder. The model was designed to be able to handle long sequences by using a Transformer architecture. It was released in 2019.

https://huggingface.co/docs/transformers/model_doc/bart

## T5 

T5 is designed to be used for a variety of tasks, including text classification, question answering, and text generation. T5 is also trained on a larger amount of data than BERT, which makes it more accurate for some tasks.

https://ai.googleblog.com/2020/02/exploring-transfer-learning-with-t5.html

## GPT-3 

Generative Pre-Trained Transformer 3 is a 175 billion parameter model that can write text similar to humans in response to an input prompt. The model is based on the transformer architecture and got released in 2020.

https://datacamp.com/blog/a-beginners-guide-to-gpt-3

## LaMDA 

Language Models for Dialog Application (LaMDA) was to enable software to better engage in a fluid and natural conversation. Unlike other language models, LaMDA was trained on dialogue and was introduced by google in 2021.

https://blog.google/technology/ai/lamda/

## Switch Transformers

Switch Transformers is the first trillion parameters model open-sourced by Google in 2022. It is based on the concept of MoE where models can choose different parameters for different inputs based to achieve higher performance.

https://deeplearning.ai/the-batch/bigger-faster-transformers/

## Lumi

Since 2022 [#Lumi](https://twitter.com/hashtag/Lumi?src=hashtag_click) from @Aleph__Alpha a language model related to 5 European languages: English, French, German, Italian and Spanish.

