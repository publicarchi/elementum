# SPARQL DataBnf


## Obtenir un id de concept par l’isni

```sparql
PREFIX isni: <http://isni.org/ontology#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
SELECT *
WHERE { 
  ?id isni:identifierValid "0000000121339458" .
}
LIMIT 100
```

```sparql
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX isni: <http://isni.org/ontology#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
SELECT *
WHERE { 
  ?idConcept isni:identifierValid "0000000121339458" ;
      foaf:focus ?idAuteur .
  OPTIONAL {
  	?idAuteur foaf:name ?nomComplet .
  }
  OPTIONAL {
	?idAuteur foaf:name ?nomComplet .
  }
  OPTIONAL {
	?idAuteur foaf:familyName ?nom .
  } 
  OPTIONAL {
	?idAuteur foaf:givenName ?prenom .
  }
}
LIMIT 100
```

# Retrouver les spectacles d’un auteur (spectacles et manifestations)

```sparql
PREFIX bnfroles: <http://data.bnf.fr/vocabulary/roles/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX isni: <http://isni.org/ontology#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
SELECT *
WHERE { 
  ?idConcept isni:identifierValid "0000000121339458" ;
      foaf:focus ?idAuteur .
  ?idSpectacle bnfroles:r500 ?idAuteur .
  
  
  OPTIONAL {
  	?idAuteur foaf:name ?nomComplet .
  }
}
```

En éliminant les manifestations

```sparql
PREFIX dcmitype: <http://purl.org/dc/dcmitype/>
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX bnfroles: <http://data.bnf.fr/vocabulary/roles/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX isni: <http://isni.org/ontology#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
SELECT ?nomComplet ?idSpectacle ?titre
WHERE { 
  ?idConcept isni:identifierValid "0000000121339458" ;
      foaf:focus ?idAuteur .
  ?idSpectacle bnfroles:r500 ?idAuteur ;
      a dcmitype:Event .
  
  OPTIONAL {
  	?idSpectacle dcterms:title ?titre
  }
  OPTIONAL {
  	?idAuteur foaf:name ?nomComplet .
  }
}
```

Avec les dates

```sparql
PREFIX bnf-onto: <http://data.bnf.fr/ontology/bnf-onto/>
PREFIX dcmitype: <http://purl.org/dc/dcmitype/>
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX bnfroles: <http://data.bnf.fr/vocabulary/roles/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX isni: <http://isni.org/ontology#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
SELECT ?nomComplet ?idSpectacle ?titre ?date
WHERE { 
  ?idConcept isni:identifierValid "0000000121339458" ;
      foaf:focus ?idAuteur .
  ?idSpectacle bnfroles:r500 ?idAuteur ;
      a dcmitype:Event .
  
  OPTIONAL {
  	?idSpectacle dcterms:title ?titre .
  }
  OPTIONAL {
    ?idSpectacle dcterms:date ?date .
  }
  OPTIONAL {
  	?idAuteur foaf:name ?nomComplet .
  }
}
```

En récupérant des informations sur le spectacle
(mais il serait sans doute plus productif de travailler directement avec les notices complètes)
nota : il manque les informations de disrtibution dans les données exposées

```sparql
PREFIX marcrel: <http://id.loc.gov/vocabulary/relators/>
PREFIX bnf-onto: <http://data.bnf.fr/ontology/bnf-onto/>
PREFIX dcmitype: <http://purl.org/dc/dcmitype/>
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX bnfroles: <http://data.bnf.fr/vocabulary/roles/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX isni: <http://isni.org/ontology#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
SELECT ?nomComplet ?idSpectacle ?titre ?date ?cost ?nomCost
WHERE { 
  ?idConcept isni:identifierValid "0000000121339458" ;
      foaf:focus ?idAuteur .
  OPTIONAL {
  	?idAuteur foaf:name ?nomComplet .
  }
  ?idSpectacle bnfroles:r500 ?idAuteur ;
      a dcmitype:Event .
  OPTIONAL {
  	?idSpectacle dcterms:title ?titre .
  }
  OPTIONAL {
    ?idSpectacle dcterms:date ?date .
  }
  OPTIONAL {
    ?idSpectacle marcrel:cst ?cost .
    ?cost foaf:name ?nomCost
  }
  
}
LIMIT 100
```

Avec la page pour pouvoir récupérer la notice en json ou jsonLD

```sparql
PREFIX marcrel: <http://id.loc.gov/vocabulary/relators/>
PREFIX bnf-onto: <http://data.bnf.fr/ontology/bnf-onto/>
PREFIX dcmitype: <http://purl.org/dc/dcmitype/>
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX bnfroles: <http://data.bnf.fr/vocabulary/roles/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX isni: <http://isni.org/ontology#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
SELECT ?nomComplet ?idSpectacle ?page ?titre ?date ?cost ?nomCost
WHERE { 
  ?idConcept isni:identifierValid "0000000121339458" ;
      foaf:focus ?idAuteur .
  OPTIONAL {
  	?idAuteur foaf:name ?nomComplet .
  }
  ?idSpectacle bnfroles:r500 ?idAuteur ;
      a dcmitype:Event ;
	  foaf:page ?page .
  OPTIONAL {
  	?idSpectacle dcterms:title ?titre .
  }
  OPTIONAL {
    ?idSpectacle dcterms:date ?date .
  }
  OPTIONAL {
    ?idSpectacle marcrel:cst ?cost .
    ?cost foaf:name ?nomCost
  }
  
}
LIMIT 100
```

## Festival Avignon

```sparql
PREFIX dcmitype: <http://purl.org/dc/dcmitype/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX bnfroles: <http://data.bnf.fr/vocabulary/roles/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
SELECT DISTINCT *
WHERE {
  ?spectacle rdf:type dcmitype:Event ;
  	bnfroles:r900 ?id ;
	dcterms:title ?title .
  ?id foaf:page ?page .
  FILTER contains(STR(?page), "festival_d_avignon")
}
LIMIT 100
```