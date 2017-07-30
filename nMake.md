---
since: 2017-07-28
author: emchateau
tags: make
---

La popularité des outils de préprocessing pour la rédaction des CSS a rendu très populaire l’utilisation d’outils d’automatisation de tâches dans le développement front-end. [Grunt](http://gruntjs.com/) et [Gulp](http://gulpjs.com/) sont certainement parmi les plus populaires d’entre eux. Il reste néanmoins toujours possible d’employer [GNU Make](http://www.gnu.org/software/make/) et ce choix peut, dans bien des cas, s’avérer préférable pour plusieurs raisons.

- Make tire parti de la puissance du Shell UNIX et est un outil très versatile
- Il est déjà disponible dans de nombreux environnement des utilisateurs
- Il dispose de tous les outils nécessaires sans nécessité d’avoir à gérer des modules et leur dépendances.

## Définition de cibles

Une bonne utilisation de Make consiste à définir des cibles couplées avec des pré-requis, de sorte que Make ne construise des nouveaux fichiers seulement quand les sources ont changées. On peut y parvenir en utilisant le dommage des tâches pour définir des cibles.

```bash
setup:
    bower install
    mkdir -p htdocs/assets/css
    mkdir -p htdocs/assets/js
```

## Utilisation de cibles et de pré-requis

Afin de tirer parti de tout le potentiel de Make, il convient de définir les résultats désirés sous forme de cibles de construction. Leur pré-requis (ou dépendances), et les recettes pour résoudre ces dépendances, et parvenir à la sortie attendue.

L’exemple suivant comporte une règle très simple qui est la construction de base d’une règle Makefile.

```bash
htdocs/robots.txt: support-files/robots.txt
    cp support-files/robots.txt htdocs/robots.txt
```

La première ligne définit la cible (*target*). Après les deux points, viennent les pré-requis. Lorsque Make parse ce Makefile, il lira cette règle et l’interprétera sous la forme "si la source a été modifiée depuis que la cible a été généré, alors re-génère la cible." Pour régénérer la cible, make exécute les lignes indentées avec une tabulation sous la paire `target: source`, appelée recette (*recipe*).

 ! Attention les recettes des Makefile doivent être intentées avec des tabulation

## Utilisation de variables automatiques

Make définit également plusieurs [variables automatiques](http://www.gnu.org/software/make/manual/make.html#Automatic-Variables). Celles-ci sont les plus souvent utilisées :

-  `$@` le nom de fichier cyble
- `$<` le nom de fichier du premier pré-requis
- `$?` une liste séparée par des espaces de tous les pré-requis

En utilisant ces variables automatiques, l’exemple précédent devient alors :

```bash
htdocs/robots.txt: support-files/robots.txt
    cp $< $@
```

On peut par exemple encore améliorer cette règle en introduisant des motifs dans la cible et les pré-requis.

```bash
htdocs/%.txt: support-files/%.txt
    cp $< $@
```

Cette fois-ci, Make copiera tous les fichiers textuels compris dans le répertoire `htdocs` à l’intérieur du répertoire `support-files`, mais à condition que les fichiers sources aient changé.

## Compiler des fichiers SASS

Mettons que nos fichiers sont contenus dans un sous-répertoire `css` placé dans un répertoire `assets`, et que le résultat compilé doit être servi sur un serveur http depuis le répertoire `htdocs`. Voici une règle Make pour générer les CSS depuis les sources SAAS en utilisant SassC.

```bash
htdocs/css/%.css: assets/css/%.scss
    sassc -t compressed -o $@ $?
```

Une recette avec une seule commande, et un seul pré-requis qui indique à Make "Si la source SASS est plus récente que les fichiers cibles construits, exécute la commande `sassc` avec la cible `$@` fournie comme sortie (option `-o`) et le pré-requis comme source."

Pour éviter l’affichage des commandes et sorties, il est possible de préfixer les commandes par `@` afin de les rendre silencieuses. On en profite pour améliorer la recette.

```bash
htdocs/css/%.css: assets/css/%.scss
    @echo Compiling $@
	@mkdir -p $(@D)
    @sassc -t compressed -o $@ $?
    @node_modules/.bin/autoprefixer $@
```

Le Make précédent exécute les commandes suivantes :

- afficher le nom des fichiers de destinations pour voir ce qui est compilé
- créer le répertoire de sortie s’il n’existe pas (en incluant ses sous-répertoires !). On emploie ici une nouvelle variable automatique `$(@D)`, le répertoire du fichier cible
- compiler les CSS depuis les sources SASS
- utiliser autoprefixer pour ajouter tous les préfixes de vendeur à la CSS 

La même approche peut être utilisée pour minifier du JavaScript ou transpiler du code CoffeeScript ou ES6.

```bash
htdocs/js/%.js: assets/js/%.js
    @echo Processing $@
	@mkdir -p $(@D)
    @node_modules/.bin/jsmin --level 2 --output $@ $?
```

Dans les deux cas, les exemples utilisent node car cet environnement dispose des meilleurs outils pour l’environnement front-end. Il n’est pour autant pas nécessaire d’envelopper ces modules nodes avec Grunt ou Gulp et les lancer dans un autre programmes node dans sa propre syntaxe.

## Pré-requis multiples

Dans de nombreux projets SASS les variables peuvent être définies dans un fichier qui doit être importé dans les autres fichiers SASS. Il faut donc tenir compte des dépendances globales dans cet exemple de compilation.

```bash
htdocs/css/%.css: assets/css/%.scss assets/css/_settings.scss
    @echo Compiling $@
	@mkdir -p $(@D)
    @sassc -t compressed -o $@ $<
    @node_modules/.bin/autoprefixer $@
```

On a simplement ajouté ici le fichier `_settings.scss` à la liste des pré-requis, et changé l’appel de la commande `sassc` pour qu’elle utilise le premier nom de fichier pré-requis (`$`) comme entrée au lieu de l’ensemble de la section pré-requis. Désormais, si les fichiers correspondant au premier filtre ou les fichiers de réglages sont modifiés, les fichiers CSS seront compilés.

Comme le motif utilisé dans les pré-requis peut correspondre à des sous-répertoires, il est nécessaire de s’assurer que ces sous-répertoires existent dans le répertoire cible. Les exemples ci-dessus emploient la variable automatique `$(@D)` pour créer ces répertoires, mais l’appel du shell avec `$(shell basedir $@)` aurait donné le même résultat.

## Utilisation de variables

Il peut être nécessaire de réduire la répétition des liens dans le cas où l’on aurait à modifier la structure du projet. Ce qui peut facilement être obtenu en utilisant des variables.

```bash
SASS_SRC := assets/css
JS_SRC   := assets/js
CSS_DIR  := htdocs/css
JS_DIR   := htdocs/js
BIN      := node_modules/bin

$(CSS_DIR)/%.css: $(SASS_SRC)/%.scss $(SASS_SRC)/_settings.scss
    @echo Compiling $@
    @mkdir -p $(@D)
    @sassc -t compressed -o $@ $<
    @$(BIN)/autoprefixer $@

$(JS_DIR)/%.js: $(JS_SRC)/%.js
    @echo Processing $@
    @mkdir -p $(@D)
    @$(BIN)/jsmin --level 2 --output $@ $?
```

L’opérateur `:=` affecte une variable, et ces variables peuvent être utilisées dans Make entre parenthèses et préfixées avec le `$`.

## Bash au bout des doigts

L’un des avantages principaux de Make est de pouvoir disposer immédiatement des outils GNU de base. Par exemple pour sauvegarder les utilisateurs, ou les multiples requêtes HTTP utilisées par nos pages web, etc.

```bash
JS_LIB_FILE := $(JS_DIR)/libs.js
JS_LIBS := bower_components/jquery/dist/jquery.min.js \
    bower_components/lodash/dist/lodash.min.js \
    bower_components/fooqux/dist/fooqux.min.js

$(JS_LIB_FILE): $(JS_LIBS)
    cat $? > $@
```

Ici, si l’une de ces librairies change (par exemple lorsque de nouvelles versions deviennent disponibles avec bower), le fichier `libs.js` sera lui-aussi mis à jour.

Pour finir, voici un exemple plus compliqué qui, tout en continuant d’employer des outils standards, est destiné à générer un manifeste de tous les noms de fichiers et un checksums de ces fichiers.

```bash
DIST := htdocs/assets

# if any compiled assets changes, regenerate the manifest
$(DIST)/.manifest: $(shell find $(DIST) -type f -name '*.css' -or -name '*.js')
    find $(DIST) -type f -exec cksum {} \; | sed -e "s#$(DIST)/##" | cut -f1,3 -d" " > $@
```

## Remarques

Les répertoires créés avec l’option -p se voient données des permissions complète rwx (chmod -R 777), il faut donc être vigilant si les fichiers doivent être servis directement sur le web.

L’un des principaux inconvénients de Make est de ne pas être multiplateforme. Un collaborateur sous Windows aura des difficultés à travailler avec de tels fichiers.

## Références

https://www.sitepoint.com/using-gnu-make-front-end-development-build-tool/

http://www.gnu.org/prep/standards/html_node/Makefile-Conventions.html

http://www.gnu.org/software/make/manual/make.html

https://blog.jcoglan.com/2014/02/05/building-javascript-projects-with-make/ cf. https://github.com/jcoglan/bake/blob/master/Makefile