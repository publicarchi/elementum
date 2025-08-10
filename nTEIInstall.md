---
author: emchateau
tags: tei
---

# Installation de la TEI sur Mac

Les sources de la TEI sont distribuées par l’intermédiaire de GitHub. Qu’il s’agisse de contribuer au projet de la TEI ou bien de pouvoir utiliser les outils développés par la TEI, il peut être intéressant de construire la TEI sur son propre ordinateur. L’installation est relativement aisée sur un système Linux, elle est toutefois plus complexe sur un Mac.

La première chose à faire consiste à installer les sources sur son ordinateurs. On téléchargemera notamment pour commencer les Guidelines et les XSL Stylesheets. Il peut être commode de garder ces dossiers à proximité dans un répertoire local `TEIC`.

Installer les sources dans un répertoire `TEIC` dans le répertoire utilisateur.

```bash
cd ~
mkdir TEIC
cd TEIC
```

```bash
git clone https://github.com/TEIC/TEI.git
```

```bash
git clone https://github.com/TEIC/Stylesheets.git
```

La TEI dispose d’un environnement de test avec docker. Sur Mac, le plus simple est d’installer Docker Desktop https://docs.docker.com/desktop/install/mac-install/

Utilities/lib/jing.jar:Utilities/lib/saxon10he.jar

/Utilities/lib/trang.jar

Suivre le tutoriel, puis exécuter make dans Stylesheet.

Pour pouvoir utiliser les conversions, ajouter le répertoire bin de Stylesheet à votre path.

Afin de fonctionner les transformations utilisent ANT qui doit être installé sur votre ordinateur.

```bash
brew install ant
```

```
brew install jing-trang
```

```
brew install saxon
```

- ant
- jing
- perl
- saxon
- trang
- xmllint
- xsltproc

## Sources

- https://tei-c.org/tools/
- How to build and test the Guidelines and Stylesheets, http://teic.github.io/TCW/testing_and_building.html