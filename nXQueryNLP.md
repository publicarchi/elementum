---
author: emchateau
tags: xquery, nlp
---



# XQuery NLP

Tutoriaux

- Text Mining at Scale https://gist.github.com/emchateau/c17de15f2d11b135116bce8f60efb6ef
- XQuery and XPath Full Text 1.0 https://gist.github.com/emchateau/8275ab308e31b686b058872ba51d5d45

Partition du corpus 

(sélection avec XPath d’une collection de poèmes dans un recueil)

Affichage d’un échantillon

Lister les titres

Normaliser 

```
  let $poemText := 
    fn:string-join($poem//text(), " ") =>
    fn:translate("—'*‘’.,?!:;-","") =>
    fn:normalize-space()
```



## Fonctionnalités 

## dplyr (R)

https://dplyr.tidyverse.org/

-  `mutate()` adds new variables that are functions of existing variables
- `transmute()` adds new variables and drops existing ones
-  `select()` picks variables based on their names.
-  `filter()` picks cases based on their values.
-  `summarise()` reduces multiple values down to a single summary.
-  `arrange()` changes the ordering of the rows.

## tidyr (R)

https://tidyr.tidyverse.org/

The goal of tidyr is to help you create **tidy data**. Tidy data is data where:

## SciPy (Python)

## NumPy (Python)

## SciKit-learn (Python)

## NLP avec Python

- We recommend NLTK only as an education and research tool. Its  modularized structure makes it excellent for learning and exploring NLP  concepts, but it’s not meant for production.
- TextBlob is built on top of NLTK, and it’s more easily-accessible.  This is our favorite library for fast-prototyping or building  applications that don’t require highly optimized performance. *Beginners should start here.*
- Stanford’s CoreNLP is a Java library with Python wrappers. It’s in many existing production systems due to its speed.
- SpaCy is a new NLP library that’s designed to be fast, streamlined,  and production-ready. It’s not as widely adopted, but if you’re building  a new application, you should give it a try.
- Gensim is most commonly used for topic modeling and similarity  detection. It’s not a general-purpose NLP library, but for the tasks it  does handle, it does them well.

https://www.nltk.org/

https://elitedatascience.com/python-nlp-libraries

https://kleiber.me/blog/2018/02/25/top-10-python-nlp-libraries-2018/

https://activewizards.com/blog/comparison-of-python-nlp-libraries/

## Interfaces

Spyder https://www.spyder-ide.org/ et RStudio