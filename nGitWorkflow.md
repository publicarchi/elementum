Git Workflow
============

Lorsque l'on travaille à plusieurs sur un projet commun avec Git, il est habituellement nécessaire de définir un flux de travail pour gérer les contributions.

Plusieurs modèles de workflows sont possibles qui offrent divers niveaux de collaboration. Un modèle centralisé autour d'un entrepôt commun, ou des configurations distribuées. Les facilités de création de branches de travail de Git, et l'utilisation d'un entrepôt distant hébergé sur un serveur comme Github incitent plutôt à des modes d'organisation distribués.

Dans une telle organisation, les collaborateurs travaillent sur des copies du projet prinicpal qu'ils peuvent modifier comme ils le souhaitent. Une fois les modifications effectuées, ceux-ci peuvent proposer d'intégrer les changements au projet principal au moyen de "pull request".


### Récupérer les sources

La commande `clone` permet d'obtenir une copie du dépôt sur sa machine :

`git clone git://github.com/user/directory.git directory`

Les commandes `branch` et `tag` permettent de lister les branches et les versions disponibles.

`git branch # lister les branches`
`git tag # lister les tags`


Avec `checkout` on peut se déplacer dans l'historique du dépôt :

`git checkout 2.0 # passer sur la branche 2.0`
`git checkout 2.0.1 # passer sur le tag 2.0.1`

Vous disposez mainenant d'un répertoire local dont la source a pu évoluer depuis que vous l'avez cloné. On peut mettre à jour la version locale de son répertoire avec le répertoire distant avec `fetch` qui ramène tous les nouveaux commits et les résumés des changements.

`git fetch # mettre à jour les sources`

N'oubliez d'utiliser `checkout` pour accéder aux nouvelles branches ou aux nouveaux tags.

### Créer une branche directement depuis l'entrepôt

La création de branches de travail est aisée avec Git, il ne faut pas s'en priver. Créer des branches de travail permettra de facilement distinguer sa contribution pour qu'elle soit évaluée avant de pouvoir être intégrée au répertoire principal.

`git checkout -b new_feature # créer une nouvelle branche`


Soit on forke le répertoire pour travailler sur une copie du répertoire. Soit on branch directement depuis dépôt distant.


### 1. forker le répertoire principal

Le projet est publié dans un répertoire principal. Chaque collaborateur dispose d'un fork de ce répertoire  principal qui sont des copies du projet et qu'ils peuvent modifier comme ils le souhaitent.

Pour forker un répertoire Gihub, cliquez sur le bouton "Fork" dans l'interface sur la page du projet.

Ainsi, on dispose maintenant de deux URLs du genre :
`project/directory.git # répertoire principal du projet`
`user/directory.git # fork du répertoire principal`

### 2. cloner votre fork

Pour pouvoir travailler sur votre fork, vous devez cloner votre répertoire, c'est-à-dire rapatrier les sources dans un répertoire local.

`git clone git://github.com/user/directory.git directory` ## cloner votre fork dans un répertoire local

### 2. configurez les remote "upstream"

Lorsque l'on clone un répertoire, celui-ci dispose toujours d'un remote par défaut appelé "origin" qui pointe vers votre fork et non pas le répertoire d'origine que vous avez forké. Pour garder un lien vers ce répertoire initial vous devez ajouter un autre remote appelé "upstream".

On ajoute à ce fork un remote nommé "upstream" pour pointer vers répertoire initial du projet.

`git remote add upstream git://github.com/project/directory.git`

La commande `fetch` permet de rapatrier les modifications du répertoire initial non présentes dans votre répertoire.

`git fetch upstream` # rapartrier les modifications du répertoire initial du projet sans modifier vos fichiers

On peut également mettre à jour sa branche master de la manière suivante :

```bash
git checkout master # se placer sur la branche master de son fork
git remote add upstream git://github.com/user/mainDirectory.git
git pull upstream master # récupérer les dernières modifications de la branche principale
git checkout new_feature # retourner sur la branche de développement
```

En utilisant l'URL du répertoire principal


### 2.

Toujours produire ses modifications dans une branche de travail et conserver la branche "master" propre. Seulement utiliser cette branche pour y placer les modifications à intégrer.

```bash
git branch new_feature # créer une nouvelle branche pour une fonctionnalité
git checkout new_feature # aller sur la branche de la nouvelle fonctionnalité
````

On peut également utiliser le raccourci suivant :

`git checkout -b new_feature`

Indexer et commiter régulièrement avec les commandes `add` et `commit`

`git add . # ajouter toutes les modifications à l'index`
`git add file.ext # ajouter les modifications d'un fichier spécifique à l'index`
`git commit -m "message" # commiter les modifications indexées avec un message`

ou directement si tout est à ajouter à l'index et à commiter

`git commit -am "message"`

Avant d'intégrer vos changements à la branche master, vérifiez vos modifications et vérifiez la qualité du code

`git diff master`


Une fois la nouvelle fonctionnalité terminée, utiliser `merge` pour les combiner dans la branche master

```bash
git checkout master # faire de "master" la branche active
git merge new_feature # fusionner les commits provenant de "new_feature" à l'intérieur de "master"
git branch -d new_feature # Effacer la branche "new_feature"

```

### Rebaser avant de commiter

Pour faciliter le travail d'intégration, il convient d'éviter d'éventuels conflits en utilisant la commande `rebase`. Cette commande permet de mettre à jour votre branche avec le dernier commit du dépôt original.

` git rebase master `

Il est également possible de fusionner tous les commits réalisés avec l'option `-i` pour proposer un historique plus simple à l'intégrateur.

Remplacer "pick" par "squash" le début des lignes qui doivent être confondues dans un même commit.

Remarque : la commande `rebase` est à éviter sur des commits ayant déjà été partagés et sur lesquelles d'autres personnes peuvent avoir basé des modifications.

Sans rebase, il est possible de mettre à jour sa branche avec l'upstream

```bash
git checkout master
git fetch upstream
git merge upstream/master
git chekout new_feature
git rebase master
```

Au cours du rebasage, vous pouvez avoir des conflits

```bash
git add ... # ajouter les fichiers résolus
git rebase --contine
```

### Rendre visible son travail

La dernière étape consiste à rendre visible son travail en le publiant sur github afin de faire un "pull request"

` git push origin new_feature `

Par l'intermédiaire de github, il est désormais possible de faire un "pull request" pour proposer au projet l'intégration de votre contribution (patch).

## processus

1. diposez d'une branche remote pointant vers le répertoire principal
2. récupérez (pull) régulièrement les changements de cette branche dans la branche master
3. créez une branche pour chaque travail sur lequel vous travaillé. Ces branches seront généralement seulement locales. Lorsque vous récupérez les changement de upstream dans master, rebaser vos branches de travail pour refléter ces changements
4. quand vous avez terminé un certain travail, merger dans master. Ainsi les personnes dérivant de votre travail ne verront pas trop d'historique puisque le rebasage intervient dans votre branche locale de travail
5. soumettez les changements : votre branche master comprendra une série de commits dont certains seront identiques à upstream, les autres les votres. Ceux-ci peuvent être adressés comme patch si vous le souhaitez
