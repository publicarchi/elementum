# XPath Tricks

## Test attribute presence

cf. https://stackoverflow.com/questions/5580372/testing-for-an-xml-attribute

```xml
//*[@src and not(string-length(@src))]
```

This selects all elements in the XML document that have a `src` attribute whose string-value has length of zero.

```xml
//*[@src and string-length(@src)]
```

This selects all elements in the XML document that have a `src` attribute whose string-value has length that is not zero.

```xml
//*[@src and string-length(normalize-space(@src))]
```

This selects all elements in the XML document that have a `src` attribute whose string-value after excluding the starting and ending whitespace has length that is not zero.

```xml
//[not(@src)]
```

This selects all elements in the XML document that don't have a `src` attribute.

Elements having a `@src` attribute which is empty (no string-value):

```xml
//*[@src[not(string())]]
```

Elements having a `@src` attribute which has value (string-value):

```xml
//*[string(@src)]
```

From http://www.w3.org/TR/xpath/#section-String-Functions

> A node-set is converted to a string by returning the string-value of the node in the node-set that is first in document order. If the node-set is empty, an empty string is returned.

From http://www.w3.org/TR/xpath/#function-boolean

> A string is true if and only if its length is non-zero.

## Unescape XML character

```xml
<xsl:template match="text">
  <body>
    <xsl:value-of select="." disable-output-escaping="yes" />
  </body>
</xsl:template>
```
