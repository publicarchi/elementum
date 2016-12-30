---
title: note WSDL
filename: nWSDL.md
date: 2014-03-05
version: 1.0
---

# WSDL ou WADL

imaginer une extension de xqDoc pour une doc en WSDL 2.0 ou WADL d’un service RESTXQ


## WSDL

WSDL est un langage XML pour la description formelle de services web.
WSDL, depuis la version 2.0 prend en charge de HTTP.
WSDL est une recommandation du W3C de 2007.

WSDL présente les contrats d’interface pour les clients. La description WSDL spécifie l’adresse, les mécanisme de communication autorisés, l’interface et le type des messages d’un service web. En somme une description WSDL fournit toutes les informations nécessaires à un client pour utiliser un service web.

WSDL permet de renseigner
- l’URL du service
- les mécanismes de communication qu’il comprend
- les opérations qu’il peut réaliser
- la structure de ses messages

Squelette d’un document WSDL 2.0 :

WSDL est un langage XML dans l’espace de nom http://www.w3.org/ns/wsdl
L’élément racine d’un document WSDL est `description`.
Il accepte quatre éléments fils qui rassemblent les détails sur le service web.
- types
- interface
- binding
- service

```xml
    <wsdl:description xmlns:wsdl="http://www.w3.org/ns/wsdl">
        <wsdl:types/>
        <wsdl:interface/>
        <wsdl:binding/>
        <wsdl:service/>
    </wsdl:description>
```

L’élément `type` contient toutes les informations de schéma XML et les définitions de type qui décrivent les messages du service web.

L’élément `interface` définit les opérations du web service, y compris les sorties et les entrées spécifiques, ainsi que les messages d’erreurs qui doivent être passés, et leur ordre.

L’élément `binding` définit comment un client peut communiquer avec un service web. Dans le cas de service REST, un binding spécifie que le client peut communiquer en utilisant HTTP.

L’élément `service` associe une adresse pour le service web avec une interface spécifique et un binding.

WSDL 2.0 définit deux espaces de noms supplémentaires qui peuvent être employés pour des services REST :

- Un espace de nom HTTP http://www.w3.org/ns/wsdl/http qui inclue l’élément binding HTTP
- un espace de nom d’extensions http://www.w3.org/ns/wsdl-extensions qui inclue les définitions de trois attributs : deux d’entre eux sont utilisés pour associer un hyperlien dans un document XML avec la description d’un service web, et le troisième pour décrire l’opération d’un web service comme sûre.


Source
-------

- [Describe REST Web services with WSDL 2.0, IBM developerWorks, 2008](http://www.ibm.com/developerworks/webservices/library/ws-restwsdl/)
- [Web Services Description Language (WSDL) Version 2.0 Part 0: Primer](http://www.w3.org/TR/2007/REC-wsdl20-primer-20070626/)
- [Describing RESTful Applications](http://www.infoq.com/articles/subbu-allamaraju-rest)
- [WADL](http://fr.wikipedia.org/wiki/Web_Application_Description_Language)
- http://bitworking.org/news/193/Do-we-need-WADL
- http://www.w3.org/Submission/wadl

Recommandations
--------
- [Web Services Description Language (WSDL) Version 2.0 Part 0: Primer](http://www.w3.org/TR/wsdl20-primer/)
- [Web Services Description Language (WSDL) Version 2.0 Part 1: Core Language](http://www.w3.org/TR/wsdl20)
- [Web Services Description Language (WSDL) Version 2.0 Part 2: Adjuncts](http://www.w3.org/TR/wsdl20-adjuncts/)
- [Semantic Annotations for WSDL and XML Schema](http://www.w3.org/TR/sawsdl/)
- [Semantic Annotations for WSDL and XML Schema — Usage Guide](http://www.w3.org/TR/sawsdl-guide/)
- [Semantic Annotations for WSDL Working Group](http://www.w3.org/2002/ws/sawsdl/)
