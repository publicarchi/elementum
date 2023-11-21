---
author: Emmanuel Château-Dutier
since: 2017-01-18
tags: machine learning

---

# Divers Machine learning

On distingue plusieurs catégories de problèmes, tâches ou activités dans l’apprentissage machine (*machine learning*) :

### L’apprentissage supervisé (*supervised learning*).

Cette suite de problèmes est comparable à celle de la régression. Des données sont disponibles sous la forme *(x<sub>i</sub>, y<sub>i</sub>)* et l’objectif est d’apprendre comment prédire *Y* à partir de *X*. En apprentissage machine, chaque *x<sub>i</sub>* est de dimension élévée. Ses éléments sont appelés caractéristiques (?) *features* et la variable *y<sub>i</sub>* est référee comme l’annotation (*label*).

Lorsque les annotations (*labels*) sont seulement 0 ou 1, ou proviennent d’un ensemble discret fini, le problème d’apprentissage supervisé est appellé problème de classification (*classification problem*). Par opposition, lorsque les annotations (*labels*) sont continus, cela est nommé un problème de régression (*regression problem*).

(Nazarathy et Klok 2021)

cf. <https://fr.wikipedia.org/wiki/Apprentissage_supervisé>

### L’apprentissage non-supervisé (*unsupervised learning*)

Dans le cas de l’apprentissage non-supervisé, il n’y a que des *features* *Y* mais pas d’étiquetage (*labels*) *Y*. On peut penser à un enfant qui apprend en découvrant le monde sans recevoir de feedback ou de directives explicites. Dans l’apprentissage non-supervisé, une tâche importante et la création de *clusters* de fpoints et la reconnaissance de *clusters*. Cela relève des algorithmes de clusturisation (*clustering*). Une autre tâche consiste à réduire la dimension des données (*data reduction*).

(Nazarathy et Klok 2021)

cf. <https://fr.wikipedia.org/wiki/Apprentissage_non_supervisé>

**L’apprentissage par renforcement (*reinforcement learning*)**

Dans ce cas un agent (*agent*) prend des décisions dynamiquement dans le temps en cherchant à maximiser plusieurs objectifs ou à réaliser certains comportements. Dans certains cas, l’agent dispose de connaissance sur la manière dont le monde répond aux décisions, mais ce savoir est souvent lacunaire ou très partiel. L’apprentissage par renforcement permet de contrôler de tels systèmes de manière presque optimale. Par exemple, jouer au Go, jouer à un jeu vidéo contre un ordinateur et s’améliorer.

(Nazarathy et Klok 2021)

cf. <https://fr.wikipedia.org/wiki/Apprentissage_par_renforcement>

**La modélisation générative (*Generative modeling*)**

Dans cette tâche, il s’agit d’observer des données similaires à celles de l’apprentissage non-supervisé et de créer un modèle qui peut alors créer des données additionnelles similaires. La technologie de *deep fake* où des images et des films peuvent être modifiés pour apparaître différemment tout en paraissant naturelle est un exemple d’application.

(Nazarathy et Klok 2021)

## Bibliographie

- Goodfellow, Ian, Yoshua Bengio, et Aaron Courville. 2016. *Deep Learning*. Adaptive Computation and Machine Learning. Cambridge, Massachusetts: The MIT Press.
- Kroese, Dirk P., Zdravko I. Botev, Thomas Taimre, et Radislav Vaisman. 2020. *Data science and machine learning: mathematical and statistical methods*. First edition. Chapman & Hall/CRC machine learning & pattern recognition. Boca Raton: CRC Press, Taylor & Francis Group.
- Nazarathy, Yoni, et Hayden Klok. 2021. « Machine Learning Basics ». In *Statistics with Julia: Fundamentals for Data Science, Machine Learning and Artificial Intelligence*, édité par Yoni Nazarathy et Hayden Klok, 361‑422. Springer Series in the Data Sciences. Cham: Springer International Publishing. https://doi.org/10.1007/978-3-030-70901-3_9.

## Références diverses

http://www.holehouse.org/mlclass/

http://www.r2d3.us/visual-intro-to-machine-learning-part-1/

https://www.pinterest.com/pin/88453580161916827/?utm_content=bufferc64ae&utm_medium=social&utm_source=twitter.com&utm_campaign=buffer

http://neuralnetworksanddeeplearning.com

http://devzum.com/2015/05/best-free-machine-learning-ebooks/

http://www.asimovinstitute.org/neural-network-zoo/?utm_content=bufferb0b5f&utm_medium=social&utm_source=twitter.com&utm_campaign=buffer

http://www.tensorflowbook.com

https://github.com/jtoy/awesome-tensorflow

https://github.com/blackecho/Deep-Learning-TensorFlow

## Cours

https://mml-book.github.io/

## Terminologie

<http://www.cse.unsw.edu.au/~billw/mldict.html>

http://www.kdnuggets.com/2016/10/deep-learning-key-terms-explained.html

## Algorithmes

https://www.dezyre.com/article/top-10-machine-learning-algorithms/202

http://machinelearningmastery.com/a-tour-of-machine-learning-algorithms/

http://thinkbigdata.in/best-known-machine-learning-algorithms-infographic/

## Visualisation

http://www.r2d3.us/visual-intro-to-machine-learning-part-1/

http://tinlizzie.org/histograms/