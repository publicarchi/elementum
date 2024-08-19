---
author: emchateau
tags: arguments
---

# Argument Mining

> La fouille d’arguments consiste en l’identification et l’extraction des structures d’inférences et de raisonnements exprimées comme des arguments présents dans le langage naturel. La compréhension des structures argumentatives permet d’identifier non seulement quelles positions les personnes adoptent mais aussi pourquoi ils tiennent certaines positions ce qui apporte des éclairages intéressants dans des domaines aussi divers que celui de la prédiction des marchés financiers ou les relations publiques. (traduit de Lawrence et Reed 2020)

Plusieurs arguments justifient d’avoir recours à des technologies d’argument mining. Celles-ci s’avèrent particulièrement intéressantes pour prendre en charge de grandes quantité de données (big data) qui seraient pas appréhendables avec des approches traditionnelles. Le recours de plus en plus fréquent au web comme média privilégié pour les débats publics et le développement d’arguments a notamment largement motivé le développement de technologies de traitement automatique en cherchant à identifier des relations structurelles de plus en plus complexes entre les concepts. Certaines approches se sont avérées particulièrement fructueuses comme l’identification d’opinion ou l’analyse de sentiment.

## Les 3Vs des *Big data*

L’idée de Big data peut remonter aux années quatre-vingt-dix. L’expression a d’abord été utilisée par John Mashey pour faire référence au fait de manipuler et d’analyser de grands ensembles de données. En 2001, Doug Laney avançait que les Big data pouvaient être caractérisés par trois traits :

- Volume (consistent en d’énormes quantité de données) : big data doesn’t sample ; it just obseves and tracks what happens
- Velocity (créées en temps réel) : big data is often available in real-time which implies speed of processing
- Variety (sont strcturées, semi-structurées ou non-structurées) : big data draws from text, images, audio, video

D’autres auteurs ont depuis pointé d’autres qualités de ces big data, incluant : l’exhaustivité, le grain, la relationnalité, l’extensionnalité, la véracité, la valeur ou la vériabilité (Kitchin et McArdle 2016).

Références sur l’enjeu dans le secteur académique

- Research Councils on Big Data. At http://www.rcuk.ac.uk/research/infrastructure/big-data
- Council Decision Establishing the Specific Programme Implementing HORIZON 2020

## L’étude de l’argumentation

Il s’agit d’une approche largement informée par l’étude de l’argumentation. La théorie de l’argumentation est un champ de recherche interdisciplinaire relativement large à cheval entre la philosophie, la communication, la linguistique et la psychologie.

(Eemeren et al. 2014)

Comprésention des propriétés dans les différentes logiques argumentatives : Prakken et Vreeswijk 2002

Spécification des dialogues argumentatifs : McBurney & Parsons 2003.



## Place centrale des technologies de NLP

L’analyse d’argument cherche à adresser cette question en transformant du texte non structuré en données structurées sur l’argumentation afin d’identifier non-seulement les arguments individuels qui sont dévelopés mais aussi la relation entre eux et comment ils fonctionnenent ensemble pour supporter (ou contredire) un message général (Lawrence et Reed 2020, p. 766).

L’extraction manuelle d’argument est une tâche chronophage qui exige des compétences particulières. L’identification et l’extraction automatique de composants ou de structure d’arguments présente donc beaucoup d’intérêt.

C’est une approche qui doit être resituée par rapport à d’autres technologies de traitement automatique de la langue naturelle (NLP) :

- Computational linguistics : statistical or rule-based modelling of natural language
- NLP : interactions between computers and human languages
- Data mining : automatic extraction of data (mostly numerical)
- Text mining : automatic extraction of data from natural language
- Argument mining (ArgMin, AM) : automatic extraction of arguments from natural language texts

Argument minging, déterminer les opinions respectives. Notamment les arguments en faveur ou contre.

Définition de l’argument

## Développements du domaine

Le champs de la fouille d’arguments s’est développé rapidement ces dernières années. Alors que l’on identifie moins d’une dizaine de publications avant 2014, le domaine émerge principalement à partir de l’organisation du premier ACL Worshop qui a lieu annuellement depuis cette date et a été rejoint par d’autres conférences organisées à Varsovie, Dundee, Dagstuhl ou plusieurs formations.

Avant 2014 : Mochales Palau and Moens 2011; Saint-Dizier 2012; Cabrio and Villata 2012b

- *From Real Data to Argument Mining*, 12th ArgDiaP Conference, Polish Academy of Sciences, Warsaw, Poland, 23-24 May 2014. (22 papers)
- *1st Workshop on Argumentation Mining*, 52nd Annual Meeting of the Association for Computational Linguistics, Baltimore, US, June 26, 2014 (18 papers)*
- *SICSA Workshop on Argument Mining: Perspectives from Information Extraction, Information Retrieval and Computational Linguistics,* ARG-tech, Dundee, Scotland, 9-10 July 2014. (ca. 25 participants)
- *Frontiers and Connections between Argumentation Theory and Natural Language Processing*, Bertinoro (Forlì-Cesena), Italy, 21-25 July 2014.
- *2nd Workshop on Argumentation Mining*, 53nd Annual Meeting of the Association for Computational Linguistics, Denver, US, June 04, 2015 (16 papers)
- *Arguments in Natural Language: The Long Way to Analyze the Reasons to Believe and the Reasons to Act*, 1st European Conference on Argumentation, Lisbon, 9-12 July 2015
- *NaturalLanguageArgumentation:Mining,Processing,andReasoningover Textual Arguments*, Dagstuhl Seminar, April 17 – 22 , 2016
- *3rd Workshop on Argumentation Mining*, 54nd Annual Meeting of the 12 Association for Computational Linguistics), Berlin, Aug 12, 2016 (20 papers) http://argmining2016.arg.tech
- [Proceedings of the 9th Workshop on Argument Mining](https://aclanthology.org/volumes/2022.argmining-1/)

IBM Debating Technologies, http://researcher.watson.ibm.com/researcher/view_group.php?id=5443

Annotation des textes manuelle ou automatique.

Marquage des arguments, et de leurs composants : assertions, reformulations, etc.

## Points de contacts

L’analyse des sentiments est partie liée à la fouille de l’argumentation. Il est en partie possible de déterminer le caractère positif ou négatif d’un document. FrameNet.

La détection des controverses permet notamment de détecter des points chauds dans la discussion.

La fouille de citations consiste à étiqueter les instances de citation dans les écrits scientifiques avec leurs rôles rhétorique dans le discours.

L’argumentative zoning (AZ) est la classification des phrases en fonction de leur rôle rhétorique et argumentatif dans un article. Teufel et al. encodage par un expert du domaine, 14 rôles possibles.

L’analyse manuelle des arguments peut permettre de produire des diagrammes.

Manque de données annotées. Cf. Green. Problèmes de classification. Techniques d’identifctaion pour faciliter le travail. Utilisaton de certains lexème pour annotation automatique (« This », « This conclusion »). Utilisation de classiffieurs. Stratégies utilisant des indicateurs du discours (cpendant, parce que, etc.). Utlisation d’arguments prototypiques.

## Applications informatiques des schèmes argumentatifs

 Verheij 2003b le premier à introduire l’utilisation des schèmes argumentatifs en contexte computationnel. Considère que tout schème argumentatif peut être exprimé sous la forme prémise 1, prémisse 2, etc. therefore Conclusion. Développement d’un outil logiciel de cartographie : ArguMed

ASPIC+ Prakken 2010, un système formel d’argumentation

Ree Wal

## Outils

### Annotation manuelle :

- Online Visualisation of Argument (OVA) analysis tool (Bex et al. 2013)
  http://ova.arg-tech.org
  https://www.arg.tech/index.php/ova/
  https://github.com/arg-tech/OVA3
- Rationale (van Gelder 2007)
- Carneades (Gordon, PRakken and Walton 2007)
- Araucaria (Reed and Rowe 2004)
- [DebateGraph](https://debategraph.org)
- [TruthMapping](https://www.truthmapping.com)
- [Debatepedia](http://www.debatepedia.org)
- [https://agora-info.spp.gatech.edu](https://agora-info.spp.gatech.edu)
- [Argunet](http://www.argunet.org)
- [Rationale Online](https://www.rationaleonline.com)
- [Argdown](https://argdown.org) 2018-
- « Carneades Argumentation System ». s. d. Consulté le 7 octobre 2023. http://carneades.github.io/.

### Corpus

- AIFdb17 (Lawrence et al. 2012) http://corpora.aifdb.org
- Argument Annotated Essays Corpus AAEC, Stab et Gurevych 2014a, 2017
- Internet Argument Corpus (IAC) (Walker et al. 2012)
- arg-microtexts An annotated corpus of argumentative microtexts https://github.com/peldszus/arg-microtexts

### Formats

Plusieurs formats informatiques ont été développés pour la notation des arguments. Les différentes tentatives pour développper des languages de balisage pour l’argumentation ont longtemps été marquée par deux limitations : D’une part, ces langages avaient été conçu pour l’utilisation de certains outils plutôt que pour faciliter l’inter-opérabilité entre une grande variété d’outils. Ainsi, leur sémantique était étroitement couplée à certains schemes pour être interprétés dans des outils donnés selon des théories sous-jascentes spécifiques. D’autre part, ils étaient le plus souvent conçu pour permettre aux utilisateurs de structurer des arguments à partir de leur liens diagrammatiques. Ce qui imposait parfois des limitation structuales sur les arguments autorisés. [(Chesñevar et al. 2006)](zotero://select/library/items/3HQV3VCG).

La réunion *AgentLink Technical Forum Group meeting de Budapest en Hongrie en  2005 était destinée à mettre sur pied un format qui ne serait pas marqué par ces limitations en consolidant le travail déjà réalisé. 

La conception de l’Argument Interchange Format (AIF) était destinée à :

- faciliter le développement (fermé ou ouvert) de systèmes multi-agents capables de raisonnement basés sur l’argumentation et d’interagir à travers un formalisme partagé
- faciliter l’échange de données entre les outils pour la manipulation d’arguments et leur visualisation

 cf. [(Bex et al. 2012)](zotero://select/library/items/6L5JZJEE) et [(Chesñevar et al. 2006)](zotero://select/library/items/3HQV3VCG)

Le modèle est conçu sur la base d’une ontologie de noyau composée de trois groupes

- les arguments et les réseaux d’arguments
- la communication
- le contexte

Legal Knowledge Interchange Format (LKIF)

Formal argumentation models tels que ASPIC+ (Prakken et al. 2015) DefLog ([Verheij, 2003a]) and the Carneades Argumentation System ([Walton and Gordon, 2012]).

### Acteurs 

- [Center for Argument Technology](https://www.arg.tech)
  https://github.com/arg-tech
- [Applied CL Discourse Research Lab](http://angcl.ling.uni-potsdam.de/index.html)

## Références

Synthèses

- Lawrence, John, et Chris Reed. 2020. « Argument Mining: A Survey ». *Computational Linguistics* 45 (4): 765‑818. https://doi.org/10.1162/coli_a_00364.
- Lippi, Marco, et Paolo Torroni. 2016. « Argumentation Mining: State of the Art and Emerging Trends ». *ACM Transactions on Internet Technology* 16 (2): 10:1-10:25. https://doi.org/10.1145/2850417.
- Stede, Manfred, et Jodi Schneider. 2019. *Argumentation Mining*. Synthesis Lectures on Human Language Technologies 40. San Rafael: Morgan & Claypool Publishers.

Divers

- Lippi, Marco, et Paolo Torroni. 2015. « Argument Mining: A Machine Learning Perspective ». In *Theory and Applications of Formal Argumentation*, édité par Elizabeth Black, Sanjay Modgil, et Nir Oren, 9524:163‑76. Lecture Notes in Computer Science. Cham: Springer International Publishing. https://doi.org/10.1007/978-3-319-28460-6_10.
- ———. 2016b. « MARGOT: A Web Server for Argumentation Mining ». *Expert Systems with Applications* 65 (décembre): 292‑303. https://doi.org/10.1016/j.eswa.2016.08.050.