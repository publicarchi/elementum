---
author: emchateau
tags: networks
---

# Analyse de Réseau

L’analyse de réseau est mobilisée depuis les années soixante dans diverses disciplines tant dans le domaine des sciences humaines et sociales, que dans celui des sciences formelles ou de la nature. L’analyse de réseau désigne un ensemble de méthodes, de notions et de concepts fondés sur la théorie des graphes destinés à étudier de manière quantitative un phénomène relationnel.

## Historique

- Développement dès les années 30, sociométrie Moreno et Jennings
- Social network analysis en Angletter puis aux États-Unis dans les années 50-60
- Écologie et physique dans les années 90
- peu d’investissement en histoire

En sciences humaines et sociales, on désigne habituellement par analyse de réseau une démarche quatitative qui vise à étudier les propriétés relationnelles d’un ensemble d’individus (Beauguitte 2023). Attention, il ne suffit pas de s’intéresser à un réseau comme un réseau social numérique, un réseau d’infrastructure, pour pratiquer une analyse de réseau. À l’inverse, certains phénomènes ou objets culturels tels que la participation à des événements des comportantemnts, des textes peuvent être étudiés en mobilisant une analyse de réseau.

Dans le monde anglophone, les sociologues qui pratiquent l’analyse de réseau parlent de *Social Network Analysis SNA*, on parle également d’analyse structurelle *structural analysis*. 

## Modélisation en graphe

L’analyse de réseau repose sur une modélisation, c’est à dire un processus au cours duquel on transforme certains aspects du monde social en données destinées à être analysées. On peut avoir recours à des modélisations graphiques ou statistiques pour décrire ou expliquer les aspects du monde social à l’aide de schémas ou de calculs. 

Si l’analyse de réseau peut mobiliser des méthodes statistiques, elle repose sur l’utilisation d’un type de modélisation en graphe issue de la théorie des graphes qui ne réclame pas nécessairement de représentation graphique.

### Un modèle issu de la théorie des graphes

En sciences de l’informatique, un graphe est une structure de données abstraite destinée à implémenter les concepts de graphes orientés ou non orientés issue des mathématiques et de la théorie des graphes. 

Une structure en graphe consiste en un ensemble fini et non vide de sommets *vertices* (aussi appelés *nodes* ou points) et d’un ensemble de paires non orientées entre ces sommets dans un graphe non-orienté, ou orienté dans un graphe orienté. Ces paires appelés aussi *edges* (ou liens ou encore lignes) ou *arrows* dans un graphe orienté. Ces relations pouvant être étiquetées.

`G = {V, E}` où `G`désigne le graphe, `V` désigne l’ensemble des sommets (*vertex*, *vertices*), et `E` l’ensemble des liens (*edges*).

### Les réseaux dans le domaine des sciences humaines et sociales

Pour pouvoir utiliser l’analyse de réseau en sciences humaines et sociales, il est nécessaire de définir un type de relations existant entre les éléments étudiés. Un même corpus pouvant d’ailleurs se prêter à différentes modélsisations en fonction des thématiques que l’on souhaite traiter.

Par exemple :

<!-- revoir avec un ex en HA -->

- on a affaire à des auteurs et on créée des liens entre deux auteurs quand ils ont publié ensemble
- si on travaille avec des mots-clefs on créer des liens lors des articles partage des articles
- cosignature d’article
- liens entre population et revue
- ...

Comme toujours, les choix opérés lors de la construction des données dépendent des questions de recherche que l’on souhaite explorer. 

Dans le domaine des sciences humaines et sociales : 

> Un réseau est constitué d’un ensemble fini et non vide de points, symbolisant des acteurs (individus, groupes, institutions, textes, etc.) et d’un ensemble fini et éventuellement vide de lignes symbolisant les relations entre ces acteurs. Le nombre de sommets est appelé ordre du graphe ; le nombre de liens taille du graphe. Dans la pratique, on parle cependant de grands graphes quand le nombre de sommets et/ou de liens est élevé.
>
> (Beauguitte 2016)

### La distinction réseau non orientés et réseaux orientés

> Une première opposition distingue les réseaux non orientés, dans lesquels toute relation d’un sommet *i* vers un sommet *j* implique une relation de *j* vers *i* et les réseaux orientés où le sens de la relation importe et où l’existence d’une relation de *i* vers *j* n’implique pas nécessairement de relation de *j* vers *i*.

 NB: Certains réseaux peuvent être mixtes comme les généalogies (qui associent des liens non orientés : être le ou la conjoint·e de ; et des liens orientés : être l’ascendant·e de.

## Exercice de modélisation

Plusieurs formats de représentation sont possibles

- format de liste
- format de matrice
- représentation graphique

Dans l’exemple d’une modélisation où l’on travaille sur des auteurs quand ils ou elles publient ensemble :

- on peut définir une **liste de liens** suivants : CB-MM, CB-GV et MM-GV.
- cette liste de liens peut être transformée en un tableau carré rempli de 1 et de 0 en fonction de l’existence de lien entre les individus, c’est-à-dire sous la forme de ce que l’on appelle une **matrice d’adjacence**

```txt
   | CB | MM | GV |
CB |  0 |  1 |  1 |
MM |  1 |  0 |  1 |
GV |  1 |  1 |  0 |
```

Ce type de tableau permet de mener à bien une analyse de réseau mais également d’autres méthodes statistiques. Il est d’ailleurs possible de combiner les méthodes d’analyse en réalisant une étude factorielle des correspondances.

## Description structurale

### À quoi peut répondre une analyse de réseau ?

Selon les données et la nature du phénomène étudié, l’analyse de réseau peut permettre de répondre à différent types de questions, telles que :

- comment qualifier le réseau ? 
- certains individus occupent-ils une place particulière dans le réseau ? 
- certaines relations sont-elles spécifiques ? 
- les individus partageant certaines caractéristiques sont-ils plus susceptibles d’être en relation les uns avec les autres ? 
- peut-on créer des sous-ensembles pertinents au sein du réseau ? 
- quels sont les mécanismes susceptibles d'expliquer la structure du réseau étudié ?
- l’ajout ou la suppression de certains liens ou de certains sommets est-elle susceptible de modifier la structure du réseau ?

(Ces questions sont tirées de Beauguitte 2023, p. 10)

La question de la centralité présente une importance particulière pour hiérarchiser les individus. Pour répondre à ces diverses questions, différents indicateurs ont été construits pour pouvoir apréhender la centralité ou évaluer la robustesse d’un réseau dans son ensemble, ou encore distinguer des éléments fortement inter-connectés entre eux.

### Vocabulaire de base

> Un graphe est un objet mathématique formé d’un ensemble ni et non vide de points et d’un ensemble ni et éventuellement vide de liens entre ces points (G = {V, E} 2). Le nombre de sommets est appelé l’ordre (*order*) du graphe ; le nombre de liens la taille (*size*) du graphe. Les sommets (*vertex*, pluriel *vertices*) sont également appelés nœuds, points ou acteurs (*node*, *point*, *actor*). Les liens (*edges*) sont aussi appelés relations, arcs ou arêtes (*relation*, *arc*, *edge*). (Beauguitte 2023, p. 21)

En science sociale, l’analyse de réseau réclame des éléments complémentaires : les sommets sont systématiquement pourvus d’attributs (*a minima* un nom), et les liens peuvent être pourvus d’attributs. On parlera alors de **réseau** plutôt que de graphe.

### Chemins et chaînes

Une suite de liens qui permettent de rejoindre deux sommets est appelée **chemin** (*path*) ou **chaîne** selon qu’on prend en compte l’orientation des liens. La **longeur d’un chemin** entre deux sommets correspond au nombre de liens sur ce chemin. Lorsqu’il s’agit du **plus court chemin** (*shortest path*) on parle de **distance géodésique** (*geodesic distance*). Un chemin qui comprend au moins trois liens et dont le sommet de départ et le sommet d’arrivé sont identiques est appelé **cycle**.

L’ensemble des sommets liés par au moins un chemin s’appele une **composante** ou **composante connexe** (*component*). Si tous les sommets d’un graphe appartiennent à une même composante, on parle de graphe connexe (*connected graph*).

<!-- développer -->

Certains sommets jouent un rôle particulier dans la connexité du réseau si leur suppression augmente le nombre de composantes. On parle de point d’articulation (*articulartion point*, *cutpoint*, *cut-vertex*) ou d’isthme (*bridge*)

Réseaux simples, complexes.

> Quel que soit l’aspect du monde social, passé ou présent, que vous étudiez, il est rare qu'un seul type de relations existe entre vos individus : choisir de modéliser ces relations par un réseau simple est une simpli cation, souvent nécessaire et utile, de la réalité et il est prudent dans s’en rappeler lorsqu'on commente ses résultats. (Beauguitte 2023, 25)

Objet construit, opérations de transformation pour les étudier. Exemple graphe bipartis.

Construit. Pb des absences et de la stabilité.



Opérations :

Plusieurs opération s

The basic operations provided by a graph data structure *G* usually include:

- `adjacent`(*G*, *x*, *y*): tests whether there is an edge from the vertex *x* to the vertex *y*;
- `neighbors`(*G*, *x*): lists all vertices *y* such that there is an edge from the vertex *x* to the vertex *y*;
- `add_vertex`(*G*, *x*): adds the vertex *x*, if it is not there;
- `remove_vertex`(*G*, *x*): removes the vertex *x*, if it is there;
- `add_edge`(*G*, *x*, *y*): adds the edge from the vertex *x* to the vertex *y*, if it is not there;
- `remove_edge`(*G*, *x*, *y*): removes the edge from the vertex *x* to the vertex *y*, if it is there;
- `get_vertex_value`(*G*, *x*): returns the value associated with the vertex *x*;
- `set_vertex_value`(*G*, *x*, *v*): sets the value associated with the vertex *x* to *v*.

Structures that associate values to the edges usually also provide:

- `get_edge_value`(*G*, *x*, *y*): returns the value associated with the edge (*x*, *y*);
- `set_edge_value`(*G*, *x*, *y*, *v*): sets the value associated with the edge (*x*, *y*) to *v*.

https://en.wikipedia.org/wiki/Graph_(abstract_data_type)

## Méthodes

Louvain algorithm hardly detects statistically 120 significant communities (modularity with resolution 1: 0.26) 121 (S.I.2). 

The relatively high edgewise reciprocity (18%, com- 122 pared to 3.5% in average for simulated networks with the same 123 density and number of edges – S.I.3)

Exponential-Random Graph (ERGM) models show that, for 138

## Ressources

### Bibliographie

- Beauguitte, Laurent. 2023. « L’analyse de réseau en sciences sociales. Petit guide pratique ». https://beauguitte.github.io/analyse-de-reseau-en-shs/.
- Beauguitte, Laurent. 2016. « L’analyse de réseaux en sciences sociales et en histoire : vocabulaire, principes et limites ». In *Le réseau. Usages d’une notion polysémique en sciences humaines et sociales*, édité par Rosemonde Letricot, Mario Cuxac, Maria Utcategui, et Andrea Cavaletto, Presses Universitaires de Louvain, 9‑24. Louvain. https://halshs.archives-ouvertes.fr/halshs-01476090
- László Barabási, Albert. s. d. *Network Science*. Consulté le 16 mai 2020. http://networksciencebook.com.
- Borgatti, Stephen P., Martin G. Everett, et Jeffrey C. Johnson. 2013. *Analyzing social networks*. Los Angeles: SAGE.

### Tutoriaux

### Webographie

- Briatte, François. (2016-). « Awesome Network Analysis ». R. https://github.com/briatte/awesome-network-analysis.
- [The Historical Network Research Community](https://historicalnetworkresearch.org)
- [GDR Analyse de réseaux en sciences humaines et sociales](https://arshs.hypotheses.org/)
- [Journal of Historical Network Research](https://jhnr.net)
- [Getty Advanced Workshop on Network Analysis and Digital Art History (NA+DAH)](https://sites.haa.pitt.edu/na-dah/)

### Chercheurs

- https://f.briatte.org
- https://www.martingrandjean.ch
