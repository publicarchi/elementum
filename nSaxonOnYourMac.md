nSaxonOnYourMac
======

Sur mac, le moyen le plus simple de rendre disponibles des fichiers JAR (ou des fichiers .class) pour toutes les applications installées une machine, il suffit d'ajouter ces fichiers dans le répertoire `/Library/Java/Extensions`.

Pour seulement les rendre disponibles pour un utilisateur donner, les placer dans le répertoire `~/Library/Java/Extensions` de l'utilisateur concerné.

http://stackoverflow.com/questions/1675765/adding-to-the-classpath-on-osx

Cela rend Saxon disponible pour basexhttp

Normalement, il est également possible de fixer le classpath directement de la manière suivante :

`export CLASSPATH=/path/to/some.jar:/path/to/some/other.jar`
mais nous n'y sommes pas parvenu

Or you can add to the existing classpath like this:

export CLASSPATH=$CLASSPATH:/path/to/some.jar:/path/to/some/other.jar


en tcsh, ou csh
dans /etc/profile
`setenv CLASSPATH (insert your classpath here)`

`echo $CLASSPASS`
pour afficher la variable d'environnement


------

pour linux

http://saxon.sourceforge.net/saxon7.0/api-guide.html

http://www.saxonica.com/welcome/welcome.xml

java -cp c:\saxon\saxon9he.jar net.sf.saxon.Query -t -qs:current-date()

for XSLT (all on one line):

`java -cp saxon9he.jar net.sf.saxon.Transform -t -s:samples\data\books.xml
     -xsl:samples\styles\books.xsl -o:c:\temp.html``

for XQuery (all on one line):

`java -cp saxon9he.jar net.sf.saxon.Query -t -s:samples\data\books.xml -q:samples\query\books-to-html.xq >c:\temp.html`

basex-talk@mailman.uni-konstanz.de

How to change processor to Saxon

Using basex for TEI-XML file, allows to profit from the Java environement and to use XSLT 2.0.
We didn't cope with putting Saxon in the Classpath for basex.

Is there any simple steps doing it ?

On a mac, we cope doing it putting the Saxon's jar files into `/Library/Java/Extensions/`
Running basexhttp, the expression `xslt:processor()` returns "Saxon" and `xslt:version()` returns "2.0".

On an ubuntu machine there is no such directory. But we've first tried to set the CLASSPATH with `export CLASSPATH=/usr/share/java/saxon9he.jar` (and various other things) unhopely without success.

Your help would be very welcome !
