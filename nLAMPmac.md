nLAMPMac.md

# LAMP on a mac

Depuis la version 10.9, l’option de partage dans l’interface graphique des préférences systèmes de Mac OSX a disparu. Apache n’en reste pas moins installé avec le système d’exploitation et il peut être activé en ligne de commande.

Ouvrir une fenêtre de Terminal (le programme se trouve dans /Applications/Utilities/Terminal)

## Démarrer le serveur Apache

```bash
  sudo apachetl start
```

## Arrêter le serveur Apache

```bash
  sudo apachetl stop
```

## Redémarrer le serveur Apache

```bash
  sudo apachetl restart
```

## Afficher la version d’Apache

```bash
  httpd -v
```

## Vérifier sa configuration

```bash
  sudo apachectl -t
```

## Racine web du système

http://localhost/

Les fichiers partagés dans le système de fichiers dans `/Library/webServer/Documents`

## Racine utilisateur web

http://localhost/Sites

Qui sert le répertoire Sites du compte utilisateur qui peut être créé à la racine de l’utilisateur.

La mise à jour conserve le dossier Sites mais ne permet pas de servir les fichiers. Il faut pour cela créer un fichier `username.conf`

`/etc.apache2/users/``

## Sources

http://www.coolestguidesontheplanet.com/downtown/get-apache-mysql-php-and-phpmyadmin-working-osx-109-mavericks

http://mallinson.ca/post/web-development-with-mavericks/

## Pour restaurer l’ancienne configuration :

```bash
  sudo cp /etc/apache2/httpd.conf.pre-update /etc/apache2/httpd.conf
  sudo apachectl restart
```

http://brianflove.com/2013/10/23/os-x-mavericks-and-apache/
