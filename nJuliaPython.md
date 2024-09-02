---
author: ecmhateau
tags: julia, python
---

# Utiliser des librairies Python dans Julia

Même si Julia présente de nombreux avantages pour le calcul scientifique et la recherche en humanités numériques, le langage reste relativement récent et ne présente pas encore un écosystème aussi large que celui de Python. Les développements récents en intelligence artificielle qui peuvent être mobilisés dans des travaux en humanités numériques ont souvent été implémentés en Python. Et bien, cela n’est pas nécessairement un problème, Julia propose plusieurs solutions pour travailler avec des librairies Python !

Deux cas de figure se présentent en Julia selon que ces librairies disposent ou pas d’une interface Julia.

## Utilisation d’une librairie Python disposant d’une interface Julia

Certaines librairies Python particulièrement populaires disposent en effet d’une interface Julia. Beaucoup de librairies Python sont écrites dans un autre langage (comme C++) et Python ne propose qu’une enveloppe pour y accéder. Souvent les utilisateurs n’y prettent même pas attention. La même approche est utilisée en Julia pour certaines librairies, parmi lesquelles :

- [PyPlot.jl](https://github.com/JuliaPy/PyPlot.jl) pour Matplotlib ;
- [Pandas.jl](https://github.com/JuliaPy/Pandas.jl) pour Pandas;
- [ScikitLearn.jl](https://github.com/cstjean/ScikitLearn.jl) pour scikit-learn;
- [Seaborn.jl](https://github.com/JuliaPy/Seaborn.jl) pour Seaborn;
- [SymPy.jl](https://github.com/JuliaPy/SymPy.jl) pour SymPy.

Dans ce cas de figure, il suffit d’installer le paquet Julia pour utiliser directement le paquet Python voulu.

## Utilisation en Julia de n’importe quelle librairie Python

Lorsqu’il n’existe pas d’înterface Julia, vous pouvez néanmoins également utiliser n’importe quelle librairie Python.

Il existe deux Paquets Julia pour faire cela : [PyCall.jl](https://github.com/JuliaPy/PyCall.jl) et [PythonCall.jl](https://github.com/cjdoris/PythonCall.jl). 

- PythonCall supporte plus de conversions entre Julia et Python, et ce mécanisme est extensible
- PythonCall ne copie jamais les objets mutables lors de la conversion mais les enveloppe, cela signifie que la modification de l’objet converti modifie l’original et que la conversion est plus rapide
- PythonCall ne conserva pas automatiquement les résultats en objet Julia, ce qui facilite l’exécution des tâches python
- PythonCall installe les dépendances dans un environnement Conda distinct pour chaque projet avec CondaPkg

## Paquets Julia

- PyCall https://github.com/JuliaPy/PyCall.jl
- PythonCall https://juliapy.github.io/PythonCall.jl

## Références

- Kamiński, Bogumił. 2023. « Julia and Python Better Together ». *Blog by Bogumił Kamiński* (blog). 17 février 2023. https://bkamins.github.io/julialang/2023/02/17/python.html.
- Baumgartner, Peter. 2021. « Incorporating Julia Into Python Programs ». *Peter Baumgartner* (blog). 9 août 2021. https://www.peterbaumgartner.com/blog/incorporating-julia-into-python-programs/.
- « MATLAB–Python–Julia cheatsheet — Cheatsheets by QuantEcon documentation ». s. d. Consulté le 11 décembre 2019. https://cheatsheets.quantecon.org/.
- https://discourse.julialang.org/t/ann-pythoncall-and-juliacall/76778/6