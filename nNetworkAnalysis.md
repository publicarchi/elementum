# Analyse de Réseau

## Méthodes

Louvain algorithm hardly detects statistically 120 significant communities (modularity with resolution 1: 0.26) 121 (S.I.2). 

The relatively high edgewise reciprocity (18%, com- 122 pared to 3.5% in average for simulated networks with the same 123 density and number of edges – S.I.3)

Exponential-Random Graph (ERGM) models show that, for 138

## Modélisation

En sciences de l’informatique, un graphe est une structure de données abstraite destinée à implémenter les concepts de graphes orientés ou non orientés issus des mathématiques et de la théorie des graphes. Une structure en graphe consiste en un ensemble fini de sommets *vertices* (aussi appelés nodes ou points) et d’un ensemble de paires non orientées entre ces sommets dans un graphe non-orienté, ou orienté dans un graphe orienté. Ces paires appelés aussi edges (ou liens ou encore lignes) ou arrows dans un graphe orienté. Relations pouvant être étiquetées.

Opérations :

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

## Formats

### Simple interaction file (SIF ou .sif format)

Le format SIF décrit seulement des nœuds et des interactions alors que d’autres formats permettent d’enregistrer d’autres informations sur la disposition du réseau et le partage de données avec d’autres programmes. 

Son cas d’usage consiste plutôt en l’importation d’interactions au début de la construction d’un réseau. Lorsque le réseau a été chargé et que l’on a opérer sa mise en page, les formats GML ou XGMML peuvent être utilisées pour interagir avec d’autres systèmes.

Ces fichiers peuvent facilement être créés dans un éditeur de texte ou avec un tableur. Il s’agit d’un format tabulaire dans lequel chaque colonne correspond à une interaction individuelle (edge) entre une source et un nœud cible.

```txt
nodeA relationship nodeB
nodeC relationship nodeA
nodeD relationship nodeE
```

http://www.cbmc.it/fastcent/doc/SifFormat.htm

### Nested network format (NNF or .nnf format)

### Graph Markup Language (GML or .gml format) [obsolète]

@name Graph Markup Language

@acronyme GML

@extension .gml

@url http://www.infosun.fmi.uni-passau.de/Graphlet/GML/ [inactif] voir https://web.archive.org/web/20170601041145/http://www.fim.uni-passau.de/index.php?id=17297&L=1

@url https://web.archive.org/web/20060824191148/http://www.infosun.fmi.uni-passau.de/Graphlet/GML/gml-tr.html

>GML (Graph Modelling Language): There are many different programs that work with graphs but almost all of them use their own file format. As a consequence, exchanging graphs between different programs is almost impossible. Simple tasks like exchange of data, externally reproducible results or a common benchmark suite are much harder than neccessary.
>Therefore, we have developed a new file format for the Graphlet system: GML. GML supports attaching arbitrary information to graphs, nodes and edges, and is therefore able to emulate almost every other format.

À la différence de SIF, GML est un riche format de graphe supporté par de nombreux package de visualisation. Le format permet d’embarquer des informations de présentation.

Ce format peut paraître obsolète car il fut notamment remplacé par le format XGMML. Néanmoins, le fait qu’il s’agisse d’un simple fichier ASCII peut s’avérer utile, il est par ailleurs toujours supporté par nombre de logiciels.

@seeAlso https://en.wikipedia.org/wiki/Graph_Modelling_Language

### Directed Graph Markup Language (DGML)

@name Directed Graph Markup Language

@acronyme DGML

@extension .dgml

@url http://schemas.microsoft.com/vs/2009/dgml/

DGML est un format XML pour les graphes orientés. Ce format est spécifié par un [schema XML](Schema http://schemas.microsoft.com/vs/2009/dgml/dgml.xsd) et a été implémenté dans Visual Studio en 2010.

@seeAlso 

- Documentation https://docs.microsoft.com/fr-fr/visualstudio/modeling/customize-code-maps-by-editing-the-dgml-files
- Schema http://schemas.microsoft.com/vs/2009/dgml/dgml.xsd

### XGMML (extensible graph markup and modelling language) [obsolète ?]

@name eXtensible Graph Markup and Modeling Language

@acronyme XGMML

@url http://cgi7.cs.rpi.edu/research/groups/pb/punin/public_html/XGMML/ [rompu], voir http://cgi7.cs.rpi.edu/research/groups/pb/punin/public_html/XGMML/

> XGMML (eXtensible Graph Markup and Modeling Language) is an XML application based on GML which is used for graph description. XGMML uses tags to describe nodes and edges of a graph. The purpose of XGMML is to make possible the exchange of graphs between differents authoring and browsing tools for graphs. The conversion of graphs written in GML to XGMML is trivial. Using XSL with XGMML allows the translation of graphs to different formats. XGMML was created to be used for the WWWPAL System that visualizes web sites as a graph. Web Robots can navigate through a web site and save the graph information as an XGMML file. XGMML, as any other XML application, can be mixed with other markup languages to describe additional graph, node and/or edge information.

Spécifié par une DTD et un Schéma XML (2001).

e**X**tensible **G**raph **M**arkup and **M**odeling **L**anguage est une application basée sur GML pour la description de graphe.

### Systems Biology Markup Language (SBML)

@name Systems Biology Markup Language

@acronyme SBML

@url http://sbml.org/documents/

Le Systems Biology Markup Language (SBML) est un format XML destiné à la description de réseaux en biochimie.

### Biological PAthways eXchange (BioPAX)

@url http://www.biopax.org/

@name Biological PAthways eXchange

@acronyme BioPAX

> Biological Pathway Exchange (BioPAX) is a standard language that aims to enable integration, exchange, visualization and analysis of biological pathway data. Specifically, BioPAX supports data exchange between pathway data groups and thus reduces the complexity of interchange between data formats by providing an accepted standard format for pathway data. It is an open and collaborative effort by the community of researchers, software developers, and institutions. BioPAX is defined in OWL DL and is represented in the RDF/XML format. For more details, see Demir E et al. 2010. The BioPAX community standard for pathway data sharing, Nature Biotechnology. 28(9).

Le BioPAX est une ontologie OWL conçue pour l’échange de données biologiques.

### PSI-MI Level 1 and 2.5

@name PSI-MI Level 1 and 2.5

@url http://psidev.sourceforge.net/mi/xml/doc/user/

Le format PSI-MI  est un format d’échange XML pour les interactions protéiques.

### GraphML

@name GraphML

@url http://graphml.graphdrawing.org/

https://web.archive.org/web/20200511231546/http://graphml.graphdrawing.org/

http://cs.brown.edu/people/rtamassi/gdhandbook/chapters/graphml.pdf 

GraphML est un format XML de description de graphes issus des efforts de la communauté des acteurs de la visualisation de graphes pour définir un format commun pour l’échange de données en structure de graphe. Le travail initié en 2000 a fait l’objet d’une spécification en 2001. Le format supporte l’ensemble des structures de graphes (orientées, non-orientées, mixtes, hyper graphes, et des attributs spécifiques pour les applications).

Un fichier GraphML est un fichier XML dont le nœud racine est un élément `graphml` qui contient un élément graph qui lui même continent une séquence non ordonnées de `node` et de `edge`. Chaque nœud `node` doit disposer d’un attribut `@id` distinct et chaque `edge` dispose d’attributs `@source` et `@target` pour identifier les sommets d’un edge.

Le format est utilisé nativement par yEd et Gephi

### Graph eXchange Language GXL

@name Graph eXchange Language

@acronyme GXL

@url http://www.gupro.de/GXL/

> GXL (Graph eXchange Language) is designed to be a standard exchange format for graphs. GXL is an XML sublanguage and the syntax is given by a XML DTD (Document Type Definition). This exchange format offers an adaptable and flexible means to support interoperability between graph-based tools. Introductions into GXL are given in [Holt et al., 2000], and [Holt/Winter, 2000], and a tutorial is given in [Winter, 2001].

Le format est initialement un merge des formats GRAph eXchange (GraX) de l’Université de Koblenz pour l’échange de graphes orientés typés, et ordonnés (TGraphs), du Tuple Attribute Language (TA) de l’université de Waterloo et du format de graphe du PROGRES graph rewriting system de Université Bw, Munich. Il inclut des idées de formats d’échanges comme le Relation Partition Algebra (RPA) de Philips Research, Eindhoven et du Rigi Standard Format (RSF) Université de Victoria. Son développement a été influence par d’autres formats de dessins de graphes comme le Graph Modelling Language (GML), Graphlet, ou encore GraphXML.

Nota : seulement spécifié par une DTD alors que GraphXML est exprimé par un Schéma XML.

@seeAlso https://en.wikipedia.org/wiki/GXL

### Delimited text

### Excel Workbook (.xls, .xlsx)

### GEXF (Graph Exchange XML Format)

https://gephi.org/gexf/format/

> GEXF (Graph Exchange XML Format) is a language for describing complex networks structures, their associated data and dynamics. Started in 2007 at Gephi project by different actors, deeply involved in graph exchange issues, the gexf specifications are mature enough to claim being both extensible and open, and suitable for real specific applications.

### Trivial Graph Format (TGF)

https://en.wikipedia.org/wiki/Trivial_Graph_Format

### Cytoscape.js

[Cytoscape.js JSON](http://cytoscape.github.io/cytoscape.js/#notation/elements-json)

### Cytoscape CX

[Cytoscape CX](https://github.com/CyComponent/CyWiki)

### Sources

http://manual.cytoscape.org/en/stable/Supported_Network_File_Formats.html

## Logiciels

### iGraph

https://igraph.org/redirect.html

> igraph is a collection of network analysis tools with the emphasis on efficiency, portability and ease of use. igraph is open source and free. igraph can be programmed in R, Python, Mathematica and C/C++.

### Cytoscape

>Cytoscape is an [open source](https://cytoscape.org/download.html) software platform for visualizing complex networks and integrating these with any type of attribute data. A lot of [*Apps*](http://apps.cytoscape.org/) are available for various kinds of problem domains, including bioinformatics, social network analysis, and semantic web.

https://cytoscape.org 

http://js.cytoscape.org

### JSNetworkX

http://jsnetworkx.org

### vis.js

http://visjs.org

### Cell-maps

http://cellmaps.babelomics.org/

>An open-source web-based HTML5 systems biology tool for visualizing and analysing biological networks http://cellmaps.babelomics.org/

https://github.com/opencb/cell-maps

### yEd

https://www.yworks.com/products/yed

### Networkx

http://networkx.github.io/