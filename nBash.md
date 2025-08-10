---
author: emchateau
since: 2018-08-23
tags: linux, bash, command_line
---

# Travailler avec le Terminal

Le terminal de votre ordinateur est un programme qui vous permet d’interagir avec les couches basses de votre système. Toutes les opérations que vous effectuez habituellement dans une interface graphique pour la manipulation de fichiers dans le Finder sur Mac ou l’Explorateur de fichiers sur PC, peuvent être réalisées directement dans le terminal en ligne de commande.

Pour accéder au Terminal sur Mac, vous pouvez ouvrir l’application Terminal dans les Utilitaires.

## Commandes usuelles

| Commandes    | Description                                                  |
| ------------ | ------------------------------------------------------------ |
| cd [dossier] | changer de répertoire (*change directory*)                   |
| cd ~         | aller au répertoire Home                                     |
| cd /         | aller à la racine du disque                                  |
| cd -         | aller au répertoire précédent                                |
| ls           | lister les fichiers et les dossiers                          |
| ls -l        | lister les fichiers et les répertoires avec les détails      |
| ls -a        | lister les fichiers et les répertoires, y compris les fichiers cachés |
| ls -lh       | lister les fichiers et les répertoires avec les détails sur leur taille |
| ls -R        | lister les fichiers et les répertoires récursivement         |

https://github.com/0nn0/terminal-mac-cheatsheet

## Travailler avec les fichiers cachés

### Supprimer tous les fichiers d’un répertoire, y compris les fichiers cachés

```bash
rm -rf ..?* .[!.]* *
```

`*` sélectionne tous les fichiers non cachés, `.[!.]*` sélectionne tous les fichiers cachés sauf `.` et les fichiers don't le nom commence par `..`, et `..?*` sélectionne tous les fichiers à deux points sauf `..`. Ensemble ils sélectionne tous les autres fichiers que `.`and `..`. Si un de ces trois motifs ne sélectionne rien, il s’étend aux autres ; `rm -f` ne tient pas compte d’arguments non spécifiés.

Il est également possible d’utiliser `find`. C’est plus complexe mais a l’avantage de fonctionner même dans le cas où le système de sélection précédent excède les limites du système de ligne de commande.

```bash
find . -name . -o -prune -exec rm -rf -- {} +
```

Toutefois, on peut également tourer plus simple de supprimer et recréer le répertoire. Cela a l’avantage (ou bien l’inconvénient, selon les cas) de produire un répertoire vide même si un autre programme créée des fichiers en concurrence dans le répertoire original.

https://unix.stackexchange.com/a/77313

Il est encore possibile d’utiliser la commande `shopt`

```bash
shopt -s dotglob
mv * xxx/
```

### Déplacer le contenu d’un répertoire vers le répertoire parent, y compris les fichiers cachés

```bash
find . -maxdepth 1 -exec mv {} .. \;  # move all files, with hidden files, to parent directory
```

## Travailler en ssh

### Connexion ssh

```bash
ssh id@ssh.server -p 22
```

### Téléchargement de fichier en ssh

```
scp local_file user@remote_host:remote_file # upload: local -> remote
```

```
scp user@remote_host:remote_file local_file # download: remote -> local
```

