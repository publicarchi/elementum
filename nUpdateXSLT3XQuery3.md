---
author: Emmanuel Château-Dutier
since: 2017-02-11
---

# Feed Back sur les Spécifications XSLT et XQuery 3 par Michael Kay

Près de 10 ans après XSLT 2, pour la version 3 des langages, Michael Kay a offert à XMLPrague 2017 un point d’information sur l’état des différents langages. Dans cette présentation, il a notamment cherché à dégager les aspects de cette nouvelle version du langage qui constituent de véritables changements.

## Fonctions de haut niveau

Appréciées pour l’élégance en terme de programmation, mais importantes car première capacité pour traiter les choses de manière dynamique. Capacité de prendre en charge la variété et le changement. En XSLT, le templating qui offrait déjà des réponses à ces questions.

On peut passer un paramètre à une requête et que l’action peut être effectuée de manière différente. Pas seulement une manière chouette de programmer mais rend les applications plus scalables.

## Support de JSON

Ne croit pas que XQuery sera largement utilisé sur le web pour traiter du JSON, pour plusieurs raisons : d’abord pour une raison culturelle, au sens où vient d’un terrain distinct. Mais aussi pour des raisons stratégiques car les personnes qui utilisent XML n’utilisent pas seulement du XML, et il est très important que leurs outils rencontrent tous les besoins de ces utilisateurs. Il s’agit donc d’étendre la portée du langage.

## Streaming et Packaging

Deux choses qui présentent des enjeux en terme de scalabilité pour XSLT. Le Streaming permet de prendre en charge de larges sources de documents, et le packaging pour la production de grandes applications très stratégiques en terme de maintenance.

## Sérialisation HTML5 et JSON

Possibilité de générer du HTML5 en XSLT.

## Bénéfices

Plusieurs bénéfices en termes de productivité.

Nombreuses personnes cherchent à tirer parti du parse/serialisation au sein du langage. Possibilités de contrôler le pipeline. Mais aussi possibilité d’inclure du XML.

Les maps et arrays sont en partie là pour le support de JSON mais dès lors que commence à les utiliser, on réalise à quel point on en avait besoin. Pour la première fois un typage et des structures de données correctes qui permet de configurer les applications, là où XML pas très adapté. Par exemple lorsque la valeur d’un attribue ne peut pas être une liste de nombre, mais seulement une chaîne. Augmente donc la faisabilité de certaines applications en XQuery et XSLT.

Standardisation des collations UCA, importante car parfois besoin de comparerais collations internationales. Un ensemble de collations standardisées par des URI que l’on peut employer de différentes manières, sans doute un réel bénéfice pour traiter des données internationales.

Collections généralisées, possibilité d’utiliser des URIs. Aujourd’hui bien plus puissantes, peut avoir des collections de n’importe quoi, de texte, de JSON, de contenus hybrides, cela fournit une abstraction très puissante entre les applications XQuery et XSLT et le monde extérieur.

Entrée et sortie non-hiérarchiques, importantes pour XSLT.

Grouping en XSLT qui augmente interopérabilité.

## Petites choses

Petites choses qui donnent le sourire et améliorent l’expérience.

Nouveaux opérateurs : `!`, `||`, `?`, `=>` (|| vient de sequel)

Possibilité de faire des chaînage de fonctions, au lieu de dire string before, etc. possibilité de mettre le résultat d’une fonction dans la suivante.

Text Value template en XSLT très appréciable évidemment.

Union Types possible maintenant d’écrire des fonctions qui opèrent sur une date ou une heure, au lieu d’écrire deux fonctions distinctes.

`tokenize()` et `contains-token()` qui 

Nous avons terminé et pense qu’avons été successfull du point de vue des implémentations fonctionnelles, du déploiement dans des applications critiques. Une masse d’utilisateurs. Qualité de la spécification du langage. Portée de l’application, et intérêt de la communauté.

## Conclusions

Michael Kay explique qu’il est désormais content de pouvoir disposer des journées que consacrait à ce groupe libres. Après vingt ans de travail, content de pouvoir dire que va pouvoir s’occuper d’autre chose.

Quelques diapositives de spéculations sur le futur. En tous les cas plusieurs choses peuvent intervenir, depuis quelques années réouvre les boîtes de plusieurs standards. Plusieurs choses que j’espère qu’interviennent, de nouvelles générations de langages de requêtes ou de tranformation qui produiront les choses encore mieux que les a pensées. Ne croit pas qu’avons là le dernier langage de transformation. Attend le moment où d’autres produiront un langage qui rendra obsolète ce que nous avons fait au cours des vingt dernières années.





