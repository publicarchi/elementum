---
author: emchateau
tags: julia
---

# Julia divers

## Préambule

- [Julia](https://julialang.org) est un langage de programmation scientifique rapide conçu est développé par le MIT. Il gagne de plus en plus en popularité et se classe 24^e^ parmi les langages de programmation au [PYPL rating](https://pypl.github.io/PYPL.html) (en septembre 2024).

> **We are greedy: we want more.** We want a language that’s **open source**, with a liberal license. We want the **speed** of C with the **dynamism** of Ruby. We want a language that’s **homoiconic**, with **true macros** like Lisp, but with obvious, **familiar mathematical notation** like Matlab. We want something as usable for **general programming** as Python, as easy for **statistics** as R, as **natural for string processing** as Perl, as powerful for **linear algebra** as Matlab, as good at **gluing programs together** as the shell. Something that is **dirt simple to learn**, yet keeps the most serious hackers happy. We want it **interactive** and we want it **compiled**.
>
> (Bezanson, Karpinski, et Viral B. Shah Alan 2012)

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

Outre ces qualités, la consistance et la clareté de sa syntaxe en font un très bon candidat pour l’apprentissage de la programmation.

### Caractéristiques de Julia

- langage dynamiquement typé, mais avec des types optionnels
- built-in types équivalent à des types définis par les utilisateurs
- compilation JIT
- utilisation de multiple dynamic dispatch
- capacités de métaprogramming
- appel natif de librairies en C et Fortan

### Historique du langage

[Julia](https://julialang.org) est un nouveau langage de programmation développé par le MIT dont la version 1.0 a été seulement été publiée en août 2018. Le projet a été débuté à la fin de 2009 par Jeff Bezanson, Alan Edelman, Stefan Karpinski, et Viral Shah. Il a été rendu public à travers un billet de blog publié le 14 février 2012 intitulé : « Why We Created Julia ».

- 0.0 – 2009
- 0.1 – Feb 14, 2012
- 1.0 – Aug 8, 2018 (LTS)
- 1.6 – Mar 24, 2021 (LTS)
- [version en cours](https://julialang.org/downloads/)

Bezanson, Jeff, Stefan Karpinski, et Edelman Viral B. Shah Alan. 2012. « Why We Created Julia ». férvier 2012. https://julialang.org/blog/2012/02/why-we-created-julia/.

### Comparaison avec Python

- facile à apprendre depuis Python
- les librairies Python sont toutes utilisables vi [PyCall.jl](https://github.com/JuliaPy/PyCall.jl) ou [PythonCall.jl](https://github.com/JuliaPy/PythonCall.jl)
- vitesse d’exécution comparable à celle de C
- la parallélisation fait partie du langage

cf. https://youtu.be/qhrY0c_BHs8?si=fyPDO-f0U-PXVoJs

## Installation

Télécharger Julia depuis la page dédiée et suivre les instructions https://julialang.org/downloads/

Plusieurs IDE sont disponibles, le plus courramment utilisé consiste en l’utilisation de [l’extension Julia](https://marketplace.visualstudio.com/items?itemName=julialang.language-julia) de Visual Studio Code.

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

ou `<Ctl-D>`

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

Consulter l’aide d’une fonction

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

[Documentation officielle](https://docs.julialang.org/en/v1.11/manual/strings/) sur les chaînes de caractères.

## Structure de données élémentaires

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

En utilisant un générateur

```julia
f(x) = x^2
Dict(i => f(i) for i = 1:10)
```

Étendre le dictionnaire

```julia
merge!(d, Dict(3 => 42.0))
```

### Style et conventions

Outre certaines restrictions sur les nom de variable, plusieurs conventions sont d’usage :

- Les noms des variables sont en minuscule.
- Les mots sont séparés par des tirets bas ('_') dans les noms de variable, mais on évite d’y avoir recours.
- Les noms de Type ou de Modules commencent par une lettre majuscule, les majuscules séparant les différents mots du nom de la variable (exemple : "MonModule")
- Les noms des fonctions et macros sont en minuscule sans tirets bas.
- Le nom des fonctions qui modifient en sortie leurs arguments d’entrée s’écrivent avec le suffixe `!`.

[Documentation officielle](https://docs.julialang.org/en/v1/manual/style-guide/) sur les guides de style.

## Tableaux et matrices

Qu’il s’agissent de vecteurs, de matrices ou d’hypermatrices, les tableaux occupent une place essentielle dans Julia.

Il n’y a qu’un seul type de tableau : **Array** dont on peut définir le nombre d’entrées. Un tableau peut contenir des matrices.

En Julia les indices commencent à 1, et l’accès aux éléments se fait en utilisant des crochets droits `[` et `]`, les parenthèses étant réservées pour les fonction.

### Itérateur

Il existe un type range

```julia
a = 1:5
a .+ 1
typeof(a)
collect(a)
```

@todo

[Documentation officielle](https://docs.julialang.org/en/v1.11/base/collections/) sur les collections et les structures de données.

## Itérations et expressions conditionnelles

### Boucles

Techniquement, des constructions telles que les boucles font partie du flux de contrôle dans les langages de programmation impératifs. Ce sont des langages qui exécutent une séquence de commandes dans un ordre défini par le flux de contrôle. Pensez-y comme à des langages où vous dites à l’ordinateur quoi faire en détail. L’alternative principale est un langage déclaratif, où vous demandez à l’ordinateur d’obtenir un résultat sans vous soucier de la manière dont il y parvient (pensez à Excel). Les langages impératifs correspondent plus naturellement au fonctionnement du matériel informatique et à notre manière de penser (ou du moins la mienne), ce qui les rend plus courants. Cependant, les langages déclaratifs peuvent être fantastiques, et en réalité, la division entre ces deux types de langages n’est souvent pas nette. Les langages déclaratifs incluent souvent aussi des constructions de contrôle de flux, et les langages impératifs modernes intègrent souvent des composants déclaratifs.

Il existe plusieurs stratégies pour créer des boucles avec Julia. La plus simple d’entre-elles est probablement d’utiliser la boucle `while`

```julia
while CONDITION
  # faire quelque chose
end
```

Cette expression fait quelque chose jusqu‘à ce que la condition devienne fausse. Une telle construction suppose implicitement que quelque chose changera et que chaque cycle d’exécution soit légèrement différent, ce qui permettra à la condition de passer de vrai à faux.

Par exemple, cette boucle compte de 1 à 10 puis s’arrête.

```julia
compteur = 1
while compteur <= 10
  @show compteur
  compteur += 1
end
```

Comme l’utilisation d’un compteur est classique dans les boucles, il existe un raccourci pour le faire.

```julia
for compteur = 1:10
  @show compteur
end
```

Cette boucle fait exactement la même chose que la boucle `while` précédente mais est plus succinte. Les boucles `for` sont très usuelles dans les langages de programmation de haut-niveau.

### Expressions conditionnelles

Les conditions s’écrivent avec les mots-clefs `if`, `elseif` et `else` :

```julia
if x >= 0
    …
elseif x <= 1
    …
else
    …
end
```

Comme langage orienté mathématiques, Julia permet d’utiliser des comparaisons multiples : pour vérifier que x est dans l’intervalle [0, 1], on peut utiliser la condition `0 <= x <= 1`.

## Déclaration de fonction

Définition en ligne

```julia
f(x) = x+1
f(2)
```

Les fonctions se déclarent avec le mot-clef `function` suivi du nom de la fonction avec ses parenthèses.

```julia
function zéro()
  return 0
end

function somme(a, b)
    return a + b
end
```

La notation `::` indique le type d’un argument :

```julia
function sum(a::Int, b::Int)
    return a + b
end
```

Les structures de données immuables sont déclarées avec le mot-clef struct :

```julia
struct Point
    x::Float64
    y::Float64
end
```

Instancier une structure de données se fait comme un appel de fonction :

```julia
p = Point(0.0, 1.0)
```

Les instances de ces objets ne peuvent pas être modifiées : pour p, on ne peut que lire les valeurs des champs x et y, pas les écrire.

```julia
println(p.x) # Affiche "0.0"
p.x = 1.0 # Erreur : "ERROR: setfield! immutable struct of type Point cannot be changed"
```

Julia oriente les utilisateurs vers un style de programmation plutôt fonctionnel. Lorsque les valeurs des structures de données ne peuvent pas changer, les sources de problème dans le code sont fortement réduites.

Néanmoins, il est possible d’outrepasser cette limitation en déclarant la structure de données comme `mutable struct` :

```julia
mutable struct Point
    x::Float64
    y::Float64
end

p = Point(0.0, 1.0)
println(p.x) # Affiche "0.0"
p.x = 1.0 # Il n’y a plus d’erreur
println(p.x) # Affiche "1.0"
```

Fonction anonyme

```julia
x->x^2
```

## Exécution du code

L’environnement de Julia est relativement flexible. Un script qui prend habituellement l’extension `.jl` peut s’exécuter dans le REPL avec `include()`. Mais il est également possible de travailler dans l’IDE.

```julia
include("script.jl")
```

En ligne de commande

```bash
$ julia script.jl
```

## Méthodes, etc.

### Retrouver tous les attributs d’un type

Supposons que l’on a un type `T`. Pour voir toutes les méthodes qui acceptent un objet de type `T` comme argument :

```julia
methodswith(T)
```

To see all **fields** (i.e.: type's "properties"):

```julia
fieldnames(T)
```

If you want to combine all info into a function, you can do one yourself, like this:

```julia
function allinfo(type)
   display(fieldnames(type))
   methodswith(type)
end
```

### Retrouver tous les attributs d’un objet

Pour connaître tous les attributs d’un objet

```julia
# See all methods
methodswith(typeof(a))

# See all fields
methodswith(typeof(a))

# Function combining both
function allinfo(a)
   type = typeof(a)
   display(fieldnames(type))
   methodswith(type)
end
```

### Retrouver tous les attributs quelque soit leur nature

Using multiple dispatch, you can define a function with three methods that gets you all info regardless of what you pass as argument.

The third case is needed in case you want to inspect methods that accept Type objects as arguments.

```julia
# Gets all info when argument is a Type
function allinfo(type::Type)
   display(fieldnames(type))
   methodswith(type)
end

# Gets all info when the argument is an object
function allinfo(a)
   type = typeof(a)
   display(fieldnames(type))
   methodswith(type)
end

# Gets all info when the argument is a parametric type of Type
function allinfo(a::Type{T}) where T <: Type
   methodswith(a)
end
```

## Julia REPL

Le REPL de Julia présente 4 modes : Julia, Package `]`, Aide `?` et Shell `;`. Les modes gestionnaire de paquets, aide et shell, sont accessibles avec les touches `]`, `?` et `;`. On revient simplement au mode normal avec la touche `backspace`.

## Utilisation du gestionnaire de paquets

Julia dispose d’un gestionnaire de paquets très efficace, [Pkg](https://pkgdocs.julialang.org/). Dans Julia, on accède au gestionnaire de paquets en tappant `]`. Tapper `backspace` ou  `Ctrl+C` pour revenir au REPL de Julia.

Ajouter un paquet (dans Pkg)

```
add nom_du_paquet
```

Supprimer un paquet et ses annotations

```
rm --manifest nom_du_paquet
```

La commande `status` ou `st` permet de voir les paquets installés.

Les commandes `add`, `up`, `remove` ou `rm` permettent de gérer les packets.

### Les environnements

Pkg est conçu autour de la notion d’environnement. Il s’agit d’ensemble de paquets qui peuvent être propres à un projet ou partagés et sélectionnés par leur nom. Ces environnements sont décrits dans un fichier de *manifest* qui peut être versionné pour faciliter la reproductibilité des projets. Cette solution permet de travailler avec des versions différentes de paquets installés à des endroits distincts en fonction de vos besoins ; une fonctionnalité est comparable à `virtualenv` en Python (moins les problèmes récurrents).

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

## Serveurs de langues Julia

cf. https://discourse.julialang.org/t/neovim-languageserver-jl/37286/7

https://github.com/fredrikekre/.dotfiles/blob/master/.julia/environments/nvim-lspconfig/Makefile

[LanguageServer.jl](https://github.com/julia-vscode/LanguageServer.jl) est une implémentation du Microsoft Language Server Protocole pour Julia.

[Helix](https://github.com/julia-vscode/LanguageServer.jl/wiki/Helix) dispose déjà d’un fichier de config pour Julia dans `languages.toml`.

Après avoir installé LanguageServer.jl

Ajouter le bloc de code suivant dans `.config/helix/languages.toml`

```
[[language]]
name = "julia"
scope = "source.julia"
injection-regex = "julia"
file-types = ["jl"]
roots = ["Project.toml", "Manifest.toml"]
comment-token = "#"
language-server = { command = "julia", args = [
    "--startup-file=no",
    "--history-file=no",
    "--quiet",
    "--project",
    "-e",
    "using LanguageServer; runserver()",
    ] }
indent = { tab-width = 4, unit = "    " }
```



## Sources

- Bezanson, Jeff, Stefan Karpinski, et Edelman Viral B. Shah Alan. 2012. « Why We Created Julia ». férvier 2012. https://julialang.org/blog/2012/02/why-we-created-julia/.
- Lauwens, Ben, et Allen Downey. s. d. *Think Julia. How to Think Like a Computer Scientist*. Consulté le 14 décembre 2019. https://benlauwens.github.io/ThinkJulia.jl/latest/book.html.

Tutoriel de Cuvelier

- https://github.com/datacraft-paris/2211-Cuvelier-Julia/blob/main/1-bases.ipynb
- https://github.com/datacraft-paris/2211-Cuvelier-Julia/blob/main/2-dataframes.ipynb
- https://github.com/datacraft-paris/2211-Cuvelier-Julia/blob/main/3-graphes.ipynb
