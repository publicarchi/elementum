---
author: Emmanuel Château-Dutier
since: 2017-01-28
tags: mac, localhost
---

# Configuration d’un serveur local sur Mac

Comme le système d’exploitation Mac OS repose sur un noyau Linux, on peut facilement configurer un serveur local sur sa machine sans avoir recours à des logiciels comme MAMP pour disposer d’un environnement de développement. La création d’un serveur local est très aisée et ne nécessite que quelques instructions en ligne de commande.

Rmq : Ce Guide est valable pour Sierra

## Créer un répertoire qui sera servi en local

Créer un répertoire personnel qui sera servi en local (ce répertoire n’est plus créé par défaut).

```bash
mkdir ~/Sites
echo "<html><body><h1>Mon site fonctionne !</h1></body></html>" > ~/Sites/index.html
```

Cette page devra être visible à l’adresse [http://localhost/~username](http://localhost/~username)

## Configurer Apache

Notre serveur sera propulsé par [Apache HTTP Serveur](https://httpd.apache.org). Nous allons le configurer avec un fichier d’utilisateur.

Pour commencer, il vous faut connaître votre nom d’utilisateur

```bash
whoami # afficher son nom d’utilisateur
```

On créer ensuite un fichier de configuration

```bash
cd /etc/apache2/users # aller dans le répertoire de configuration d’Apache
vim username.conf # remplacez `username` par votre nom utilisateur
```

On entre dans ce fichier la configuration du répertoire, et un renseigne la configuration du répertoire en remplaçant `username` par son nom d’utilisateur mac.

```xml
<Directory "/Users/username/Sites/">
   AllowOverride All
   Options Indexes MultiViews FollowSymLinks
   Require all granted
</Directory>
```

Le répertoire doit être accessible en lecture pour Apache 

```bash
sudo chmod 644 username.conf # remplacer username par son nom d’utilisateur
```

Le 6 donne les droits d’écriture et de lecture au propriétaire du fichier. Les deux 4 restreignent l’accès en lecture seule au Group et Other.

Aller dans `etc/apache2`, et activer les modules http

D’abord faire une copie du fichier de configuration

````bash
cd ..
pwd # vous devez vous trouver dans `/etc/apache2`
cp httpd.conf httpd.conf.bak # faire une copie de sauvegarde du fihier de configuration par défaut
````

Dans le fichier `http.conf` un certain nombre modules doivent être activés : les lignes doivent être décommantées en enlevant le `#`.

Ouvrir le fichier avec sudo.

```LoadModule authz_host_module libexec/apache2/mod_authz_host.so
LoadModule authz_host_module libexec/apache2/mod_authz_host.so
LoadModule authz_core_module libexec/apache2/mod_authz_core.so
LoadModule userdir_module libexec/apache2/mod_userdir.so
LoadModule vhost_alias_module libexec/apache2/mod_vhost_alias.so

Include /private/etc/apache2/extra/httpd-userdir.conf
Include /private/etc/apache2/extra/httpd-vhosts.conf
```

## Mettre à jour le httpd-userdir.conf

éditer le `http-userdir.conf` situé dans le répertoire `extra`

```bash
cd /etc/apache2/extra
sudo cp httpd-userdir.conf httpd-userdir.conf.bak # faire une copie de sauvegarde
```

Puis éditer `httpd-userdir.conf`, en décommandant la ligne suivante :

```
Include /private/etc/apache2/users/*.conf
```

## Redémarrer Apache

```bash
sudo apachectl restart
```

Rendez-vous avec votre navigateur sur [http://localhost/~username](http://localhost/~username) (en remplaçant username par votre nom d’utilisateur). Bravo, vous avez configuré votre serveur local !

## Actions optionnelles

### Créer des Virtual hosts

En créant des hôtes virtuels vous pouvez exactement dire à Apache où regarder pour servir un contenu spécifique en fonction des directives de nom de serveur liées dans le block VirtualHost. Par exemple pour que l’adresse `toto.dev` serve le répertoire `~/Sites/toto`.

Faîtes une copie de sauvegarde de `etc/apache2/extra/httpd-vhosts.conf`

Puis remplacez le contenu du fichier par

```
#Virtual Host Entry for foo.dev
<VirtualHost *:80>
    DocumentRoot "/Users/john/Sites/foo"
    ServerName foo.dev
    ErrorLog "/private/var/log/apache2/foo-error_log"
    CustomLog "/private/var/log/apache2/foo-access_log" common
</VirtualHost>

#Virtual Host Entry for bar.dev
<VirtualHost *:80>
    DocumentRoot "/Users/john/Sites/bar"
    ServerName bar.dev
    ErrorLog "/private/var/log/apache2/bar-error_log"
    CustomLog "/private/var/log/apache2/bar-access_log" common
</VirtualHost>
```

Après avoir sauvé, mettez à jour la liste des hôtes dans `/etc/hosts`

```
##
# Host Database
#
# localhost is used to configure the loopback interface
# when the system is booting.  Do not change this entry.
##
127.0.0.1       localhost
255.255.255.255 broadcasthost
::1             localhost

#Local dev sites
127.0.0.1       foo.dev
127.0.0.1       bar.dev
```

Redémarrer Apache

```bash
sudo apachectl restart
```

## Activer PHP

PHP n’est plus activé par défaut sur les versions récentes de Mac OS X. Vous devez l’activer.

```bash
sudo vim /etc/apache2/httpd.conf
```

Décommenter la ligne suivante :

`#LoadModule php5_module libexec/apache2/libphp5.so` en retirant le `#` (avec vim, taper la touche x à l’endroit du caractère pour l’effacer, quittez vim avec `:wq`.

Permettre l’interprétation de PHP en ajoutant en haut de votre fichier `http-vhosts.conf`

```
#Enable PHP interpretation within HTML files
<FilesMatch ".+\.html$">
   SetHandler application/x-httpd-php
</FilesMatch>

```

Redémarrez apache

Pour vérifier que tout fonctionne, créez un fichier php de test dans votre répertoire de travail

```php
<?php
  $greeting = 'Hello, PHP World!';
  echo '<h1>' . $greeting . '</h1>';
?>
```



## Sources

https://web.archive.org/web/20161018141829/http://digitalshore.io/local-web-development-environment-apache-macos-sierra-10-12/



