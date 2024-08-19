---
title: Installer le processeur Saxon sur Mac
tags: saxon, java, mac, outils, xslt
---

# Installer Saxon sur son Mac

Le paquet Saxon contient une collection d’outils destinés à manipuler des documents XML soit sous la forme de processeurs XSLT ou XQuery, soit sous la forme de bibliothèques Java.

Un processeur XSLT est un produit logiciel capable de prendre en entrée un document XML et un programme XSLT et d’exécuter une transformation en fonction de certains paramètres. Un processeur XQuery est quant à lui un logiciel capable d’interpréter des requêtes sur des documents XML. Ces deux langages ont l’avantage de reposer entièrement sur le modèle de données XML Data Model. Le processeur Saxon permet de pleinement bénéficier de l’expressivité des langages XML dans le cadre de la manipulation de données XML. Il s’agit actuellement du processeur XSLT libre et open source le plus avancé disponible sur le marché, il est notamment compatible avec les versions 2 et 3 du langage.

## Pré-requis

Saxon est un logiciel qui fonctionne dans un environnement Java. L’utilisation de Saxon requiert un environnement de développement Java (JDK). La commande suivante permet d’afficher la version de Java disponible dans l’environnement.

```bash
java -version
```

Si Java n’est pas installé, une JDK peut être téléchargée depuis le [site d’Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html). Cf. le tutoriel [Java Divers](nJavaDivers.md) pour un guide sur Mac OS.

## Installer Saxon

Les sources du processeur Saxon sont téléchargeables depuis le site de [Saxonica](http://www.saxonica.com/download/download_page.xml).

La version libre et open-source du processeur Saxon est la version dénommée `saxon9he.jar`. 

Un fichier JAR (extension `.jar`) est une archive java exécutable, il contient toutes les classes java du programme. 

Lorsque Saxon est installé sur une machine, on peut l’invoquer de la manière suivante :

```bash
java -jar /path/to/saxon.jar path/to/xmlfile.xml path/to/xslfile.xsl
```

- La liste des options disponibles pour une transformation XSLT est présentée à cette adresse : http://www.saxonica.com/documentation/html/using-xsl/commandline.html
- La liste des options disponibles pour une requête XQuery est présentée à cette adresse : http://www.saxonica.com/documentation/html/using-xquery/commandline.html


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
export CLASSPATH=$CLASSPATH:/Library/Java/Extensions/SaxonHE9-5-1-6J/saxon9he.jar  # put saxon in the path
```

pour afficher la variable d’environnement :

`echo $CLASSPASS`

Pour une utilisation avec [BaseX](http://basex.org), cela suffit pour rendre Saxon disponible pour basexhttp si les classes Java sont chargées par le script de lancement qui doit être modifié en conséquence. Sinon, la classe java de Saxon peut-être directement placée à l’intérieur du répertoire `lib/` de BaseX.

## Créer un alias

Afin d’invoquer facilement Saxon en ligne de commande, le plus simple est de créer un alias dans son fichier `.bash_profile`

```bash
alias saxon='java -jar /Library/Java/Extensions/SaxonHE9-5-1-6J/saxon9he.jar'
```

Il est désormais possible d’exécuter Saxon avec l’alias `saxon` en lui passant les paramètres nécessaires.

Par exemple, on exécute la classe de la manière suivante

```bash
saxon -o:fichierRésultat.html source.xml programme.xsl
```

## Créer un script

Il est également possible de créer un script shell qui sera disponible dans le PATH. 

```bash
cd /usr/local/bin
printf '%s\n' '#!/bin/sh' 'java -jar /Library/Java/Extensions/SaxonHE9-5-1-6J/saxon9he.jar "$@"' | sudo tee saxon # add -a for append
sudo chmod +x saxon
```

(

Voir si l’alternative ci-dessous ne serait pas préférable ?

```bash
#!/bin/sh
exec java -cp /usr/share/java/saxon9he.jar net.sf.saxon.Query "$@"
```

)

Dès lors les options sont passées sous la forme suivante :

```bash
saxon [options] [params] # pour `java  -jar dir/saxon9he.jar [options] [params]`
```

On peut plus spécifiquement adresser des les différentes classes de saxon pour des transformations XSLT ou XQuery.

Le processeur XQuery peut être invoqué depuis la ligne de commande ou à travers une API dans une application développée par l’utilisateur.

```bash
java net.sf.saxon.Query [options] -q:queryfile [ params...] ## XQuery invocation
```

Invocation d’une transformation XSL.

```bash
java net.sf.saxon.Transform -s:source -xsl:stylesheet -o:output # XSLT transform invocation
```

- Voir la [documentation](http://www.saxonica.com/documentation/index.html#!using-xsl/commandline) des options et des paramètres pour XSLT.
- Voir la [documentation](http://www.saxonica.com/documentation/index.html#!using-xquery/commandline) des options et des paramètres pour XQuery.

## Installer Saxon avec Homebrew

Il existe une formule Homebrew pour Saxon qui peut faciliter l’installation sur un mac.

http://brewformulas.org/Saxon

## pour linux

http://saxon.sourceforge.net/saxon7.0/api-guide.html

http://www.saxonica.com/welcome/welcome.xml

`java -cp c:\saxon\saxon9he.jar net.sf.saxon.Query -t -qs:current-date()`

Pour exécuter une XSLT :

`java -cp saxon9he.jar net.sf.saxon.Transform -t -s:samples\data\books.xml
     -xsl:samples\styles\books.xsl -o:c:\temp.html``

Pour exécuter une requête XQuery :

`java -cp saxon9he.jar net.sf.saxon.Query -t -s:samples\data\books.xml -q:samples\query\books-to-html.xq >c:\temp.html`


## How to change processor to Saxon in BaseX

On a mac, we cope doing it putting the Saxon’s jar files into `/Library/Java/Extensions/`
Running basexhttp, the expression `xslt:processor()` returns "Saxon" and `xslt:version()` returns "2.0".

## Divers

Il faut noter qu’une version de Saxon a été portée en C et est disponible dans un environnement node.

https://www.npmjs.com/package/saxon-node

## Références

- [Saxonica, Getting started with Saxon on the Java platform](http://www.saxonica.com/html/documentation/about/gettingstarted/gettingstartedjava.html)
- [Installing Saxon-HE 9.3 manually on Lucid Lynx](http://johnbokma.com/mexit/2011/07/04/installing-saxon-he-ubuntu.html)
- http://www.sagehill.net/docbookxsl/InstallingAProcessor.html