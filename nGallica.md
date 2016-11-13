# Travailler avec Gallica

## Manipulations à partir des ARK

Des identifiants ARKs ont été définis pour deux types distincts de ressources à la BnF : Les documents numérisés disponibles dans la bibliothèque numérique en ligne [Gallica](http://gallica.bnf.fr) utilisant `http://gallica.bnf.fr` comme Name  Mapping  Authority (NMAH), et pour les enregistrements du catalogue qui nécessitaient des identifiants pour l’échange avec les entrepôts OAI de la Bnf et utilisent le NMAH  `http://catalogue.bnf.fr`.

Pour les deux Name  Mapping  Authority, un ensemble initial de qualificateurs ont été définis pour nommés les sous-parties et les variants.

Par exemple, dans gallica.bnf.fr, des qualificateurs ont été définis pour designer les pages des livres.

*par exemple* : 

http://gallica.bnf.fr/ark:/12148/bpt6k5834013m/f10 pour identifier la page dix du document numérisé, `/f10n5` pour identifier l’intervalle de page dix à quatorze. 

http://gallica.bnf.fr/ark:/12148/bpt6k5834013m/f10.highres, `.medres`,  `.lowres`  and `.thumbnail`sont des qualificateurs qui peuvent  être employés pour identifier les variants d’une même page d’un ouvrage. `.text` et `.vocal`permettent d’accéder au plein texte ou la version vocale du même enregistrement.

## Anatomie des ARK

L’ARK est typiquement un identifiant opaque, dépourvu de signification. Ce nom est souvent étendu avec un qualificateur qui peut être moins opaque. Un ARK actionnable sur le web présente trois parties principales.

Le **noyau invariable de l’identifiant** lui-même est obligatoire et est conçu pour être globalement non-ambigu, persistant et opaque. Pour ce faire, il présente une structure qui procède du plus général au plus spécifique de gauche à droite.

- Le schème d’identification (`ark:/`) est une étiquette facilement accessible pour des processeurs textuels
- Le numéro de l’autorité de nommage, _Name  Assigning  Authority  (NAA)_ composée de cinq à neuf chiffres pour l’opacité. L’unicité est garantie via un registre basé à la Bibliothèque de Californie. 
- Ce nom d’ARK qui doit être opaque désigne un sous-domaine correspondant à des préfixes.
- L’autorité de mappage de nom, _Name Mapping Authority (NMA)_ pour résoudre une ressource à partir de son nom de domaine.
- Les parties qualifiantes optionnelles, qui permettent des services supplémentaires fournis par le NMAH en utilisant le standard ARK et les caractères réservés `.` et `/`. Ceux-ci sont habituellement utilisés à la BnF comme suit : pour le nommage des sous-partie d’une ressource (ex. une page spécifique d’un livre numérisé). Cela est réalisé par des qualificateurs précédés d’un `/` (ex : `/f19`).
- Des variants de nom ou des services pour les ressources (ex : une version spécifique dans le cycle de vie d’un livre numérisé, ou la miniature d’une image spécifique). Cela est réalisé par des qualificateurs précédés par un `.` (`.highres`).  

### Qualificateurs offerts par Gallica

### Accéder aux données liées

- http://texashistory.unt.edu/ark:/67531/metapth346793/  (ARK for the resource)
- http://texashistory.unt.edu/ark:/67531/metapth346793/?  (its metadata)
- http://texashistory.unt.edu/ark:/67531/metapth346793/??  (the NMA’s commitment) 

### Accéder au texte brut

ajouter `f1.texteBrut` dans l’URL pour accéder au texte brut.

### Invoquer les variants

Accéder aux différents variants d’une même page

`.highres` version haute-résolution, `.medres` version moyenne-résolution,  `.lowres` version basse-résolution  et `.thumbnail` version miniature

`.text` plein-texte, `.vocal` version sonore

http://gallica.bnf.fr/ark:/12148/bpt6k5834013m/f10

http://gallica.bnf.fr/ark:/12148/bpt6k5834013m/f10.highres

## à voir

Qualificateurs génériques `.description`, `.policy`

Qualificateurs de type de contenu : rdf, xml, etc.

Qualificateurs spécifiques à l’application

ex : `.r=food` pour flaguer un contenu

Avec les ARKs, l’URI qui référence la resource descriptive est construite en ajoutant un `?`, malheureusement, l’infrastructure technique de la Bnf n’a pas permis le support du `?` sans chaîne de requête (qui était confondu avec une requête vide).

La bibliothèque nationale de France a donc fait le choix d’implémenter directement les ressources descriptives directement en utilisant des ARKs. Le mécanisme est donc inversé : depuis la ressource descriptive identifiée par un ARK, on accède à son contenu sous-jascent et pas l’inverse.

Deux choix étaient alors possibles

-  “suffix hash URI” : cas dans lequel on a l’URI http://example.com/resource pour une ressource web (par ex. une page web à propos d’une personne), et http://example.com/resource#classifier pour la chose sous-jascente (par ex. la personne elle-même). Un client de navigation pouvant automatiquement enlever le # pour la consommation ce qui repose sur l’architecture standard du web et les bonnes pratiques. 
-  “prefix slash URI” : dans lequel on a l’URI http://example.com/doc/resource pour le document web et http://example.com/id/resource  pour la chose sous-jascente.  Cela requière une redirection HTTP (`HTTP 303 redirect`) depuis l’URI de la ressource vers l’URI du document web.

Les bonnes pratiques du web sémantique mettent en évidence des questions encore irrésolues par les qualificateurs ARK. Comment nommé la chose sous-jascente quand un ARK est assigné à une ressource descriptive. Ce problème n’est pas entièrement  résolu par l’usage des `/`, et ce n’est ni réellement le cas d’un service ou d’un variant adressé par le `.` parce que les deux choses identifiées sont distinctes.

With ARKs only the  “prefix slash  URI” strategy is possible for the current state of the standard, which means using e.g. http://data.bnf.fr/id/ark:/12148/ark:/12148/cb118905823 (the French poet Charles Baudelaire) and http://data.bnf.fr/doc/ark:/12148/cb118905823 (the record describing him). This was not implemented because the redirection rules would present too great an extra server burden for our application.  

From a technical standpoint, in data.bnf.fr the decision was made to locally extend ARKs and use “hash URIs”. For example, we separate http://data.bnf.fr/ark:/12148/cb118905823 (web page about  Charles  Baudelaire)  from  http://data.bnf.fr/doc/ark:/12148/cb118905823#foaf:Person (Charles Baudelaire himself). 

## Références

http://dcpapers.dublincore.org/pubs/article/view/3704