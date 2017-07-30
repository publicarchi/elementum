---
author: emchateau
since: 2017-07-28
tags: sass, css
---

# Modulariser ses CSS

Parmi les nombreuses fonctionnalités qu’apportent l’utilisation d’un pré-processeur CSS ou les dernières versions du langage, la possibilité de modulariser l’organisation de ses CSS et l’emploie de variables sont sans doute parmi les plus notables. Outre une maintenance plus aisée, l’un des principaux avantages liés à la modularisation des CSS consiste à faciliter l’accès à certaines parties du code. Cela suppose notamment l’adoption de convention de nommage explicites et qui permettent d’immédiatement identifier la relation entre les différents fichiers.

Même si les dernières fonctionnalités de CSS pour la modularisation et l’utlisation de variables ne sont pas encore implémentées dans tous les navigateurs, il est dès à présent possible de les employés en utilisant un pré-processing ou un post-processing. Les pré-processeurs tels que SASS ou LESS sont des stratégies bien établies qui offrent aux designers de nombreuses commodités. L’utilisation d’une stratégie de pré-processing permet quant à elle d’employer une pure syntaxe CSS et de mettre à jour son code au fur et à mesure que certaines fonctions sont supportées par les navigateurs.

## Contrôle

Avant toute chose, il convient de définir un fichier qui importe tous les sous-fichiers que nous allons créer. Ce fichier peut être considéré comme un fichier de contrôle car il permettra rapidement d’ajouter ou de désactiver un objet. Tous les segments seront compilés dans ce fichier avant d’être convertis en fichier CSS.

Par commodité ce fichier peut être appelé `main.css` ou `main.scss`

## Utilitaires

La conception atomique suggère de penser dans un premier temps de manière le plus vague possible et de se concentrer plus tard sur des petites parties du code. Pour commencer, on emploiera donc un répertoire destiné à recueillir les fondations de la mise en page. Comme nous allons aussi avoir besoin de définir des mixings et des styles qui puissent être utilisés ailleurs, ce répertoire est important pour définir des classes globales ou des styles qui peuvent être utilisés partout ailleurs.

```
main.css
utilities/
├─ _base-spacing.css
├─ _clearfix.css
└─ _reset.css
```

## Quarks

On va ensuite définir les blocs de construction de base du site web, ceux-ci comprennent les paragraphes, les listes, les tables ou les liens et les images. Il s’agit ici d’entrer doucement dans la complexité. Dans un premier temps, il convient de penser le plus globalement possible et de réserver pour plus tard les stellages particuliers de certaines sections prévus dans le design.

Les fichiers ne contiennent que les styles par défaut de ces éléments et pas leurs modification. La fine granularité des fichiers est ici destinée à faciliter l’accès aux contenus.

```quarks/
main.css
.../
quarks/
├─ _lists.css
├─ _paragraphs.css
├─ _tables.css
└─ _links.css
```

## Atomes

```quarks/
main.css
.../
atoms/
├─ _media.css
├─ _flag.css
├─ _buttons.css
└─ _grids.css
```

## 

## Molecules

Lorsque l’on a besoin d’éléments uniques qu’il n’est pas nécessaire de répliquer mais qui peuvent être combinés dans plusieurs quarks et atomes, sans interférer avec les styles globaux, ceux-ci sont classés dans les molécules. Ces molécules profitent des atoms pour la mise en page mais permettent ici d’étendre, de modifier et de combiner d’autres styles et modules.

```quarks/
main.css
.../
molecules/
├─ _banner.css
├─ _custom-post.css
└─ _footer-nav.css
└─ _heading-group.css
```

## Rmq

Ce n’est pas la seule manière d’organiser son code css. On prête ici attention à l’interface du développeur pour faciliter le travail. 

Une autre manière d’organiser son code plus explicite

```
// Config
@import "vars/*";
@import "functions/*";
@import "mixins/*";
 
// Bower Components
@import "../bower_components/normalize-scss/_normalize";
 
// General DOM selector styles
@import "base/*";
 
// Fonts & General Type Styling
@import "typography/*";
 
// 3rd Party Addons
@import "plugins/*";
 
// Atomic Design
@import "atoms/**/*";
@import "molecules/**/*";
@import "organisms/**/*";
@import "templates/**/*";
@import "pages/**/*";
 
// Variations thru Events
@import "states/*";
 
// General UI Helpers
@import "utility/*";

```

Contenu des fichiers

```
- atoms
  - _buttons.scss
  - _links.scss
  - _inputs.scss
- molecules
  - _navigation.scss
  - _search-form.scss
  - _contact-form.scss
- organisms
  - _header.scss
  - _footer.scss
  - _content.scss
- templates
  - _sticky-footer.scss
  - _grid-2column.scss
  - _grid-3column.scss
- pages
  - _home.scss
  - _about.scss
  - _contact.scss
```

```
- vars
- functions
- mixins
- base
- typography
- plugins
- toolbox
- components
- layout
- pages
- states
- utility
style.scss
```





## Références

http://sass-lang.com/guide#id1

https://www.smashingmagazine.com/2013/08/other-interface-atomic-design-sass/

http://bradfrostweb.com/blog/post/atomic-web-design

http://patternlab.io http://demo.patternlab.io

https://webdesign.tutsplus.com/articles/structuring-sass-saying-goodbye-to-atomic-design-ambiguity--cms-26679