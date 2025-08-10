---
author: emchateau
since: 2015-12-02
tags: git
---
# Versionner ses fichiers avec Git [tutoriel]

---

# Git

Git est un logiciel de gestion de version (*versionning*), c’est à dire un logiciel qui permet de conserver la trace des changements effectués sur des fichiers au cours du temps. Git enregistre les modifications afin de pouvoir y faire référence ou pour revenir à une version antérieure du fichier.

Initialement développé par Linus Torvalds pour la gestion des sources informatiques du noyau Linux, Git est aujourd’hui un de slogiciel de gestion de version le plus populaire. Il constitue une infrastructure essentielle pour la collaboration sur des projets de logiciel libre et open source.

Dans ce tutoriel, nous allons travailler à la rédaction d’un simple fichier texte pour apprendre l’utilisation de Git.

---

# TP Création d’un fichier texte

Dans un répertoire `projet`, commençons par créer un fichier texte intitulé `texte-1.txt`, ajoutons-y notre texte dans un éditeur et sauvons.

```bash
  mkdir projet
  cd projet
  vim texte-1.txt
```

Rmq : Pour sauver et quitter dans vim `ESC puis :wq`

---

# Initialiser le versionning

Maintenant que nous avons commencé à travailler sur notre projet, nous allons transformer ce répertoire de travail en un projet Git.

```bash
  git init # initialise un répertoire git
```

La commande `init` initialise le versionning d’un répertoire. Elle met en place tous les outils dont Git a besoin pour commencer à conserver la trace de tous les changements réalisés au projet.

---

## TP Initialisation d’un nouveau projet

Dans le terminal, initialisons un nouveau projet Git.

Notez la sortie :

```
  Initialized empty Git repository in /Users/emmanuelchateau/Desktop/projet/.git/
```

Le projet Git a été créé.

---

## Le workflow de GIt

1 Working Directory
Faire les changements aux fichiers
+ ajouts
- suppressions
  modifications

-->

2 Staging Area
Mettre les changements dans la zone d’indexation

-->

3 Repository
Sauver les changements en tant que _commit_

???

Super ! nous disposons maintenant d’un projet Git. Un tel projet peut être considéré comme comportant trois parties :
1. Un _répertoire de travail (Working Directory)_ où vous allez réaliser tout le travail : création, édition, suppression et réorganisation de fichiers
2. Une _zone d’indexation (Staging Area)_ où vous allez lister les changements que vous faîtes au répertoire de travail.
3. Un _répertoire (Repository)_ où Git stocke de manière permanente ces changements en tant que versions différentes du projet.

Le workflow de Git consiste à éditer des fichiers dans le répertoire de travail, ensuite à les ajouter à la zone d’indexation, enfin de les enregistrer dans le répertoire Git. Avec Git, on sauve les changements avec un _commit_. C’est ce que nous allons voir plus en détail.

---

# Vérifier le statut

Au fur et à mesure de votre travail, vous allez faire des modifications aux fichiers contenus dans le répertoire de travail. Vous pouvez vérifier le statut de ces changements avec la commande

```bash
  git status
```

Sortie :

```
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	texte-1.txt

nothing added to commit but untracked files present (use "git add" to track)
```

Remarquez la ligne rouge dans la sortie. _Untracked files_ signifie que ces fichiers n’ont pas encore commencé à être suivis.

---
name: add

# Suivre des fichiers

Pour commencer à suivre le fichier `texte-1.txt`, celui-ci doit d’abord être ajouter à la zone d’indexation (_staging area_).

On peut l’ajouter avec la commande suivante :

```bash
  git add nom-fichier
```

Où _nom-fichier_ est le chemin du fichier que vous ajoutez (par exemple `texte-1.txt`)

---

# TP Suivre des fichiers

1. Ajoutez `texte-1.txt` à la zone d’indexation de Git. Souvenez-vous que vous allez devoir identifier le fichier par son nom.

2. Vérifiez le statut du projet dans Git.
Dans la sortie, notez que Git indique maintenant les changements à commiter avec "new file: texte-1.txt"

???

```bash
  git add texte-1.txt
  git status
```

```
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   test.xq
```

---

# Visualiser les différences

Bon travail ! Maintenant que vous savez comment ajouter des fichiers à la zone d’indexation, voyons comment visualiser les modifications.

Imaginons que vous fassiez des modifications dans votre fichier, par exemple en tapant une ligne supplémentaire après que ce fichier soit suit. On peut désormais visualiser les différences entre le répertoire de travail (_working directory_) et la zone d’indexation (_staging area_) avec la commande suivante :

```bash
  git diff filename
```

---

# TP Visualisation des différences

1. Dans votre éditeur, ajoutez du texte au fichier `texte-1.txt`
2. Sauvez
3. Depuis le terminal, utilisez cette nouvelle commande pour visualiser les différences entre le répertoire de travail et la zone d’indexation.
4. Remarquez la sortie

!! Pour quitter le mode diff tapez `q` sur votre clavier. Par défaut, Git utilise l’éditeur Vim.

5. Ajoutez les changements à la zone d’indexation de Git. Souvenez-vous que vous devez identifier le fichier par son nom.
[Coup de pouce](#add)

???

Remarquez la sortie :

```bash
  git diff texte-1.txt
```

```
diff --git a/test.xq b/test.xq
index e69de29..c02977f 100644
--- a/test.xq
+++ b/test.xq
@@ -0,0 +1 @@
+du texte ajouté
```

Comme on vous l’indique en blanc, le fichier est dans la zone d’indexation.

Les changements au fichier sont marqués précédé d’un `+` et apparaissent en vert.

---

# Créer un commit

La dernière étape du workflow Git est la création d’un commit. Il s’agit d’enregistrer de manière permanente les changements effectués dans la zone d’indexation.

Pour cela, on utilise la commande `git commit`. Il faut lui ajouter l’option `-m` suivie d’un message entre guillemets.

```bash
  git commit -m "Ajout d’une première ligne de texte"
```

Par convention, les messages de commit doivent être
- entre guillemets
- rédigés au présent
- brefs (moins de 50 caractères lorsque l’on utilise l’option `-m`)

---

# Création d’un premier commit

1. Créez maintennant votre premier commit ! Dans le terminal tapez cette commande avec un message de commit. Ce message doit décrire les modifications que vous enregistrez.

Si vous rencontrez des difficultés à trouver le message, pensez à la manière dont le projet a évolué depuis son commencement.

---

# logs

Il vous sera souvent nécessaire avec Git de vous référer à des versions précédentes d’un projet. Les commits sont stockés chronologiquement dans le répertoire et peuvent être visualisés avec :

```bash
  git log
```

---

# Visualisation des commits

1. Dans un terminal, affichez la liste de vos commits

Notez dans la sortie,
- un code de 40 charactères en orange appelé SHA qui identifie de manière unique le commit.
- l’auteur du commit : vous !
- la date et l’heure du commit
- le message de commit.

???

```bash
  git log
```

```
commit 6744995b21f5fcccdde437aa73b26504d776b31d
Author: Emmanuel Chateau <emchateau@laposte.net>
Date:   Wed Dec 2 12:47:34 2015 -0500

    ajout de texte
```

---

# Recap

Dans cette introduction vous avez découvert les fondamentaux du workflow de Git.

Git est un système de contrôle de version

Vous pouvez employer les commandes Git pour garder la trace des changements réalisés dans un projet
- `git init` créée un nouveau répertoire Git
- `git status` inspecte le contenu du répertoire de travail (_working directory_) et de la zone d’indexation (_staging area_)
- `git add` ajoute des fichiers du répertoire de travail à la zone d’indexation (_staging area_)
- `git diff` montre la différence entre le répetoire de travail (_working directory_) et la zone d’indexation (_staging area_)
- `git commit` stocke de manière permanente les modifications de fichiers du répertoire intervenues dans la zone d’indexation (_staging area_)
- `git log` affiche la liste des commits précédents

---

# sources

- cf. CodeCademy