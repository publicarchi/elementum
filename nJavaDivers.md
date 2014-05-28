Le CLASSPATH en Java
========

Lorsque l'on travaille avec des applications Java, il est parfois nécessaire de placer certains composants dans le CLASSPATH.

En Java, le CLASSPATH est un chemin vers un répertoire ou une liste de répertoire qui est employé par `ClassLoaders` pour trouver et charger les classes dans des programmes Java.

Il est possible de spécifier le classpath en utilisant la variable d'environnement `CLASSPATH`, ou l'option de ligne de commande `-cp` ou `-classpath` ou encore l'attribut `Class-Path` dans le `manifest.mf` à l'intérieur d'un fichier JAR.

Source :
http://javarevisited.blogspot.fr/2011/01/how-classpath-work-in-java.html


### Fixer le CLASSPATH sur Windows

1. Aller dans la fenêtre de variables d'environnement en appuyant sur "Windows + Pause" puis "Advanced", "Environment variable" ou directement en faisant un clic droit et choisissant "propriétés", puis "avancées", puis "variable d'environement".
2. Spécifier votre variable d'environnement `CLASSPATH` et définissez la valeur de votre `JAVA_HOME\lib` en incluant également le répertoire courant (avec le signe point).
3. Vérifiez la valeur du classpath en tappant `echo %CLASSPATH` dans une ligne de commande DOS.

Il est également possible de fixer le classpath avec la ligne de commande suivante :

set CLASSPATH=%CLASSPATH%;JAVA_HOME\lib;


### Fixer le CLASSPATH sur UNIX ou Linux

Il suffit d'inclure la `ligne export CLASSPATH="your classpath"` dans votre .bash_profile ou votre .bashrec qui sont les scripts lancés dès que vous ouvrez une ligne de commande.

Pour vérifier la valeur du classpath, tapez `echo ${CLASSPATH}`

Il est possible de surcharger la variable d'environnement en fournissant l'option -cp ou -classpath en lançant un programme java. C'est la manière la plus aisée d'avoir différents classpath pour différentes applications Java fonctionnant sur la même machine.

La manière standard de définir un classpath pour une application Java est donc de créer un script de démarrage du programme Java et de fixer le classpath de la manière suivante :

```bash
CLASSPATH=/home/tester/classes
java -cp $CLASSPATH Test
```
Par défaut le CLASSPATH Java pointe vers le répertoire courant dénoté par `.` et il cherchera n'importe quelle classe dans le répertoire courant.

Les fichiers JAR
=========

Les fichiers JAR en java sont des sortes d'archive compressées comme zip qui comportent tous les composants d'une application Java y compris les fichiers de classes, les ressources telles que les images, et un fichier de manifeste optionnel.

JAR signifie Java ARchive et constitue une manière de délivrer des programmes ou des librairies java. Il est possible d'exécuter un fichier JAR avec n'importe quel système d'exploitation disposant de Java.
