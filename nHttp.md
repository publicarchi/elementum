---
filename: nHTTP.md
author: Emmanuel Chateau
version: 0.2
tags: http, rest
---

# Note HTTP


## Présentation

L’Hypertext Transfer Protocol HTTP est un des protocoles à la base du World Wide Web (WWW), qu’on appelle plus généralement le web.

Un **client web**, habituellement appelé navigateur (browser), communique avec un **serveur web** en utilisant une ou plusieurs connections TCP. Le port du serveur web est habituellement le port TCP 80 mais on peut également utiliser le port 8080 pour les connexions sur proxy par exemple. Le **protocole** qu’utilisent le client et le serveur pour communiquer sur la connexion TCP est appelé HTTP, Hypextext Transfer Protocol. Un serveur donné peut pointer vers d’autres serveurs web (ou autres, FTP, etc.) au moyen de **liens hypertextuels**. Les serveurs web peuvent retourner au client des documents HTML (hypertext markup langage), ou d’autres types de **ressources** comme des images, des fichiers postScript, des fichiers plein-texte, etc.).

## Historique

Bien qu’HTTP ait été employé dès 1990, la première documentation a seulement été publiée en 1993, elle décrit à peu-près la version 1.0 (1996). Une nouvelle documentation est restée à l’état de brouillon en 1995. La spécification en vigueur est la version 1.1 qui date de juin 1999, [RFC2616](http://www.w3.org/Protocols/rfc2616/rfc2616.html) qui a fait l’objet d’extension. C’est cette version qui a introduit le concept de négociation de contenu et plusieurs statuts et méthodes supplémentaires.

HTTP est un protocole simple. Le client établit une connexion TCP avec le serveur, adresse une requête, et lit la réponse du serveur. Le serveur dénote la fin de sa réponse en fermant la connexion. Le fichier retourné par le serveur contient normalement des pointeurs (hypertext links) vers d’autres fichiers qui peuvent résider sur le serveur ou d’autres serveurs. Pour l’utilisateur, il suffit simplement de suivre ces liens de serveur à serveur, éventuellement à travers une interface graphique. Les navigateurs fournissent cette facilité aux utilisateurs.

Pour comprendre les mécanismes en jeu, il suffit de lancer un client pour visualiser les communications avec le serveur.
C’est possible avec HTTP car le client envoie des lignes contenant des commandes ASCII au serveur, terminées par des retour chariot et subit d’un saut de ligne appelé CR/LF. La réponse du serveur commence avec des lignes ASCII. HTTP utilise l’ensemble de caractères 8 bit ISO Latin 1 (ASCII avec des extensions pour les langues d’Europe de l’Ouest).

[donner exemple de connexion
connexion au port 80 sur le serveur
Trying ... (réponse du client...)
Connected to ... (réponse du client...)
GET / (commande)]
Réponse...
Connection closed by foreign host (sortie du client ...)

On s’est contenté d’enter la ligne GET / et le serveur retourne xx lignes qui comprennent xx octets. Ce ramène la page d’accueil du serveur depuis le répertoire racine du serveur web. La dernière ligne de la sortie du client ... indique que le serveur a fermé la connexion TCP après avoir écrit la dernière ligne de la sortie.
Le contenu de cette sortie contient des directives précisant par exemple le format de la ressource envoyée, etc.

HTTP est énormément utilisé parce qu’il est simple et modulaire et qu’il est très facile à contrôler. Il faut cependant avoir conscience de ses limites qui tiennent à son fonctionnement intrinsèque : le modèle requête-réponse sans connexion permanente :
- c’est toujours le client qui est à l’initiative des échanges avec le serveur. Pour qu’un serveur envoie quelque chose au client, il faut d’abord que celui-ci contacte le serveur.
- l’absence de maintient de la connexion implique un fonctionnement déconnecté du point de vue applicatif. D’une requête à l’autre, le serveur ne reconnaît pas le client.
- c’est un protocole sans état (stateless), c’est-à-dire qu’il ne conserve aucune information entre deux transactions.

### Les requêtes

#### Les méthodes

Les requêtes HTTP en invoquant des méthodes. Plusieurs méthodes sont disponibles :

GET 		|	HTTP/0.9	|	obtient une ressource
HEAD		|	HTTP/1.0	|	obtient l’en-tête de la réponse
POST		|	HTTP/1.0	|	envoie du contenu au serveur
PUT			|	HTTP/1.1	|	demande au serveur d’enregistrer la ressource envoyée
DELETE	|	HTTP/1.1	|	permet d’effacer un fichier sur le serveur
TRACE		|	HTTP/1.1	|	permet de contrôler la requête reçue par le serveur
CONNECT	|	HTTP/1.1	|	mot réservé pour les proies permettant de créer des tunnels
OPTIONS	|	HTTP/1.1	|	liste les options possibles pour une ressource donnée

Les méthodes introduites par HTTP/1.1 sont destinée à la gestion de la communication client/serveur et à la gestion des documents du serveur. Elles permettent de concevoir une interface d’administration entièrement "web".

#### Format des requêtes

Depuis HTTP/1.0, les requête disposent d’un format précis. La première ligne de la requête indique la requête. Cette requête se compose ensuite de deux parties distinctes (en excluant la première ligne constituée uniquement de la méthode) : l’en-tête et le corps de la requête (ou "corps de l’entité" au sein d’une requête donnée). L’en-tête contient des informations génériques (comme la date) et précise la requête en fournissant des directives telles que le type de navigateur, des informations sur qui demande la ressource,etc. [Elle est optionnelle avec HTTP/1.0 pour être compatible avec HTTP/0.9.] Le corps de la requête n’est présent que lorsque le client envoie des données au serveur avec les méthodes POST ou PUT.

Nota : avec HTTP/1.0 il faut préciser l’URL absolue de la ressource.

L’en-tête de la requête

directives			|	signification
From:				|	donne l’e-mail de la personne contrôlant le navigateur (pb de confidentialité)
Referer:				|	URL de l’objet qui amène la requête (URL de la page dans laquelle figure le lien)
User-Agent:			|	l’identifiant du navigateur pour adapter la réponse
Authorization:		|	permet à un client de s’authentifier auprès du serveur
If-Modified-Since:	|	permit de faire des GET confitionnels

L’en-tête de l’entité

Il est optionnel, et n’est généralement présent que lorsque le client utilise les méthodes POST et PUT. Les principales directives sont les suivantes :

directives			|	signification
Content-Type:		|	le type de l’information envoyée (les types MIME)
Content-Length:	|	le nombre d’octets d’information (en octets)
Content-Encoding:	|	utilize sir l’information est codée ou compressée (gzip, etc.)

Il faut relever qu’il est possible d’envoyer autre chose que des réponses à des formulaires comme par exemple envoyer des fichiers.
HTTP/1.1 a porté à 48 le nombre de directives. Celles-ci permettent d’assurer la gestion du cache, la négociation de contenu, etc. La liste des directives de HTTP1.1 est disponible [ici](http://www.themanualpage.org/http/http_dir11.php). La directive Host: est obligatoire pour permettre une gestion des serveur virtuels et l’utilisation d’URL relatives.

Le corps de l’entité

Le corps de l’entité n’est présent que lorsque le client utilise les méthodes POST et PUT. Il est séparé de l’en-tête de l’entité par un saut de ligne supplémentaire.


### Réponses du serveur

Depuis HTTP/1.0 la réponse du serveur présente le même format qu’une requête en comportant deux parties (hormis la ligne initiale) : l’en-tête de la réponse et le corps de la réponse (également appelé "corps de l’entité" au sein d’une réponse donnée). L’en-tête contient des informations également précisées par des directives sur la réponse et l’entité renvoyée (par exemple le format de la ressource renvoyée, sa taille, etc.). Le corps de l’entité est le résultat même de la requête. La première ligne de la réponse précise le statut de la réponse. Il sert à préciser la manière dont s’est passé le traitement de la requête par le serveur (si elle a abouti ou pas, etc.).

#### Le statut de la réponse

Avec HTTP/1.0 et après le client connaît le type de la réponse grâce à la première ligne qui indique comment la transaction s’est déroulée.

ex. HTTP/1.0 200 OK

Ce statut fournit la version de HTTP utilisée par le serveur, le statut de la réponse sous forme numérique, le statut de la réponse sous forme de texte.
Il existe cinq classes de statuts :
- 1xx : Informations		pas utilisé en HTTP/1.0, employée avec HTTP/1.1
 - 2xx : Succès		requête traitée avec succès
  - 3xx : Redirectionredirection. La requête n’a pas été trouvée mais on sait où elle est
  - 4xx : Erreur clientrequête incorrecte (par exemple erreur de syntaxe)
 - 5xx : Erreur serveurrequête correcte mais non satisfaite (problème interne au serveur, pas encore implémenté, etc.)

### Les caches

Les caches sont un mécanisme qui permet de réduire le nombre de requêtes complètes que doit traiter le serveur. Il s’agit d’une sorte de mémoire "tampon", une machin qui stocke en mémoire certaines ressources façon à lorsque l’on demande une ressource déjà mise en cache on puisse la fournir sans que le serveur n’ait à traiter la requête complète.

Les directives Date:, Expires:, et Last-Modified: introduites par HTTP/1.0 permettent de savoir quand le document demandé a été modifié depuis la dernière fois, ou de calculer le temps qu’une ressource doit rester dans le cache, voire tout simplement de dire à partir de quand on doit demander au serveur le nouveau document.

Entités non cachables
Pragma: no-cache indique que le résultat ne doit pas être gardé dans le cache.

La méthode HEAD et Get conditionnel permettent d’obtenir la date de la dernière modification et de récupérer une ressource si celle-ci a été modifiée.


### Négociation de contenu

HTTP/1.1 essaye d’apporter une gestion intelligente des ressources avec les caches et la négociation de contenu (content negociation). Les négociation de contenu permet de récupérer la ressource qui correspondra le mieux aux attentes de l’utilisateurs. Trois mécanismes sont possibles : Server-driven Negociation, Agent-driven Negociation, Transparent Negotiation.

#### Server-driven Negociation

C’est le serveur qui essaye de déterminer par l’intermédiaire d’un algorithme la ressource qui correspond le mieux à l’utilisateur. Le client peut adresser une directive au serveur en ce sens (ex : "Accept-Language:")

pb cache

#### Agent-driven Negociation

C’est le client HTTP qui demande la meilleure ressource, la sélection se fait sur la base d’une liste renvoyée par le serveur de toutes les représentations possiibles.

en deux temps
efficace seulement avec une gestion des caches
Les statuts 300 (Multiple Choices) et 406 (Not Acceptable) jouent un rôle important dans cette négociation.

#### Transparent Negotiation

Elle combine les deux types précédents.


### Sécurité

HTTP/1.0 a introduit un mécanisme d’authentification de l’utilisateur qui permet notamment de protéger une partie de site wbe par mot de passe. Lors de la connexion le serveur renvoie un statut "HTTP/1.0 401 Authorization Required" avec une directive WWW-Authenticate qui dit au client comment procéder pour l’authentification. Dans cette méthode basique, le mot-de-passe circule codé mas pas crypté.
Le mécanisme d’authentification n’a pas beaucoup changé avec HTTP/1.1 hormis l’introduction d’un mécanisme d’authentification par challenge plus sûr. Il s’agit de la méthode "digest" qui s’ajoute à la méthode précédente "Basic".

voir http://www.themanualpage.org/http/http_auth_basic.php


Définitions (extraits de la spécification 1.0)
---------

Connexion
Un circuit virtuel s’appuyant sur une couche de transport pour la communication d’information entre deux applications.

Message
L’unité de base d’une communication HTTP, consistant en une séquence structurée d’octets définie à la Section 4 et transmis via la connexion.

Requête
Un message de requête HTTP (défini en Section 5).

Réponse
Un message de réponse HTTP (défini en Section 6).

Ressource
Un service ou objet du réseau pouvant être identifié par une URI (Section 3.2).

Entité
Une représentation particulière de données, ou la réponse d’une ressource de type service, incluse dans une requête ou une réponse. Une entité représente une métainformation sous la forme d’une en-tête et d’un contenu sous la forme d’un corps, ou "body".

Client
Un programme applicatif dont la fonction principale est d’émettre des requêtes.
Utilisateur
Le client qui a émis la requête. Celui-ci peut être un navigateur, un éditeur, un "spiders" (robot d’exploration), ou autre utilitaire.
Utilisateur final
L’utilisateur humain pilotant le programme utilisateur.

Serveur
Un programme applicatif acceptant des connexions dans le but traiter des requêtes en délivrant une réponse.
Serveur origine
Le serveur dans laquelle se situe physiquement une ressource.

Proxy
Un programme intermédiaire qui cumule les fonctions de serveur et de client. Les requêtes sont soit traitées en interne ou répercutées, éventuellement converties, sur d’autres serveurs. Un proxy doit interpréter, puis reconstituer un message avant de le réemettre. Les proxies sont souvent utilisés comme portes d’accès côté utilisateur à des réseaux protégés par un "firewall" ou comme intermédiaire pour convertir des protocoles non supportés par l’utilisateur.

Gateway ou routeur
Un serveur jouant le rôle d’intermédiaire pour d’autres serveurs. Contrairement à un Proxy, un routeur reçoit les requêtes comme s’il était le serveur origine pour la ressource; le client n’étant pas nécessairement conscient de "communiquer" avec un routeur. Les routeurs sont souvent utilisés comme porte d’accès côté serveur d’un réseau protégé par "firewall" et comme convertisseur de protocole pour accéder à es ressources hébergées sur des systèmes non-HTTP.

Tunnel
Un tunnel est un programme applicatif servant de relais "transparent" entre deux connexions. Une fois actif, cet élément n’est plus considéré comme faisant partie de la connexion HTTP, bien qu’il soi issu d’une requête HTTP. Le tunnel cesse d’exister lorsque les deux sens de la connexion ont été fermés. Les tunnels sont utilisés lorsqu’une "porte" est nécessaire et que l’intermédiaire ne peut, ou ne doit pouvoir interpréter la communication.

Cache
Un espace de stockage local destiné à enregistrer les réponses et le sous-système contrôlant ces enregistrements, leur relecture et leur effacement. Un cache enregistre des réponses dans le but de diminuer le temps d’accès et la charge du réseau lors de requêtes identiques ultérieures. Tout client ou serveur peut implémenter un cache, bien que le serveur ne puisse exploiter ce cache, faisant office de tunnel.
Un programme pouvant aussi bien être serveur que client; l’utilisation que nous ferons de ces termes s’appliquera à la situation qu’à le programme vis à vis d’une connexion particulière, plutôt qu’à ses possibilités effectives. De même tout serveur peut être à la fois serveur origine, proxy, routeur, ou tunnel, changeant alors de comportement en fonction des requêtes reçues.

This specification uses a number of terms to refer to the roles played by participants in, and objects of, the HTTP communication.

connection
connexion
Un circuit virtuel de couche transport établi entre deux programmes pour les besoins de la communication.

message
message
Unité de base de la communication HTTP, consistant en une séquence structurée d’octets satisfaisant à la syntaxe définie à la section 4 et transmise via la connexion.

request
requête
Un message de demande HTTP, comme défini à la section 5.

response
réponse
Un message de réponse HTTP, comme défini à la section 6.

resource
ressource
Un objet ou service de données de réseau qui peut être identifié par un URI, comme défini au paragraphe 3.2. Les ressources peuvent être disponibles dans plusieurs représentations (par exemple, plusieurs langages, formats de données, taille, et résolutions) ou varier dans d’autres façons.

entity
entité
Ce sont les informations transférées comme charge utile d’une demande ou réponse. Une entité consiste en méta informations sous la forme de champs d’en-tête d’entité et en contenu sous la forme d’un corps d’entité, comme décrit à la section 7.

representation
représentation
C’est une entité incluse avec une réponse qui est sujette à négociation de contenu, comme décrit à la section 12. Il peut exister plusieurs représentations associées à un état de réponse particulier.

content negotiation
négociation de contenu
Mécanisme pour choisir la représentation appropriée lors de la satisfaction d’une demande, comme décrit à la section 12. La représentation des entités dans toute réponse peut être négociée (y compris les réponses d’erreur).

variant
variante
Une ressource peut avoir une, ou plus d’une, représentations associées à tout instant donné. Chacune de ces représentations est appelée une ’variante’. L’utilisation du terme ’variante’ n’implique pas nécessairement que la ressource soit soumise à une négociation de contenu.

client
client
Un programme qui établit des connexions pour les besoins de l’envoi des demandes.

user agent
agent utilisateur
Le client qui initie une demande. Ce sont souvent des navigateurs, des éditeurs, des robots araignées (robots de traversée de la Toile), ou autres outils d’utilisateur terminal.

server
serveur
Un programme d’application qui accepte les connexions afin de servir des demandes en renvoyant des réponses. Tout programme donné peut être capable d’être à la fois un client et un serveur ; notre utilisation de ces termes se réfère seulement au rôle effectué par le programme pour une connexion particulière, plutôt qu’aux capacités du programme en général. De même, tout serveur peut agir comme un serveur d’origine, un mandataire, une passerelle, ou un tunnel, changeant de comportement sur la base de la nature de chaque demande.

origin server
serveur d’origine
Le serveur sur lequel une ressource donnée réside ou est à créer.

proxy
mandataire (proxy)
Un programme intermédiaire qui agit à la fois comme un serveur et un client dans le but de faire des demandes au nom d’autres clients. Les demandes sont servies en interne ou en les transmettant, avec une éventuelle traduction, à d’autres serveurs. Un mandataire DOIT mettre en œuvre à la fois les exigences de client et de serveur de la présente spécification. Un "mandataire transparent" est un mandataire qui ne modifie pas la demande ou réponse au delà de ce qui est requis pour l’authentification et l’identification par le mandataire. Un "mandataire non transparent" est un mandataire qui modifie la demande ou réponse afin de fournir des services supplémentaires à l’agent d’utilisateur, tels que des services d’annotation de groupe, de transformation de type de support, de réduction de protocole, ou de filtrage de l’anonymat. Excepté lorsque le comportement transparent ou non transparent est explicitement déclaré, les exigences de mandataire HTTP s’appliquent aux deux types de mandataires.

gateway
passerelle
Serveur qui agit comme intermédiaire pour un autre serveur. À la différence d’un mandataire, une passerelle reçoit des demandes comme si elle était le serveur d’origine pour la ressource demandée ; le client demandeur peut n’être pas avisé qu’il communique avec une passerelle.

tunnel
tunnel
Un programme intermédiaire qui agit comme un relais aveugle entre deux connexions. Une fois actif, un tunnel n’est pas considéré comme partie à la communication HTTP, bien que le tunnel puisse avoir été initialisé par une demande HTTP. Le tunnel cesse d’exister lorsque les deux extrémités de la connexion relayée sont closes.

cache
antémémoire
Mémoire locale d’un programme de messages de réponse et le sous-système qui contrôle sa mémorisation, restitution et suppression de messages. Une antémémoire stocke les réponses éligibles afin de réduire le temps de réponse et la consommation de bande passante du réseau sur les demandes futures, équivalentes. Tout client ou serveur peut inclure une antémémoire, bien qu’elle ne puisse pas être utilisée par un serveur qui agit comme un tunnel.

cacheable
mémorisable
Une réponse est mémorisable si une antémémoire est autorisée à stocker une copie du message de réponse pour l’utiliser à répondre à des demandes ultérieures. Les règles de détermination de la possibilité de mémoriser les réponses HTTP sont définies à la section 13. Même si une ressource est mémorisable, il peut y avoir des contraintes supplémentaires sur la question de savoir si une antémémoire peut utiliser la copie mémorisée pour une demande particulière.

first-hand
première main
Une réponse est de première main si elle vient directement et sans délai inutile du serveur d’origine, éventuellement via un ou plusieurs mandataires. Une réponse est aussi de première main si sa validité vient d’être vérifiée directement avec le serveur d’origine.

explicit expiration time
heure d’expiration explicite
C’est l’heure à laquelle le serveur d’origine a prévu qu’une entité ne devrait plus être retournée par une antémémoire sans autre validation.

heuristic expiration time
heure d’expiration euristique
Heure d’expiration allouée par une antémémoire lorsque aucune heure d’expiration explicite n’est disponible.

age
âge
L’âge d’une réponse est le temps écoulé depuis qu’elle a été envoyée, ou validée avec succès avec le serveur d’origine.

freshness lifetime
fraîcheur de durée de vie
Temps entre la génération d’une réponse et son heure d’expiration.

fresh
fraîcheur
Une réponse est fraîche si son âge n’a pas encore excédé sa fraîcheur de durée de vie.

stale
périmée
Une réponse est périmée si son âge a dépassé sa fraîcheur de durée de vie.

semantically transparent
sémantiquement transparent
Une antémémoire se comporte d’une façon "sémantiquement transparente", par rapport à une réponse particulière, lorsque son utilisation n’affecte ni le client demandeur ni le serveur d’origine, excepté pour améliorer la performance. Lorsque une antémémoire est sémantiquement transparente, le client reçoit exactement la même réponse (excepté pour les en-têtes de bond par bond) qu’il aurait reçue si sa demande avait été traitée directement par le serveur d’origine.

validator
valideur
Élément de protocole (par exemple, une étiquette d’entité ou une heure de dernière modification) qui est utilisé pour trouver si une entrée d’antémémoire est une copie équivalente d’une entité.

upstream/downstream
vers l’amont/vers l’aval
Vers l’amont et vers l’aval décrivent les flux de messages : tous les messages vont de l’amont vers l’aval.

inbound/outbound
entrant/sortant
Entrant et sortant se réfère aux chemins de la demande et de la réponse pour les messages : "entrant" signifie "voyager vers le serveur d’origine", et "sortant" signifie "voyager vers l’agent d’utilisateur"

Aller plus loin
-----------
[Configuration du serveur Apache HTTP](http://httpd.apache.org/docs/trunk/fr/compliance.html)

[HTTP, sur MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP)

[HTTP access control (CORS) sur sur MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS)

[Using Fetch sur sur MDN](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)

Sources
--------
- [Pages de TheManualPage sur HTTP](http://www.themanualpage.org/http/)
- voir Websocket
- http://zero202.free.fr/cs67-http/html/
