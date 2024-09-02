---
author: emchateau
tags: julia, machine learning
---

# Julia ML

| Purpose                  | Python                                                       | Julia                                                        |
| :----------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Linear algebra           | [Numpy](https://numpy.org/)                                  | Built in arrays, [LinearAlgebra](https://docs.julialang.org/en/v1/stdlib/LinearAlgebra/)package |
| Work with datasets       | [Pandas](https://pandas.pydata.org/)                         | [DataFrames.jl](https://dataframes.juliadata.org/stable/)    |
| Data visualization       | [Matplotlib](https://matplotlib.org/)                        | [Plots.jl](https://docs.juliaplots.org/stable/)              |
| Classic Machine learning | [SciKit-Learn](https://scikit-learn.org/)                    | [MLJ.jl](https://alan-turing-institute.github.io/MLJ.jl/dev/about_mlj/), [ScikitLearn.jl](https://scikitlearnjl.readthedocs.io/en/latest/), [BetaML.jl](https://github.com/sylvaticus/BetaML.jl) |
| Neural Networks          | [TensorFlow](https://www.tensorflow.org/) or [Pytorch](https://pytorch.org/) | [Flux.jl](https://fluxml.ai/Flux.jl/stable/), [BetaML.jl](https://github.com/sylvaticus/BetaML.jl), [Lux.jl](https://lux.csail.mit.edu/stable/) |

## Machine Learning

https://fr.wikipedia.org/wiki/Apprentissage_automatique

modèles courants tels que la Logistic Regression, Decission Tree ou Random Forest

- [Supervised Learning](http://scikit-learn.org/stable/supervised_learning.html) (linear regression, support vector machines, random forest, neural nets, ...)
- [Unsupervised Learning](http://scikit-learn.org/stable/unsupervised_learning.html) (clustering, PCA, mixture models, manifold learning, ...)
- [Dataset Transformation](http://scikit-learn.org/stable/data_transforms.html) (preprocessing, text feature extraction, one-hot encoding, ...)

### ScikitLearn.jl

ScikitLearn.jl implements the popular [scikit-learn](http://scikit-learn.org/stable/) interface and algorithms in Julia. It supports both models from the Julia ecosystem and those of the [scikit-learn library](http://scikit-learn.org/stable/modules/classes.html) (via PyCall.jl).

Would you rather use a machine-learning framework specially-designed for Julia? Check out [MLJ.jl](https://github.com/alan-turing-institute/MLJ.jl), from the Alan Turing institute.

https://github.com/cstjean/ScikitLearn.jl

https://cstjean.github.io/ScikitLearn.jl/dev/

### A Machine Learning Framework for Julia

MLJ (Machine Learning in Julia) is a toolbox written in Julia providing a common interface and meta-algorithms for selecting, tuning, evaluating, composing and comparing about [200 machine learning models](https://alan-turing-institute.github.io/MLJ.jl/dev/model_browser/#Model-Browser) written in Julia and other languages.

https://github.com/alan-turing-institute/MLJ.jl

https://alan-turing-institute.github.io/MLJ.jl/dev/

## Packages utiles

- [Distances.jl](https://github.com/JuliaStats/Distances.jl), A Julia package for evaluating distances (metrics) between vectors. Notamment la similarité cosinus (*Cosine distance*)

La **similarité cosinus** donne la similarité de deux vecteurs à *n* dimensions en déterminant le cosinus de leur angle. Ce score est fréquemment utilisée en fouille de textes.

En règle générale, pour mesurer finement la similarité entre des séquences de texte, les vecteurs sont construits d'après un calcul de type TF-IDF (*term frequency–inverse document frequency*) qui permet d'estimer l'importance d'un mot par rapport au document qui le contient, en tenant compte du poids de ce mot dans le corpus complet.

Sur le softMax Bendersky, Eli. 2016. « The Softmax function and its derivative - Eli Bendersky’s website ». *Eli Bendersky’s website* (blog). 18 octobre 2016. https://eli.thegreenplace.net/2016/the-softmax-function-and-its-derivative/

## Références

- https://github.com/ablaom/HelloJulia.jl/wiki/JuliaCon-2022-workshop:-Getting-started-with-Julia-and-MLJ
- Germanov, Andrey. 2023. « Machine Learning with Julia – How to Build and Deploy a Trained AI Model as a Web Service ». *DEV Community* (blog). 17 février 2023. https://dev.to/andreygermanov/machine-learning-with-julia-solve-titanic-competition-on-kaggle-and-deploy-trained-ai-model-as-a-web-service-f9l.
- https://juliaai.github.io/DataScienceTutorials.jl/
- https://juliaai.github.io/DataScienceTutorials.jl/
- An Introduction to Statistical Learning https://www.statlearning.com pour Julia https://github.com/tndoan/ISLR.jl