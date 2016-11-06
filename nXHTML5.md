author: Emmanuel Chateau
name: nXHTML5.md
date: 2014-06-27

# Note XHTML5

## Introduction

L’abandon de XHTML2 et le choix effectué par le W3C de poursuivre le développement de HTML5 se caractérise d’abord par le renoncement aux contraintes syntaxiques propres au méta-langage XML. Toutefois, même si l’information à ce sujet est souvent restée peu claire, ou difficile à trouver, il est toujours resté possible d’écrire ses pages web en (X)HTML5. Le recours à ce formalisme s’avère particulièrement nécessaire lorsque l’on travaille avec le langage de requêtes XQuery ou le langage de transformation XSLT, ou bien généralement dans l’univers XML (sources XML, Xlink, SVG,  MathML, etc.).

En effet, si le langage de balisage HTML5 paraissait signer la fin de XHTML, la réalité s’est avérée un peu plus complexe. D’une part, la syntaxe XML subsiste et reste toujours valide puisque HTML5 a été conçu afin de rester rétrocompatible avec HTML4 et XHTML. D’autre part, certaines règles syntaxiques propres à XHTML demeurent comme l’imbrication des éléments sans chevauchement, ou bien sont supportées comme des conventions optionnelles. Tout (X)HTML5 est du HTML5 valide, et (X)HTML5 présente plusieurs des propriétés de XML comme l’extensibilité en utilisant des espaces de noms, ou encore l’utilisation de XSLT pour transformer la page dans le navigateur. Ainsi, il demeure donc possible de bénéficier à la fois du meilleur de XHTML et des nouveaux éléments offerts HTML5.

La [note du Groupe de travail W3C qui définit des documents polyglotes pour HTML5](https://www.w3.org/TR/html-polyglot/) résout définitivement la question en offrant un cadre pour la compatibilité des deux langages de balisage.


## Se conformer aux règles syntaxiques de XHTML

Il est possible de contraindre la syntaxe de HTML5 pour qu’elle se conforme à XML, en produisant un document polyglotte. Pour ce faire, il convient d’ajouter explicitement une déclaration d’espace de nom XHTML à l’élément <html> et respecter la syntaxe XML en fermant les éléments, en respectant la casse pour les noms d’éléments et en donnant des valeurs à tous les attributs. Un document XHTML doit être un document XML bien formé.

```html
<!DOCTYPE html>
<html lang="fr" xml:lang="fr" xmlns="htpp://www.w3.org/1999/xhtml">
   <head>
      <meta charset="utf-8"/>
      <title>Un document xHTML minimal</title>
      <link href="styles.css" rel="stylesheet"/>
      <script src="scripts.js"></script>
   </head>
   <body>
      <p>Faisons chauffer le navigateur en mode XHTML5.</p>
   </body>
</html>
```

Il est désormais possible de valider son XHTML5 avec un validateur pour obtenir un contrôle plus strict des erreurs. Cela n’est pour le moment pas proposé par le W3C, mais il on peut utiliser le service en ligne [http://html5.validator.nu]([http://html5.validator.nu]) (en choisissant l’option "Be lax about HTTP Content-Type"), ou bien un schéma [mais la spécification ne définit pas de DTD].

Le projet [unsoup](https://github.com/unsoup) propose dorénavant également des schémas RelaxNG pour valider ses documents en HTML5 contre un schema. cf. https://github.com/unsoup/validator


## Servir la page comme du XHTML

Si, au moyen de ces précautions, on produit du XHTML, les navigateurs traiteront toujours les pages comme des documents HTML5, sans essayer d’appliquer aucune règle complémentaire. Pour utiliser XHTML5 plus complètement, il est nécessaire de configurer son serveur pour servir les pages avec type MIME `application/xhtml+xml` ou  `application/xml` au lieu de `text/html`. Attention, un tel changement peut empêcher vos pages d’être affichées par les navigateurs Internet Explorer antérieurs à la version IE 9. C’est la raison pour laquelle ce format est dans l’immédiat peu employé. Incidemment, il faut aussi avoir conscience que les navigateurs qui supportent XHTML5 se comportent différemment qu’avec HTML5, en essayant de traiter la page comme un document XML, et en interrompant le traitement si le document est mal formé.

Avec nombre de navigateurs, l’utilisation d’une extension `.xhtml` permet d’afficher la page comme avec un type MIME correspondant.


## Utiliser une déclaration XML

Enfin, c’est une bonne pratique que d’ajouter une déclaration XML, même si elle n’est pas obligatoire lorsque l’encodage par défaut UTF-8 est utilisé. Cependant, il alors recommandé de configurer l’encodage en utilisant les en-tête Content-Type du serveur, sinon cette déclaration peut être fournie dans une balise méta `<meta charset="UTF-8" />`.

Il faut noter que la déclaration XML est illégale avec l’en-tête HTTP Content-Type `text/html`. Elle devra donc être réservée aux pages servies en XML.


## Documents Polyglottes

Il est parfois utile de pouvoir servir des documents HTML5 qui sont également des documents XML bien formés ; par exemple, lorsque l’on utilise des outils XML pour générer un document et que l’on veut traiter ces documents avec des outils XML. Un langage qui permet de créer des documents qui peuvent être à la fois traités par des parseurs HTML et XML est appellé un balisage polyglotte. C’est un profil entièrement optionnel du vocabulaire HTML qui permet aux auteurs de rendre leurs documents plus robustes.

Un document qui utilise un balisage polyglotte est un document qui forme des arbres identiques (à quelques exceptions près) lorsqu’il est parsé aussi bien en tant que document HTML ou en tant que document XML. Les documents polyglottes utilisent un DOCTYPE spécifique, une déclaration d’espace de nom, et une casse spécifique pour les noms d’éléments ou d’attributs (généralement bas de casse, et parfois camel case.

Le W3C ne recommande pas particulièrement de publier des documents polyglottes. De manière générale, les auteurs sont encouragés à publier du contenu HTML en employant la syntaxe HTML5 et les types de médias correspondants (soit la syntaxe HTML avec `text/html`, soit XHTML avec `application/xhtml+xml`). Un document polyglotte peut être indistinctement servi comme `text/html` (si le contenu est transmis à un agent utilisateur compatible avec HTML) ou "application/xhtml+xml" (si le contenu est transmis à un agent utilisateur compatible avec XHTML). Les types MIME `text/xml`, `application/xml` et tous les sous-types se terminant par les quatre caractères "+xml" sont également permis.


Les documents polyglottes sont :
- des documents HTML valides
- des document XML bien formés
- ont des DOMs identiques lorsqu’ils sont traités comme HTML ou XML à l’exception notable des DOMs différents générés par les parseurs pour les attributs xml (xml:lang, xml:space, xml:base), xmlns (xmlns="" et xmlns:xlink=""), et xlink (tels que xlink:href). XML rexquière ces attributs et HTML5 les permets dans certains endroits. L’exception ne doit pas empêcher que le document doit être un document HTML valide.

Le support est maximisé :
- par le support du parsing tant HTML que XML
- l’utilisation de code équivalents en DOM
- la possibilité de réutilisation avec d’autres parseurs

Un document polyglot ne doit donc pas utiliser d’éléments  `document.write` ou `noscript` par exemple.

Polyglot markup triggers non-quirks mode in HTML parsers, as non-quirks mode is closest to XML-mode rendering, in regard to both DOM and CSS.

L’extensibilité est supportée lorsque le document est servi comme `application/xhtml+xml`.


### Règles de rédaction

Les instructions de traitement et les déclarations XML sont proscrites.

La spécification de l’encodage du document utilise seulement UTF-8. HTML requière une déclaration explicite, tandis qu’UTF-8 est un encodage par défaut de XML. Les documents servis avec un Content-type `xml` ne nécessitent aucune des deux déclarations HTML, toutefois puisque le document pourrait être interprété comme `text/html` cette déclaration est préférable.

Les documents polyglottes utilisent la déclaration suivante, séparément ou en combinaison (notez qu’il ne peut y avoir qu’une seule déclaration d’encodage HTML) :
- Au sein du document
  En utilisant le Byte Order Mark (BOM) character
  En utilisant la déclaration d’encodage HTML soit dans l’attribut `charset` de `<meta charset="UTF-8"/>` soit dans la forme alternative `<meta http-equiv="Content-Type" content="text/htm; charset=UTF-8"/>`
- En dehors du document
  En ajoutant `charset=utf-8` au type MIME/HTTP de l’en-tête Content-Type comme ci-dessous :
  `Content-type: text/html; charset=utf-8`
  `Content-type: application/xhtml+xml; charset=utf-8`

Le DOCTYPE
Les documents polyglottes utilisent une déclaration de type de document (DOCTYPE) telle que définie dans le standard HTML5 et conforme aux règles suivantes :
- DOCTYPE en capitales
- SYSTEM, si présent en capitales
- PUBLIC, si présent en capitales
- Un identifiant formel public (FPI), si présent, sensible à la casse
- Une URI, si présente dans la déclaration de type de document sensible à la casse
   par exemple `about:legacy-compat`
   Notez que l’usage de about:legacy-compat dans des document XML peut conduire à des résultats de parsing non prévisibles.

 Namespace
 HTML5 a introduit un espace de nom par défaut pour l’élément racine html, svg, et MathMl. Les documents polyglotes déclarent ces espaces de noms par défaut sur l’élément racine pour maintenir la compatibilité avec XML.

 `<html xmlns="http://www.w3.org/1999/xhtml"> <math xmlns="http://www.w3.org/1998/Math/MathML"> <svg xmlns="http://www.w3.org/2000/svg">`

Document polyglotte minimal
```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" lang="" xml:lang="">
  <head>
    <title></title>
  </head>
  <body>
  </body>
</html>
```


## Questions

QUST: Vérifier quel impact sur les navigateurs ?
`<?xml version="1.0" encoding="UTF-8" ?>`

QUST: Doubler les déclarations UTF-8 1° lorsque page servie en HTML / 2° lorsque page servie en XML ?

QUST: Doubler attribut lang avec xml:lang="fr" pour rester conforme à la syntaxe XML ?

```html
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="fr" lang="fr" dir="ltr">
  <head>
    <title>Exemple</title>
  </head>
   <body>
     <!-- Contenu de la page respectant la syntaxe XML. -->
   </body>
</html>
```

## Remarques diverses

Rendre du XHTML dans IE8 requiert un tip XSLT.
Ajouter l’instruction de traitement suivante
```xml
<?xml version="1.0" encoding="iso-8859-1"?>
<?xml-stylesheet type="text/xsl" href="copy.xsl"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
          "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
```
où copy.xsl contient le contenu suivant :
```xml
<stylesheet version="1.0"
     xmlns="http://www.w3.org/1999/XSL/Transform">
    <template match="/">
        <copy-of select="."/>
    </template>
</stylesheet>
```

Déclarer l’encodage dans une balise meta ne fonctionne pas en XHTML, c’est seulement utile pour les documents polyglotes.

La balise meta pour l’encodage est ignorée lorsque le document XHTML est traité en tant que XML.

La déclaration XML est illégale avec l’en-tête HTTP "text/html".

Les documents XML n’ont pas nécessairement besoin d’un DOCTYPE, la spécification ne définit ni identifiant public ni DTD.

À la différence de XHTML1 par rapport à HTML4, le choix entre XHTML5 et HTML5 est exclusivement définit par le type Mime plutôt que par le DOCTYPE : HTML5 n’est plus formellement basé sur SGML, et n’est plus spécifié par une DTD.


## Références

- [Summarized test results : Character encoding (XHTML5), W3C Internationalization,  2009-2012](http://www.w3.org/International/tests/html-css/character-encoding-xhtml/results-xhtml-encoding)
- [HTML5 A vocabulary and associated APIs for HTML and XHTML, W3C Last Call Working Draft, 17 june 2014](http://www.w3.org/TR/html5/) et en particulier http://www.w3.org/TR/html5/introduction.html#html-vs-xhtml et
- http://www.w3.org/TR/html5/the-xhtml-syntax.html
- [Polyglot Markup: A robust profile of the HTML5 vocabulary, W3C Working Group Note 29 September 2015](https://www.w3.org/TR/html-polyglot/)
- http://www.nicolas-hoffmann.net/source/1419-Servir-un-site-en-application-xhtml-xml-XHTML5-et-IE.html
- [Validateur unsoup](https://github.com/unsoup/validator)
- [The Nu Html Checker (v.Nu)](https://validator.github.io/validator/)