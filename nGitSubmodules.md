

# Utilisation des sous-modules de Git

L'utilisation des sous-modules de Git permet de versionner séparément des bibliothèques de code, ou des répertoires spécifiques à l'intérieur d'un projet pour gérer des extensions.

Ajouter une extension ou un projet sous la forme d'un sous-module git est une bonne pratique car cela permet de tenir votre code et celui de l'application clairement séparés. De plus vous allez pouvoir versionner votre projet ou votre extension et pouvoir gérer les éventuels conflits avec SynopsX. Pour ajouter un sous-module dans le répertoire d'installation de SynopsX, il suffit de lancer la commande suivante :

```bash
git submodule add git://github.com/user/project.git projects/project-name
```

Après avoir ajouté votre projet ou votre extension comme sous-module, il est probable que vous ayez envie de mettre à jour ses sources. Depuis le répertoire d'installation de SynopsX executez la commande suivante :

```bash
cd projects/project-name
git pull origin master
cd ../..
git commit -m "I updated extension-name" # si vous versionnez l'ensemble
```

Pour mettre à jour vos sources SynopsX vous auriez probablement maintenant tendance à vouloir faire un `git pull`. Mais une telle commande risquerait d'écraser les modifications concernant vos extension ou votre projet.

G

Références
- http://www.getsymphony.com/learn/articles/view/getting-git-for-symphony-development/
- http://www.getsymphony.com/learn/articles/view/on-git-submodules/
