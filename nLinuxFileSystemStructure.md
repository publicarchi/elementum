---
title: Structure de fichiers Linux
since: 2014-05-28
tags: linux
---

# Structure de Fichiers Linux

/
|-  /bin        User Binaries
|-  /sbin       System Binaries
|-  /etc        Configuration Files
|-  /dev        Device Files
|-  /proc       Process Information
|-  /var        Variable Files
|-  /tmp        Temporary Files
|-  /usr        User Programs
|-  /home       Home Directories
|-  /boot       Boot Loader Files
|-  /lib        System Libraries
|-  /opt        Optional add-on Apps
|-  /mnt        Mount Directory
|-  /media      Removable Devices
|-  /srv        Service Data


## / – Root

Racine des répertoires
Seul l’utilisateur root a les privilèges d’écriture dans ce répertoire.
Ce répertoire et le home de l’utilisateur root.


## /bin – User Binaries

Contient tous les binaires exécutables.
Les commandes linux communes aux utilisateurs sont placées dans ce répertoire.
Par exemple : `ls`, `ping`, `grep`, `cp`, etc.


## /sbin – System Binaries

Contient également les binaires exécutables.
Les commandes linux placées dans ce répertoires sont typiquement utilisées par les administrateurs système pour la maintenance.

Par exemple : `iptables`, `reboot`, `fdisk`, `ifconfig`, etc.


## /etc – Configuration Files

Contient les fichiers de configurations communs à tous les programmes.
Contient également les scripts de démarrage et d’arrêt des programmes individuels.


## /dev – Device Files

Contient les fichiers de périphériques, y compris les terminaux, usb, ou tout périphériques attachés au système.


## /proc – Process Information

Contient les information sur les processus système.
C’est un pseudo système de fichier.
Par exemple : `/proc/{pid}` ou `/proc/uptime``


## /var – Variable Files

Contient les fichiers dont le contenu est susceptible d’augmenter.
Cela inclut les fichiers de log system (`/var/log`), les paquets et fichiers de base de données (`/var/lib`), les emails (`/var/mail`), la file d’attente d’impression (`/var/spool`), les fichiers de locks (`/var/lock`), les fichiers temporaires pour les rebootages (`/var/tmp`).


## /tmp – Temporary Files

Ce répertoire contient les fichiers temporaires créés par le système et les utilisateurs.
Ces fichiers sont effacés lors du reboot.


## /usr – User Programs

Contient les fichiers binaires, les bibliothèques, la documentation et le code source des programmes de second niveau.
`/usr/bin` contient les binaires des programmes utilisateur. Lorsqu’un programme n’est pas dans `/bin`, le chercher dans `/usr/bin`.
`/usr/sbin` contient les fichiers binaires pour les administrateurs système.
`/usr/lib` contient bibliothèques pour `/usr/bin` et `/usr/sbin`.
`/usr/local` contient les programmes utilisateurs installés depuis les sources. Par exemple Apache.


## /home – Home Directories

Les répertoires dans home servent à stocker les fichiers personnels de chaque utilisateur.
Par exemple : `/home/emmanuel`, `/home/thomas`


## /boot – Boot Loader Files

Contient les fichiers de chargement et de boot.


## /lib – System Libraries

Contient les fichiers de bibliothèques qui supportent les binaires localisés sous `/bin` et `/sbin`


## /opt – Optional add-on Apps

Contient les applications add-on des vendeurs.

## /mnt – Mount Directory

Répertoire de montage temporaire où les sysadmins peuvent monter des systèmes de fichiers.


## /media – Removable Devices

Fichiers temporaires de montage pour les périphériques amovibles.


## /srv – Service Data

Contient les données relatives au services spécifiques.

[revoir détail]

## Sources
http://www.thegeekstuff.com/2010/09/linux-file-system-structure/
