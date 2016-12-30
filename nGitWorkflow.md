# Git Workflow

Lorsque l’on travaille à plusieurs sur un projet commun avec Git, il est habituellement nécessaire de définir un flux de travail pour gérer les contributions.

Plusieurs modèles de workflows sont possibles qui offrent divers niveaux de collaboration : un modèle centralisé autour d’un entrepôt commun, ou des configurations distribuées. Les facilités de création de branches de travail offertes par Git, et l’utilisation d’un entrepôt distant hébergé sur un serveur comme Github incitent plutôt à utiliser des modes d’organisation distribués.

Dans une telle organisation, les collaborateurs travaillent sur des copies du projet principal qu’ils peuvent modifier comme ils le souhaitent. Une fois les modifications effectuées, ceux-ci peuvent proposer d’intégrer les changements au projet principal au moyen de "pull request".


## Opérations élémentaires

### Récupérer les sources

La commande `clone` permet d’obtenir une copie du dépôt sur sa machine :

`git clone git://github.com/user/directory.git directory`


Les commandes `branch` et `tag` permettent de lister les branches et les versions disponibles.

`git branch # lister les branches`

`git tag # lister les tags`


Avec `checkout` on peut se déplacer dans l’historique du dépôt :

`git checkout 2.0 # passer sur la branche 2.0`

`git checkout 2.0.1 # passer sur le tag 2.0.1`


Vous disposez maintenant d’un répertoire local dont la source a pu évoluer depuis que vous l’avez cloné. On peut mettre à jour la version locale de son répertoire avec cette du répertoire distant avec `fetch` qui ramène tous les nouveaux commits et les résumés des changements.

`git fetch # mettre à jour les sources`

N’oubliez d’utiliser `checkout` pour accéder aux nouvelles branches ou aux nouveaux tags.


### Créer une branche directement depuis l’entrepôt

La création de branches de travail est aisée avec Git, il ne faut pas s’en priver. Créer des branches de travail permettra de facilement distinguer sa contribution pour qu’elle soit évaluée avant de pouvoir être intégrée au répertoire principal.

`git checkout -b new_feature # accéder à la  nouvelle branche`


Soit on forke le répertoire pour travailler sur une copie du répertoire. Soit on branch directement depuis dépôt distant.


### 1. forker le projet d’origine

Le projet est publié dans un répertoire principal. Chaque collaborateur dispose d’un fork de ce projet initial qui sont des copies et qu’ils peuvent modifier comme ils le souhaitent.

Pour forker un répertoire Gihub, cliquez sur le bouton "Fork" dans l’interface sur la page du projet.

Ainsi, on dispose maintenant de deux URLs du genre :

`project/directory.git # répertoire du projet initial`

`user/directory.git # fork du projet initial`


Pour pouvoir travailler sur votre fork, vous devez cloner votre répertoire, c’est-à-dire rapatrier les sources dans un répertoire local.

`git clone git://github.com/user/directory.git directory` ## cloner votre fork dans un répertoire local


### 2. configurez les remote "upstream"

Lorsque l’on clone un répertoire, celui-ci dispose toujours d’un remote par défaut appelé "origin" qui pointe vers votre fork et non pas le répertoire d’origine que vous avez forké. Pour garder un lien vers ce répertoire initial vous devez ajouter un autre remote appelé "upstream".

On ajoute à ce fork un remote nommé "upstream" pour pointer vers répertoire initial du projet.

`git remote add upstream git://github.com/project/directory.git`

La commande `fetch` permet de rapatrier les modifications du répertoire initial non présentes dans votre répertoire.

`git fetch upstream # rapartrier les modifications du répertoire initial du projet sans modifier vos fichiers`


Il est possible d’afficher la configuration des remotes avec la commande suivante :

`git remote -v # lister les remote en mode verbose`


Une fois la branche `upstream` configurée, il est désormais possible de mettre à jour sa branche master à partir du projet d’origine de la manière suivante :

```bash
git checkout master # se placer sur la branche master de son fork
git fetch upstream master # récupérer les dernières modifications de la branche principale de upstream
git pull upstream master # remplacer la branche locale par les dernières modifications de la branche principale de upstream : préférer un rebase
git checkout new_feature # retourner sur la branche de développement
```


### 3. toujours conserver la branche `master` propre

Par convention, on produit toujours ses modifications dans une branche de travail et l’on conserve la branche `master` propre et fonctionnelle. On peut notamment y placer les modifications destinées à être intégrées au projet.

```bash
git branch new_feature # créer une nouvelle branche pour une fonctionnalité
git checkout new_feature # aller sur la branche de la nouvelle fonctionnalité
```

On peut également utiliser le raccourci suivant :

`git checkout -b new_feature # créer une nouvelle branche pour une fonctionnalité et s’y rendre`


Indexer et faire des commits régulièrement avec les commandes `add` et `commit`

```bash
git add . # ajouter toutes les modifications à l’index
```

```bash
git add file.ext # ajouter les modifications d’un fichier spécifique à l’index
```

```bash
git commit -m "message" # commiter les modifications indexées avec un message`
```

ou directement si tout est à ajouter à l’index et à commiter

```bash
git commit -am "message"
```


Avant d’intégrer vos changements à la branche master, vérifiez vos modifications et vérifiez la qualité du code

```bash
git diff master
```


Une fois la nouvelle fonctionnalité terminée, utiliser `merge` pour les combiner dans la branche master

```bash
git checkout master # faire de "master" la branche active
git merge new_feature # fusionner les commits provenant de "new_feature" à l’intérieur de "master"
git branch -d new_feature # Effacer la branche "new_feature"
```

### Rebaser avant de commiter

Pour faciliter le travail d’intégration, on peut éviter d’éventuels conflits en utilisant la commande `rebase`. Cette commande permet de mettre à jour votre branche avec le dernier commit du dépôt original. Elle permet de créer un historique de commits plus linéaire et le rebasage interactif permet de modifier l’historique des commits.

```bash
git rebase master # rebase la branche courante avec master
```

Afin de proposer un historique plus simple à l’intégrateur, il est possible de fusionner tous les commits réalisés au cours d’un rebase interactif avec l’option `-i`.

```bash
git rebase -i master # rebase la branche courante avec master
```

Dans l’éditeur de recombinaison interactive, http://alx.github.io/gitbook/4_recombinaison_interactive.html

Remplacer "pick" par "squash" au début des lignes qui doivent être confondues dans un même commit.

Si ’pick’ est sélectionné, git essayera simplement d’appliquer le patch et de sauvegarder le commit avec le même message qu’avant.

Si ’squash’ est sélectionné, il combinera ce commit avec le précédent pour former un nouveau commit. Vous trouverez alors un autre éditeur pour merger les messages des 2 commit qui ont étés assemblés ensemble.

En effaçant la ligne, on peut également retirer un commit de l’historique (et ses modifications ??).


Remarque : la modification de l’historique avec le rebasage interactif `rebase -i` est à éviter sur des commits ayant déjà été partagés et à partir desquels d’autres personnes peuvent avoir fondés des modifications.

Sans rebase, il est possible de mettre à jour sa branche avec l’upstream

```bash
git checkout master # passer sur la branche master
git fetch upstream # synchroniser upstream
git merge upstream/master # mettre à jour master avec upstream/master
git chekout new_feature # repasser sur la branche de nouvelles fonctionnalités
git rebase master # rebaser avec master
git checkout master # revenir sur la branche master
git merge new_feature # merger la branche master avec new_feature
git branch -d new_feature # supprimer la branche new_feature
```

Au cours du rebasage, vous pouvez éventuellement rencontrer des conflits

```bash
git add ... # ajouter les fichiers résolus
git rebase --contine
```


### Rendre visible son travail

La dernière étape consiste à rendre visible son travail en le publiant sur github afin de faire un "pull request"

` git push origin new_feature `

Par l’intermédiaire de github, il est désormais possible de faire un "pull request" pour proposer au projet l’intégration de votre contribution (patch).

## processus

1. cloner le fork et ajouter une branche remote pointant vers le répertoire initial du projet
2. récupérez (pull) régulièrement les changements de cette branche dans la branche master
3. créez une branche pour chaque travail sur lequel vous travaillez. Ces branches seront généralement seulement locales. Lorsque vous récupérez les changement de upstream dans master, rebaser vos branches de travail pour refléter ces changements
4. quand vous avez terminé un certain travail, merger dans master. Ainsi les personnes dérivant de votre travail ne verront pas trop d’historique puisque le rebasage intervient dans votre branche locale de travail
5. soumettez les changements : votre branche master comprendra une série de commits dont certains seront identiques à upstream, les autres les vôtres. Ceux-ci peuvent être adressés comme patch si vous le souhaitez


## Commandes avancées

### Annuler le dernier commit non propagé

Lorsque l’on a commité, il arrive parfois que l’on s’aperçoive que le commit comporte des fichiers qui ne doivent pas en faire partie ou qu’il manque certains changement.

Lorsque le commit n’est pas propagé (`push`), il est encore possible d’annuler ce dernier commit tout en conservant les changements à l’aide de la commande suivante.

```bash
git reset HEAD^ # replace la tête à l’emplacement avant le précédent commit
```

Autrement

```bash
git commit -a --amend # équivaut à `git reset ^HEAD && git commit -a`
```

permet d’intégrer les dernières modifications au commit précédent.


### ajout interactif

http://alx.github.io/gitbook/4_ajout_interactif.html


## Références

- http://git-scm.com/book/fr/v1/Git-distribué-Contribution-à-un-projet

- https://www.atlassian.com/fr/git/workflows
