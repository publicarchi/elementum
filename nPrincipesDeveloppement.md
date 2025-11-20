---
tags: bonnes pratiques, programmation
---

# Principes de développement et philosophie Unix

## Ken Thomson

Ken Thompson fut à l’origine d’un ensemble de normes culturelles et d’une approche philosophique d’un développement logiciel modulaire et minimaliste.

## Philosophie d’Unix d’après Douglas McIloroy

En 1978, Douglas McIlory et ses collègues résument dans le *Bell System Technical Journal* quelques unes des maximes en vigueur au sein de la communauté de développement Unix qui déterminent sont style de programmation distinct :

> - (i) Make each program do one thing well. To do a new job, build afresh rather than complicate old programs by adding new « features ».
> - (ii) Expect the output of every program to become the input to another, as yet unknown, program. Don’t clutter output with extraneous information. Avoid stringently columnar or binary input formats. Don’t insist on interactive input.
> - (iii) Design and build software, even operating systems, to be tried early, ideally withing weeks. Don’t hesitate to throw away the clumsy parts and rebuild them.
> - (iv) Use tools in preference to unskilled help to lighten a programming task, even if you have to detour to build the tooks and expect to throw some of them out after you’ve finished using them.
>
> (McIlroy et al. 1978, p. 1902-1903)

Traduction française :

> - (i) Faites en sorte que chaque programme accomplisse une seule tâche, mais qu’il la fasse bien. Pour réaliser un nouveau travail, créez un nouveau programme plutôt que de compliquer les anciens en leur ajoutant de nouvelles « fonctionnalités ».
> - (ii) Attendez-vous à ce que la sortie de chaque programme devienne l’entrée d’un autre programme, encore inconnu. Ne surchargez pas la sortie avec des informations superflues. Évitez les formats d’entrée trop rigides, en colonnes ou binaires. N’exigez pas une saisie interactive.
> - (iii) Concevez et développez les logiciels — y compris les systèmes d’exploitation — de manière à pouvoir les tester très tôt, idéalement en quelques semaines. N’hésitez pas à jeter les parties maladroites et à les reconstruire.
> - (iv) Préférez l’utilisation d’outils plutôt que de recourir à une aide non qualifiée pour alléger une tâche de programmation, même s’il faut faire un détour pour construire ces outils et en jeter certains une fois leur usage terminé.
>
> (McIlroy et al. 1978, p. 1902-1903)

En 1994, l’inventeur des pipes Unix, Doug McIlroy résuma cette philosophie dans *A Quarter Century of Unix* de la manière suivante : « Write programs that do one thing and do it well. Write programs to work together. Write programs to handle text streams, because that is a universal interface. » (Salus 1994, p. 52) Il s’agit donc de « concevoir des programmes qui fassent une seule chose, mais qui la fassent bien, et qui fonctionnent correctement ensemble avec d’autres programmes ».

## Pike et la programmation en C

Rob Pike propose dans *Notes on Programming in C* plusieurs maximes de programmation qui peuvent être considérées comme faisant partie d’une philosophie Unix :

> - Règle n° 1 : Vous ne pouvez pas prévoir quelle partie d’un programme consommera le plus de temps. Les goulots d’étranglements se produisent en des parties surprenantes, alors n’essayez pas de deviner à l’avance où, et n’essayez pas d’optimiser le temps d’exécution avant d’avoir prouvé que le goulot d’étranglement se trouve là.
> - Règle n° 2 : Mesurez. N’optimisez pas la vitesse avant d'avoir mesuré, et quand bien même, abstenez-vous de le faire tant qu’une partie du code prédomine sur le reste.
> - Règle n° 3 : Les algorithmes élaborés sont lents si `n` est petit, et `n` est petit la plupart du temps. Les algorithmes élaborés comportent de grandes constantes. À moins d’être certains que `n` sera grand la plupart du temps, n’essayez pas de faire élaboré. (Même si `n` devient réellement grand, utilisez d’abord la règle n° 2). Par exemple, les arbres binaires sont toujours plus rapides que les arbres splay pour les problèmes courants.
> - Règle n° 4 : Les algorithmes élaborés comportent plus d’erreurs que ceux qui sont plus simples, et ils sont plus difficiles à appliquer. Utilisez des algorithmes simples ainsi que des structures de données simples.
> - Règle n° 5 : Les données prévalent sur le code. Si vous avez conçu la structure des données appropriée et bien organisé le tout, les algorithmes viendront d'eux-mêmes. La structure des données est le cœur de la programmation, et non pas les algorithmes.
> - Règle n° 6 : Il n’y a pas de règle n° 6.

Les règles n° 1 et 2 de Pike reformulent la fameuse maxime de Charles Antony Richard Hoare : « L’optimisation du code prématurée est la cause de tous les maux. »

Kenneth Thompson a reformulé les règles de Pike n° 3 et 4 par la phrase « En cas d’hésitation, utilisez la recherche exhaustive » ; le sens est « N’essayez pas d’être malins, essayez d’abord d’être forts. »

Les règles n° 3 et 4 sont des instances de la philosophie de conception KISS.

La règle n° 5 fut énoncée auparavant par Fred Brooks dans *The Mythical Man-Month*.

Les *Programming Pearls* de Jon Bentley comportent aussi un chapitre sur le même principe de conception.

La règle n° 5 est souvent résumée par « Écrivez du code stupide qui utilise des données futées. » Elle est aussi une instance de la recommandation « Si la structure de vos données est suffisamment bonne, l’algorithme pour les utiliser sera évident. »

La règle 6 est simplement une référence humoristique au sketch Bruces sketch des Monty Python. En C, une chaîne de caractères se termine par un caractère-octet nul (valeur zéro). Comme il est nécessaire d’indiquer la fin de la liste, la dernière règle se doit donc d’être nulle.

cf. https://fr.wikipedia.org/wiki/Philosophie_d%27Unix

> #### Epilogue
>
> > If men could learn from history, what lessons it might teach us! But passion and party blind our eyes, and the light which experience gives is a lantern on the stem, which shines only on the waves behind us!  
> >
> > (Samuel Taylor Coleridge, Recollections)
>
> The world of computing changes all the time, and the pace seems to accelerate. Programmers must cope with new languages, new tools, new systems, and of course incompatible changes to old ones. Programs are bigger, interfaces are more complicated, deadlines are shorter.
>
> But there are some constants, some points of stability, where lessons and insight from the past can help with the future. The underlying themes in this book are based on these lasting concepts. 
>
> ***Simplicity*** and ***clarity*** are first and most important, since almost everything else follows from them. Do the simplest thing that works. Choose the simplest algorithm that is likely to be fast enough, and the simplest data structure that will do the job; combine them with clean, clear code. Don't complicate them unless performance measurements show that more engineering is necessary. Interfaces should be lean and spare, at least until there is compelling evidence that the benefits outweigh the added complexity. 
>
> ***Generality*** often goes hand in hand with simplicity, for it may make possible solving a problem once and for all rather than over and over again for individual cases. It is often the right approach to portability as well: find the single general solution that works on each system instead of magnifying the differences between systems. 
>
> ***Evolution*** comes next. It is not possible to create a perfect program the first time. The insight necessary to find the right solution comes only with a combination of thought and experience; pure introspection will not produce a good system, nor will pure hacking. Reactions from users count heavily here; a cycle of prototyping, experiment. user feedback, and further refinement is most effective. Programs we build for ourselves often do not evolve enough; big programs that we buy from others change too fast without necessarily improving. 
>
> ***Interfaces*** are a large part of the battle in programming. and interface issues appear in many places. Libraries present the most obvious cases. but there are also interfaces between programs and between users and programs. The desire for simplicity and generality applies especially strongly to the design of interfaces. Make interfaces consistent and easy to learn and use; adhere to them scrupulously. Abstraction is an effective technique: imagine a perfect component or library or program; make the interface match that ideal as closely as possible; hide implementation details behind the boundary, out of harm's way. 
>
> ***Automation*** is under-appreciated. It is much more effective to have a computer do your work than to do it by hand. We saw examples in testing, in debugging, in performance analysis, and notably in writing code, where for the right problem domain, programs can create programs that would be hard for people to write. 
>
> ***Notation*** is also under-appreciated,and not only as the way that programmers tell computers what to do. It provides an organizing framework for implementing a wide range of tools and also guides the structure of the programs that write programs. We are all comfortable in the large general-purpose languages that serve for the bulk of our programming. But as tasks become so focused and well understood that programming them feels almost mechanical, it may be time to create a notation that naturally expresses the tasks and a language that implements it. Regular expressions are one of our favorite examples, but there are countless opportunities to create little languages for specialized applications. They do not have to be sophisticated to reap benefits.  
>
> As individual programmers, it's easy to feel like small cogs in a big machine, using languages and systems and tools imposed upon us, doing tasks that should be done for us. But in the long run, what counts is how well we work with what we have. By applying some of the ideas in this book, you should find that your code is easier to work with, your debugging sessions are less painful, and your programming is more confident. We hope that this book has given you something that will make your computing more productive and more rewarding.
>
> (Kernighan et Pike 2010, pp. 247-248)

>#### Épilogue
>
>> Si les hommes pouvaient apprendre de l’histoire, quelles leçons elle pourrait nous enseigner ! Mais la passion et les partis pris aveuglent nos yeux, et la lumière que donne l’expérience est une lanterne à la poupe, qui n’éclaire que les vagues que nous avons laissées derrière nous.
>> — *Samuel Taylor Coleridge, Recollections*
>
>Le monde de l’informatique change sans cesse, et le rythme semble s’accélérer. Les programmeurs doivent faire face à de nouveaux langages, de nouveaux outils, de nouveaux systèmes, et bien sûr à des modifications incompatibles apportées aux anciens. Les programmes sont plus volumineux, les interfaces plus complexes, les délais plus courts.
>
>Mais il existe certaines constantes, des points de stabilité, où les leçons et les intuitions du passé peuvent éclairer l’avenir. Les thèmes fondamentaux de ce livre reposent sur ces principes durables.
>
>La ***simplicité*** et la ***clarté*** sont les premières et les plus importantes, car presque tout découle d’elles. Faites la chose la plus simple qui fonctionne. Choisissez l’algorithme le plus simple qui soit probablement assez rapide, et la structure de données la plus simple qui accomplira la tâche ; combinez-les avec un code propre et clair. Ne les compliquez pas, sauf si des mesures de performance montrent qu’un effort d’ingénierie supplémentaire est nécessaire. Les interfaces doivent être épurées et légères, du moins tant qu’il n’existe pas de preuve convaincante que les bénéfices compensent la complexité ajoutée.
>
>La ***généralité*** va souvent de pair avec la simplicité, car elle permet parfois de résoudre un problème une fois pour toutes, plutôt que de le refaire encore et encore pour chaque cas particulier. C’est aussi souvent la bonne approche pour la portabilité : trouver la solution générale unique qui fonctionne sur chaque système, au lieu d’amplifier les différences entre eux.
>
>L’***évolutivité*** vient ensuite. Il est impossible de créer un programme parfait du premier coup. L’intuition nécessaire pour trouver la bonne solution ne vient qu’avec une combinaison de réflexion et d’expérience ; la pure introspection ne produira pas un bon système, pas plus que le simple bidouillage. Les réactions des utilisateurs jouent ici un rôle essentiel : un cycle de prototypage, d’expérimentation, de retours et de perfectionnements successifs est le plus efficace. Les programmes que nous construisons pour nous-mêmes n’évoluent souvent pas assez ; les grands programmes que nous achetons à d’autres changent trop vite sans nécessairement s’améliorer.
>
>Les ***interfaces*** constituent une grande part du défi en programmation, et les questions d’interface apparaissent à de nombreux niveaux. Les bibliothèques en sont les cas les plus évidents, mais il existe aussi des interfaces entre programmes, et entre utilisateurs et programmes. Le désir de simplicité et de généralité s’applique tout particulièrement à la conception des interfaces. Faites des interfaces cohérentes, faciles à apprendre et à utiliser ; respectez-les scrupuleusement. L’abstraction est une technique efficace : imaginez un composant, une bibliothèque ou un programme parfait ; faites en sorte que l’interface corresponde le plus possible à cet idéal ; cachez les détails d’implémentation derrière la frontière, à l’abri des interférences.
>
>L’***automatisation*** est sous-estimée. Il est bien plus efficace de laisser un ordinateur faire votre travail que de le faire à la main. Nous en avons vu des exemples dans les tests, le débogage, l’analyse des performances, et surtout dans la génération de code, où, pour un domaine de problème bien choisi, des programmes peuvent créer d’autres programmes qu’il serait difficile pour un humain d’écrire.
>
>La ***notation*** est elle aussi sous-estimée, non seulement comme moyen pour les programmeurs d’indiquer à l’ordinateur ce qu’il doit faire, mais aussi comme cadre d’organisation pour la mise en œuvre d’un large éventail d’outils, et comme guide pour la structure des programmes qui en écrivent d’autres. Nous sommes tous à l’aise dans les grands langages polyvalents qui servent pour l’essentiel de notre programmation. Mais lorsque les tâches deviennent si ciblées et bien comprises que les programmer semble presque mécanique, il est peut-être temps de créer une notation qui exprime naturellement ces tâches, ainsi qu’un langage qui la mette en œuvre. Les expressions régulières en sont l’un des exemples privilégié, mais les occasions de créer de petits langages pour des applications spécialisées sont innombrables. Il n’est pas nécessaire qu’ils soient sophistiqués pour en tirer des bénéfices.
>
>En tant que programmeurs individuels, il est facile de se sentir comme de petits rouages dans une grande machine, utilisant des langages, des systèmes et des outils imposés, effectuant des tâches qui devraient être automatisées. Mais à long terme, ce qui compte, c’est la manière dont nous travaillons avec ce que nous avons. En appliquant certaines des idées présentées dans ce livre, vous constaterez que votre code est plus facile à gérer, vos sessions de débogage moins pénibles, et votre programmation plus assurée. Nous espérons que ce livre vous aura apporté quelque chose qui rendra votre pratique de l’informatique plus productive et plus gratifiante.
>
>(Kernighan et Pike, 2010, p. 247-248)

## Philosophie Unix selon Mike Gancarz

En 1994, Mike Gancarz qui fut un des membres de l’équipe qui conçut le système X Window, utilisa son expérience personnelle d’Unix et ses discussions avec d’autres programmeurs pour proposer *La Philosophie Unix* énoncée en neuf préceptes :

> 1. La concision est merveilleuse.
> 2. Écrivez des programmes qui font une seule chose mais qui le font bien.
> 3. Concevez un prototype dès que possible.
> 4. Préférez la portabilité à l’efficacité.
> 5. Stockez les données en ASCII.
> 6. Utilisez le levier du logiciel à votre avantage.
> 7. Utilisez les scripts shell pour améliorer l’effet de levier et la portabilité.
> 8. Évitez les interfaces utilisateur captives.
> 9. Faites de chaque programme un filtre.

## Pire c’est mieux

Richard P. Gabriel suggère que le point clé pour UNIX est qu’il incarne un concept philosophique qu’il désigna par « Pire c’est mieux » (*Worse is better*). Selon ce principe de conception, la simplicité à la fois de l’interface et à la fois de l’implantation compte plus que n’importe quelle autre caractéristique du système — y compris l’exactitude, la cohérence et la complétude. 

## Keep It Simple, Stupid (KISS)

Appelé *KISS principle* en anglais, l’acronyme KISS est décliné en :

> - *Keep it simple, stupid* : « laisse-le simple, stupide » ;
> - *Keep it stupidly simple* : « laisse-le stupidement simple » ;
> - *Keep it stupid simple* : « laisse-le stupidement simple » ;
> - *Keep it simple and stupid* : « laisse-le simple et stupide » ;
> - *Keep it simple, silly* : « laisse-le simple, idiot » ;
> - *Keep it small and simple* : « laisse-le simple et bref » ;
> - *Keep it sweet and simple* : « laisse-le simple et agréable » ;
> - *Keep it simple and straightforward* : « laisse-le simple et direct » ;
> - *Keep it short and simple* : « laisse-le simple et court » ;
> - *Keep it simple and smart* : « laisse-le simple et intelligent » ;
> - *Keep it strictly simple* : « laisse-le strictement simple » ;
> - *Keep it speckless and sane* : « laisse-le sain et impeccable » ;
> - *Keep it super-simple* : « laisse-le super-simple » ;
> - *Keep it sober and significant* : « laisse-le sobre et explicite » ;
> - *Keep it short and sweet* : « laisse-le court et sympa ».
> - *Keep information security simple* : « garde simple la sécurité des informations ».
> - *Keep it safe and simple* : « laisse-le sûr et simple ».

## Raymond : L’Art de la Programmation Unix

Dans son livre *The Art of Unix Programming*, Eric S. Raymond résume la philosophie Unix par le principe KISS : « Keep it Simple, Stupid ». 

> Règle de **modularité** : Écrire des éléments simples reliés par de bonnes interfaces.
>
> Règle de **clarté** : la clarté vaut mieux que l’ingéniosité.
>
> Règle de **composition** : concevoir des programmes qui peuvent être reliés à d’autres programmes.
>
> Règle de **séparation** : séparer les règles du fonctionnement ; Séparer les interfaces du mécanisme.
>
> Règle de **simplicité** : concevoir pour la simplicité ; ajouter de la complexité seulement par obligation.
>
> Règle de **parcimonie** : écrire un gros programme seulement lorsqu’il est clairement démontrable que c’est l’unique solution.
>
> Règle de **transparence** : concevoir pour la visibilité de façon à faciliter la revue et le débugage.
>
> Règle de **robustesse** : la robustesse est l’enfant de la transparence et de la simplicité.
>
> Règle de **représentation** : inclure le savoir dans les données, de manière que l’algorithme puisse être bête et robuste.
>
> Règle de la **moindre surprise** : pour la conception d’interface, réaliser la chose la moins surprenante.
>
> Règle du **silence** : Quand un programme n’a rien d’étonnant à dire, il doit se taire.
>
> Règle de **dépannage** : Si le programme échoue, il faut le faire bruyamment et le plus tôt possible.
>
> Règle d’économie : Le temps de programmation est cher, le préserver par rapport au temps de la machine.
>
> Règle de **génération** : éviter la programmation manuelle ; écrire des programmes qui écrivent des programmes autant que possible.
>
> Règle d’**optimisation** : prototyper avant de fignoler. Mettre au point avant d’optimiser.
>
> Règle de **diversité** : se méfier de la prétention d’une « unique bonne solution ».
>
> Règle d’**extensibilité** : concevoir pour le futur, car il arrivera plus vite que prévu.

## Citations

- « Unix est simple. Il faut juste être un génie pour comprendre sa simplicité. » – Dennis Ritchie
- « Unix n’a pas été conçu pour empêcher ses utilisateurs de commettre des actes stupides, car cela les empêcherait aussi de réaliser des actes ingénieux. » – Doug Gwyn
- « Unix ne dit jamais ‘s’il vous plaît’. » – Rob Pike
- « Unix est convivial. Cependant Unix ne précise pas vraiment avec qui. » – Steven King
- « Ceux qui ne comprennent pas Unix sont condamnés à le ré-inventer, lamentablement. » – Henry Spencer.

## Références

- McIlroy, Douglas, E. N. Pinson, et B. A. Tague. 1978. « UNIX Time-Sharing System: Forward ». *The Bell System Technical Journal* 57 (6). https://doi.org/10.1002/j.1538-7305.1978.tb02135.x.
- The Linux Information Project. 2006. « Unix Philosophy : A Brief introduction ». https://www.linfo.org/unix_philosophy.html.
- Kernighan, Brian W., et Rob Pike. 1999. *The Practice of Programming*. Addison-Wesley.