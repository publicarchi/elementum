---
title: Le modèle conceptuel de référence CIDOC
filename: nCIDOC-CRM.md
author: 
date: 2014-02-23
version: 0.1
---


Le modèle conceptuel de référence CIDOC
================

Présentation
--------

>
>Le modèle conceptuel de référence (CRM) CIDOC fournit des définitions et une structure formelle pour la description de concepts implicites et explicites et leurs relations qui s’utilisent dans la documentation du patrimoine culturel.

CIDOC-CRM est destiné à promouvoir une compréhension partagée de l’information culturelle en fournissant un cadre de travail sémantique commun extensible vers lequel n’importe quelle information du patrimoine culturel puisse être alignée (_mapped to_). Il est destiné à être un language commun pour les experts et les implémentateurs pour formuler les pré-requis des systèmes d’information et pour servir de guide de bonnes pratiques pour la modélisation conceptuelle. De ce point de vue, il peut fournir la "colle sémantique" nécessaire pour médier différentes sources de d’information patrimoniale telles que celles publiées par les musées, les bibliothèques et les archives.

Le CIDOC-CRM est issue de dix années de travail du CIDOC Documentation Standards Working Group et du CIDOC CRM SIG qui sont des groupes de travail de CIDOC. Depuis le 9 décembre 2006 c’est devenu une norme internationale [ISO 21127:2006](http://www.iso.org/iso/catalogue_detail?csnumber=34424).


Le modèle conceptuel de référence CIDOC est une ontologie formelle destinée à faciliter l’intégration, la médiation et l’échange d’informations patrimoniales et culturelles hétérogènes. Il a été développé par une équipe interdisciplinaire composée d’experts issus de différents champs tels que les sciences informatiques, l’archéologie, le monde des musées ou de la documentation, l’histoire de l’art, les sciences naturelles, ou les sciences des bibliothèques, et la philosophie, sous l’égide du comité international pour la documentaion (CIDOC) de l’International Council of Museums (ICOM).

CIDOC-CRM a été harmonisé avec le modèle FRBR de l’IFLA, et EAD a été mappé vers CIDOC-CRM.

CIDOC-CRM se définit comme un formalisme orienté objet permettant des définitions compactes avec abstration et généralisation. Le modèle est centré sur les événements, ce qui signifie que les acteurs, les lieux et les objets sont connectés par l’intermédiaire d’événements. CIDOC-CRM est une ontologie de noyau (_core ontology_) au sens où le modèle ne dispose pas de classes pour tous les cas particuliers comme par exemple les milliers de concepts de l’Art and Architecture Thesaurus. CIDOC-CRM dispose d’un peu plus de 80 classes et 130 propriétés.

Historique
-------

- EAD a été mappé vers CIDOC-CRM en 2001 [Theodoridou 2001][Theodoridou 2001]

- En 2005 le CRM a été reformulé en une simple DTD XML dénommée CRM-Core pour permettre un encodage conforme au modèle conceptuel de référence de métadonnées multimédias [Sinclair 2006][Sinclair 2006].

- Le Conseil allemand pour les musées a basé son standard XML pour l’échange de données muséales, MUSEUMDAT, sur une combinaison du CDWA Lite du Getty et CRM-Core.

- La révision de CDWA Lite en 2006 envisageait d’apporter des changements à CDWA Lite pour le rendre compatible avec le CRM.


- Une harmonisation de CIDOC-CRM et FRBR a été conduite en ?? [c. 2006]

- Normalisation ISO le 9 décembre 2006 [ISO 21127:2006](http://www.iso.org/iso/catalogue_detail?csnumber=34424).

Utilisation
-------

Un modèle conceptuel de référence peut être employé comme une aide intellectuelle pour la formulation d’un modèle de données et son implémentation.

## Exemples d’utilisations

### CIDOC-CRM Best practices

http://www.cidoc-crm.org/best_practices

### Consortium for Open Research Data in the Humanities 

https://docs.cordh.net

### **S**wiss **A**rt **R**esearch **I**nfrastructure project - SARI

https://docs.swissartresearch.net

### Linked Art

https://linked.art


Références
-------

- [Sinclair 2006][ Sinclair, Patrick & al.(2006). “The use of CRM Core in Multimedia Annotation.” Proceedings of First International Workshop on Semantic Web Annotations for Multimedia (SWAMM 2006). URL: http://cidoc.ics.forth.gr/docs/paper16. pdf (checked 2007-11-25)]
- [Theodoridou 2001][Theodoridou, Maria and Martin Doerr (2001). Mapping of the Encoded Archival Description DTD Element Set to the CIDOC CRM, Technical Report FORTH-ICS/TR-289. URL: http:// cidoc.ics.forth.gr/docs/ead.pdf (checked 2007-11-25)]
- CDWA Lite www.getty.edu/research/conducting_research/ standards/cdwa/cdwalite.html (checked 2007-11-25)
- MUSEUMDAT (www.museumdat.org/, checked 2007-11-25)
