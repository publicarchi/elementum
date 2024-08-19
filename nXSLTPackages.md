---
author: emchateau
tags: xslt
---

# Utiliser des Packages en XSLT

Depuis la version 3 du langage, il est possible d’utiliser des packages en XSLT. 

Plusieurs packages permettent notamment de travailler facilement avec des fichiers JSON ou CSV. Un exemple rudimentaire de package pour manipuler des fichiers CSV est proposé avec la spécification de XSLT 3.0 cf. https://www.w3.org/TR/xslt-30/#csv-example-customizing-parse



## Créer un fichier de configuration

Le processeur XSLT a besoin d’un fichier de configuration pour déterminer où se trouve les packages.

```xml
<!-- config.xml -->
<configuration edition="HE" xmlns="http://saxon.sf.net/ns/configuration">
     <xsltPackages>
          <package name="http://example.com/csv-parser" version="1.0"
               sourceLocation="https://github.com/w3c/xslt30-test/raw/master/tests/decl/package/package-100.xsl"
          />
     </xsltPackages>
</configuration>
```

En ligne de commande avec Saxon, il faut passer les options `-it -xsl:your-xslt-code.xsl -lib:package-file.xsl` ou fournir un fichier de configuration avec `-config:config.xml`.

Sur Oxygen, on peut configurer un fichier de configuration dans les options de la transformation.

### Exemple

```xml
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
   xmlns:xs="http://www.w3.org/2001/XMLSchema"
   xmlns:csv="http://example.com/csv"
   exclude-result-prefixes="xs csv"
   version="3.0">

   <xsl:output indent="yes"/>

   <xsl:use-package name="http://example.com/csv-parser" 
                    package-version="*"/>

   <!-- example input "file"  -->
   <xsl:variable name="input" as="xs:string">
       name,id,postal code
       "Abel Braaksma",34291,1210 KA
       "Anders Berglund",473892,9843 ZD
   </xsl:variable>

   <!-- entry point -->
   <xsl:template name="xsl:initial-template">
       <xsl:copy-of select="csv:parse($input)"/>
   </xsl:template>

</xsl:stylesheet>
```

Cette feuille de transformation utilise un initial-template.

Avec le processeur Saxon, passer le paramètre `-it` avec la valeur `{http://www.w3.org/1999/XSL/Transform}initial-template`

Dans les paramètres de transformation d’Oxygen renseigner la variable `-it` avec `{http://www.w3.org/1999/XSL/Transform}initial-template`

Ou bien de remplacer la déclaration `xsl:initial-template` par le QName directement dans la XSLT.

## Références

- https://stackoverflow.com/questions/60128285/how-to-use-the-xml-csv-parser-package-in-a-transform-namespace-give-invalid-ob