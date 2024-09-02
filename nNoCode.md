---
author: emchateau
since: 2024-08-28
tags: outils
---

# Applications Low code - No code

Les applications dites *low code* ou *no code* sont des logiciels qui proposent des interfaces graphiques  pour faciliter la saisie et la gestion de données ou procéder à leur analyse. Ce type de solution a gagné en popularité paryticulièrmeent au tournant des années 2020 avec l’émergence de certains logiciels propriétaires comme [Notion](https://www.notion.so) ou [Air Table](https://www.airtable.com).

En raison de leur polyvalence et de leur facilité d’utilisation, de nombreux chercheurs ont rapidement choisi d’adopter ces logiciels pour la gestion de leur données de recherche. Toutefois, il s’agit d’outils propriétaires qu ne reposent pas sur des formats ou des modèles de donnés standardisés. Les possibilités d’exportation sont parfois incomplètes et l’utilisation de ces logiciels présente des risques sérieux en matière de gestion des données de recherche. Leur généralisation risque de produire une situation comparable à celle que nous avons connu ces dernières années avec l’utilisation du logiciel FileMaker dans la recherche historique.

Il est donc important de pouvoir identifier des solutions alternatives offrant des services comparables tout en garantissant une meilleure pérennité des données.

## Alternatives Open Source à Notion et Air Table

Face au succès des logiciels propriétaires, plusieurs solutions libres et open source ont émergées. Leur développement a été rapide et ces logiciels commencent à offrir des fonctionnalités comparables. Selon les modèles économiques adoptés par leur concepteurs, ces logiciels peuvent être auto-hébergées ou être proposés sous forme de service payant en ligne.

### AppFlowy

> Bring projects, wikis, and teams together with AI. AppFlowy is an AI collaborative workspace where you achieve more without losing control of your data. The best open source alternative to Notion.

- url: https://www.appflowy.io
- code: https://github.com/AppFlowy-IO/AppFlowy/
- Licence: AGPL v3 +
- language: Dart + Rust

### Baserow

Baserow est une application destinée à créer des bases de données et des application sans programmation. Si le logiciel est open source, il ne s’agit pas réellement d’un logiciel libre.

>Create it. Scale it. Own it. The open platform to create scalable databases and applications—without coding.

- url: https://baserow.io
- code: https://gitlab.com/bramw/baserow
- licence: custom
- language: Python

### Espocrm

> EspoCRM is a web application that allows users to see, enter and evaluate all your company relationships regardless of the type. People, companies, projects or opportunities — all in an easy and intuitive interface.

- url: https://www.espocrm.com
- licence: https://github.com/espocrm/espocrm
- licence: GPL V3
- language: PHP

### Grist

>Simple. Flexible. Powerful. A modern, open source spreadsheet that goes beyond the grid.

- url: https://www.getgrist.com
- code: https://github.com/gristlabs/grist-core
- licence: Apache 2.0
- language: TypeScript

### NocoDB

>Build Databases As Spreadsheets : No-Coding Required. NocoDB allows building no-code database solutions with ease of spreadsheets. Bring your own database or choose ours! Millions of rows? Not a problem. Your Data. Your rules. You are in control.

- url: https://nocodb.com
- code: https://github.com/nocodb/nocodb
- licence: AGPL V3
- language: JavaScript

### Mathesar

>Quickly enter and analyze your data – in one open source interface. Mathesar is an **open source** and web-based interface that works on top of your database. You can enter and slice and filter and structure your data… **in minutes**. No technical skills required.

- url: https://mathesar.org
- code: https://github.com/mathesar-foundation/mathesar
- licence: GPL v3
- language: Python + Svelte

### Metabase

>Don’t be a bottleneck. Fast analytics with the friendly UX and integrated tooling to let your company explore data on their own.

- url: https://www.metabase.com
- code: https://github.com/metabase/metabase
- licence: AGPL v3 + divers
- language: Clojure + TypeScript

### Rowy

> Low-code Backend. Manage your database on a spreadsheet-UI and build powerful backend cloud functions, scalably without leaving your browser. Start like no-code, extend with code. 

- url: https://www.rowy.io
- code: https://github.com/rowyio/rowy
- licence: Apache 2.0
- language: TypeScript

## CMS spécialisés pour la recherche historique

### Omeka-S

Omeka-S est un logiciel de gestion de contenu spécialisé pour le domaine patrimonial et culturel développé par le Center for history and new media. Très flexible, le logiciel intègre plusieurs modèles documentaires et des fonctionnalités pour l’utilisation de vocabulaires contrôlés et une compatibilité avec [Zotero](https://www.zotero.org) et [Tropy](https://tropy.org). Il permet une publication partielle des données par l’intermédiaire d’une API.

- url: https://omeka.org/s/
- code: https://github.com/omeka/omeka-s
- licence: GNU GPL v3
- language: PHP (Laminas)

### Arches

Arches est une plateforme de gestion de données open source généraliste pour le partimoine culturel développée par le Getty Conservation Institute et le World Monuments Fund.

- url: https://www.archesproject.org
- code: https://github.com/archesproject/arches
- licence: AGPL3
- language: Python + JavaScript

### Research-Space

Research-Space est un logiciel développé en collaboration entre les historiens de l’art, les conservateurs et les archéologues pour créer un système numérique de documentation de recherche développé par le British Museum et soutenu par la fondation Andrew W. Mellon.

- url: https://www.researchspace.com
- code: https://github.com/researchspace
- licence: AGPL3
- language: TypeScript