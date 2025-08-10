---
author: emchateau
tags: xslt, csv
---

# XSLT et CSV

Dans sa version 3, XSLT ne propose pas de traitement par défaut pour CSV. Il est toutefois possible d’utiliser des package pour travailler avec XSLT.

```xml
<?xml version="1.0"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
<xsl:output method="text" encoding="iso-8859-1"/>
<xsl:strip-space elements="*" />

<xsl:template match="/*/child::*">
<xsl:for-each select="child::*">
<xsl:if test="position() != last()"><xsl:value-of select="normalize-space(.)"/>,    </xsl:if>
<xsl:if test="position()  = last()"><xsl:value-of select="normalize-space(.)"/><xsl:text>&#xD;</xsl:text>
</xsl:if>
</xsl:for-each>
</xsl:template>

</xsl:stylesheet>
```

```xml
<?xml version="1.0" encoding="UTF-8"?>

<xsl:template match="property">
  <xsl:variable name="property" select="."/>
  
  <!-- Loop through the columns in order  -->
  <xsl:for-each select="document('')/*/csv:columns/*">
    <!-- Extract the column name and value  -->
    <xsl:variable name="column" select="."/>
    <xsl:variable name="value" select="$property/*[name() = $column]"/>
    
    <!-- Quote the value if required -->
    <xsl:choose>
      <xsl:when test="contains($value, '&quot;')">
        <xsl:variable name="x" select="replace($value, '&quot;',  '&quot;&quot;')"/>
        <xsl:value-of select="concat('&quot;', $x, '&quot;')"/>
      </xsl:when>
      <xsl:when test="contains($value, $delimiter)">
        <xsl:value-of select="concat('&quot;', $value, '&quot;')"/>
      </xsl:when>
      <xsl:otherwise>
        <xsl:value-of select="$value"/>
      </xsl:otherwise>
    </xsl:choose>
    
    <!-- Add the delimiter unless we are the last expression -->
    <xsl:if test="position() != last()">
      <xsl:value-of select="$delimiter"/>
    </xsl:if>
  </xsl:for-each>
  
  <!-- Add a newline at the end of the record -->
  <xsl:text>&#xa;</xsl:text>
</xsl:template>

</xsl:stylesheet>
```



### Outils

https://github.com/fordfrog/xml2csv

https://stackoverflow.com/questions/365312/xml-to-csv-using-xslt

https://pragmaticintegrator.wordpress.com/2012/10/28/transforming-xml-to-csv-via-xslt/