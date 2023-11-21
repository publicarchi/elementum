# Julia Data

## Travailler avec des données

### Opération courantes pour manipuler des données

#### Read

- [CSV](https://csv.juliadata.org)
- Parquet
- SASLibe
- ReadStat
- JSON, JSON2, JSON3
- LightXML, EzXML
- XLSX, ExcelReaders, Taro
- PDFIO

#### Clean, Tidy, Analyse

- DataFrames
- DataFramesMeta
- Query
- JuliaDB, JuliaDBMeta

#### Visualize

- [https://docs.juliaplots.org](https://docs.juliaplots.org/stable/), [StatsPlots](https://github.com/JuliaPlots/StatsPlots.jl)
- [Makie](https://github.com/MakieOrg/Makie.jl), [StatsMakie](https://github.com/JuliaPlots/StatsMakie.jl)
- [Gadfly](http://gadflyjl.org)
- [Gaston](https://github.com/mbaz/Gaston.jl)
- [VegaLite](https://www.queryverse.org/VegaLite.jl/)
- [UnicodePlots](https://github.com/JuliaPlots/UnicodePlots.jl)
- [PrettyTables](https://ronisbr.github.io/PrettyTables.jl/stable/)

#### Nettoyer des fichiers CSV

Les fichiers peuvent être assez librement formé, ils peuvent parfois comporter une ligne d’entête, utiliser des séparateurs différents. En raison de cette hétérogénéité, il peut parfois être difficile de manipuler des fichiers CSV. La librairie CSV.jl offre de nombreuses fonctionnalités facilitant l’utilisation de données au format CSV.

Pour nettoyer les fichiers, il est notamment possible de :

- de supprimer des colonnes inutiles
- de supprimer les lignes avec des valeurs nulles
- renommer les colonnes
- régler les problèmes de type de données
- etc.

#### Opération courantes pour le nettoyage de données avec les DataFrame

```julia
# Take a quick overview of data
describe(df)
```

```julia
# Keep good columns or delete bad ones
select!(df, 1:5)
select!(df, Not(["badcol1", "badcol2"]))
```

```julia
# Fix column names
rename!(df, "Region Name" => "region_name")
```

```julia
# Remove rows having missing data
dropmissing!(df)
drompmissing!(df, Between(:x3, :x5))
```

Tip : utiliser `Not` et `Between` pour sélectionner les données

Des données biens structurées présentent un certain nombre de caractéristiques

- chaque variable forme une colonne
- chaque observation forme une ligne
- chaque type d’unité d’observation forme un tableau

Il est donc parfois nécessaire de décomposer des tableaux pour regrouper les informations par ligne de sorte que chaque ligne constitue une observation. Cette transformation des données facilite souvent leur traitement et leur représentation graphique.

#### Opérations courantes pour la préparation des données

`stack` et `unstack`permettent de modifier la présentation des données

```julia
# Stack all date columns into rows, the new column names are stored in a new column Date
sdf = stack(df, Not(:RegionName); variable_name = :Date)
sdf = stack(df, Not(1); variable_name = :Date)
sdf = stack(df, 2:5; variable_name = :Date)
```

```julia
# Date column is a CategoricalArray type, make it a Date type
sdf.Date = [Date(get(x)) for x in sdf.Date]
```

```julia
# How to turn it back to a wide format ?
df2 = unstack(sdf, :Date, :value)
```

```julia
# It may introduce Union{Missing, T} column type, let’s fix it
disallowmissing!(df2, 2:5)
```

### Analyse des données

Opérations courantes pour analyser les données

```julia
# Select by column
select(df, :RegionName, 4:5)
```

```julia
# Filter (alors le DataFrame est le 2e argument)
filter(:RegionName => ==("Abilene, TX"), df)
filter("2020-01-31" => >(400_000), df)
```

L’opérateur `=>` est un opérateur qui forme paire. `==` est une fonction anonyme, une clôture capture une valeur...

```julia
# Sort
sort(df, :RegionName)
sort(df, :RegionName, rev = true)
```

Une manière d’appliquer une fonction à chacune des cellules

```julia
# Transform (add new columns)
transform(df, :RegionName => ByrRow(length) => :RegionNameLength)
```

Regroupement des données

```julia
# Group the row by certain column(s)
groupby(sdf, :Date)
```

```julia
# Summarize the grouped data
combine(groupby(df, :Date), :value => mean => :avg)
```

Construction de pipelines

```julia
@pipe sdf |>
		groupby(_, :Date) |>
		combine(_, :value => mean => :avg)
```

Jointures

```julia
# Let’s say we have a reference data frame
country = DataFrame(Name = ["United States"])
```

```julia
# Joining data
innerjoin(df, counrty, on = [:RegionName => :Name])
leftjoin(df, counrty, on = [:RegionName => :Name])
rightjoin(df, counrty, on = [:RegionName => :Name])
outerjoin(df, counrty, on = [:RegionName => :Name])

semijoin(df, counrty, on = [:RegionName => :Name])
antijoin(df, counrty, on = [:RegionName => :Name])
```

## Visualisation

Toutes ces données manipulées peuvent être visualisées pour les explorer. Il existe de nombreux packets pour la visualisation de données.

Avec Plots.jl, de nombreux graphes standards sont disponibles (plot, scatter, histogramme, heatmap, bar, etc.). StatsPlots.jl (groupbar, corrplot, marginhist, boxplot, violin, etc.).

## Mise en pratique

Importation d’un fichier CSV

Exploitation d’un grand tableau de données

Description du tableau

Stack du tableau

possibilité de faire apparaître le type des colonnes

Filtrer pour voir toutes les lignes contennant un... utilisant broadcasting



## Références

https://github.com/JuliaCommunity/YouTubeVideoTimestamps/tree/main/videos

- Julia DataFrame Tutorials, https://github.com/bkamins/Julia-DataFrames-Tutorial
- Tom Kwong, Data Wrangling Techniques in Julia, https://youtu.be/txme9o0EdLk?si=VS_s2kZ9eZya5hFR
- Kwong, Tom. « Data Wrangling with DataFrames.jl Cheat Sheet ». Consulté le 29 septembre 2023. https://www.ahsmart.com/assets/pages/data-wrangling-with-data-frames-jl-cheat-sheet/DataFramesCheatSheet_v1.x_rev1.pdf.



