---
tags: xslt
---

# Trucs XSLT

Questions : comment systématiser les liens vers les références

- https://www.w3.org/TR/xslt20/#element-result-document et versions ?
- https://www.saxonica.com/documentation9.5/xsl-elements/result-document.html

## Exécution d’une XSLT sur plusieurs fichiers avec XSLT 2.0

Avec XSLT 2.0, il est possible d’utiliser la fonction [`fn:collection()`](https://www.w3.org/TR/xpath-functions-31/#func-collection)

```xml
<xsl:stylesheet version="2.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:fn="http://www.w3.org/2005/xpath-functions">
<xsl:template match="/">
    <xsl:for-each select="fn:collection(concat('file:///c:/filesarehere', '?select=*.xml;recurse=yes'))">
        <!--process nodes-->
    </xsl:for-each>
</xsl:template>
```

Lorsque l’on souhaite directement travailler sur des listes de fichiers, il peut être intéressant d’utiliser un initial-template avec `<xsl:template name="main">` comme point d’entrée et `-it:main` en ligne de commande pour éviter d’avoir un document d’entrée inutile pour `match="/"`.

Il est possible de renommer les fichiers avec l’instruction [`xsl:result-document`](https://www.w3.org/TR/xslt20/#element-result-document).

```xml
<xsl:template name="main">
  <xsl:for-each select="collection('file:///D:/hdbook-Convertor/input/?recurse=yes;select=*.xml')">
    <xsl:result-document href="output/{tokenize(document-uri(.), '/')[last()]">
      <xsl:apply-templates/>
    </xsl:result-document>
  </xsl:for-each>
</xsl:template>
```

Avec Saxon, pour créer un fichier de sortie pour chaque fichier d’entrée avec un nom correspondant, il est possible d’utiliser les options `-s:inputDir` and `-o:outputDir` en ligne de commande pour traiter tous les fichiers du répertoire. Mais cela ne permet que de s’occuper des fichiers XML. Contrôler le processus en utilisant la fonction `fn:collection()` est plus flexible.

Depuis 2015, EXPtah a spécifié un [File Module](https://expath.org/spec/file) qui est souvent implémenté par les processeurs.

### Références

- [How to run Saxon XSLT for all the files in the folder (Stack Overflow)](https://stackoverflow.com/questions/28724503/how-to-run-saxon-xslt-for-all-the-files-in-the-folder)
- [Making multiple files from multiple files with one command in gnu make (Stack Overflow)](https://stackoverflow.com/questions/14914870/making-multiple-files-from-multiple-files-with-one-command-in-gnu-make)

