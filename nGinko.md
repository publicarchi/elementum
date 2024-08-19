---
author: emchateau
tags: thesaurus, outils
---

# Gestion de Thesaurus avec Ginco

Note d'information DGP/SIAF/2014/007 du 7 octobre 2014relative à la mise en œuvre d'un environnement de création, de gestion et de diffusion de vocabulaires (listes d'autorité, thésaurus, terminologies) https://francearchives.fr/file/720dbf0bd1d5e6966d200c086a546428e3d266a5/static_7780.pdf

Thésaurus pour la description et l'indexation des archives locales https://francearchives.fr/article/37828

The Thesaurus for French Local Archives and the Semantic Web
. Author links open the author workspace.Claire Sibille-deGrimoüard http://www.sciencedirect.com/science/article/pii/S1877042814040725

HADOC Penser la production des données culturelles dans un contexte d'interopérabilitésémantique et organisationnelle Katell BriatteAtelier « Passés dans le présent », 10 avril 2014 http://passes-present.eu/sites/default/files/projets/intervention_hadoc_briatte.pdf

http://www.culturecommunication.gouv.fr/Divers/Harmonisation-des-donnees-culturelles/Referentiels/Les-vocabulaires-scientifiques-et-techniques/L-application-GINCO

http://blog.sparna.fr/2013/09/19/ginco-un-editeur-skos-open-source/

https://github.com/culturecommunication/ginco

http://culturecommunication.github.io/ginco/

https://github.com/culturecommunication/ginco-diff

## Utiliser Ginco en LOD

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