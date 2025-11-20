---
since: 2025-10-27
---

# Design Pattern

Le développement logiciel utilise souvent des patrons de conception (*design pattern*) réutilisables pour solutionner des problèmes récurrents. 

Idiotismes de programmation

L’ouvrage *Design Patterns. Elements of Reusable Object-Oriented Software* a largement contribué à fixer cette terminologie en décrivant des solutions « simples et élégantes pour des problèmes spécifiques en conception logicielle orientée-objet » (Gamma et al. 1994, p. XI). 

> One thing expert designers know not to do is solve every problem from  first principles. Rather, they reuse solutions that have worked for them in the past. When they find a good solution, they use it again and  again. Such experience is part of what makes them experts. Consequently, you’ll find recurring patterns of classes and communicating objects in  many object-oriented systems. **These patterns solve specific design problems and make object-oriented designs more flexible, elegant, and  ultimately reusable.** They help designers reuse successful designs by basing new designs on prior experience. A designer who is familiar with  such patterns can apply them immediately to design problems without  having to rediscover them. 
>
> (Gamma et al. 1994, p. 1) 

Dans leur ouvrage, les auteurs font explicitement référence au travail de l’architecte Christopher Alexander sur les design patterns (Gamma et al. 1994, p. 2). 

> For this book we have concentrated on patterns at a certain level of  abstraction. Design patterns are not about designs such as linked lists and hash tables that can be encoded in classes and reused as is. Nor are they complex, domain-specific designs for an entire application or  subsystem. The design patterns in this book are *descriptions of  communicating objects and classes that are customized to solve a general design problem in a particular context*. 
>
> (Gamma et al. 1994, p. 3) 

### L’exemple Modèle/Vue/Contrôleur (MVC)

La triade de classes Model/View/Controller est employée pour construire des interfaces en Smalltalk-80. Ce patron de développement consiste en trois types d’objets. Le Modèle est l’objet d’application, la Vue est sa présentation à l’écran, le Contrôleur définit la manières dont l’interface utilisateur réagit aux entrées de l’utilisateur. Le patron MVC découple ces éléments pour augmenter leur flexibilité et leur réutilisation.

Ce patron découple les vues et les modèles en établissant entre eux un protocole subscribe/notification. La vue doit assuréer que son apparence reflète l’état du modèle. Lorsque les données changent, le modèle notifie ces changements aux vues qui en dépendent. Celles-ci se mettent à jour. Dans cette approche, il est également possible d’avoir des vues multiples pour un même modèle.

Cette conception découplée est applicable à un problème plus général où l’on découple des objets de sorte que les changements puissent affecter plusierus autres sans exciger de changer l’objet pour connaître le détails des autres. Ce patron général est décrit par l’Observer.

[@todo autres parties du dispositifs correspondant autres méthodes]

## Types de patrons

Vingt-trois *design patterns* sont proposés dans (Gamma et al. 1994, p. 3). Les patrons les plus couramment utilisés sont les suivants : Abstract Factory ; Factory Method ; Adapter ; Observer ; Composite ; Strategy ; Decorator ; Template Method.

La liste suivante propose une traduction de celle donnée dans Gamma et al. 1994, pp. 9 et 10.

- **Abstract Factory.** Fournit une interface pour créer des familles d’objets liés ou dépendants sans spécifier leurs classes concrètes. 
  *cf. Gamma et al. 1994, p. 87.*
- Adapter (139) Convertit l’interface d’une classe en une autre interface attendue par les clients. L’adaptateur permet à des classes de collaborer alors qu’elles ne le pourraient pas autrement à cause d’interfaces incompatibles. 
  *cf. Gamma et al. 1994, p. 139.*
- ***Bridge***. Dissocie une abstraction de son implémentation de sorte que les deux puissent évoluer indépendamment. 
  *cf. Gamma et al. 1994, p. 151.*
- ***Builder***. Sépare la construction d’un objet complexe de sa représentation, de façon à ce que le même processus de construction puisse créer différentes représentations. 
  *cf. Gamma et al. 1994, p. 97.*
- ***Chain of Responsibility***. Évite de coupler l’émetteur d’une requête à son récepteur en donnant à plusieurs objets la possibilité de traiter la requête. Les objets récepteurs sont chaînés et la requête est transmise le long de la chaîne jusqu’à ce qu’un objet la prenne en charge. 
  *cf. Gamma et al. 1994, p. 223.*
- ***Command***. Encapsule une requête dans un objet, permettant ainsi de paramétrer les clients avec différentes requêtes, de mettre en file ou de journaliser les requêtes, et de supporter l’annulation des opérations. 
  *cf. Gamma et al. 1994, p. 233.*
- ***Composite***. Compose des objets en structures arborescentes pour représenter des hiérarchies partie-tout. Le composite permet de traiter de manière uniforme les objets individuels et les compositions d’objets.
  *cf. Gamma et al. 1994, p. 163.*
- ***Decorator***. Ajoute dynamiquement des responsabilités supplémentaires à un objet. Les décorateurs offrent une alternative flexible à l’héritage pour étendre les fonctionnalités. 
  *cf. Gamma et al. 1994, p. 175.*
- ***Facade***. Fournit une interface unifiée à un ensemble d’interfaces dans un sous-système. La façade définit une interface de plus haut niveau qui rend le sous-système plus facile à utiliser. 
  *cf. Gamma et al. 1994, p. 185.*
- ***Factory Method***. Définit une interface pour créer un objet, mais laisse les sous-classes décider quelle classe instancier. La méthode fabrique permet à une classe de déléguer l’instanciation à ses sous-classes. 
  *cf. Gamma et al. 1994, p. 107.*
- ***Flyweight***. Utilise le partage pour supporter efficacement un grand nombre d’objets de petite granularité. 
  *cf. Gamma et al. 1994, p. 195.*
- ***Interpreter***. Pour un langage donné, définit une représentation de sa grammaire ainsi qu’un interpréteur qui utilise cette représentation pour interpréter des phrases dans ce langage. 
  *cf. Gamma et al. 1994, p. 243.*
- ***Iterator***. Fournit un moyen d’accéder séquentiellement aux éléments d’un objet agrégé sans exposer sa représentation sous-jacente. 
  *cf. Gamma et al. 1994, p. 257.*
- ***Mediator***. Définit un objet qui encapsule la manière dont un ensemble d’objets interagit. Le médiateur favorise un couplage faible en évitant que les objets se réfèrent explicitement les uns aux autres, ce qui permet de faire varier leurs interactions indépendamment. 
  *cf. Gamma et al. 1994, p. 273.*
- ***Memento***. Sans violer l’encapsulation, capture et externalise l’état interne d’un objet afin que celui-ci puisse être restauré à cet état ultérieurement. 
  *cf. Gamma et al. 1994, p. 283.*
- ***Observer***. Définit une dépendance un-à-plusieurs entre des objets de sorte que lorsque l’un change d’état, tous ses dépendants sont automatiquement notifiés et mis à jour. 
  *cf. Gamma et al. 1994, p. 293.*
- ***Prototype***. Spécifie les types d’objets à créer au moyen d’une instance prototypique et crée de nouveaux objets par copie de ce prototype. 
  *cf. Gamma et al. 1994, p. 117.*
- ***Proxy***. Fournit un substitut ou un représentant pour un autre objet afin d’en contrôler l’accès. 
  *cf. Gamma et al. 1994, p. 207.*
- ***Singleton***. Garantit qu’une classe n’a qu’une seule instance et fournit un point d’accès global à celle-ci. 
  *cf. Gamma et al. 1994, p. 127.*
- ***State***. Permet à un objet de modifier son comportement lorsque son état interne change. L’objet semble alors changer de classe. 
  *cf. Gamma et al. 1994, p. 305.*
- ***Strategy***. Définit une famille d’algorithmes, encapsule chacun d’eux et les rend interchangeables. La stratégie permet à l’algorithme de varier indépendamment des clients qui l’utilisent. 
  *cf. Gamma et al. 1994, p. 315.*
- ***Template Method***. Définit l’ossature d’un algorithme dans une opération, en reportant certaines étapes à des sous-classes. La méthode modèle permet aux sous-classes de redéfinir certaines étapes de l’algorithme sans en modifier la structure. 
  *cf. Gamma et al. 1994, p. 325.*
- **Visiteur (*Visitor*)**. Représente une opération à effectuer sur les éléments d’une structure d’objets. Le visiteur permet de définir une nouvelle opération sans modifier les classes des éléments sur lesquels il opère. 
  *cf. Gamma et al. 1994, p. 331.*

Catégorisation. Voir Table 1.1 : Design pattern space (Gamma et al. 1994, p. 10) 

Ces design patterns peuvent être classés selon deux critères, d’après les auteurs : en fonction de leur buts et de leur portée.

Le but reflète ce que font ces patterns qui peuvent être relatifs à la création d’objets, la structure ou le comportement. La portée spécifie si un pattern s’applique en premier lieu à des classes ou des objets.

Les patterns peuvent également avoir des relations entre eux.

## Références

Gamma, Erich, Richard Helm, Ralph Johnson, et John Vlissides. 1994. *Design Patterns: Elements of Reusable Object-Oriented Software (Joanne Romanovich’s Library)*. Addison-Wesley professional computing series. Addison-Wesley.

https://fr.wikipedia.org/wiki/Patron_de_conception

https://en.wikipedia.org/wiki/Adapter_pattern

