# XQuery

# Caractéristiques

### Langage fonctionnel

### Analogue à SQL

### Basé sur XPath

### Standardisé par le W3C

???
# Caractéristiques

### Langage fonctionnel

### Analogue à SQL

### Basé sur XPath

### Standardisé par le W3C

---

# FLOWR

```xquery
  let $document := fn:doc("tei.xml") 
  for $persName in $document//tei:persName
  where $persName/@id
  order by $persName/@id 
  return $persName/text()
```

---

http://www.tutorialspoint.com/xquery/xquery_quick_guide.htm
