# OAI-PMH

L’Open Archives Initiative – Protocol for Metadata Harvesting (OAI-PMH) permet la collecte et l’échange de métadonnées entre institutions. Ce protocole soutient l’Initiative pour les archives ouvertes  en faciliant le signalement et l’accès à des documents numériques sur internet.

Même si ce protocole est déjà ancien, il s’agit d’une brique fondamentale de l’opérabilité sur le web. Celui-ci permet le moissonnage de métadonnées afin de reconstituer numériquement des corpus à partir de ressources accessibles sur différents sites, ou d’alimenter des portails thématiques. Son utilisation est libre et sa spécification est publiée sur le site de l’Open Access initiative.

## L’Open Archives Initiative

Spécification : http://www.openarchives.org/OAI/openarchivesprotocol.html

![Logo de l’Open Archives Initiative](http://www.openarchives.org/images/OA100.gif)

> L’Open Archives Initiative promeut l’interopérabilité et des standards pour faciliter la dissémination éfficiante des contenus. Elle trouve ses racines dans l’accès ouvert (*Open Access*) et le mouvement de création de dépôts institutionnels. Avec le temps, cependant, le travail de l’OAI s’est étendu à la promotion large des ressources numériques pour la recherche numérique, l’enseignement et la science numérique.

L’organisation est à l’origine de la création de plusieurs standard. OAI-PHM est le premier d’entre eux et fut publié en 2001. Il reste très utilisé dans les bibliothèques et la communauté universitaire. [Open Archives Initiative Object Reuse and Exchange (OAI-ORE)](https://www.openarchives.org/ore/) et le vocabulaire pour l’aggrégation et son modèle de données sont très utilisés. En 2017, elle a publié la [ResourceSync Framework Specification](https://www.openarchives.org/rs/1.1/resourcesync) (NISO Z39.99-2017.

## Le protocole OAI-PMH

OAI-PMH est un protocole très simple qui s’articule autour des standards HTTP et XML : le protocole de transfert hypertextuel permet l’échange de données entre dépôts et moissonneur (*harvester*), tandis que XML est utilisé pour la structuration des données échangées. Il est donc possible d’interroger un dépôt à l’aide d’un simple navigateur[^1].

Le protocole définit deux types d’acteurs, les fournisseurs de données et les fournisseurs de service :

- les **fournisseurs de données** (*data providers*) qui donnent accès à leurs métadonnées à travers ce que l’on nomme un « entrepôt ».
- les **fournisseurs de services** (*service providers*) qui utilisent les métadonnées mises à disposition par le protocole pour créer des services à valeur ajoutée.

Le protocole repose sur une communication client/serveur. Un client envoie une requête à un serveur par l’intermédiaire de HTTP, et le serveur répond avec un flux de données XML.

Chaque enregistrement doit au moins faire l’objet d’une description au format Dublin Core qui constitue le plus petit dénominateur commun. Les notices peuvent toutefois également être décrites avec plusieurs autres formats de métadonnées.

Plusieurs outils existent pour mettre en place de tels services. Des fonctionnalités OAI-PMH sont habituellement implémentées dans les archives institutionnelles.

## Formalisme des requêtes

Les requêtes sont exprimées sous la forme de requêtes HTTP. L’URL de base du dépôt doit être complétée par une série d’arguments renseignés sous la forme de paires clef/valeur. La réponse d’un dépôt est toujours au format XML.

Le protocole définit six instructions appelées verbes qui permettent d’intéroger une service.

| Instruction         | Paramètre                                      | Description                                                  |
| :------------------ | :--------------------------------------------- | :----------------------------------------------------------- |
| Identify            |                                                | Informations à propos du dépôt                               |
| ListMetadataFormats | identifier                                     | Liste des formats disponibles                                |
| ListSets            | resumptionToken                                | Liste des ensembles (*set*) disponibles dans un dépôt.       |
| ListIdentifiers     | from until metadataPrefix* set resumptionToken | Liste des identifiants des documents d'un dépôt. Peut être limité par date et par ensemble (*set*). |
| ListRecords         | from until metadataPrefix* set resumptionToken | Liste des enregistrements d'un dépôt peut être limité par date et par ensemble (*set*). |
| GetRecord           | identifier* metadataPrefix*                    | Demande un enregistrement spécifique                         |

La syntaxe pour utiliser ces instructions et paramètres dans une requête OAI-PMH est de la forme suivante : `[URL de base du dépôt]?verb=[instruction]&[paramètre]=valeur&[paramètre]=valeur` (remplacer les valeurs entre crochets)

## Exemples d’entrepôt

Persée

- Documentation : https://www.persee.fr/entrepot-oai
- Adresse du serveur OAI : http://oai.persee.fr/oai?

Papyrus (Université de Montréal)

- Documentation : https://bib.umontreal.ca/guides/bd/depot-institutionnel-papyrus?tab=5239477
- Adresse du dépôt : https://papyrus.bib.umontreal.ca/oai/request?
- Adresse actuelle du dépôt : https://umontreal.scholaris.ca/server/oai/request

## Exemples de requêtes OAI-PMH

### Exemples de requêtes OAI-PMH

Ces exemples sont tirés de la [page de documentation de Papyrus](https://bib.umontreal.ca/guides/bd/depot-institutionnel-papyrus?tab=5239477)

- Lister les **formats des métadonnées** disponibles :
  https://papyrus.bib.umontreal.ca/oai/request?verb=ListMetadataFormats
- Lister les **ensembles** (qui correspondent aux collections) du dépôt :
  https://papyrus.bib.umontreal.ca/oai/request?verb=ListSets
- Lister **uniquement les identifiants** des documents de l’ensemble « **Faculté de l'aménagement – Thèses et mémoires** »
  (identifiant "col_1866_2593" obtenu dans la réponse à la requête précédente)
  https://papyrus.bib.umontreal.ca/oai/request?verb=ListIdentifiers&metadataPrefix=oai_dc&set=col_1866_2593
- Obtenir les métadonnées, selon le schéma de métadonnées **Dublin Core**, du document portant l’identifiant « oai:papyrus.bib.umontreal.ca:1866/15932 » (chapitre de livre par Gilles Dupuis) :
  https://papyrus.bib.umontreal.ca/oai/request?verb=GetRecord&metadataPrefix=oai_dc&identifier=oai:papyrus.bib.umontreal.ca:1866/15932
- Obtenir les métadonnées, selon le schéma de métadonnées **ETDMS**, du document portant l’identifiant « oai:papyrus.bib.umontreal.ca:1866/23952 » (mémoire de maîtrise) :
  https://papyrus.bib.umontreal.ca/oai/request?verb=GetRecord&metadataPrefix=etdms&identifier=oai:papyrus.bib.umontreal.ca:1866/23952
- Obtenir les métadonnées, selon le schéma de métadonnées **MARC21**, du document portant l’identifiant « oai:papyrus.bib.umontreal.ca:1866/23952 å (mémoire de maîtrise) :
  https://papyrus.bib.umontreal.ca/oai/request?verb=GetRecord&metadataPrefix=marc21&identifier=oai:papyrus.bib.umontreal.ca:1866/23952
- Obtenir les métadonnées, selon le schéma **OpenAire v4**. du document portant l’identifiant « oai:papyrus.bib.umontreal.ca:1866/12289 » (article avec embargo) :
  https://papyrus.bib.umontreal.ca/oai/request?verb=GetRecord&metadataPrefix=oai_openaire&identifier=oai:papyrus.bib.umontreal.ca:1866/12289
- Pour une **récolte périodique** par exemple, lister uniquement les métadonnées des enregistrements déposés/modifiés depuis le 20 juin 2021 :
  [https://papyrus.bib.umontreal.ca/oai/request?verb=ListRecords&metadataPrefix=oai_dc&from=2021-06-20T00:00:00Z](https://papyrus.bib.umontreal.ca/oai/request?verb=ListRecords&metadataPrefix=oai_dc&from=2020-06-20T00:00:00Z)

Ces requêtes peuvent être lancées en ligne de commande dans un shell Unix avec l’outil curl : `curl -s 'https://papyrus.bib.umontreal.ca/oai/request?verb=Identify'`

## Moissonnage

Les moissonneurs doivent s’attendre à recevoir des listes de réponse incomplètes pour les requêtes de `ListIdentifiers`, `ListRecords` et `ListSets`. Une réponse incomplète est indiquée par la présence d’un élément `resumptionToken` dans la réponse. 

```xml
<resumptionToken completeListSize="20"
    cursor="9">2001-01-03:2001-01-03:0</resumptionToken>
```



## Références

- Lagoze, Carl, Herbert Van de Sompel, Michael Nelson, et Simeon Warner. 2002. « Open Archives Initiative - Protocol for Metadata Harvesting - v.2.0 ». Open Archives Initiative. https://www.openarchives.org/OAI/openarchivesprotocol.html.
- ———. 2005. « Protocol for Metadata Harvesting – Guidelines for Harvester Implementers ». Open Archives Initiative. https://www.openarchives.org/OAI/2.0/guidelines-harvester.htm.
- « Guide d’interopérabilité OAI-PMH pour un référencement des documents numériques dans Gallica ». 2018. Bibliothèque nationale de France (Bnf).

## Outils

Outil de validation technique Validité technique : http://re.cs.uct.ac.za/

## Notes

[^1]: Certains services associent d’ailleurs une XSLT aux sorties XML pour présenter un contenu plus facilement lisible par l’homme.