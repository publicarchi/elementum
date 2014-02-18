# Comment contribuer à ce contenu ou ce projet ?

* Faites un Fork du projet
* Ajouter le projet original comme *upstream remote*
	
		git remote add upstream <original project .git URL>
	
* Créer une branche de développement pour la fonctionnalité

		git checkout -b fonctionnality-name

* Éditer le code
* Committer localement
* Synchroniser votre fork avec l'upstream du master:

		git checkout <your-branch-name>
		git fetch upstream
		git rebase upstream/master

* Faites un Push vers votre fork et créez un pull-request sur GitHub
