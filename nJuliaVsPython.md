---
author: emchateau
tags: Python, Julia
---

# Julia vs Python

### Comparaison avec Python

- facile à apprendre depuis Python
- les librairies Python sont toutes utilisables vi PyCall.jl ou PythonCall.jl
- vitesse d’exécution comparable à celle de C
- parallélisation fait partie du langage

## Syntaxe élémentaire

Il n’y a pas d’indentation en Julia. Pour définir un bloc d’instruction, on commence par un mot-clef et ce bloc se termine par un `end`

```julia
if a >= b
end
```

En Python

```python
if a >= b:
    pass
```

Pour concaténer une chaîne de caractère on utilise `*`. Le symbole puissance `^` permet de répéter un caractère. En Julia on peut représenter un caractère explicitement avec des apostrophes simples `''` et des chaînes de caractères avec `""`

```julia
'a'^5 * "bc"
```

En Python

```python
'a'*5 + 'bc'
```

C’est souvent l’utilisation des types qui permet à Julia une exécution très rapide. Il est possible de créer une liste non typée ou des listes typées. Pour ajouter un type à tous les éléments de la liste, on le précise avant la liste.

```julia
slow = []
fast = Int[]
```

En Python, il faudrait utilser par exemple numpy

```python
slow = []
fast = np.zeros(shape=(3,2),
               dtype=np.intc)
```

Dans la syntaxe de Julia le premier élément est `1` et non pas `0`. Le dernier élément n’est pas `-1`, on peut y accéder avec le mot-clef `end`. La dernière valeur est incluse dans la plage.

```julia
list[1] == first(list)
list[end] == last(list)
list[begin+1:end-1]
```

En Python

```python
list[0]
list[-1]
list[1:-1]
```

Julia ne dispose pas de classe à proprement parler tandis que Python est un langage orienté objet plus classique. Pour créer une structure de données en Julia `struct`. Pour créer une structure mutable, on précède par le mot-clef `mutable`. Cette distinction est permise pour permettre l’accélération du code.

```julia
struct X
	field
end
mutable struct X
	field::Float64
end
```

En Python

```python
class X: pass
X = namedtyple('X', ['field'])
# Immutable
@dataclass
class X:
  field: float
```

Julia propose une compilation à la volée JIT. Tout le code est compilé avant d’être exécuté lors du chargement des modules. Le code plus simple sera souvent plus lent qu’en python, mais ce n’est pas ce qui est le plus important.

Multiméthode, le code à exécuter pour une fonction dépend des types de **tous** les arguments.

- fonction : un nom (`+`, `read`), souvent partagé entre des paquets (`filter!`)
- méthode : une implémentation d’une fonction selon les types `+(::Int, ::Int)`
- polymorphisme à la C++, en Python seul le type de l’objet est considéré

Contrairement à Julia, de nombreuses fonctions destinées au calcul scientifiques font partie du cœur du langage.

Avec Julia, la création de matrices est très directe et le code est plus concis :

```julia
A = [1 2; 3 4]
A = zeros(2, 2)
A = ones(2, 2)
A = I # will adopt 2x2 dims if demanded by neighboring matrices
```

En Python

```python
A = np.array([[1, 2], [3, 4]])
A = np.zeros((2, 2))
A = np.ones((2, 2))
A = np.eye(2)
```



## Voir aussi

[Utiliser des librairies Python dans Julia](./nJuliaPython.md)

## Références

- [MATLAB--Python--Julia cheatsheet](https://cheatsheets.quantecon.org)

