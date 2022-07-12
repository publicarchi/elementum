# OpenRefine

- Hooland, Seth van, Ruben Verborgh, et Max De Wilde. 2013. « Nettoyer ses données avec OpenRefine ». *Programming Historian*, août. https://programminghistorian.org/fr/lecons/nettoyer-ses-donnees-avec-openrefine.
- Little, John. s. d. *Cleaning Data with OpenRefine*. Consulté le 6 mars 2022. https://libjohn.github.io/openrefine/index.html.
- dinh. s. d. « [Useful recipes for achieving some tasks in OpenRefine] #openrefine #datawrangling #data ». Gist. Consulté le 6 mars 2022. https://gist.github.com/dinh/1ec70e8c29cd013a0a36bc77b424b940.
- Padilla, Thomas. s. d. « Getting Started with OpenRefine ». Consulté le 6 mars 2022. http://www.thomaspadilla.org/dataprep/.
- Saby, Mathieu. s. d. *Tutoriel OpenRefine 3.4 : nettoyer, préparer et transformer des données - 06/11/2020*. Consulté le 6 mars 2022. https://msaby.gitlab.io/tutoriel-openrefine.

## Explorer les données

### Facettes textuelles

## Normaliser les données

### Splitter une colonne selon un caractère

### Supprimer un caractère inutile en fin de colonne

```GREL
value.chomp("/")
```

### Mettre la colonne en bas-de-casse sauf la première lettre

### Mettre la colonne en bas-de-casse sauf la première lettre avec des tirets

```GREL
replace(toTitlecase(replace(value,"-",".")),".","-")
```



## Convertir une date

```GREL
value.toDate("YYYY-MM-DD").toString("dd-MM-YYYY")
```

## Enrichir des données avec des données ouvertes

### GeoAPI

https://geo.api.gouv.fr/

```GREL
"https://geo.api.gouv.fr/communes?code=" + value
```

Un problème avec les listes JSON



## Divers

Réconciliation avec VIAF

http://refine.codefork.com/reconcile/viaf

https://github.com/RubenVerborgh/Refine-NER-Extension

https://github.com/sparkica/refine-stats

https://github.com/fadmaa/grefine-rdf-extension/releases

https://github.com/antoinecourtin/AAF2018/blob/master/utils.md

TUTO : “Reconcilier” une liste de nom d’architectes avec Wikidata en utilisant OpenRefine : https://medium.com/@seeksanusername/reconcilier-une-liste-darchitecte-avec-wikidata-en-utilisant-openrefine-16819fbb2903