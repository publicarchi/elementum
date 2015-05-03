nSaxonOnYourMac
======

Le paquet Saxon contient une collection d’outils destinés à manipuler des documents XML soit sous la forme de processeurs XSLT ou XQuery, soit sous la forme de bibliothèques Java.

Un processeur XSLT est un produit logiciel capable de prendre en entrée un document XML et un programme XSLT et d’exécuter une transformation en fonction de certains paramètres.


## Installer Saxon

Les sources du processeur Saxon sont téléchargeables sur le site de Saxonica à l’adresse suivante : http://saxonica.com/welcome/welcome.xml

La version libre et open-source du processeur Saxon est la version dénommée `saxon9he.jar`.

Un fichier JAR (extension `.jar`)est une archive java exécutable, il contient toutes les classes java du programme.

Saxon étant installé sur votre machine, vous pouvez l’invoquer de la manière suivante :

```bash
java -jar /path/to/saxon.jar path/to/xmlfile.xml path/to/xslfile.xsl
```

- La liste des options disponibles pour une transformation XSLT est présentée à cette adresse : http://www.saxonica.com/documentation/html/using-xsl/commandline.html
- La liste des options disponibles pour une requête XQuery est présentée à cette adresse : http://www.saxonica.com/documentation/html/using-xquery/commandline.html


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


## Placer Saxon dans le CLASSPATH java

Sur mac, le moyen le plus simple de rendre disponibles des fichiers JAR (ou des classes JAVA, fichiers `.class`) pour toutes les applications installées sur une machine, consiste à ajouter ces fichiers dans le répertoire `/Library/Java/Extensions`.

Pour seulement les rendre disponibles pour un utilisateur donné, on peut les placer dans le répertoire `~/Library/Java/Extensions` de l’utilisateur concerné.

http://stackoverflow.com/questions/1675765/adding-to-the-classpath-on-osx

Pour une utilisation avec BaseX, cela suffit à rendre Saxon disponible pour basexhttp si les classes Java sont chargées par le script de lancement qui doit être modifié en conséquence. Sinon, la classe java de Saxon peut-être placée dans le répertoire `lib/` de BaseX.

Il est aussi possible de fixer le classpath directement de la manière suivante :

`export CLASSPATH=/path/to/some.jar:/path/to/some/other.jar`

ou d’ajouter la ligne suivante dans `.bash_profile`
`export CLASSPATH=$CLASSPATH:/Library/Java/Extensions/SaxonHE9-4-0-6J/saxon9he.jar  # put saxon in the path`


en tcsh, ou csh
dans /etc/profile
`setenv CLASSPATH (insert your classpath here)`

`echo $CLASSPASS`
pour afficher la variable d’environnement


------

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

On a mac, we cope doing it putting the Saxon's jar files into `/Library/Java/Extensions/`
Running basexhttp, the expression `xslt:processor()` returns "Saxon" and `xslt:version()` returns "2.0".
