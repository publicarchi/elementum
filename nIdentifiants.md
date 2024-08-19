---
author: emchateau
tags: identifiants
---

## Identifiants

- une réalisation de la NCDD (Netherlands Coalition for Digital Preservation) qui propose des vidéos pédagogiques (<http://www.ncdd.nl/en/pid/>) et un guide pour choisir le format d'identifiant adapté à ses besoins (<http://www.ncdd.nl/en/pid-wijzer/>).
- un tutoriel sur DoraNum : <http://dev.doranum.fr/thematique-identifiants-perennes-pid/>



Bonjour,

Pour compléter les références indiquées par Alain Marois qui, malgré leur qualité, souffrent du poids des ans (Emmanuelle le reconnaissant elle-même, elle ne m'en voudra pas ;) ), quelques précisions :

\- DOI, ARK, Handle sont trois mécanismes de construction d'identifiants différents. Ils présentent leurs avantages et leurs inconvénients qui tiennent bien souvent à leurs origines. DOI a été créé pour plutôt identifier des articles tout comme Handle (d'ailleurs DOI se repose sur les principes techniques d'Handle), ARK a été mis au point pour identifier des ressources dans des bibliothèques numériques.

\- Ces différents systèmes sont apparus pour résoudre le problème de la persistance de l'accès aux données en ligne et vaincre le spectre des erreur HTTP 404, nous pensions alors que la solution résidait dans la mise en place de systèmes techniques indépendants des technologies (y compris HTTP, c'est-à-dire le Web), il reposent donc tous sur le principe des URIs dont ils sont des schemes (cf. les articles d'Emmanuelle sur cette question).

\- MAIS, nous avons fait une erreur, cette problématique de l'identification pérenne des ressources en ligne n'est pas un problème technique, mais un problème organisationnel et politique : il est nécessaire de mettre au point une politique de nommage des ressources et de se donner les moyens de les maintenir dans le temps (ou d'effectuer des redirections vers leur nouvel emplacement si cela est inévitable)

\- Ainsi, ces mécanismes ne permettent pas en soi de résoudre le problème, ils permettent simplement de vous simplifier certains choix dans la mise au point de la politique de nommage et permettent de s'abstraire de toute adhérence avec des systèmes locaux ou des logiciels, bref, il vous donne des identifiants opaques.

\- Si vos ressources sont moissonnées et indexées par Isidore et qu'ils n'ont pas déjà un identifiant ARK, DOI ou Handle, ils reçoivent automatiquement un identifiant Handle. Ce choix a été fait pour garantir l'accès dans le temps à la ressource via un identifiant unique même si l'URL de la ressource en question est modifiée. Handle a été choisi pour des raisons de simplicité, d'indépendance, d'adéquation au ressource identifié et aux objectifs visés.

\- Enfin, nous nous sommes aperçus que dans une perspective d'exposition des données selon les principes du Web de données (ou Linked Data), ces identifiants étaient en soi incompatibles et qu'il fallait de toute manière les préfixer avec une URL en HTTP (cf. [data.bnf.fr](http://data.bnf.fr/) et gallica)

Bref, pour résumer, l'enjeu n'est pas tant de savoir si vous devez utiliser DOI, Handle ou ARK, mais la mise au point d'une politique de nommage à l'échelle de votre projet voire de votre établissement et des moyens que vous vous donnez pour garantir l'accès dans le temps aux ressources exposées via leurs identifiants. Ces systèmes ne sont là que pour éventuellement vous simplifier (quoique....) ce travail mais ne résolvent en aucun cas le problème...

Cordialement

Gautier Poupeau

@lespetitescases



Bonjour Jeanne,

Si cela peut aider, les pages pro du site web de la BNF ainsi que les écrits d'Emmanuel Bermès sur la question peuvent aider à éclaircir ce point. Quelques réf. (tout sauf suffisant) :

Bermès E. Les identifiants pour les objets  numériques [Internet]. 2007 Sep 20 [cited 2018 Jan 29]. Available from: <http://pin.association-aristote.fr/lib/exe/fetch.php/public/presentations/2007/pin20070920pin-identifiants.pdf>

Bermès E. Identifiants pérennes pour les ressources culturelles. Vade-meccum pour les producteurs de données. Version 1.0 [Internet]. Paris: Ministère de la Culture et de la Communication; 2015 décembre [cited 2018 Jan 29]. Available from: <http://www.bnf.fr/documents/identifiants_perennes_vademecum.pdf>

Bermès E. Des identifiants pérennes pour les ressources numériques [Internet]. BNF; 2006 May [cited 2018 Jan 29]. Available from: <http://www.bnf.fr/documents/ark_presentation_bermes_2006.pdf>

Cordialement,



Je me permets de vous signaler l'ouverture des inscriptions au sommet ARK le mercredi 21 mars 2018 prochain :<http://www.bnf.fr/fr/professionnels/anx_journees_pro_2018/a.jp_180321_ark.html>
Si vous êtes intéressés, ne tardez pas à vous inscrire : les places sont en quantité limitée.