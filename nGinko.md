# Utiliser Ginco en LOD

Ginco est une des briques fonctionnelles du système d’information du Ministère de la culture et de la communication destinée à la gestion des référentiels. Ginco met en œuvre les principes définis dans la norme ISO 25964 : Information et documentation -- Thésaurus et interopérabilité avec d’autres vocabulaires publiée en 2011 et 2012. L’outil est mis en production pour plusieurs référentiels du ministère de la culture sur http://data.culture.fr/thesaurus/ Il permet notamment la publication des thésaurus sous forme de données liées dans les formats du web sémantique.

La documentation de Ginco présente surtout l’interface de gestion du logiciel. Or celui-ci offre également là mise à disposition des référentiels par l’intermédiaire d’API. Celles-ci sont de plusieurs types, SOAP ou REST.

## REST

L’API REST De Ginco est accessible en utilisant le scheme d’URI.

Le chemin `/resource/ark:/etc.` pointe vers la ressource. Avec un navigateur, l’URI redirige vers la présentation web de la ressource.

```
http://data.culture.fr/thesaurus/resource/ark:/67717/2db8b61c-4279-425a-a1b0-7c34a7edd517
```

La page web d’une ressource est accessible au chemin composé de la manière suivante `/page/ark:/etc.`

```
http://data.culture.fr/thesaurus/page/ark:/67717/2db8b61c-4279-425a-a1b0-7c34a7edd517
```

Les représentations au format de la même ressource sont disponibles au chemin  `/data/ark:/etc.`

```
http://data.culture.fr/thesaurus/data/ark:/67717/2db8b61c-4279-425a-a1b0-7c34a7edd517
```

Regarder si service SOAP au chemin /soap/

## Web services SOAP

service: ThesaurusService

adresse: /thesaurus

thesaurusTermSOAPService



service: ThesaurusTermService

adresse: /thesaurusTerm

thesaurusTermSOAPService



service: ThesaurusConceptService

adresse: /thesaurusConcept

[thesaurusConceptSOAPService](https://github.com/culturecommunication/ginco/blob/master/ginco-webservices/src/main/java/fr/mcc/ginco/soap/ISOAPThesaurusConceptService.java)

Get hierarchical relations between two concepts

@param firstConceptId identifier of first concept

@param secondConceptId identifier of second concept

@return 2 if first concept is child of second concept

Get preferredTerm by the identifier of a concept

@param conceptId identifier of a concept

@return reduced preferred term



service: ThesaurusArrayService

adresse: /thesaurusArray

thesaurusArraySOAPService

@param thesaurusId

@param thesaurusArrayId



## Références

http://www.culturecommunication.gouv.fr/Divers/Harmonisation-des-donnees-culturelles/Referentiels/Les-vocabulaires-scientifiques-et-techniques/L-application-GINCO/En-savoir-plus-sur-GINCO