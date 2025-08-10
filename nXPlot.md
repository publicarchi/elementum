---
author: emchateau
tags: xslt
---

# XPlot

## CR discussion avec David J. Birnbaum

Pas formé en mathématiques besoin aide.

Craintes de faire quelque chose qui soit problématique pour des staticiens.

Voudrait avoir construire suffisamment pour m’assurer que l’architecture envisagée fonctionne. En même temps ne pas trop m’engager au risque de devoir revoir l’architecture.

Envisage balisage comme première étape.

Pour balisage envisage low level functions. Puis package modulaire.

Dot function products, mais besoin de fournir des tests.

Serait intéressant avoir les deux développés en parallèle.

https://docs.basex.org/wiki/Unit_Module

- Courbes de Bézier et autres
- Parabolique regression line (pour cela qu’implémente multiplication de matrices).
- Lowest regression, calculer régression et sliding windows.

Lib : Package, expose fonctions disponibles. Documentation pour tester et porter vers XQuery. Fonctions privées 

Spline plots, importe la librairie générale, expose version avec trois arithmétique pour spécifier curviness et option debug.

Régression linaire dans son propre fichier, une option debug #2

D’abord focalisé sur la visualisation. Fonctions basiques déjà supportées. Pour l’adoucisement gaussien, une fonction pour calculer déviation statistique.

Peut être pas maintenant mais plus tard, discuter architecture générale. Pour cela être plus stable. Regarder organisation, documentation mais fausse.

Fait le choix de séparer les rendus avec CSS.

Faire en sorte que les utilisateurs

Travailler pour balisage et réécrire la documentation ainsi que le texte. Début de juillet pour cela. Dans le même temps peut-être essayer de prendre connaissance du brouillon et repo et discuter de l’architecture globale.

Regarder les bibliothèques et voir ce qu’elles supportent et peuvent faire. Définir quels paramètres offrent aux utilisateurs. Peut être utile et pas d’autres obligations après balisage. 

Forced-directed graph, une priorité.

Travailler sur une archietcture

Exist NLP library aller voir

## Visualisations

- Auto boxplot
- Factorial
- Chronologie

## Perimeter

This library aims to help the user to easily plot data with XML technologies. These data can be displayed on one-dimensional, two-dimensional plots, boxplots and histograms.

The plot is written to produce a Scalable Vector Graphic image in XML that can also be easily converted to other graph types.

- one-dimensional plots
- two-dimensional plots 
- boxplots
- histograms

- Scatter Plots
  - Line and Scatter Plot
- Line Charts
  - Area Chart
- Bar Charts
  - Culumn Chart
- Pie Charts
- Tree Map
- others

## Functionnalities

Scales

Axes

Legends

Axis scaling

Data Labels

Color dimensions

Graph and Axes Titles

Line Dash

Connect Gaps Between Data

Labelling Lines with Annotations

## Contraintes

- place des CSS vs SVG
- Lower learning curve for XML guys

## Other librairies

- SVG_plot, C++, par Jake Voytko, Paul A. Bristow, 2007, BSL https://sourceforge.net/projects/svgplot/ https://github.com/pabristow/svg_plot
- New scala plotting library https://pityka.github.io/nspl/
- https://plotly.com/javascript/
- [**g.raphael**](http://g.raphaeljs.com/)  is an SVG+VML library (using RaphaelJS, from the same author of  RaphaelJS). It is very good for infographics, less good for classical  charts. (last version 0.4.1 from 2009) Mit Licensed.
- [**Grafico**](http://grafico.kilianvalkhof.com/) is again an SVG+VML library (again RaphaelJS based). It has much more  chart types than gRaphael or Elycharts but less options/configurability  than Elycharts. MIT licensed.
- [**D3.js**](http://d3js.org/) Is a JavaScript library for manipulating documents based on data. D3 helps you bring data to life using HTML, SVG and CSS.
- [**HighCharts**](http://www.highcharts.com/) - A very complete SVG+VML library having a very good documentation and a very complete feature set. It has a free for personal use license but  it shows a very "strict" interpretation of personal and your own blog  may not be considered "personal", that's why I show it under "commercial options".
- https://developers.google.com/chart
- https://matplotlib.org/
- https://docs.racket-lang.org/plot/intro.html#%28part._.Terminology%29
- https://graphviz.org/

Pew Research Center & Storytelling with data