# Wordpress en local sur MacOS

## Installer Wordpress

Ouvrir une fenêtre de terminal et télécharger la dernière version des sources du CMS Wordpress

```bash
curl -O https://wordpress.org/latest.tar.gz
```

Extraire les fichiers de l’archive tar

```bash
tar -xvzf latest.tar.gz
```

Déplacer les fichiers vers le répertoire du projet à l’intérieur de votre ~/Sites

```bash
mkdir ~/Sites/projet
mv wordpress ~/Sites/projet
```

Nettoyez le répertoire où vous aviez téléchargé l’archive

```bash
rm latest.tar.gz
```

Régler les permissions des fichiers sur Mac OSX, le serveur HTTP fonctionne avec l’utilisateur _www qui appartient au groupe _www. Pour permettre à Wordpress de configurer wp-config.php pendant l’installation et la mise à jour et l’actualisation du fichier .htaccess pour les permaliens, donner les droits suivants :

```bash
sudo chown -R _www ~/Sites/projet
sudo chmod -R g+w ~/Sites/projet # peu sécuritaire
```

cf. Guide chmod <https://www.washington.edu/computing/unix/permissions.html>

Script pour la configuration des fichiers Wordpress <https://gist.github.com/macbleser/9136424>

Faire les modifications récursivement 

```
find ~/Sites/projet -type d -exec chmod 750 {} \;
find ~/Sites/projet -type f -exec chmod 640 {} \;
```

## Création de la base de données

Il faut ensuite créer une base de données vide pour Wordpress. Cette opération peut être réalisée avec phpMyAdmin ou Sequel Pro mais aussi en mysql par l’intermédiaire de la ligne de commande.

Exécuter mysql (substituer le texte avec les crochets par le nom de la base de données et le mot de passe root de mysql)

```mysql
mysql -u [username] -p [password]
```

Créer une base de données en choisissant son nom (remplacer le texte avec les crochets par le nom de la base de données)

```bash
create database [database name];
exit;
```

Créer un utilisateur pour la base de données et lui donner tous les droits

```mysql
GRANT ALL PRIVILEGES ON database_name.* TO 'username'@'localhost';
FLUSH PRIVILEGES;
```

## Configurer Wordpress

Vous pouvez aller sur la page http://localhost/projet et configurez Wordpress.