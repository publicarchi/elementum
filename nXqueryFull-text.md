---
author: emchateau
tags: xquery
---

# Recherche full-text avec XQuery



## Exemple de requête croisée

```xquery
for $x in doc('Documents')/Docs/Doc[. contains text 'Tom' ftand ftnot 'jerry'] 
```

Cette requête est longue à exécuter car elle est exécutée sur tous les contenus textuels de l’élément `Doc` comme s’ils avaient été concaténés en une seule chaîne. Cela ne peut pas actuellement être réalisé par BaseX qui indexe chaque nœud texte séparément.

Il est possible de parvenir à peu près au même résultat en réalisant les recherches plein-texte pour chaque terme séparément puis en mélangeant les résultats.

```xquery
for $x in (doc('Documents')/Docs/Doc[.//text() contains text 'Tom']
            except doc('Documents')/Docs/Doc[.//text() contains text 'Jerry'])
return $x/Name
```

La requête est alors réécrite pour être optimisée par BaseX

```xquery
for $x in (db:fulltext("Documents", "Tom")/ancestor::*:Doc
            except db:fulltext("Documents", "Jerry")/ancestor::*:Doc)
return $x/Name
```

Il est alors possible, de choisir l’ordre de mélange pour garder les résultats intermédiaires peu nombreux.

https://stackoverflow.com/questions/14955164/xquery-full-text-search-with-word1-and-not-word2

## Recherche sur les contenus mixtes

Les documents textuels XML tels que HTML, TEI ou DocBook contiennent typiquement des contenus mixtes, c’est-à-dire des éléments qui contiennent un mélange de texte et de balises.

Dans ces cas là, le flux textuel n’est pas interrompu par les éléments fils qui servent seulement à baliser par exemple la mise en forme ou des entités-nommées. Lors d’une recherche plein-texte, on souhaitera typiquement réaliser la recherche sans tenir compte de ces éléments.

cf. [XQuery and XPath Full Text 1.0 Use Cases](http://www.w3.org/TR/xpath-full-text-10-use-cases/#Across). 

Pour résoudre ces cas de figure, la spécification de XQuery Full-text définit une option pour ignorer ces contenus mixtes, `without content` [W3C XQuery Full Text 1.0](http://www.w3.org/TR/xpath-full-text-10/#ftignoreoption).

Cette option n’est malheureusement pas encore supportée par BaseX

## Réalisation de recherche sur des contenus mixtes avec BaseX

Pour rendre ce genre de recherches possibles avec BaseX, il est recommandé de :

- conserver les espaces lors de l’importation des documents
- ne pas indenter automatiquement les documents

Une requête du type :

```xquery
//p[. contains text 'real text'] 
```

fonctionne, toutefois elle n’utilise pas les indexes plein-texte. 

Pour employer les index, il faudrait réécrire la requête de la manière suivante :

```xquery
//p[text() contains text 'real text']
```

mais dans ce cas, le texte correspondant est morcelé en plusieurs nœuds textes.

Comme BaseX ne supporte pas encore l’option `without content` de la spécification XQuery Full Text, il est nécessaire de créer une seconde base de données en excluant les contenus mixtes.

### Exemple

https://stackoverflow.com/questions/11791349/what-is-the-difference-between-these-two-xqueries

```xquery
ft:count(doc('BHCR')/Datas/Data/Desc[. contains text 'revolution'])
```

```xquery
ft:count(doc('BHCR')/Datas/Data/Desc[text() contains text 'revolution'])
```

Différences

In your first query, the context item `.` will lead to a merge of all text nodes of an element (i.e., to the creation of its *string value*), which will then be used to find full-text tokens. This merge can result in new keywords. As an example,  the following query will return  true...

```xml
<xml><b>H</b>i</xml>/. contains text 'hi'
```

..where as The following query will return true...

```xml
<xml><b>H</b>i</xml> contains text 'hi'
```

As the new keywords cannot be stored in the full-text index, no index access takes place, and the query will take much longer.

Your second query will return all `Desc` elements that have `revolution` in their child text nodes. If you want to parse all descending texts of the `Desc` elements, the following query will give you the expected results:

```xml
ft:count(doc('BHCR')/Datas/Data/Desc[.//text() contains text 'revolution']
```

The [Full Text: Mixed Context](http://docs.basex.org/wiki/Full-Text#Mixed_Content) Section in the BaseX documentation will give you more details.

Hope this helps, Christian

voir aussi https://www.w3.org/TR/xpath-full-text-10-use-cases/#Across



Nota : pour la recherche plein-texte sur des contenus mixte, l’option indent=no lors de l’importation de la base de données.

De même, ne pas supprimer les espaces.

### Fonctions additionnelles de BaseX

cf. http://docs.basex.org/wiki/Full-Text_Module

## Sources

http://docs.basex.org/wiki/Full-Text#Mixed_Content

https://www.w3.org/TR/xpath-full-text-10-use-cases/#Across