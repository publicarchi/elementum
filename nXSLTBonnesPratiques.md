# Bonnes pratiques XSLT

Bonnes pratiques pour écrire du code XSLT efficace

- bien structuré et lisible
- simple et concis
- efficient en termes de performances

## Utilisation non-efficace

- L’utilisation trop abondante de `for-each` marque souvent l’utilisation de techniques de programmation traditionnelle et d’une mauvaise compréhension du caractère déclaratif du langage
- La sous-utilisation de XPath souvent liée à une mauvaise maîtrise des prédicats, des spécifications d’axes ou des fonctions (position(), current() dont la logique ne nécessite pas d’être implémentés avec XSLT
- La sous-utilisation des métadonnées qui peut permettre d’éliminer une grande quantité de traitement
- La sous-utilisation du pré-processing. Par exemple, lorsqu’un document XML contient des données qui doivent être passées à l’aide de manipulation de chaînes, il est souvent plus simple de passer le résultat passé à l’extérieur comme argument de la transformation.

## Bonnes pratiques

Tenir compte du double caractère du langage, fonctionnel et déclaratif.

- titrer parti de la structure du document pour guider le processeur et diriger les traitements

- éviter l’emploi de l’opérateur `//`dans les expressions XPath près de la racine d’un arbre important

- utiliser les fonctions node-set

- utiliser les types XML schéma

- éviter les sélecteurs d’axe trop longs ou trop complexes

- utiliser des constructeurs directs lorsque c’est possible

- tirer parti des nouveaux éléments XSL

- modulariser le code

- limiter l’emploi des named template aux contenus répétés

- utiliser des fonctions pour réduire la complexité

- employer des noms de variables, de fonction ou de template pertinents

- placer les regex dans des variables

- tirer parti de l’emploi des modes

- éviter d’assigner des valeurs à une variable avec la syntaxe `select` pour une chaîne

- éviter l’emploi d’instruction avec des contenus vides comme for-each, if, when

- éviter une trop petite granularité des templates

- éviter l’emploi de déclarations redondantes d’espace de nom

- éviter les fonctions non employées

- éviter les variables non employées

- éviter les paramètres inutiles

- utiliser des stérilisations appropriées

  ​

## Difficultés

Le code mort. Rien ne permet logiquement de déterminer quelle partie du code est inutile dans un programme.

Attention aux erreurs avec les booléens

etc.

## Références

http://conferences.idealliance.org/extreme/html/2006/Novatchev01/EML2006Novatchev01.html

https://stackoverflow.com/questions/741050/writing-effective-xslt/741128#741128