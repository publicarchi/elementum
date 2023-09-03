---
title: Guide TEI Stylesheets
author: Emmanuel Château-Dutier
since: 2015-05-02
---

# Guide TEI Stylesheets

## Présentation

Les feuilles de style distribuées par le Consortium de la TEI (https://github.com/TEIC/Stylesheets) sont un ensemble de transformations XSLT qui constituent une suite logicielle configurable destinée à manipuler et convertir des documents TEI dans différents formats (MSWord, Open Office, ePub, Docbook, etc.).

Développées par Sebastian Rahtz, les feuilles de style TEI sont également distribuées comme transformations par défaut pour la TEI dans l’éditeur XML Oxygen. Il est par ailleurs mis en œuvre dans le service web OxGarage.

Ces feuilles de styles couvrent la plupart des cas courants et un grand nombre de formats. Il est également possible d’y contribuer. Toutefois, leur utilisation peut s’avérer, au départ, relativement ardue.


## Personnalisation des transformations

La personnalisation des transformations proposées par les feuilles de style TEI reposent sur une large utilisation des instructions xsl `import` et `include`.

- `xsl:import` inclue un fichier de règles XSLT en les surchargeant comme de besoin ;
- `xsl:include` inclue un fichir de règles XSLT mais sans les surcharger.

Ainsi, si vous voulez importez ou incluez des règles identiques à celles du fichier courant :
- en utilisant `import`, les règles dans le fichier courant auront une priorité plus élevée
- en utilisant `include`, vous obtiendrez une erreur à moins d’assigner une priorité plus élevée à l’une ou l’autre des règles.


## Paramétrage des transformations

Les variables peuvent être déclarées comme fils de l’élément `stylesheet` avec des éléments `variable`.

```xsl
  <xsl:variable name="TEI">Text Encoding Initiative</xsl:variable>
```

Il est également possible d’employer des paramètres directement comme fils de `stylesheet`, mais ceux-ci peuvent être écrasés lors de l’appel de la feuille de style.

```xsl
  <xsl:param name="logo">../Graphics/logo</xsl:param>
```

En ligne de commande :

```bash
saxon data.xml test.xsl logo=myLogo
```


### Exemple d’importation

Dans l’exemple ci-dessous, on importe une transformation et l’on renseigne certains paramètres. Ensuite, on fournit une règle nommée.

```xsl
  <xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
    xmlns:xs="http://www.w3.org/2001/XMLSchema"
    exclude-result-prefixes="xs"
    version="2.0">
    <xsl:import href="/Users/emmanuelchateau/Documents/informatique/TEIC/Stylesheets/release/xsl/xml/tei/stylesheet/slides/teihtml-slides.xsl"/>
      <xsl:param name="logoFile">../Graphics/logo.png</xsl:param>
      <xsl:param name="cssFile">teislides.css</xsl:param>
      <xsl:param name="showNamespaceDecls">false</xsl:param>
      <xsl:param name="forceWrap">true</xsl:param>
      <xsl:param name="spaceCharacter"> </xsl:param>
    <xsl:template name="lineBreak">
      <xsl:param name="id"/>
      <br/>
    </xsl:template>
  </xsl:stylesheet>
```

Tandis qu’un `template match` s’applique à un élément, un `template name` ne s’applique à aucun élément en particulier mais définit seulement une règle qui pourra être appelée ailleurs.

Ici, on propose un remplacement pour la règle nommée `lineBreak`


## Organisation des fichiers

Les feuilles de styles TEI se présentent sous la forme d’une hiérarchie de fichiers. Pour les employer, on inclue ou importe ces fichiers.

L’arborescence de fichiers rassemble les feuilles de style par formats de sortie (docx, epub, html, html5, latex, slides, etc.).

- `docx/` conversion depuis ou vers MSWord
- `epub/` conversion vers ePub
- `html/` constructeur XSL FO
- `latex/` constructeur LaTeX
- `html/` conversion vers html
- `html5/` conversion vers html5
- `odd/` transformation de spécifications ODD
- `pdf/` conversions vers pdf
- …

Outre ces répertoires, il y a trois répertoires spécifiques :
- `profiles/` personnalisations
- `commons/` transformations utilisées pour tout format de sortie
- `tools/` utilitaires.

À l’intérieur des répertoires de formats, le contenu des transformation est organisé en fonction des modules de la TEI :
- `core.xsl` Éléments de base de la TEI
- `dictionnaries.xsl` Module Dictionaries
- `drama.xsl` Module Drama
- …

Le fichier `tei-params.xsl` fixe les paramètres et `tei.xsl` importe les règles communes.

Le répertoire de profil `profile/` contient des sous-répertoires de personnalisation avec les normes de nommage suivantes : `nom/format/from.xsl` ou `nom/format/to.xsl` selon qu’il s’agit d’une conversion _depuis_ ou _vers_ un format donné.

Dans ces fichiers, on peut faire référence à la transformation maître, de la manière suivante :

```xsl
  <xsl:import jref="../../../epub/tei-to-epub.xsl"/>
```


## Configuration des scénarios dans Oxygen

Les feuilles de style TEI sont distribuées avec l’éditeur XML oXygen. On peut donc y faire référence depuis le chemin de l’application, à l’intérieur du répertoire `framework`. La configuration du scénario de transformation permet de renseigner les valeurs de paramètres en donnant accès à leur documentation.


## Sources

- Sebastian Rahtz, _Developing with the TEI Stylesheet family_, Mutec, Lyon, may 2011.
