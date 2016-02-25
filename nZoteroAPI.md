# Zotero API

Outre la publication de groupes bibliographiques, le logiciel de gestion de références bibliographiques Zotero propose une Interface programmable (API) qui peut vous permettre d’accéder programmatiquement à vos données.

Ce type d’interface est devenu crucial dans le développement logiciel moderne sur le Web. Il permet par exemple de republier ses données dans d’autres contextes comme sur un blog.

L’API Zotero est de type REST, c’est-à-dire qu’elle repose sur l’architecture du web. Les instructions peuvent donc être passées par l’URL au moyen d’une syntaxe spécifique.

Pour travailler sur l’API, vous avez besoin d’avoir un groupe bibliographique et un utilisateur disposant des droits nécessaires. Vous pouvez récupérer l’identifiant de l’utilisateur en accédant aux pages suivantes (utilisateur connecté) :
- https://www.zotero.org/settings/keys

Le numéro de groupe peut quant à lui être récupéré dans l’URL de la page du groupe.


## Url de base de l’API

https://api.zotero.org

https://www.zotero.org/emchateau

https://www.zotero.org/groups/416169/

https://api.zotero.org/groups/tags


Pour les bibliographies en accès réservé ou pour écrire les données, nécessité d’une clé apiKey :
api.zotero.org/users/87937/item/102472156?username=apitest&apiKey={apiKey}


## Sources


- [Tutoriel API Zotero](http://www.ahp-numerique.fr/index.php?title=Tutoriel_API_Zotero)
- [Programmation en PHP de l’API Zotero](http://alpha.ahp-numerique.fr/phpZotero/)
- [Zotero Web API v3 (documentation)](https://www.zotero.org/support/dev/web_api/v3/start)
