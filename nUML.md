---
author: emchateau
tags: uml
---

# note UML

UML (Unified Modeling Language) est un outils particulièrement utilisé pour la modélisation orientée-objet. UML découle de la vue d’analyse et de conception orientée-objet (OOA&D) de la fin des années 80. Le langage unifie les méthodes de Grady Booch, Rumbaugh (Object Management Group OMT) et Jacobson, mais les supplante en devenant un langage de modélisation et plus simplement une méthode.

UML est rapidement devenu le standard de fait pour la construction de logiciels orientés-objets. Il offre un langage commun et une notation graphique pour créer des modèles de système technique ou de business. La spécification de l’Object Management Group, indique :

> The Unified Modeling Language (UML) is a graphical language for visualizing, specifying, constructing, and documenting the artifacts of a software-intensive system. The UML offers a standard way to write a system’s blueprints, including conceptual things such as business processes and system functions as well as concrete things such as programming language statements, database schemas, and reusable software components.

## Standard

UML est un langage semi-formel créé en 1994-1996, il a depuis fait l’objet de plusieurs mises à jours

UML est utilisé pour la conception des parties de systèmes, principalement dans le domaine du génie logiciel

Il peut faire l’objet d’une représentation en XML Metadata Interchange (XMI) ou encore faire l’objet de représentation visuelle sous forme de diagrammes.

Plusieurs types de diagrammes peuvent être produits avec UML, des diagrammes de structure ou de comportements.

Les diagrammes de classe sont employés pour présenter l’information sur des classes et leurs relations. 

Les **classes** sont présentées sous forme de rectangles qui comprennent trois sections : le nom, les attributs, et les opérations ou méthodes.

Les **attributs** sont représentés par un nom, optionnellement suivi par deux points et un type.

La visibilité d’un attribut est représentés comme

- privé (-)
- public (+)
- protégé (#)
- package (~)

Les attributs sont le plus souvent privés.

Les **méthodes** sont similaires aux attributs et elles peuvent également recevoir une liste de paramètres. Elles sont le plus souvent publiques.

Les **énumérations** sont utilisées pour définir un type avec un ensemble de valeurs. Ce type peut ensuite être employé dans la définition des classes.

Ces énumérations se présentent un peu comme des classes mais contiennent des listes sans valeurs.

L’**héritage** est représenté par une flêche triangulaire et une ligne continue, la fêche pointant vers la superclasse.

Le nom des classes abstraite est italicisé.

Les **associations** modélisent des relations générales entre des classes. Elles peuvent être nommées, et reçoivent des cardinalités. L’association est représentée par une simple ligne sans flêche.

L’**agrégation** est une association de type "has" qui connecte deux classes. Elle est employée pour modéliser les relations partitives (de tout à partie). Le tout n’est pas responsable de la création et de la destruction de ses parties. Les parties peuvent être en agrégation avec autre chose que le tout. L’agrégation est représentée par un losange vide.

La **composition** est similaire à l’agrégation mais modélise une relation plus forte. Le tout gouverne la partie et est responsable de la création ou de sa destruction. Les parties peuvent être en relation de composition avec un tout. La composition est représentée par une ligne se terminant par un losange plein.

La **multiplicité** est utilisée pour décrire la quantité dans les relations associatives. Elle peut également être employée pour l’agrégation et la composition.

- Quand l’objet est requis, les cardinalices possibles sont 1 (exactement un) et 1..* (1 ou plus)
- Quand l’objet est optionnel, les multiplicités possibles sont 0..1 (zéro ou 1) et 0..* (0 ou plus).

Il existe donc les relations possibles

- relation un-à-un (one-to-one)
- relation un-à-plusieurs (one-to-many)
- relation plusieurs-à-plusieurs (many-to-many)

Les diagrammes de classe UML peuvent être employés pour représentés la hiérarchie (structure) des classes. Les classes sont utilisées pour créer des objets.

Les diagrammes de classes peuvent être employés pour représenter des types et des relations (contraintes) des objets

On emploie XML pour représenter les données et leur hiérarchie (structure). Les objets sont des données.



## Format d’échange

DI2 (Diagram Interchange) standard

<http://www.omg.org/cgi-bin/doc?formal/2006-04-04.pdf>



## Outils de modélisation

[Papyrus](http://www.eclipse.org/papyrus)

https://www.visual-paradigm.com/solution/freeumltool/

http://www.bouml.fr

https://www.modelio.org

Payants

http://staruml.io



