---
author: emchateau
tags: julia
---

# Julia divers

## Préambule

> We are greedy: we want more. We want a language that’s open source, with a liberal license. We want the speed of C with the dynamism of Ruby. We want a language that’s homoiconic, with true macros like Lisp, but with obvious, familiar mathematical notation like Matlab. We want something as usable for general programming as Python, as easy for statistics as R, as natural for string processing as Perl, as powerful for linear algebra as Matlab, as good at gluing programs together as the shell. Something that is dirt simple to learn, yet keeps the most serious hackers happy. We want it interactive and we want it compiled.
>
> Bezanson, Jeff, Stefan Karpinski, et Edelman Viral B. Shah Alan. 2012. « Why We Created Julia ». férvier 2012. https://julialang.org/blog/2012/02/why-we-created-julia/.

- [Documentation du langage](https://docs.julialang.org/en/v1/)
- [Noteworthy Differences from other Languages](https://docs.julialang.org/en/v1/manual/noteworthy-differences/#Noteworthy-Differences-from-other-Languages)
- [The Fast Track to Julia (aide-mémoire)](https://cheatsheet.juliadocs.org)

### Avantages

* Julia est **composable**
* Julia est **concis**
* Julia est **performant**
* Julia est **productif**
* Julia est **facile à maintenir**
* Julia est **libre et open-source**

Outre ces qualités, il nous semble que la consistance et la clareté de sa syntaxe en fait un très bon candidat pour l’apprentissage de la programmation.

### Caractéristiques de Julia

- langage dynamiquement typé, mais avec des types optionnels
- built-in types équivalent à des types définis par les utilisateurs
- compilation JIT
- utilisation de multiple dynamic dispatch
- capacités de métaprogramming
- appel natif de librairies en C et Fortan

### Historique du langage

- 0.0 – 2009
- 0.1 – Feb 14, 2012
- 1.0 – Aug 8, 2018 (LTS)
- 1.6 – Mar 24, 2021 (LTS)
- 1.9 – May 07, 2023
- 1.10 – December 27, 2023 cf. https://julialang.org/blog/2023/12/julia-1.10-highlights/

### Comparaison avec Python

- facile à apprendre depuis Python
- les librairies Python sont toutes utilisables vi PyCall.jl ou PythonCall.jl
- vitesse d’exécution comparable à celle de C
- parallélisation fait partie du langage

cf. https://youtu.be/qhrY0c_BHs8?si=fyPDO-f0U-PXVoJs

## Installation

Télécharger Julia depuis la page dédiée et suivre les instructions https://julialang.org/downloads/

Plusieurs IDE sont disponible, le plus courramment utilisé consiste en l’utilisation de [l’extension Julia](https://marketplace.visualstudio.com/items?itemName=julialang.language-julia) de Visual Studio Code.

Il existe un [Kernel Julia](https://github.com/JuliaLang/IJulia.jl) pour les notebooks Jupyter mais aussi un environnement de notebooks interactifs nativement développé en Julia [Pluto.jl](https://plutojl.org)

## Premiers pas dans le terminal

Démarrer Julia

```bash
julia
```

Arrêter Julia

```julia
exit()
```

ou

````
<Ctl-D>
````

Premiers pas en ligne de commande ou REPL (Read-Eval-Print-Loop)

```julia
println("Hello world !")
```

```julia
1 + 2
```

```julia
sqrt(4)
```

Accéder à de l’aide

```julia
?
println
```

`Enter` ou `Backspace` pour quitter l’aide.

Shell

```julia
;
pwd
```

Gestionnaire de paquets

```julia
]
```

`Backspace` pour quitter le gestionnaire de paquets.

## Syntaxe de base

Il n’y a pas d’indentation en Julia. Pour définir un bloc d’instruction, on commence par un mot-clef et ce bloc se termine par un `end`

```julia
if a >= b
end
```

Pour concaténer une chaîne de caractère on utilise `*`. Le symbole puissance `^` permet de répéter un caractère. On peut représenter un caractère explicitement avec des apostrophes simples `''` et des chaînes de caractères avec `""`

```julia
'a'^5 * "bc"
```

C’est souvent l’utilisation des types qui permet à Julia une exécution très rapide. Il est possible de créer une liste non typée ou des listes typées. Pour ajouter un type à tous les éléments de la liste, on le précise avant la liste.

```julia
slow = []
fast = Int[]
```

Dans la syntaxe de Julia le premier élément est `1` contrairement à d’autres langages où l’index est `0`. On peut accéder avec le mot-clef `end` au dernier élément. La dernière valeur est incluse dans la plage.

```julia
list[1] == first(list)
list[end] == last(list)
list[begin+1:end-1]
```

Julia ne dispose pas de classe à proprement parler. Toutefois, il est possible de créer une structure de données avec `struct`. Pour créer une structure mutable, on précède par le mot-clef `mutable`. Cette distinction est permise pour permettre l’accélération du code.

```julia
struct X
	field
end
mutable struct X
	field::Float64
end
```

Julia propose une compilation à la volée JIT. Tout le code est compilé avant d’être exécuté lors du chargement des modules. 

Multiméthode, le code à exécuter pour une fonction dépend des types de **tous** les arguments.

- fonction : un nom (`+`, `read`), souvent partagé entre des paquets (`filter!`)
- méthode : une implémentation d’une fonction selon les types `+(::Int, ::Int)`
- polymorphisme à la C++, en Python seul le type de l’objet est considéré

## Mise en pratique

```julia
println("Vive Julia !")
```

Les types sont importants en Julia. Attention on ne peut concaténer que des chaînes

```julia
println("Vive Julia " * VERSION * " !")
# La constante VERSION a pour type VersionNumber.
```

```julia
println("Vive Julia " * string(VERSION) * " !")
```

Lors de la définition d’une variable, l’interpréteur lui assigne un type

```julia
a = 42
println(typeof(a))
    
b = 3.14159
println(typeof(b))
    
c = 'c'
println(typeof(c))
    
d = "Julia"
println(typeof(d))
```

Le type d’une variable peut changer au cours de sa vie

```julia
a = 42
println(typeof(a))
a = 'c'
println(typeof(a))
```

Pour le débogage, @show affiche aussi l’expression :

```julia
@show a;
```

Commentaires

```julia
# commentaire simple
```

```julia
#=
Commentaire
Multi-ligne
=#
```

## Les chaînes de caractères

L’interpolation des chaînes de caractère est utile

```julia
langage = "Julia"
println("Vive $langage $(Version) !")
```

Unicode est géré nativement, même pour les noms de variables.

```julia
γs_regex = r"γ|Γ" # \gamma et \Gamma dans l’interpréteur, Jupyter et la plupart des environnements
match(γs_regex, "abγ")
```

Texte multiligne

```julia
multi_line = """
   This is a
   multi-line string.
"""
print(multi_line)
```

## Structure de données de base

Les éléments d’un tableau de base peuvent avoir un type. Un type par défaut est attribué.

```julia
a = Int[1, 2, 3]
# Int[1, 2, 3.14] retourne une erreur
```

```julia
b = [1, "2", 3.14159] # type inféré : Any
```

```julia
c = [1, 2, 3] # type inféré : Int
```

Les fonctions dont le nom se termine par `!` modifient leur premier argument (conventionnellement), en respectant les types.

```julia
push!(a, 4)
```

```julia
push!(a, ℯ) # \euler
```

```julia
push!(b, ℯ)
```

Il est également possible de créer des dictionnaires avec `Dict{k, v}`

```julia
d = Dict{Int, Float64}(1 => π, 2 => ℯ)
```

## Manipuler des données structurées comme des DataFrames

cf. https://github.com/datacraft-paris/2211-Cuvelier-Julia/blob/main/2-dataframes.ipynb

Charger les paquets pour travailler

```julia
using DataFrames
using RDatasets
using Statistics
using Chain
```

Charger le jeu de données Iris.

### Sélectionner des données

L’indexation sélectionne ici un groupe de ligne et avec `:` toutes les colonnes.

```julia
iris = dataset("datasets", "iris")[[1, 51, 101], :]
```

On peut également faire l’inverse et renvoyer les données d’une colonne.

```julia
iris = dataset("datasets", "iris")[:, :SepalLength] # renvoie un vecteur
```

```julia
iris = dataset("datasets", "iris")[:, [:SepalLength]] # renvoie un dataframe
```

Avec la fonction `select()`, il est également possible de sélectionner une colomne par son numéro, son symbole ou une chaîne de caractère

```julia
select(iris, :SepalLength, 2, "PetalLength")
```

Toutes les colomnes sauf...

```julia
select(iris, Not(2)) # Not() est une fonction de DataFrames pas de Julia
```

Utilisation d’un prédicat

```julia
select(iris, Cols(endswith("Length")))
# endswith("Length") renvoie une fonction
# endswith("Length")("sepalLength") == true
# x -> endswith(x, "Length")
```

On ne peut pas sélectionner la même colonne plusieurs fois dans les arguments.

### Transformer des données

Il est également possible de transformer les données pour obtenir des informations plus intéressantes. Par exemple, il est possible de calculer la moyenne de la longueur des pétals.

`combine` fusionne toutes les ligens en une seule avec l’opération indiquée.

On peut ainsi appliquer une fonction `mean` sur toute une colonne :

```julia
combine(iris, :PetalLength => mean) # renvoie un dataFrame
```

Pour récupérer la valeur, le DataFrame peut être appelé comme une matrice :

```julia
combine(iris, :PetalLength => mean)[1, 1] # rapporte la valeur scalaire
```

### Création de nouvelles colonnes

Avec `select`, on effectue l’opération ligne par ligne. 

Avec la syntaxe précédente, `select()` permet de créer une nouvelle colonne avec un calcul simple donné par une fonction à appliquer sur toute la colonne.

Retourner la valeur moyenne des longueurs de pétales dans tout le DataFrame et recopier cette valeur dans chaque ligne :

```julia
select(iris, [:PetalLength, :PetalWidth] => mean)
```

Il est possible de transformer plusieurs colonnes à la fois et de générer une nouvelle colonne. Attention, la fonction utilisée doit avoir le bon nombre d’arguments :

```julia
select(iris, [:PetalLength, :PetalWidth] => +)
```

Pour des opérations plus compliquées, il faudra écrire une lambda qui devra gérer les vecteurs complets pour chacune des colonnes pour faire les opérations d’un coup.

On peut définir une fonction anonyme qui prendra en argument les colonnes complètes (`.+` ) pour effectuer l’opération `+` ligne par ligne.

Pour faire la somme des deux valeurs divisées par leur différence. Ici le point devant l’opérateur est utilisé pour dire que l’on va appliquer l’opération élément par élément. Sinon Julia aurait additionné les vecteurs.

```julia
select(iris, [:PetalLength, :PetalWidth] => (pl, pw) -> (pl .+ pw) ./ (pl .- pw))
```

On peut encore utiliser la même notation pour faire plusieurs opérations sur les colonnes. Ce qui produit le résultat de chaque fonction pour chaque colonne (produit cartésien) avec `.=>` au lieu de `=>`

La fonction pour la transformation doit prendre toute la colonne en entrée, pas seulement la valeur sur une ligne. Si l’on souhaite réaliser une opération pour une ligne, on peut utiliser `ByRow` :

```julia
select(iris, :PetalLength => ByRow(sqrt))
```

Si l’on veut renvoyer plusieurs valeurs à partir d’une colonne, il est possible de renvoyer un tuple avec une transformation `AsTable` pour dire que la colonne ne doit pas contenir le tuple.

```julia
select(iris, :PetalLength => ByRow((pl) -> (pl, pl.^2)) => AsTable)
```

Ce genre d’opération peut être utilsée pour ajouter de nouvelles colonnes.

```julia
transform(iris, :PetalLength => ByRow((pl) -> (pl, pl.^2)) => AsTable)
```

Il est encore possible d’utiliser la syntaxe des tuple nommés pour attribuer un nom aux colonnes.

```julia
transform(iris, :PetalLength => ByRow((pl) -> (pl=pl, pl_sq=pl.^2)) => AsTable)
```

### Groupements de ligne

`groupby` permet de grouper des lignes selon un critère, on peut alors applique `combine` pour produire une valeur par groupe, comme une moyenne.

```julia
combine(
	groupby(iris, :Species),
	Not(:Species) .=> mean
)
```

Afin de faciliter le travail avec les DataFrame, on utilise la macro `@chain` qui permet une réécriture complète du code. Ici les opérations sont réalisées successivement sur le DataFrame qui est implicite

```julia
@chain iris begin
  groupby(:Species),
  combine(Not(:Species) .=> mean)
end
```

## Travailler avec des graphes

@todo

https://github.com/datacraft-paris/2211-Cuvelier-Julia/blob/main/3-graphes.ipynb

## Notebook IJulia

https://github.com/JuliaLang/IJulia.jl

> **IJulia** is a [Julia-language](http://julialang.org/) backend combined with the [Jupyter](http://jupyter.org/) interactive environment (also used by [IPython](http://ipython.org/)).  This combination allows you to interact with the Julia language using Jupyter/IPython's powerful [graphical notebook](http://ipython.org/notebook.html), which combines code, formatted text, math, and multimedia in a single document. IJulia is a Jupyter language kernel and works with a variety of notebook user interfaces. In addition to the classic Jupyter Notebook, IJulia also works with [JupyterLab](https://jupyterlab.readthedocs.io/en/stable/), a Jupyter-based integrated development environment for notebooks and code. The [nteract notebook desktop](https://nteract.io/) supports IJulia with detailed instructions for its [installation with nteract](https://nteract.io/kernels/julia).

```julia
add IJulia
```

```julia
using IJulia
notebook()
```

Si Jupyter n’est pas installé, l’installer.

## Utilisation du gestionnaire de paquets

Julia dispose d’un très gestionnaire de paquets efficace, [Pkg](https://pkgdocs.julialang.org/). Dans Julia, on accède au gestionnaire de paquets en tappant `]`. Tapper `backspace` ou  `Ctrl+C` pour revenir au REPL de Julia.

Ajouter un paquet (dans Pkg)

```
add nom_du_paquet
```

Supprimer un paquet et ses annotations

```
rm --manifest nom_du_paquet
```

La commande `status` ou `st` permet de voir les paquets installés.

Pkg est conçu autour de la notion d’environnement. Il s’agit d’ensemble de paquets qui peuvent être propres à un projet ou partagés et sélectionnés par leur nom. Ces environnements sont décrits dans un fichier de *manifest* qui peut être versionné pour facilité la reproductibilité des projets. Cette solution permet de travailler avec des versions différentes de paquets installés à des endroits distincts en fonction de vos besoins ; une fonctionnalité est comparable à `virtualenv` en Python.

Pour activer un environnement (dans Pkg)

```
activate nom_du_projet
```

Lorsqu’on utilise un projet existant, la commande `instantiate` télécharge les dépendances manquantes ou vérifie que l’environnement est prêt à être utilisé (dans Pkg)

```
instantiate
```

Au lieu d’utiliser la commande `activate` depuis Julia, il est également possible de spécifier lors du démarage l’environnement à utiliser

```julia
julia --project=somepath myscript.jl
```

Les fichiers `Project.toml` contiennent les informations générales sur le projet (nom, id, auteurs) et les dépendances directes, tandis que `Manifest.toml` contient la date exacte des versions des dépendances directes et indirectes.

Pour générer les fichiers d’un paquet (dans Pkg)

```
generate my_project
```

Un sous répertoire `src` est destiné à accueillir le code

### Configuration par défaut de l’environnement de travail

Pour répliquer le comportement par défaut proposé dans Visual Studio code.

https://log-dh.vercel.app/notes/2024-02-16_julia-gestion-des-environnements/

### Ressources pédagogiques sur les environnements

- Documentation de PKG https://pkgdocs.julialang.org/v1/
- « Modern Julia Workflows ». 2023. Consulté le septembre 10. https://modernjuliaworkflows.github.io/.

## Sources

- Lauwens, Ben, et Allen Downey. s. d. *Think Julia. How to Think Like a Computer Scientist*. Consulté le 14 décembre 2019. https://benlauwens.github.io/ThinkJulia.jl/latest/book.html.

Tutoriel de Cuvelier

- https://github.com/datacraft-paris/2211-Cuvelier-Julia/blob/main/1-bases.ipynb
- https://github.com/datacraft-paris/2211-Cuvelier-Julia/blob/main/2-dataframes.ipynb
- https://github.com/datacraft-paris/2211-Cuvelier-Julia/blob/main/3-graphes.ipynb
