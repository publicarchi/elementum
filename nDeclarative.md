# Programmation déclarative

La programmation déclarative est un paradigme de programmation dans lequel on exprime la logique de la computation sans décrire les structures de contrôle. Les composants logiciels sont indépendants du contexte et n’utilisent pas d’état interne ainsi l’appel d’un de ses composanst avec les mêmes arguments produit exactement le même résultat.

Dans ce type de programmation on décrit plutôt le problème, le *quoi* tandis que dans une programmation impérative on décrit le *comment*, c’est-à-dire la structure de contrôle qui correspond à la solution.

Il s’agit d’une forme de programmation dite sans effet de bord qui présente une correspodance avec la logique mathématique. Plusieurs formes de programmation sont dites déclaratives

- la programmation descriptive (description de structures de données : HTML, XML)
- la programmation fonctionnelle qui envisage les applications comme un ensemble de fonctions mathématiques (Lisp, Caml, Haskell, etc.)
- la programmation logique pour laquelle les composants d’une application sont des relations logiques (Prolog, Mercury)
- la programmation par contraintes

Langage de haut niveau qui décrit ce que la computation doit effectuée

Langage de programmation sans effet de bord (ou plus spécifiquement référentiellement transparent)

## Programmation logique

Prolog

Programmation par contraintes paradigme de programmation apparu dans les années 1970 et 1980 permettant de résoudre des problèmes cobinatoires de grande taille plannification, ordonnancement.

Sépare la modélisation de la résolution. Utilisation des contraintes pour réduire l’espace des solutions à parcourir (propagation des contraintes).

>En informatique, de toutes les approches en programmation, la  programmation par contraintes se rapproche le plus de l'idéal :  l'utilisateur décrit le problème, l'ordinateur le résout.
>
>E. Freuder

Variante de la programmation dûe à Jaffar et Lassez qui étendirent en 1987 une classe spécifique de contraintes qu’ils introduirent dans Prolog II.

Mackworth, Consistency in networks of relations, *Artificial Intelligence*, 9:99-118, 1977

Haralick, Eliott, Increasing Tree search efficiency for Constraint Satisfaction Problems, *Artificial Intelligence*, 14:263-313, 1980.

Jean-Louis Laurière, Un langage et un programme pour énoncer et résoudre des problèmes combinatoires, Paris, Thèse d'Etat, Université Pierre et Marie Curie, 1976, 227 p. ([SUDOC](https://fr.wikipedia.org/wiki/Système_universitaire_de_documentation) [029557313](https://www.sudoc.fr/029557313))

Jaffar, Joxan, and J-L. Lassez. "[Constraint logic programming](https://dl.acm.org/citation.cfm?id=41635)." Proceedings of the 14th ACM SIGACT-SIGPLAN symposium on Principles of programming languages. ACM, 1987.

(en) Jean-Louis Laurière, « A language and a program for stating and solving combinatorial problems », *Artificial Intelligence*, vol. 10, no 1,‎ février 1978, p. 29-127 ([lire en ligne](http://www.sciencedirect.com/science/article/pii/0004370278900292) [[archive](http://archive.wikiwix.com/cache/?url=http%3A%2F%2Fwww.sciencedirect.com%2Fscience%2Farticle%2Fpii%2F0004370278900292)], consulté le 7 janvier 2018)

## Programmation fonctionnelle

> The 1977 ACM Turing Award was given to John Backus for his work in the development of Fortran. Each recipient of this award presents a lecture when the award is formally given, and the lecture is subsequently published in the *Communications of the ACM*. In his Turing Award lecture, Backus (1978) made a case that purely functional programming languages are better than imperative languages because they result in programs that are more readable, more reliable, and more likely to be correct.
>
> (Sebesta 2019, p. 1079)

États

## Langages de domaines

yacc parser generator input langage, QML, Make build, Puppet, regular expression, sous-ensemble de SQL

Nombreux langages de balisages ou d’interface sont souvent déclaratifs : HTML, MXML, XAML, XSLT.

Representational state transfer (REST)

XSLT

> declarative (functional) tree transformation language with referential transparency and implicit dispatch

## Déclarative langage

NicoVerwer https://youtu.be/hlFoT26nWhA

## Sources

- https://fr.wikipedia.org/wiki/Structure_de_contr%C3%B4le
- https://fr.wikipedia.org/wiki/Programmation_d%C3%A9clarative
- Peter Van Roy, Seif Haridi. *Concepts, Techniques, and Models of Computer Programming*. MIT Press, 2004.

