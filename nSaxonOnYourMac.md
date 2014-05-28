nSaxonOnYourMac
======

http://stackoverflow.com/questions/1675765/adding-to-the-classpath-on-osx

If you want to make a certain set of JAR files (or .class files) available to every Java application on the machine, then your best bet is to add those files to /Library/Java/Extensions.

Or, if you want to do it for every Java application, but only when your Mac OS X account runs them, then use ~/Library/Java/Extensions instead.

EDIT: If you want to do this only for a particular application, as Thorbjørn asked, then you will need to tell us more about how the application is packaged.

Cela rend Saxon disponible pour basexhttp

Normalement, il est également possible de ficher le classpath directement

`export CLASSPATH=/path/to/some.jar:/path/to/some/other.jar`
mais nous n'y sommes pas parvenu

Or you can add to the existing classpath like this:

export CLASSPATH=$CLASSPATH:/path/to/some.jar:/path/to/some/other.jar

This is answering your exact question, I'm not saying it's the right or wrong thing to do; I'll leave that for others to comment upon.


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
