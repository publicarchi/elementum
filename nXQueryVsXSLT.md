---
author: emchateau
tags: xslt, xquery
---

# Différences entre XQuery et XSLT


## Traitement par défaut

Pas de règle par défaut.

## Namespace par défaut

Une différence principale avec le `xpath-default-namespace` de XSLT consiste dans le faire que cette déclaration par default s’applique à la fois aux noms d’éléments dans les expressions de chemin et aux constructeurs d’éléments, ce qui peut êrte un inconvénient lorsque les documents en entrée et en sortie sont dans des espaces de nom différents.

Lorsque l’entrée et la sortie sont tous deux dans un espace de nom et que l’on souhaite que la sortie soit dans un espace de nom sans préfixe, on peut choisir les options suivantes :

- utiliser `*:name` dans les expressions de chemin (ce qui peut ne pas être toujours suffisamment spécifique)
- lier un prefix `p` à l’espace de nom en entrée et utiliser `p:name` dans les expressions de chemin (solution moyenne)
- utiliser un `Q{}name` dans les expressions de chemin (seulement dans la version 3.0, et moyen)
- utiliser des constructeurs d’élément computés, et lier l’espace de nom par défaut à l’espace de nom d’entrée
- utiliser XSLT 2.0 avec l’attribut `default-xpath-namespace`.

Michael Kay rapporte qu’il a essayé de persuadé le Groupe de travail XQuery de permettre des espaces de nom par défaut différents pour l’entrée et la sortie pour les noms d’élément, et que la réaction générale fut « Mike, why do you keep trying to make namespaces even more complicated than they are already? ». Ainsi XQuery répéta l’erreur de XSLT 1.0, simplement avec une forme légèrement différente.


## Sources

- XQuery-talk
- http://www.xml.com/pub/a/2005/03/09/xquery-v-xslt.html
- http://www.ibm.com/developerworks/library/x-wxxm34/
- http://lists.xml.org/archives/xml-dev/200102/msg00570.html
- http://www.balisage.net/Proceedings/vol5/html/Birnbaum01/BalisageVol5-Birnbaum01.html
- https://en.wikibooks.org/wiki/XQuery/XQuery_and_XSLT
