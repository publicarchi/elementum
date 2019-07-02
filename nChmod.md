---
author: emchateau
since: 2018-07-08
tags: bash, chmod
---

# Chmod

La commande bash `chmod` sert à configurer les droits des fichiers sur des systèmes Linux.

Elle s’exécute habituellement en mode root car cet utilisateur dispose de tous les droits et est à même de configurer des droits aux autres utilisateurs.

Dans un répertoire de fichier, on peut facilement prendre connaissance des droits relatifs aux fichiers et au répertoires avec la commande `ls -la`les options `l` présentent les droits et `a` ajoute les fichiers cachés.

Dans cette liste, la série de lettres placées au début de chaque ligne présente les droits pour chaque type d’utilisateur (propriétaire, groupe, public). 

- `r`  signifie Read (lire)
- `w` signifie Write (écrire)
- `x` signifie eXecute (exécuter)

Ces permission s’expriment aussi sous la forme de nombres à trois chiffres d’après le calcul suivant

- 4 pour le droit de lecture (Read)
- 2 pour le droit d’écriture (Write)
- 1 pour le droit d’exécution (eXecute)

Ainsi, pour des droits en lecture et écriture on additionne 4 et 2 = 6. Ainsi de suite pour chaque groupe d’utilisateur.

## Gestion des droits

Sous Linux, un fichier hérite des droits du groupe de l’utilisateur qui le créée. Dans le cas de fichiers et de répertoires sur un serveur web, il est préférable que ce fichier hérite du groupe du répertoire parent (habituellement `/var/www/`). Il faut pour cela activer le bit [SGID](https://fr.wikipedia.org/wiki/Permissions_UNIX#Droit_SGID) (Set Group ID) du répertoire parent. 



## Sources et références

- https://tech.feub.net/2008/03/setuid-setgid-et-sticky-bit/
- https://tech.feub.net/2014/06/permissions-des-fichiers-et-repertoires-dun-serveur-web/

