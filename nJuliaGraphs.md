---
author: emchateau
tags: julia, networks
---

# Tutoriel 2020

https://youtu.be/K3z0kUOBy2Y

https://github.com/matbesancon/lightgraphs_workshop

LightGraphs Assumptions

- Vertices are Integer
- Vertices are Contiguous
- Directed XOR Undirected
- No Multiedges
- No Self Loops (you can have, but not garantied that every algorithm behave well with sefl loops)

Pas de named table lors de la conception de la bibliothèque *LightGraphs*, aussi le support des métadonnées reste limité. Pour cela, il faut utiliser *MetaGraphs* où chaque edge ou vertex peut disposer de sa propriété.

Timothy Lin benchmarked all the network packages. Souvent le plus rapide mais pas pour toutes les tâches (en dehors du chargement des données et Connected components, mieux que Graph-tool). Besoin de plus de 8 cores pour pouvoir en profiter pleinement.

- Lin, Timothy. 2020. « Benchmark of popular graph/network packages v2 ». 10 mai 2020. https://www.timlrx.com/blog/benchmark-of-popular-graph-network-packages-v2.

Multigraph, https://github.com/AlgebraicJulia/Catlab.jl qui propose vrai multigraph.

Isolated vertexes, disconnected components possibles.





## Divers

The JuliaGraphs ecosystem: build fast - don't break things | James Fairbanks https://youtu.be/OZuQoxTPoyM

GraphIO.jl

- GML ou GraphML
- GEXF seulement en écriture



JuliaCon 2018 | Complex Network Anaylsis of Political Data | Ollin Demain Langle Chimal https://youtu.be/pTZOKB10rpY



Sur la visualisation de données

- Yuri Vishnevsky https://youtu.be/Ns09HR43zEY

Qu’ont en commun ?

Markup et interaction

hyperscript + vitalize

https://github.com/yurivish/Hyperscript.jl

https://github.com/yurivish/Vitalize.jl

http://yuri.is/

Hyperscript: A lightweight DOM representation for Julia

Multiscale https://github.com/yurivish/TuringPatterns.jl



https://github.com/queryverse/Query.jl