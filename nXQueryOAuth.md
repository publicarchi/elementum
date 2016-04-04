# nXQueryOAuth

Différents protocole d’indentification sur le web, plus ou moins sécurisés, peuvent être implémentés en XQuery.


## Les protocoles d’identification

### Authentication simple

### Authentification Digest

### OpenAuthentification


## Mise en œuvre en XQuery pour OAuth

L’identification avec les services basés sur OAuth se fait en deux étapes.

Dans un premier temps, il faut obtenir les autorisations nécessaires pour le service ("consumer key" et "consumer secret") et un "access token" qui ne doit pas être confondu avec un "request token". Dans un second temps, il est alors possible de signer les requêtes avec ses autorisations.

__Obtention des autorisations__
Chaque service fournit le "consumer key" et "consumer secret" directement, mais l’obtention de l’"access token" est plus ou moins compliqué. Certains services comme Twitter permettent de générer un access token sur leur site qu’il est ensuite possible de copier  coller dans son code. Si les services ne permettent pas de générer un access token directement, il peut être nécessaire de d’abord demander un "access token", puis de se connecter avec le code du "consumer secret".

__Signature des requêtes__
Dès lors que vous disposez des autorisations, vous pouvez commencer à formuler des requêtes. Cela inmplique de construire ces requêtes et de les signer. Pour cela, vous devez consulter la documentation de l’API du service. La signature d’une requête avec OAuth est un peu complexe, elle implique des paramières spécifiques d’ordre et d’encodage et de hasher le résultat avec un algorithme cryptographique, avant de soumettre la requête.

## Code

[XQuery-OAuth](https://github.com/ndw/XQuery-OAuth)
Utilise des annotations propriétaires de MarkLogic

[XQuery-OAuth pour Basex 7.4+](https://github.com/apb2006/XQuery-OAuth)


## Sources
Norman Walsh, OAuth from XQuery, http://norman.walsh.name/2010/09/25/oauth
- Joe Living in an OAuth & JSON World, joewiz.org, http://joewiz.org/2013/07/04/living-in-an-oauth-json-world/
module https://gist.github.com/joewiz/5929809
- XQuery/Basic Authentication, Wikibook XQuery, https://en.wikibooks.org/wiki/XQuery/Basic_Authentication
- XQuery/Digest Authentication, Wikibook XQuery, https://en.wikibooks.org/wiki/XQuery/Digest_Authentication
- XQuery/OAuth, Wikibook XQuery, https://en.wikibooks.org/wiki/XQuery/OAuth
