---
tags: git
---

# Utilisation des sous-modules de Git

Le développement informatique implique souvent la réutilisation de bibliothèques de code déjà existantes. L’utilisation des sous-modules (*submodules*) de Git permet d’intégrer dans des répertoires spécifiques des composants qui sont versionnés séparément. C’est une manière d’ajouter des dépendances ou des extensions en tirant pleinement parti des fonctionnalités du versionnement de fichiers.

L’utilisation de sous-modules Git pour l’intégration de dépendances ou la gestion d’extensions est une bonne pratique car cela permet de clairement séparer leur code informatique. Elle permet en outre de pouvoir versionner le projet de manière fine et de gérer d’éventuels conflits avec les versions des composants. 

## Ajout d’un sous-module

Pour ajouter un sous-module dans un répertoire Git, il suffit de lancer la commande suivante :

```bash
git submodule add https://github.com/user/project.git
```

Il est possible de choisir le chemin du sous-module de la manière suivante :

```bash
git submodule add https://github.com/user/project.git <repository/name>
```

## Cloner un répertoire et ses sous-modules

Il faut ajouter une close `--recursive` pour cloner un répertoire avec ses sous-modules.

```bash
git clone --recursive https://github.com/user/project.git
```

## Mettre à jour le répertoire

Git n’ajoute pas automatiquement les sous-modules à un répertoire. Afin de les ajouter lancer la commande.

```bash
git submodule update
```

S’il y a des répertoires imbriqués

```bash
git submodule update --recursive
```

## Mettre à jour un sous-module

Les sous-modules ne se mettent pas automatiquement à jour avec le répertoire distant. Pour ce faire, il est nécessaire de se rendre dans le répertoire du sous-module pour le mettre à jour manuellement.

```bash
cd projects/project-name
git pull origin master
cd ../..
git commit -m "I updated extension-name" # si vous versionnez l'ensemble
```

Ou encore, pour mettre à jour les changements du répertoire, incluant les changements dans les sous-modules

```bash
git pull --recurse-submodules
```

Mettre à jour tous les changements des sous-modules

```bash
git submodule update --remote
```

## Supprimer un sous-module

```bash
mv a/submodule a/submodule_tmp
git submodule deinit -f -- a/submodule    
rm -rf .git/modules/a/submodule
git rm -f a/submodule
```

Ou si vous voulez le conserver dans l’arbre de travail

```bash
git rm --cached a/submodule
mv a/submodule_tmp a/submodule
```

## Références

- [Atlassian, Git submodules](https://www.atlassian.com/git/tutorials/git-submodule)
- [Git Documentation, Submodules](https://git-scm.com/docs/gitsubmodules)
- [GitBook, Git Tools - Submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules)

- http://www.getsymphony.com/learn/articles/view/getting-git-for-symphony-development/
- http://www.getsymphony.com/learn/articles/view/on-git-submodules/
