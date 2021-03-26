---
author: emchateau
since: 2017-07-30
tags: xml, outils, jing, mac
---

# Jing sur mon mac

[Jing](https://github.com/relaxng/jing-trang) est une application qui permet de valider des documents XML contre un schema [RelaxNG](http://relaxng.org) dans les syntaxes XML ou compacte. [Trang](https://github.com/relaxng/jing-trang) est une application de conversion de schémas XML vers ou depuis RelaxNG. Ce sont des logiciels libres et ouverts (licence BSD) écrits en Java par James Clark.

## Pré-requis

Jing fonctionne dans un environnement Java. Avant l’installation, il convient de s’assurer de disposer de Java. L’utilisation de Jing requiert un environnement de développement Java (JDK). La commande suivante permet d’afficher la version de Java disponible dans l’environnement.

```bash
java -version
```

Si Java n’est pas installé, une JDK peut être téléchargée depuis le [site d’Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html). Cf. le [tutoriel Java Divers](nJavaDivers.md) pour un guide sur Mac OS.

## Installation de Jing

Les sources de Jing peuvent être téléchargées à l’adresse suivante : https://github.com/relaxng/jing-trang

## Placer Saxon dans le CLASSPATH java

Sur Mac, le moyen le plus simple de rendre disponibles des fichiers JAR (ou des classes JAVA, fichiers `.class`) pour toutes les applications installées sur une machine, consiste à ajouter ces fichiers dans le répertoire `/Library/Java/Extensions`.

Pour seulement les rendre disponibles pour un utilisateur donné, on peut les placer dans le répertoire `~/Library/Java/Extensions` de l’utilisateur concerné.

http://stackoverflow.com/questions/1675765/adding-to-the-classpath-on-osx

http://www3.ntu.edu.sg/home/ehchua/programming/howto/environment_variables.html

Il est aussi possible de fixer le classpath directement de la manière suivante :

```bash
export CLASSPATH=/path/to/some.jar:/path/to/some/other.jar
```

ou d’ajouter la ligne suivante dans `.bash_profile`

```bash
export CLASSPATH=$CLASSPATH:/Library/Java/Extensions/jing-trang/build/jing.jar  # put jing in the path
```

pour afficher la variable d’environnement :

`echo $CLASSPASS`

## Créer un script

Il est également possible de créer un script shell qui sera disponible dans le PATH. 

```bash
cd /usr/local/bin
echo "java -jar /Library/Java/Extensions/jing-trang/build/jing.jar" | sudo tee saxon # add -a for append
sudo chmod +x saxon
```



## Créer un écrit

## Installaton avec Brew

```bash
brew install jing-trang
```

## Références

- https://github.com/relaxng/jing-trang

- http://relaxng.org/#validators

- [Jing, A Relax NG validator in Java](http://www.thaiopensource.com/relaxng/jing.html)

- http://www.thaiopensource.com/relaxng/

  