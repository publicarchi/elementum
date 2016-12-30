# nXQueryOpenId

## Les protocoles d’identification

### Authentification simple

### Authentification Digest

### OpenID

[OpenID](http://openid.net/) est un mécanisme d’authentification décentralisé où l’identité de l’utilisateur est maintenue par un fournisseur d’identité de confiance (Identity Provider IdP). Celui-ci est en charge de maintenir et de sécuriser les mot-de-passes des utilisateurs sans que le fournisseur de service n’y ait accès.

Pour accéder à un service compatible OpenID, l’utilisateur fournit simplement le nom de son IDP auquel le service (RP, Relying Party) déléguera la tâche d’authentifier l’utilisateur.

Ce système présente plusieurs avantages.
- 1°. Il évite d’avoir à créer plusieurs profils sur plusieurs sites différents. L’utilisateur peut se contenter d’avoir recours à un profil unique sur un IDP pour accéder à tout site supportant OpenID ("Single Sign On").
- 2°. Cela permet de ne confier ses informations personnelles qu’à un seul site auquel on fait confiance. Le fournisseur de service n’a à connaître que l’OpenID de l’utilisateur et jamais son mot de passe.
- 3°. Le système place l’utilisateur au cœur de la transaction et améliore de ce fait la protection de la vie privée.




http://www.openidenabled.com/openid/openid-protocol


## Implémentations en XQuery

La base de données XML native eXist implémente le service OpenID lib/extensions/exist-security-openid.jar mais celui-ci doit être activé.

## Sources

- Cerdic Elafargue, OpenID, SPIP-Contrib, http://contrib.spip.net/OpenID-pour-SPIP
- OpenID enabled, http://janrain.com/openid-enabled/
- http://dotnetopenauth.net
