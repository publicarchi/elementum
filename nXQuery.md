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

## Littéraux

1

'test'

string(16+1)

concat((16+1),  1)

fn:concat('test', 'ajout')

'e' || 1

1 = 2

```
if (1 = 1)
  then 'oui'
  else 'non'
```



# FLOWR

```
let $msg := 'Hello World !'
return $msg
```

```
let $seq := (3, 2, 1)
for $i in $seq
return $i + 1
```

```
let $seq := (3, 2, 1)
for $i in $seq
order by $i
return $i 
```

```
let $seq := (3, 2, 1)
for $i in $seq
order by $i ascending
return $i 
```

```
let $seq := (3, 2, 1)
for $i in $seq
order by $i descending
return $i 
```



```xquery
  let $document := fn:doc("tei.xml")
  for $persName in $document//tei:persName
  where $persName/@id
  order by $persName/@id
  return $persName/text()
```



```xquery
for $i in (1, 2, 3)
return $i
```

```xquery
for $i in (1, 2, 3)
return $i * $i
```





```xquery
for $i in (1, 2, 3)
return if ($i mod 2 = 0) then $i * $i
```



```xquery
for $i in (1, 2, 3)
return if ($i mod 2) then $i * $i
```





---

http://www.tutorialspoint.com/xquery/xquery_quick_guide.htm

https://www.ibm.com/docs/en/db2-for-zos/11?topic=zos-xml
