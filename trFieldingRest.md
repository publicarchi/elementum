Essai de traduction de Fielding
=========

La traduction française n'étant pas très bonne http://opikanoba.org/tr/fielding/rest/

Chapitre 5
Representational State Transfer (REST)

Ce chapitre propose et introduit le paradigme architectural Representational State Transfer (REST) pour des systèmes hypermédia distribués. Il décrit les principes de conception logicielle qui guident REST et les contraintes d'interaction choisies pour maintenir ces principes en les comparant aux contraintes d'autres paradigmes architercturaux. REST est un style hybride qui dérive de plusieurs des paradigmes architecturaux basés sur les réseaux décrits dans le Chapitre 3, qui a été combiné avec des contraintes additionnelles définissant une interface de connexion uniforme. Le cadre de travail d'architecture logiciel du Chapitre 1 est employé pour définir les éléments architecturaux de REST et pour examiner les exemples de processus, de connecteurs, et de vues sur les données d'architectures prototypales.


## Dériver REST

Le rationnel de conception qui préside à l'architecture du Web peut être décrit par un modèle architectural qui consiste en un ensemble de contraintes appliquées aux éléments au sein de cette architecture. En examinant l'impact de chacune de ces contraintes telles qu'elles s'ajoutent au style en évolution, nous pouvons identifier les propriétés induites par les contraintes du Web. Des contraintes additionnelles peuvent ensuite être appliquées pour former un nouveau paradigme architectural qui reflète mieux les propriétés souhaitées d'une architecture moderne du Web. Cette section fournit un panorama général de REST à partir d'un processus de dérivation comme modèle architectural. Les sections ultérieures décriront plus en détails les contraintes spécifiques qui composent le paradigme REST.


### 5.1.1 En commençant par le modèle vide [null]

Il existe deux perspectives communes sur le processus de conception architectural qu'il s'agisse de construction ou de logiciel. Dans la première, le concepteur part de rien – d'une table rase, d'un tableau blanc, ou d'une feuille vide – et construit une architecture à partri de composants familiers jusqu'à ce qu'elle satisfasse les besoins du système attendu. Dans la seconde, le concepteur part des besoins du système comme un tout, sans contraintes, puis identifie et applique de manière incrémentielle les contraintes aux éléments du système dans le but de différentier l'espace de conception et de permettre aux forces qui influent sur le comportement du système de se développer naturellement, en harmonie avec le système. Lorsque la première perspective met l'accent sur la créativité et une vision sans limite, la seconde met l'accent sur la restriction et la compréhension du contexte du système. REST a été développé en utilisant cette dernière approche. Les figures 5-1 à 5-8 dépeignent en termes graphiques, comment les contraintes appliquées diférentieraient la vue du processus d'une architecture lorsqu'un ensemble incrémentiel de contraintes est appliqué.

Le modèle vide (_Null style_) ([Figure 5-1]) consiste simplement en un ensemble vide de contraintes. D'un point de vue architectural, le modèle vide décrit un système dans lequel il n'y a pas de frontières identifiables entre les composants. C'est le point de départ de notre description de REST.

[Figure 5-1]()


### 5.1.2 Client-Server

Les premières contraintes que l'on ajoute à notre modèle hybride sont celles du paradigme  architectural client-serveur ([Figure 5-2]), décrit à la [Section 3.4.1]. La principale contrainte sous-jascente au modèle client-serveur est la séparation des préoccupations. en séparant ce qui a rapport à l'interface utilisateur du stockage de données, on augmente la portabilité de l'utilisation de l'interface sur des plateformes multiples et on améliore la scalabilité en simplifiant les composants du serveur. Cependant, et c'est peut-être le plus significatif pour le Web, cette séparation permet aux composants d'évoluer indépedamment, et ainsi de supporter les besoins d'accoroissement du web en termes de domaines organisationnels multiples.

[Figure 5-2]()


### Sans-état (_stateless_)

On ajoute ensuite une contrainte à l'interaction client-serveur : la communication doit être sans état par nature, comme dans le paradigme client-serveur sans-état de la [Section 3.4.3] ([Figure 5-3]), de telle sorte que chaque requête d'un client au serveur doit contenir toutes les informations nécessaires pour comprendre la requête, et qu'elle ne puisse prendre avantage d'aucun contexte stocké sur le serveur. L'état de la session est ainsi entièrement conservé par le client.

[Figure 5-3]()

Cette contrainte induit les propriétés de visibilité, de fiabilité et de scalabilité. La visibilité est améliorée car un système de suivi (_monitoring_) n'a pas besoin de passer par l'intermédiaire d'un journal de données pour déterminer la nature complète de la requête. La fiabilité est accrue compte-tenu de la possibilité de de réparatir d'échecs partiels. La scalabilité est augmentée par le fait de



to be continued...
###

###
