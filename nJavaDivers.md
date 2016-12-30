# Java Divers

## Le CLASSPATH en Java

Lorsque l’on travaille avec des applications Java, il est parfois nécessaire de placer certains composants dans le CLASSPATH.

En Java, le CLASSPATH est un chemin vers un répertoire, ou une liste de répertoires, qui est employé par `ClassLoaders` pour trouver et charger les classes dans des programmes Java.

Il est possible de spécifier le classpath soit en utilisant la variable d’environnement `CLASSPATH`, soit avec l’option de ligne de commande `-cp` ou `-classpath` lors de l’exécution d’un fichier JAR, ou bien encore avec l’attribut `Class-Path` dans le `manifest.mf` à l’intérieur d’un fichier JAR.

Source :
http://javarevisited.blogspot.fr/2011/01/how-classpath-work-in-java.html

### Fixer le CLASSPATH sur Windows

1. Aller dans la fenêtre de variables d’environnement en appuyant sur « Windows + Pause » puis « Advanced », « Environment variable » ou directement en faisant un clic droit et choisissant « propriétés », puis « avancées », puis « variable d’environement ».

2. Spécifier votre variable d’environnement `CLASSPATH` et définissez la valeur de votre `JAVA_HOME\lib` en incluant également le répertoire courant (avec le signe point).

3. Vérifiez la valeur du classpath en tappant `echo %CLASSPATH` dans une ligne de commande DOS.

Il est également possible de fixer le classpath avec la ligne de commande suivante :

```bash
  set CLASSPATH=%CLASSPATH%;JAVA_HOME\lib;
```

### Fixer le CLASSPATH sur Unix ou Linux

Il suffit d’inclure la ligne `export CLASSPATH="your classpath"` dans votre `.bash_profile` ou votre `.bashrc` qui sont les scripts lancés lorsque que vous ouvrez une ligne de commande.

Réexécutez les scripts de configuration du terminal pour mettre à jour les variables d’environnement :
```bash
  .  chemin/.bashrc # exécuter à nouveau le .bashrc
```

Vérifier la valeur du classpath
```bash
  echo ${CLASSPATH}
```

Les options `-cp` ou `-classpath` surchargent la variable d’environnement lors du lancement d’un programme java. C’est la manière la plus facile pour utiliser  différents classpath pour différentes applications Java qui fonctionnent sur la même machine.

La manière standard de définir un classpath pour une application Java consiste à créer un script de démarrage du programme Java et de fixer le classpath de la manière suivante :

```bash
  CLASSPATH=/home/tester/classes
  java -cp $CLASSPATH Test
```
Par défaut, le CLASSPATH Java pointe vers le répertoire courant dénoté par `.` et il cherchera n’importe quelle classe dans le répertoire courant.


## Les fichiers JAR

Les fichiers JAR en java sont des sortes d’archive compressées comme zip qui comportent tous les composants d’une application Java y compris les fichiers de classes, les ressources telles que les images, et un fichier de manifeste optionnel.

JAR signifie « Java ARchive », c’est une manière commode de délivrer des programmes ou des librairies Java. Il est possible d’exécuter un fichier JAR avec n’importe quel système d’exploitation qui dispose de la bonne version de Java.


## Java 8 sur Mac OSX 10.9.5

À partir de Mac OSX 10.8, l’installation par défaut de la JDK se fait dans le répertoire suivant :
`/System/Library/Java/`

Structuration du répertoire :
Java
-- Extensions
-- JavaVirtualMachines
-- -- 1.8.0_11.jdk
-- Support

liens dans usr/bin/
vers jar, jarsigner, java, javac, javadoc, javah, javap, javaws, jcmd, jcondole, jdb, jhat, jinfo, jmap, jmc, etc.

<file:///usr/share/java/Stubs/AppleJavaExtensions.jar>


## Installation de JDK 8 (Mac OSX)

Pour exécuter BaseX en mode serveur ou d’autres programmes, vous pourriez avoir besoin du Java Development Kit de la version 8. Ce programme n’est pas distribué par défaut avec Mac OSX.

- Télécharger Java Development kit version 8
- Allez sur la page http://www.oracle.com/technetwork/java/javase/downloads/index.html
- Cliquez sur le bouton « Download » sous JDK
- Dans le nouvel écran, cochez la case « Accept Licence agreement »
- Puis choisissez la version appropriée à télécharger dans la liste.
Sur Mac OS X, sélectionnez `x64	221.98 MB  jdk-8u45-macosx-x64.dmg`
- Ouvrez l’image disque téléchargée (nommé quelque chose comme  `jdk-8u45-macosx-x64.dmg`)
- Dans la fenêtre qui s’ouvre, exécutez le programme d’installation en double-cliquant sur l’icône en forme de paquet.
- Suivre les instructions du programme d’installation de JDK

**Et voilà !**


sh ./basexhttp
