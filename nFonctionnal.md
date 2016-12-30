---
author: Emmanuel Château-Dutier
since: 2016-03-20
---


# Programmation fonctionnelle

XQuery et XSLT ont la qualité d’être des langages fonctionnels. Si la notion de programmation fonctionnelle a bénéficié d’un regain d’intérêt récemment on évoque plus habituellement les langages [Haskell](https://www.haskell.org/) ou [Lisp](https://en.wikipedia.org/wiki/Lisp_%28programming_language%29). On peut également programmer de manière fonctionnelle avec [Elm](http://elm-lang.org/) ou [Clojurescript](https://github.com/clojure/clojurescript) deux langages qui se compilent en JavaScript.

## Notion de fonction

Au cœur de la notion de programmation fonctionnelle réside la notion de logique descriptive issue des mathématiques formelle de lambda-calcul (ou λ-calcul). Il s’agit d’un système formel inventé par Alonzo Church dans les années 30 qui fonde les concepts de fonction et d’application et a joué un rôle important dans le développement de la théorie des langages de programmation.

L’emploi de fonctions pures et un des fondement du paradigme de programmation fonctionnelle. On dit d’une fonction pure si celle-ci répond à ces deux conditions :
- la fonction est déterministe : elle retourne toujours la même valeur pour les mêmes arguments. Le résultat de la fonction ne peut dépendre d’information cachée ou d’état qui peut changer au cours de l’exécution du programme ou entre plusieurs exécutions.
- l’évaluattion du résultat ne doit provoquer aucun effet de bord observable comme des changements d’état ou entrée-sortie.

## Transparence référentielle


## Programmation fonctionnelle versus programmation impérative

La programmation impérative s’appuie sur le modèle des machines à états, avec une mémoire centrale et des instructions qui modifient son état grâce à des affectations successives. Cela nécessite pour le programmateur d’avoir à tout instant un modèle exact de l’état de la mémoire que le programme modifie. En programmation impérative, les effets de bord sont de facto la règle et sont la source de nombreuses difficultés ou de bugs.

La programmation fonctionnelle s’affranchit de manière radicale des effets de bords en interdisant toute opération d’affectation. Chaque composant du programme peut être conçu comme une fonction qui prend plusieurs paramètre en entrée et produit une sortie qui est fonction de cette entrée. Un programme est donc une application au sens mathématique qui ne donne qu’un seul résulat pour chaque ensemble de valeurs entrée.

Un langage dit purement fonctionnel n’autorise pas la programmation impérative. Il est de ce fait dénué d’effet de bord et permet potentiellement l’exécution concurrente.


Cette manière de penser la programmation peut poser des difficultés particulières pour certaines tâches. Notamment il ne permet pas l’assignement d’une variable dans une boucle.


## Historique

Lisp un des premiers langages fonctionnels développé par John McCarty au MIT pour l’IBM 700/7000 à la fin des années 1950 (1958).

## Sources

- https://en.wikipedia.org/wiki/Lambda_calculus
- https://fr.wikipedia.org/wiki/Lambda-calcul
- https://en.wikipedia.org/wiki/Pure_function
- https://fr.wikipedia.org/wiki/Fonction_pure
- https://fr.wikipedia.org/wiki/Programmation_fonctionnelle
- https://en.wikipedia.org/wiki/Functional_programming
- Hughes, John. "Why Functional Programming Matters." In Research Topics in Functional Programming. Edited by D Turner. Addison-Wesley, 1990. Why Functional Programming Matters.
- Backus, John. "Can Programming Be Liberated From the Von Neumann Style?: A Functional Style and Its Algebra of Programs." Commun. ACM 21, no. 8 (1978): doi:10.1145/359576.359579. http://doi.acm.org/10.1145/359576.359579.
