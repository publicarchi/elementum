---
since: 2025-04-06
tags: JavaScript, npm
---

# NPM

[NPM](https://www.npmjs.com) est le gestionnaire de paquets de Node.js. Il facilite le partage et le déploiement de modules de code pour les développeurs JavaScript. Le projet a été créé en 2009 comme projet objet source.

## Commandes de base en NPM

Créer un paquet : `npm init`

Exécuter dans un environnement de production : `NODE_ENV=production npm install`

### Installation des paquets

Installer un paquet : `npm install <nom-du-paquet>`

Installer les paquest globalement : `npm install <nom-du-paquet> -g`

Installer un paquet et l’enregistrer comme dépendance : `npm install <nom-du-paquet> --save`

### Mises à jour

Contrôler la mise à jour des paquets : `npm outdated`

Mettre à jour les paquets locaux : `npm update`

Mettre à jour les paquets globaux : `npm update <nom-du-paquet> -g`

### Désinstallation

Désinstaller un paquet local : `npm uninstall <nom-du-paquet>`

Désinstaller un paquet local et le garder dans `package.json` : `npm uninstall <nom-du-paquet> --no-save`

Désinstaller un paquet local et le retirer de `package.json` : `npm uninstall <nom-du-paquet> --save`

Désinstaller un paquet de développement local et le retirer de `package.json` : `npm uninstall <nom-du-paquet> --save-dev`

Désinstaller un paquet global : `npm uninstall <nom-du-paquet> -g`