---
tags: networks, outils
---

# Librairies d’analyse de réseau, comparaison des fonctionnalités

NetworkX

R : Statnet, Graph

igraph : développé par des informaticiens et des physiciens. Nombreuses mesures issues de la sociologie et de physique.

statnet : ensemble de package développé par des sociologues. Nombreuses mesures issues de la sociologie et de la physique et modèles statistiques (ERGM Exponentiel Random Graph Model).

bipartite : analyse de réseaux bipartis développé par des écologues

enaR : analyse de réseaux écologiques (procédures MatLab)

tnet : analyse de réseaux valués (simples et bipartis)

egonet : analyse de réseaux personnels

inter graph : transforme les objets network (statnet) en objet i graph et vice et versa.

\+ Calcul matriciel

mesures de base :

|                          | statnet       | igraph         |
| ------------------------ | ------------- | -------------- |
| densité                  | gden          | graph.density  |
| comp. connexes           | components    | clusters       |
| degré                    | degree        | degree         |
| betweenness              | betweeness    | betweenness    |
| closeness                | closeness     | closeness      |
| PCC* (plus court chemin) | geodist       | shortest.paths |
| cliques                  | clique.census | cliques        |
| k-cores                  | krores        | graph.coreness |



| features         | Networks     | Junet | graphs |
| ---------------- | ------------ | ----- | ------ |
| langage          | Python       | Julia |        |
| since            | 2002         |       |        |
| author           | Aric Hagberg |       |        |
| version          | 2.4          | alpha |        |
| date             | 2019-10      |       |        |
| **Graph types**  |              |       |        |
| undirected graph | yes          |       |        |
| directed graphs  | yes          |       |        |
| multigraph       | yes          |       |        |
| multidigraph     | yes          |       |        |

https://github.com/inguar/Junet.jl

https://github.com/JuliaGraphs

## Algorithms

List from NetworkX 2.4

### Approximations and Heuristics

- [Connectivity](https://networkx.github.io/documentation/stable/reference/algorithms/approximation.html#module-networkx.algorithms.approximation.connectivity)
- [K-components](https://networkx.github.io/documentation/stable/reference/algorithms/approximation.html#module-networkx.algorithms.approximation.kcomponents)
- [Clique](https://networkx.github.io/documentation/stable/reference/algorithms/approximation.html#module-networkx.algorithms.approximation.clique)
- [Clustering](https://networkx.github.io/documentation/stable/reference/algorithms/approximation.html#module-networkx.algorithms.approximation.clustering_coefficient)
- [Dominating Set](https://networkx.github.io/documentation/stable/reference/algorithms/approximation.html#module-networkx.algorithms.approximation.dominating_set)
- [Independent Set](https://networkx.github.io/documentation/stable/reference/algorithms/approximation.html#module-networkx.algorithms.approximation.independent_set)
- [Matching](https://networkx.github.io/documentation/stable/reference/algorithms/approximation.html#module-networkx.algorithms.approximation.matching)
- [Ramsey](https://networkx.github.io/documentation/stable/reference/algorithms/approximation.html#module-networkx.algorithms.approximation.ramsey)
- [Steiner Tree](https://networkx.github.io/documentation/stable/reference/algorithms/approximation.html#module-networkx.algorithms.approximation.steinertree)
- [Treewidth](https://networkx.github.io/documentation/stable/reference/algorithms/approximation.html#module-networkx.algorithms.approximation.treewidth)
- [Vertex Cover](https://networkx.github.io/documentation/stable/reference/algorithms/approximation.html#module-networkx.algorithms.approximation.vertex_cover)

### Assortativity

- [Assortativity](https://networkx.github.io/documentation/stable/reference/algorithms/assortativity.html#id1)
- [Average neighbor degree](https://networkx.github.io/documentation/stable/reference/algorithms/assortativity.html#average-neighbor-degree)
- [Average degree connectivity](https://networkx.github.io/documentation/stable/reference/algorithms/assortativity.html#average-degree-connectivity)
- [Mixing](https://networkx.github.io/documentation/stable/reference/algorithms/assortativity.html#mixing)

### Asteroidal

- [networkx.algorithms.asteroidal.is_at_free](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.asteroidal.is_at_free.html)
- [networkx.algorithms.asteroidal.find_asteroidal_triple](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.asteroidal.find_asteroidal_triple.html)

### Bipartite

- [Basic functions](https://networkx.github.io/documentation/stable/reference/algorithms/bipartite.html#module-networkx.algorithms.bipartite.basic)
- [Matching](https://networkx.github.io/documentation/stable/reference/algorithms/bipartite.html#module-networkx.algorithms.bipartite.matching)
- [Matrix](https://networkx.github.io/documentation/stable/reference/algorithms/bipartite.html#module-networkx.algorithms.bipartite.matrix)
- [Projections](https://networkx.github.io/documentation/stable/reference/algorithms/bipartite.html#module-networkx.algorithms.bipartite.projection)
- [Spectral](https://networkx.github.io/documentation/stable/reference/algorithms/bipartite.html#module-networkx.algorithms.bipartite.spectral)
- [Clustering](https://networkx.github.io/documentation/stable/reference/algorithms/bipartite.html#module-networkx.algorithms.bipartite.cluster)
- [Redundancy](https://networkx.github.io/documentation/stable/reference/algorithms/bipartite.html#module-networkx.algorithms.bipartite.redundancy)
- [Centrality](https://networkx.github.io/documentation/stable/reference/algorithms/bipartite.html#module-networkx.algorithms.bipartite.centrality)
- [Generators](https://networkx.github.io/documentation/stable/reference/algorithms/bipartite.html#module-networkx.algorithms.bipartite.generators)
- [Covering](https://networkx.github.io/documentation/stable/reference/algorithms/bipartite.html#module-networkx.algorithms.bipartite.covering)

### Boundary

- [networkx.algorithms.boundary.edge_boundary](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.boundary.edge_boundary.html)
- [networkx.algorithms.boundary.node_boundary](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.boundary.node_boundary.html)

### Bridges

- [networkx.algorithms.bridges.bridges](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.bridges.bridges.html)
- [networkx.algorithms.bridges.has_bridges](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.bridges.has_bridges.html)
- [networkx.algorithms.bridges.local_bridges](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.bridges.local_bridges.html)

### Centrality

- [Degree](https://networkx.github.io/documentation/stable/reference/algorithms/centrality.html#degree)
- [Eigenvector](https://networkx.github.io/documentation/stable/reference/algorithms/centrality.html#eigenvector)
- [Closeness](https://networkx.github.io/documentation/stable/reference/algorithms/centrality.html#closeness)
- [Current Flow Closeness](https://networkx.github.io/documentation/stable/reference/algorithms/centrality.html#current-flow-closeness)
- [(Shortest Path) Betweenness](https://networkx.github.io/documentation/stable/reference/algorithms/centrality.html#shortest-path-betweenness)
- [Current Flow Betweenness](https://networkx.github.io/documentation/stable/reference/algorithms/centrality.html#current-flow-betweenness)
- [Communicability Betweenness](https://networkx.github.io/documentation/stable/reference/algorithms/centrality.html#communicability-betweenness)
- [Group Centrality](https://networkx.github.io/documentation/stable/reference/algorithms/centrality.html#group-centrality)
- [Load](https://networkx.github.io/documentation/stable/reference/algorithms/centrality.html#load)
- [Subgraph](https://networkx.github.io/documentation/stable/reference/algorithms/centrality.html#subgraph)
- [Harmonic Centrality](https://networkx.github.io/documentation/stable/reference/algorithms/centrality.html#harmonic-centrality)
- [Dispersion](https://networkx.github.io/documentation/stable/reference/algorithms/centrality.html#dispersion)
- [Reaching](https://networkx.github.io/documentation/stable/reference/algorithms/centrality.html#reaching)
- [Percolation](https://networkx.github.io/documentation/stable/reference/algorithms/centrality.html#percolation)
- [Second Order Centrality](https://networkx.github.io/documentation/stable/reference/algorithms/centrality.html#second-order-centrality)
- [VoteRank](https://networkx.github.io/documentation/stable/reference/algorithms/centrality.html#voterank)

### Chains

- [networkx.algorithms.chains.chain_decomposition](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.chains.chain_decomposition.html)

### Chordal

- [networkx.algorithms.chordal.is_chordal](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.chordal.is_chordal.html)
- [networkx.algorithms.chordal.chordal_graph_cliques](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.chordal.chordal_graph_cliques.html)
- [networkx.algorithms.chordal.chordal_graph_treewidth](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.chordal.chordal_graph_treewidth.html)
- [networkx.algorithms.chordal.find_induced_nodes](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.chordal.find_induced_nodes.html)

### Clique

- [networkx.algorithms.clique.enumerate_all_cliques](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.clique.enumerate_all_cliques.html)
- [networkx.algorithms.clique.find_cliques](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.clique.find_cliques.html)
- [networkx.algorithms.clique.make_max_clique_graph](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.clique.make_max_clique_graph.html)
- [networkx.algorithms.clique.make_clique_bipartite](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.clique.make_clique_bipartite.html)
- [networkx.algorithms.clique.graph_clique_number](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.clique.graph_clique_number.html)
- [networkx.algorithms.clique.graph_number_of_cliques](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.clique.graph_number_of_cliques.html)
- [networkx.algorithms.clique.node_clique_number](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.clique.node_clique_number.html)
- [networkx.algorithms.clique.number_of_cliques](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.clique.number_of_cliques.html)
- [networkx.algorithms.clique.cliques_containing_node](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.clique.cliques_containing_node.html)

### Clustering

- [networkx.algorithms.cluster.triangles](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.cluster.triangles.html)
- [networkx.algorithms.cluster.transitivity](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.cluster.transitivity.html)
- [networkx.algorithms.cluster.clustering](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.cluster.clustering.html)
- [networkx.algorithms.cluster.average_clustering](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.cluster.average_clustering.html)
- [networkx.algorithms.cluster.square_clustering](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.cluster.square_clustering.html)
- [networkx.algorithms.cluster.generalized_degree](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.cluster.generalized_degree.html)

### Coloring

- [networkx.algorithms.coloring.greedy_color](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.coloring.greedy_color.html)
- [networkx.algorithms.coloring.equitable_color](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.coloring.equitable_color.html)
- [networkx.algorithms.coloring.strategy_connected_sequential](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.coloring.strategy_connected_sequential.html)
- [networkx.algorithms.coloring.strategy_connected_sequential_dfs](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.coloring.strategy_connected_sequential_dfs.html)
- [networkx.algorithms.coloring.strategy_connected_sequential_bfs](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.coloring.strategy_connected_sequential_bfs.html)
- [networkx.algorithms.coloring.strategy_independent_set](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.coloring.strategy_independent_set.html)
- [networkx.algorithms.coloring.strategy_largest_first](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.coloring.strategy_largest_first.html)
- [networkx.algorithms.coloring.strategy_random_sequential](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.coloring.strategy_random_sequential.html)
- [networkx.algorithms.coloring.strategy_saturation_largest_first](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.coloring.strategy_saturation_largest_first.html)
- [networkx.algorithms.coloring.strategy_smallest_last](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.coloring.strategy_smallest_last.html)

### Communicability

- [networkx.algorithms.communicability_alg.communicability](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.communicability_alg.communicability.html)
- [networkx.algorithms.communicability_alg.communicability_exp](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.communicability_alg.communicability_exp.html)

### Communities

- [Bipartitions](https://networkx.github.io/documentation/stable/reference/algorithms/community.html#module-networkx.algorithms.community.kernighan_lin)
- [K-Clique](https://networkx.github.io/documentation/stable/reference/algorithms/community.html#module-networkx.algorithms.community.kclique)
- [Modularity-based communities](https://networkx.github.io/documentation/stable/reference/algorithms/community.html#module-networkx.algorithms.community.modularity_max)
- [Label propagation](https://networkx.github.io/documentation/stable/reference/algorithms/community.html#module-networkx.algorithms.community.label_propagation)
- [Fluid Communities](https://networkx.github.io/documentation/stable/reference/algorithms/community.html#module-networkx.algorithms.community.asyn_fluid)
- [Measuring partitions](https://networkx.github.io/documentation/stable/reference/algorithms/community.html#module-networkx.algorithms.community.quality)
- [Partitions via centrality measures](https://networkx.github.io/documentation/stable/reference/algorithms/community.html#module-networkx.algorithms.community.centrality)
- [Validating partitions](https://networkx.github.io/documentation/stable/reference/algorithms/community.html#module-networkx.algorithms.community.community_utils)

### Components

- [Connectivity](https://networkx.github.io/documentation/stable/reference/algorithms/component.html#connectivity)
- [Strong connectivity](https://networkx.github.io/documentation/stable/reference/algorithms/component.html#strong-connectivity)
- [Weak connectivity](https://networkx.github.io/documentation/stable/reference/algorithms/component.html#weak-connectivity)
- [Attracting components](https://networkx.github.io/documentation/stable/reference/algorithms/component.html#attracting-components)
- [Biconnected components](https://networkx.github.io/documentation/stable/reference/algorithms/component.html#biconnected-components)
- [Semiconnectedness](https://networkx.github.io/documentation/stable/reference/algorithms/component.html#semiconnectedness)

### Connectivity

- [Edge-augmentation](https://networkx.github.io/documentation/stable/reference/algorithms/connectivity.html#module-networkx.algorithms.connectivity.edge_augmentation)
- [K-edge-components](https://networkx.github.io/documentation/stable/reference/algorithms/connectivity.html#module-networkx.algorithms.connectivity.edge_kcomponents)
- [K-node-components](https://networkx.github.io/documentation/stable/reference/algorithms/connectivity.html#module-networkx.algorithms.connectivity.kcomponents)
- [K-node-cutsets](https://networkx.github.io/documentation/stable/reference/algorithms/connectivity.html#module-networkx.algorithms.connectivity.kcutsets)
- [Flow-based disjoint paths](https://networkx.github.io/documentation/stable/reference/algorithms/connectivity.html#module-networkx.algorithms.connectivity.disjoint_paths)
- [Flow-based Connectivity](https://networkx.github.io/documentation/stable/reference/algorithms/connectivity.html#module-networkx.algorithms.connectivity.connectivity)
- [Flow-based Minimum Cuts](https://networkx.github.io/documentation/stable/reference/algorithms/connectivity.html#module-networkx.algorithms.connectivity.cuts)
- [Stoer-Wagner minimum cut](https://networkx.github.io/documentation/stable/reference/algorithms/connectivity.html#module-networkx.algorithms.connectivity.stoerwagner)
- [Utils for flow-based connectivity](https://networkx.github.io/documentation/stable/reference/algorithms/connectivity.html#module-networkx.algorithms.connectivity.utils)

### Cores

- [networkx.algorithms.core.core_number](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.core.core_number.html)
- [networkx.algorithms.core.k_core](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.core.k_core.html)
- [networkx.algorithms.core.k_shell](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.core.k_shell.html)
- [networkx.algorithms.core.k_crust](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.core.k_crust.html)
- [networkx.algorithms.core.k_corona](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.core.k_corona.html)
- [networkx.algorithms.core.k_truss](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.core.k_truss.html)
- [networkx.algorithms.core.onion_layers](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.core.onion_layers.html)

### Covering

- [networkx.algorithms.covering.min_edge_cover](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.covering.min_edge_cover.html)
- [networkx.algorithms.covering.is_edge_cover](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.covering.is_edge_cover.html)

### Cycles

- [Cycle finding algorithms](https://networkx.github.io/documentation/stable/reference/algorithms/cycles.html#cycle-finding-algorithms)
- [networkx.algorithms.cycles.cycle_basis](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.cycles.cycle_basis.html)
- [networkx.algorithms.cycles.simple_cycles](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.cycles.simple_cycles.html)
- [networkx.algorithms.cycles.find_cycle](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.cycles.find_cycle.html)
- [networkx.algorithms.cycles.minimum_cycle_basis](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.cycles.minimum_cycle_basis.html)

### Cuts

- [networkx.algorithms.cuts.boundary_expansion](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.cuts.boundary_expansion.html)
- [networkx.algorithms.cuts.conductance](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.cuts.conductance.html)
- [networkx.algorithms.cuts.cut_size](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.cuts.cut_size.html)
- [networkx.algorithms.cuts.edge_expansion](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.cuts.edge_expansion.html)
- [networkx.algorithms.cuts.mixing_expansion](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.cuts.mixing_expansion.html)
- [networkx.algorithms.cuts.node_expansion](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.cuts.node_expansion.html)
- [networkx.algorithms.cuts.normalized_cut_size](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.cuts.normalized_cut_size.html)
- [networkx.algorithms.cuts.volume](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.cuts.volume.html)

### Directed Acyclic Graphs

- [networkx.algorithms.dag.ancestors](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.dag.ancestors.html)
- [networkx.algorithms.dag.descendants](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.dag.descendants.html)
- [networkx.algorithms.dag.topological_sort](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.dag.topological_sort.html)
- [networkx.algorithms.dag.all_topological_sorts](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.dag.all_topological_sorts.html)
- [networkx.algorithms.dag.lexicographical_topological_sort](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.dag.lexicographical_topological_sort.html)
- [networkx.algorithms.dag.is_directed_acyclic_graph](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.dag.is_directed_acyclic_graph.html)
- [networkx.algorithms.dag.is_aperiodic](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.dag.is_aperiodic.html)
- [networkx.algorithms.dag.transitive_closure](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.dag.transitive_closure.html)
- [networkx.algorithms.dag.transitive_reduction](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.dag.transitive_reduction.html)
- [networkx.algorithms.dag.antichains](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.dag.antichains.html)
- [networkx.algorithms.dag.dag_longest_path](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.dag.dag_longest_path.html)
- [networkx.algorithms.dag.dag_longest_path_length](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.dag.dag_longest_path_length.html)
- [networkx.algorithms.dag.dag_to_branching](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.dag.dag_to_branching.html)

### Distance Measures

- [networkx.algorithms.distance_measures.barycenter](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.distance_measures.barycenter.html)
- [networkx.algorithms.distance_measures.center](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.distance_measures.center.html)
- [networkx.algorithms.distance_measures.diameter](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.distance_measures.diameter.html)
- [networkx.algorithms.distance_measures.eccentricity](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.distance_measures.eccentricity.html)
- [networkx.algorithms.distance_measures.extrema_bounding](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.distance_measures.extrema_bounding.html)
- [networkx.algorithms.distance_measures.periphery](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.distance_measures.periphery.html)
- [networkx.algorithms.distance_measures.radius](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.distance_measures.radius.html)
- [networkx.algorithms.distance_measures.resistance_distance](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.distance_measures.resistance_distance.html)

### Distance-Regular Graphs

- [Distance-regular graphs](https://networkx.github.io/documentation/stable/reference/algorithms/distance_regular.html#id1)
- [networkx.algorithms.distance_regular.is_distance_regular](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.distance_regular.is_distance_regular.html)
- [networkx.algorithms.distance_regular.is_strongly_regular](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.distance_regular.is_strongly_regular.html)
- [networkx.algorithms.distance_regular.intersection_array](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.distance_regular.intersection_array.html)
- [networkx.algorithms.distance_regular.global_parameters](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.distance_regular.global_parameters.html)

### Dominance

- [networkx.algorithms.dominance.immediate_dominators](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.dominance.immediate_dominators.html)
- [networkx.algorithms.dominance.dominance_frontiers](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.dominance.dominance_frontiers.html)

### Dominating Sets

- [networkx.algorithms.dominating.dominating_set](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.dominating.dominating_set.html)
- [networkx.algorithms.dominating.is_dominating_set](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.dominating.is_dominating_set.html)

### Efficiency

- [networkx.algorithms.efficiency_measures.efficiency](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.efficiency_measures.efficiency.html)
- [networkx.algorithms.efficiency_measures.local_efficiency](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.efficiency_measures.local_efficiency.html)
- [networkx.algorithms.efficiency_measures.global_efficiency](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.efficiency_measures.global_efficiency.html)

### Eulerian

- [networkx.algorithms.euler.is_eulerian](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.euler.is_eulerian.html)
- [networkx.algorithms.euler.eulerian_circuit](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.euler.eulerian_circuit.html)
- [networkx.algorithms.euler.eulerize](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.euler.eulerize.html)
- [networkx.algorithms.euler.is_semieulerian](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.euler.is_semieulerian.html)
- [networkx.algorithms.euler.has_eulerian_path](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.euler.has_eulerian_path.html)
- [networkx.algorithms.euler.eulerian_path](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.euler.eulerian_path.html)

### Flows

- [Maximum Flow](https://networkx.github.io/documentation/stable/reference/algorithms/flow.html#maximum-flow)
- [Edmonds-Karp](https://networkx.github.io/documentation/stable/reference/algorithms/flow.html#edmonds-karp)
- [Shortest Augmenting Path](https://networkx.github.io/documentation/stable/reference/algorithms/flow.html#shortest-augmenting-path)
- [Preflow-Push](https://networkx.github.io/documentation/stable/reference/algorithms/flow.html#preflow-push)
- [Dinitz](https://networkx.github.io/documentation/stable/reference/algorithms/flow.html#dinitz)
- [Boykov-Kolmogorov](https://networkx.github.io/documentation/stable/reference/algorithms/flow.html#boykov-kolmogorov)
- [Gomory-Hu Tree](https://networkx.github.io/documentation/stable/reference/algorithms/flow.html#gomory-hu-tree)
- [Utils](https://networkx.github.io/documentation/stable/reference/algorithms/flow.html#utils)
- [Network Simplex](https://networkx.github.io/documentation/stable/reference/algorithms/flow.html#network-simplex)
- [Capacity Scaling Minimum Cost Flow](https://networkx.github.io/documentation/stable/reference/algorithms/flow.html#capacity-scaling-minimum-cost-flow)

### Graphical degree sequence

- [networkx.algorithms.graphical.is_graphical](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.graphical.is_graphical.html)
- [networkx.algorithms.graphical.is_digraphical](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.graphical.is_digraphical.html)
- [networkx.algorithms.graphical.is_multigraphical](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.graphical.is_multigraphical.html)
- [networkx.algorithms.graphical.is_pseudographical](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.graphical.is_pseudographical.html)
- [networkx.algorithms.graphical.is_valid_degree_sequence_havel_hakimi](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.graphical.is_valid_degree_sequence_havel_hakimi.html)
- [networkx.algorithms.graphical.is_valid_degree_sequence_erdos_gallai](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.graphical.is_valid_degree_sequence_erdos_gallai.html)

### Hierarchy

- [networkx.algorithms.hierarchy.flow_hierarchy](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.hierarchy.flow_hierarchy.html)

### Hybrid

- [networkx.algorithms.hybrid.kl_connected_subgraph](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.hybrid.kl_connected_subgraph.html)
- [networkx.algorithms.hybrid.is_kl_connected](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.hybrid.is_kl_connected.html)

### Isolates

- [networkx.algorithms.isolate.is_isolate](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.isolate.is_isolate.html)
- [networkx.algorithms.isolate.isolates](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.isolate.isolates.html)
- [networkx.algorithms.isolate.number_of_isolates](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.isolate.number_of_isolates.html)

### Isomorphism

- [networkx.algorithms.isomorphism.is_isomorphic](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.isomorphism.is_isomorphic.html)
- [networkx.algorithms.isomorphism.could_be_isomorphic](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.isomorphism.could_be_isomorphic.html)
- [networkx.algorithms.isomorphism.fast_could_be_isomorphic](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.isomorphism.fast_could_be_isomorphic.html)
- [networkx.algorithms.isomorphism.faster_could_be_isomorphic](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.isomorphism.faster_could_be_isomorphic.html)
- [Advanced Interfaces](https://networkx.github.io/documentation/stable/reference/algorithms/isomorphism.html#advanced-interfaces)

### Link Analysis

- [PageRank](https://networkx.github.io/documentation/stable/reference/algorithms/link_analysis.html#module-networkx.algorithms.link_analysis.pagerank_alg)
- [Hits](https://networkx.github.io/documentation/stable/reference/algorithms/link_analysis.html#module-networkx.algorithms.link_analysis.hits_alg)

### Link Prediction

- [networkx.algorithms.link_prediction.resource_allocation_index](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.link_prediction.resource_allocation_index.html)
- [networkx.algorithms.link_prediction.jaccard_coefficient](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.link_prediction.jaccard_coefficient.html)
- [networkx.algorithms.link_prediction.adamic_adar_index](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.link_prediction.adamic_adar_index.html)
- [networkx.algorithms.link_prediction.preferential_attachment](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.link_prediction.preferential_attachment.html)
- [networkx.algorithms.link_prediction.cn_soundarajan_hopcroft](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.link_prediction.cn_soundarajan_hopcroft.html)
- [networkx.algorithms.link_prediction.ra_index_soundarajan_hopcroft](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.link_prediction.ra_index_soundarajan_hopcroft.html)
- [networkx.algorithms.link_prediction.within_inter_cluster](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.link_prediction.within_inter_cluster.html)

### Lowest Common Ancestor

- [networkx.algorithms.lowest_common_ancestors.all_pairs_lowest_common_ancestor](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.lowest_common_ancestors.all_pairs_lowest_common_ancestor.html)
- [networkx.algorithms.lowest_common_ancestors.tree_all_pairs_lowest_common_ancestor](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.lowest_common_ancestors.tree_all_pairs_lowest_common_ancestor.html)
- [networkx.algorithms.lowest_common_ancestors.lowest_common_ancestor](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.lowest_common_ancestors.lowest_common_ancestor.html)

### Matching

- [networkx.algorithms.matching.is_matching](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.matching.is_matching.html)
- [networkx.algorithms.matching.is_maximal_matching](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.matching.is_maximal_matching.html)
- [networkx.algorithms.matching.is_perfect_matching](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.matching.is_perfect_matching.html)
- [networkx.algorithms.matching.maximal_matching](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.matching.maximal_matching.html)
- [networkx.algorithms.matching.max_weight_matching](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.matching.max_weight_matching.html)

### Minors

- [networkx.algorithms.minors.contracted_edge](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.minors.contracted_edge.html)
- [networkx.algorithms.minors.contracted_nodes](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.minors.contracted_nodes.html)
- [networkx.algorithms.minors.identified_nodes](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.minors.identified_nodes.html)
- [networkx.algorithms.minors.quotient_graph](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.minors.quotient_graph.html)

### Maximal independent set

- [networkx.algorithms.mis.maximal_independent_set](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.mis.maximal_independent_set.html)

### non-randomness

- [networkx.algorithms.non_randomness.non_randomness](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.non_randomness.non_randomness.html)

### Moral

- [networkx.algorithms.moral.moral_graph](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.moral.moral_graph.html)

### Node Classification

- [Harmonic Function](https://networkx.github.io/documentation/stable/reference/algorithms/node_classification.html#module-networkx.algorithms.node_classification.hmn)
- [Local and Global Consistency](https://networkx.github.io/documentation/stable/reference/algorithms/node_classification.html#module-networkx.algorithms.node_classification.lgc)

### Operators

- [networkx.algorithms.operators.unary.complement](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.operators.unary.complement.html)
- [networkx.algorithms.operators.unary.reverse](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.operators.unary.reverse.html)
- [networkx.algorithms.operators.binary.compose](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.operators.binary.compose.html)
- [networkx.algorithms.operators.binary.union](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.operators.binary.union.html)
- [networkx.algorithms.operators.binary.disjoint_union](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.operators.binary.disjoint_union.html)
- [networkx.algorithms.operators.binary.intersection](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.operators.binary.intersection.html)
- [networkx.algorithms.operators.binary.difference](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.operators.binary.difference.html)
- [networkx.algorithms.operators.binary.symmetric_difference](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.operators.binary.symmetric_difference.html)
- [networkx.algorithms.operators.binary.full_join](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.operators.binary.full_join.html)
- [networkx.algorithms.operators.all.compose_all](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.operators.all.compose_all.html)
- [networkx.algorithms.operators.all.union_all](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.operators.all.union_all.html)
- [networkx.algorithms.operators.all.disjoint_union_all](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.operators.all.disjoint_union_all.html)
- [networkx.algorithms.operators.all.intersection_all](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.operators.all.intersection_all.html)
- [networkx.algorithms.operators.product.cartesian_product](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.operators.product.cartesian_product.html)
- [networkx.algorithms.operators.product.lexicographic_product](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.operators.product.lexicographic_product.html)
- [networkx.algorithms.operators.product.rooted_product](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.operators.product.rooted_product.html)
- [networkx.algorithms.operators.product.strong_product](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.operators.product.strong_product.html)
- [networkx.algorithms.operators.product.tensor_product](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.operators.product.tensor_product.html)
- [networkx.algorithms.operators.product.power](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.operators.product.power.html)

### Planarity

- [networkx.algorithms.planarity.check_planarity](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.planarity.check_planarity.html)

### Planar Drawing

- [networkx.algorithms.planar_drawing.combinatorial_embedding_to_pos](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.planar_drawing.combinatorial_embedding_to_pos.html)

### Reciprocity

- [networkx.algorithms.reciprocity.reciprocity](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.reciprocity.reciprocity.html)
- [networkx.algorithms.reciprocity.overall_reciprocity](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.reciprocity.overall_reciprocity.html)

### Rich Club

- [networkx.algorithms.richclub.rich_club_coefficient](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.richclub.rich_club_coefficient.html)

### Shortest Paths

- [networkx.algorithms.shortest_paths.generic.shortest_path](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.shortest_paths.generic.shortest_path.html)
- [networkx.algorithms.shortest_paths.generic.all_shortest_paths](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.shortest_paths.generic.all_shortest_paths.html)
- [networkx.algorithms.shortest_paths.generic.shortest_path_length](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.shortest_paths.generic.shortest_path_length.html)
- [networkx.algorithms.shortest_paths.generic.average_shortest_path_length](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.shortest_paths.generic.average_shortest_path_length.html)
- [networkx.algorithms.shortest_paths.generic.has_path](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.shortest_paths.generic.has_path.html)
- [Advanced Interface](https://networkx.github.io/documentation/stable/reference/algorithms/shortest_paths.html#module-networkx.algorithms.shortest_paths.unweighted)
- [Dense Graphs](https://networkx.github.io/documentation/stable/reference/algorithms/shortest_paths.html#module-networkx.algorithms.shortest_paths.dense)
- [A* Algorithm](https://networkx.github.io/documentation/stable/reference/algorithms/shortest_paths.html#module-networkx.algorithms.shortest_paths.astar)

### Similarity Measures

- [networkx.algorithms.similarity.graph_edit_distance](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.similarity.graph_edit_distance.html)
- [networkx.algorithms.similarity.optimal_edit_paths](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.similarity.optimal_edit_paths.html)
- [networkx.algorithms.similarity.optimize_graph_edit_distance](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.similarity.optimize_graph_edit_distance.html)
- [networkx.algorithms.similarity.optimize_edit_paths](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.similarity.optimize_edit_paths.html)
- [networkx.algorithms.similarity.simrank_similarity](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.similarity.simrank_similarity.html)
- [networkx.algorithms.similarity.simrank_similarity_numpy](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.similarity.simrank_similarity_numpy.html)

### Simple Paths

- [networkx.algorithms.simple_paths.all_simple_paths](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.simple_paths.all_simple_paths.html)
- [networkx.algorithms.simple_paths.is_simple_path](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.simple_paths.is_simple_path.html)
- [networkx.algorithms.simple_paths.shortest_simple_paths](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.simple_paths.shortest_simple_paths.html)

### Small-world

- [networkx.algorithms.smallworld.random_reference](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.smallworld.random_reference.html)
- [networkx.algorithms.smallworld.lattice_reference](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.smallworld.lattice_reference.html)
- [networkx.algorithms.smallworld.sigma](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.smallworld.sigma.html)
- [networkx.algorithms.smallworld.omega](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.smallworld.omega.html)

### s metric

- [networkx.algorithms.smetric.s_metric](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.smetric.s_metric.html)

### Sparsifiers

- [networkx.algorithms.sparsifiers.spanner](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.sparsifiers.spanner.html)

### Structural holes

- [networkx.algorithms.structuralholes.constraint](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.structuralholes.constraint.html)
- [networkx.algorithms.structuralholes.effective_size](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.structuralholes.effective_size.html)
- [networkx.algorithms.structuralholes.local_constraint](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.structuralholes.local_constraint.html)

### Swap

- [networkx.algorithms.swap.double_edge_swap](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.swap.double_edge_swap.html)
- [networkx.algorithms.swap.connected_double_edge_swap](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.swap.connected_double_edge_swap.html)

### Tournament

- [networkx.algorithms.tournament.hamiltonian_path](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.tournament.hamiltonian_path.html)
- [networkx.algorithms.tournament.is_reachable](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.tournament.is_reachable.html)
- [networkx.algorithms.tournament.is_strongly_connected](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.tournament.is_strongly_connected.html)
- [networkx.algorithms.tournament.is_tournament](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.tournament.is_tournament.html)
- [networkx.algorithms.tournament.random_tournament](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.tournament.random_tournament.html)
- [networkx.algorithms.tournament.score_sequence](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.tournament.score_sequence.html)

### Traversal

- [Depth First Search](https://networkx.github.io/documentation/stable/reference/algorithms/traversal.html#module-networkx.algorithms.traversal.depth_first_search)
- [Breadth First Search](https://networkx.github.io/documentation/stable/reference/algorithms/traversal.html#module-networkx.algorithms.traversal.breadth_first_search)
- [Beam search](https://networkx.github.io/documentation/stable/reference/algorithms/traversal.html#module-networkx.algorithms.traversal.beamsearch)
- [Depth First Search on Edges](https://networkx.github.io/documentation/stable/reference/algorithms/traversal.html#module-networkx.algorithms.traversal.edgedfs)
- [Breadth First Search on Edges](https://networkx.github.io/documentation/stable/reference/algorithms/traversal.html#module-networkx.algorithms.traversal.edgebfs)

### Tree

- [Recognition](https://networkx.github.io/documentation/stable/reference/algorithms/tree.html#module-networkx.algorithms.tree.recognition)
- [Branchings and Spanning Arborescences](https://networkx.github.io/documentation/stable/reference/algorithms/tree.html#module-networkx.algorithms.tree.branchings)
- [Encoding and decoding](https://networkx.github.io/documentation/stable/reference/algorithms/tree.html#module-networkx.algorithms.tree.coding)
- [Operations](https://networkx.github.io/documentation/stable/reference/algorithms/tree.html#module-networkx.algorithms.tree.operations)
- [Spanning Trees](https://networkx.github.io/documentation/stable/reference/algorithms/tree.html#module-networkx.algorithms.tree.mst)
- [Exceptions](https://networkx.github.io/documentation/stable/reference/algorithms/tree.html#exceptions)

### Triads

- [networkx.algorithms.triads.triadic_census](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.triads.triadic_census.html)

### Vitality

- [networkx.algorithms.vitality.closeness_vitality](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.vitality.closeness_vitality.html)

### Voronoi cells

- [networkx.algorithms.voronoi.voronoi_cells](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.voronoi.voronoi_cells.html)

### Wiener index

- [networkx.algorithms.wiener.wiener_index](https://networkx.github.io/documentation/stable/reference/algorithms/generated/networkx.algorithms.wiener.wiener_index.html)