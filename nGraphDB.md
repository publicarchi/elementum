---
author: emchateau
tags: graphdb, outils
---

# Graph Databases

Une base de données orientée graphe est une base de données orientée objets utilisant la théorie des graphes pour représenter et stocker les données. Depuis 2016, ce genre de base de données a reçu beaucoup d’intérêt pour le développement web. 

L’émergence des bases de données en graphe pour la gestion des contenus web a généré une course entre les systèmes pour s’imposer comme standard de fait. [Neo4j](https://neo4j.com) est rapidement devenu le système données le plus populaire, il est récemment concurrencé par [ArangoDH](https://www.arangodb.com) et [OrientDB](https://orientdb.org/). Mais aussi une solution libre comme [TinkerPop](https://tinkerpop.apache.org).

### Labeled-property graph

>Un modèle de graphe de propriété étiquetée est représenté par un ensemble de nœuds, de relations, de propriétés et d’étiquettes. Les deux nœuds de données et leurs relations sont nommés et peuvent stocker des propriétés représentées par des paires clé/valeur. Les nœuds peuvent être étiquetés pour être regroupés. Les arêtes représentant les relations ont deux qualités : elles ont toujours un nœud de départ et un nœud d'arrivée, et sont dirigées, ce qui fait du graphe un graphe dirigé. Les relations peuvent aussi avoir des propriétés. Cela est utile pour fournir des métadonnées et une sémantique supplémentaires aux relations des nœuds. Le stockage direct des relations permet un parcours en temps constant.
><https://en.wikipedia.org/wiki/Graph_database#Labeled-property_graph>

## Languages

Faute de standardisation, plusieurs langages de données structurées ont émergé.

- Cypher
  Produits : [Neo4j](https://neo4j.com)
- Gremlin
  Produits : [TinkerPop](https://tinkerpop.apache.org), [JanusGraph](https://janusgraph.org), [Neo4j](https://neo4j.com)

### Graph Query Languages : GraphQL, OpenCypher, Gremlin and SPARQL

La concurrence entre les divers systèmes de bases de données pour s’imposer comme standard de fait, a également généré l’émergence de nombreux langages de requêtes dédiés. Aucun effort de standardisation n’a jusqu’à présent été réalisé.

#### GraphQL

[GraphQL](http://graphql.org/) se décrit comme un langage de requête de données et de runtime. Il cible la communication entre serveurs en utilisant des méthodes [RESTful](https://en.wikipedia.org/wiki/Representational_state_transfer). Il s’agit d’un projet Open Source de FaceTime, c’est une bonne solution pour créer des API.

Travail de standardisation en cours http://spec.graphql.org

#### OpenCypher et Gremlin

Les deux langages sont comparables à SQL dans le domaine des bases de données relationnelles. Ils permettent la recherche et la manipulation de données directement au niveau de la base de donnée en graphe.

[OpenCypher](http://www.opencypher.org) est un effort récent d’ouvrir le langage populaire Cypher utilisé par Neo4j lancée en octobre 2015 pour rendre le langage indépendant d’outil propriétaire.

#### Gremlin

[Gremlin](https://github.com/tinkerpop/gremlin/wiki) se décrit comme un langage pour traverse des graphes. Il est développé depuis 2009 par le projet Apache est fait partie du [Tinkerpop project](https://tinkerpop.incubator.apache.org/). Ce langage a été adopté par plusieurs produits dont OrientDB et Neo4j.

[SQL2Gremlin](http://sql2gremlin.com/) ressource éducative.

Ces deux langages sont actuellement les deux candidats pour s’imposer comme langage commun dans le domaine des bases de données en Graph. Gremlin a pris de l’avance, mais OpenCypher jouit de la grande popularité de Neo4j.

#### SPARQL

[SPARQL](https://www.w3.org/TR/sparql11-query/) est un langage conçu pour requêter des [graphes RDF](https://en.wikipedia.org/wiki/Resource_Description_Framework). C’est une recommandation du W3C qui cible le web sémantiques. Cependant le langage ne dispose pas de constrictions pour l’expression de requête arbitraire de graphe (looping, branching constructs).

Réunion W3C 2018-2019. Possible convergence des modèles.



https://blazegraph.com/

Blazegraph est un système de gestion de base de données orientée graphe et un triplestore. C'est un logiciel libre, sous licence GPLv2. 

https://comunica.dev/

Flexible SPARQL and GraphQL over decentralized RDF on the Web.

https://neo4j.com/product/graphql-library/

https://developers.mews.com/intro-to-graph-databases/

GraphDB

https://www.ontotext.com/products/graphdb/

https://www.topquadrant.com/

https://www.stardog.com/

https://tinkerpop.apache.org/docs/current/reference/#gremlin-javascript

https://janusgraph.org/
