---
author: emchateau
since: 2017-07-25
tags: ruby
---

# Travailler avec des gems Ruby

Depuis les dernières versions de Mac OS, l’installation de Gem par l’utilisateur pose un problème de droits.

Par défaut, on utilise la version de Ruby du system. Celle-ci installe les gems dans un répertoire dédié dans `/Library/Ruby/Gems/2.0.0` qui n’est pas accessible en écriture.

On obtient le message suivant :

> ERROR:  While executing gem ... (Errno::EPERM) Operation not permitted

On peut visualiser sa configuration de Ruby avec la commande suivante

````bash
gem env
````

Le répertoire des gems de l’utilisateur est indiqué à la ligne… Son chemin prend la forme suivante : `~/.gem/ruby/2.0.0/bin`.

Lors de l’installation d’une gem, il est possible de spécifier l’installation dans ce répertoire dédié de l’utilisateur en utilisant l’option `--user-install`.

Par exemple :

````bash
gem install maGem --user-install
````

Au moyen de cette option, on ne rencontre plus de problème de droits. Néanmoins, les commandes des gems installées ne sont pas encore disponibles dans le Path. Pour rendre les programmes installés disponibles, il est nécessaire d’ajouter le répertoire des gems exécutables dans la variable d’environnement de l’utilisateur.

Il suffit alors d’ajouter la ligne suivante dans `~/.bash_profile` :

```bash
if which ruby >/dev/null && which gem >/dev/null; then
    PATH="$(ruby -rubygems -e 'puts Gem.user_dir')/bin:$PATH"
fi
```

Et tout devrait fonctionner à merveille !