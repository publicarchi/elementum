---
since: 2017-07-07
author: emchateau
tags: wikidata
---

# Wikidata, divers

Créer un élément dans Wikidata https://youtu.be/-PiS-A3w3AM

Requête de Benoit, Café des savoirs

```sparql
SELECT ?item ?itemLabel ?genderLabel (GROUP_CONCAT(DISTINCT ?occupationLabel; SEPARATOR=", ") AS ?occupations) (GROUP_CONCAT(DISTINCT ?countryLabel; SEPARATOR=", ") AS ?countries) ?death {
  VALUES ?target_country { wd:Q16 wd:Q31 wd:Q39 wd:Q142 } . #countries: Canada, France, Switzerland, Belgium. Remove this line to get worldwide.
  VALUES ?occupation { wd:Q483501 wd:Q36834 wd:Q639669 wd:Q753110 wd:Q488205 wd:Q49757 wd:Q4964182 wd:Q1281618 wd:Q36180 wd:Q482980 wd:Q1028181 wd:Q6625963 wd:Q28389 wd:Q1930187 wd:Q33999 wd:Q3282637 wd:Q81096 wd:Q201788 wd:Q18939491 wd:Q486748 wd:Q3658608 wd:Q214917 wd:Q11774202 wd:Q205375 } . #occupation: composer, poet, sculptor, writer, artist, painter...
   ?item wdt:P31 wd:Q5;
               wdt:P21 ?gender;
               wdt:P570 ?death;
               wdt:P27 ?target_country;
               wdt:P27 ?country;
               wdt:P106 ?occupation .
   FILTER( YEAR( ?death ) = 1967 ) .
   SERVICE wikibase:label {
       bd:serviceParam wikibase:language "fr,en,ru,el,es,fa" .
       ?item rdfs:label ?itemLabel .
       ?gender rdfs:label ?genderLabel .
       ?occupation rdfs:label ?occupationLabel .
       ?country rdfs:label ?countryLabel .
   } .
} GROUP BY ?item ?itemLabel ?genderLabel ?death ORDER BY ?itemLabel
```

Exemple Domaine public

```sparql
#added before 2019-02

#Shows people raised in the public domain "life + 50 years".
SELECT ?item ?itemLabel ?genderLabel (GROUP_CONCAT(DISTINCT ?occupationLabel; SEPARATOR=", ") AS ?occupations) (GROUP_CONCAT(DISTINCT ?countryLabel; SEPARATOR=", ") AS ?countries) ?death ?articles {
  VALUES ?target_country { wd:Q16 wd:Q142 wd:Q39 wd:Q31 wd:Q30 } . #countries: Canada, France, Switzerland, Belgium, USA. Removing this line to get worldwide may cause a query timeout.
  VALUES ?occ { wd:Q2500638 wd:Q20826540 wd:Q215627 } . #occupation: creator, erudite, person. These 3 occupations will also look for subclasses. Example: Alan Turing is a cryptographer, a subclass of cryptologist, a subclass of mathematician, a subclass of scientist, a subclass of erudite.
   ?item wdt:P31 wd:Q5;
               wdt:P21 ?gender;
               wdt:P27 ?target_country;
               wdt:P27 ?country;
               wdt:P106/wdt:P279* ?occ ;
               wdt:P106 ?occupation;
               wikibase:sitelinks ?articles . #Service to count the number of articles in Wikipedia language versions. The higher the number, the greater the chances that the person is very notorious.
   ?item wdt:P570 ?death . hint:Prior hint:rangeSafe true .
   FILTER( ?death >= "1969-01-01T00:00:00"^^xsd:dateTime && ?death < "1970-01-01T00:00:00"^^xsd:dateTime ) #death: public domain "life+50 years". Change both years to get a list in different legislation. Example for USA: life+70 years
   SERVICE wikibase:label {
       bd:serviceParam wikibase:language "fr,en" . #Service to retrieve the labels of items, in order of language. Example: if the label does not exist in French, the service will take the English label
       ?item rdfs:label ?itemLabel .
       ?gender rdfs:label ?genderLabel .
       ?occupation rdfs:label ?occupationLabel .
       ?country rdfs:label ?countryLabel .
   } .
} GROUP BY ?item ?itemLabel ?genderLabel ?death ?articles ORDER BY DESC (?articles) #Order by the number of articles in Wikipedia language versions. The most notorious people will be at the top of the list.
```



Exemple de requête en chronologie

<https://query.wikidata.org/embed.html#%23defaultView%3ATimeline%0ASELECT%20DISTINCT%20%3Fauthor%20%3FauthorLabel%20%3Fimage%20%3Fdate%20%20WHERE%20%7B%0A%20%20%3Fauthor%20wdt%3AP106%20wd%3AQ11900058%20.%0A%20%20%3Fauthor%20wdt%3AP569%20%3Fdate%20FILTER((YEAR(%3Fdate)%3E500)%26%26(YEAR(%3Fdate)%3C1440)).%0A%20%20OPTIONAL%20%7B%3Fauthor%20wdt%3AP18%20%3Fimage%20.%7D%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%2C%20it%2C%20de%2C%20es%2C%20fr%22%20%7D%0A%7D%20ORDER%20BY%20%3FauthorLabel>



Exemple #Liste de souverains de France et de Navarre illustrés avec leur date de naissance et/ou de décès

```sparql
SELECT ?human ?humanLabel ?dob ?dod ?isni
WHERE
{
	?human wdt:P31 wd:Q5
    ; wdt:P39 wd:Q3439798 .
	?human wdt:P18 ?picture .
	OPTIONAL { ?human wdt:P569 ?dob . ?human wdt:P570 ?dod }.
    OPTIONAL { ?human wdt:P213 ?isni }.
	BIND(YEAR(?dob) as ?yob) . #if available: year
	BIND(YEAR(?dod) as ?yod) .
	SERVICE wikibase:label {
		bd:serviceParam wikibase:language "fr" .
	}
}
LIMIT 88
```

Le problème, c’est qu’aussi peu croyable que cela puisse paraître, le modèle de Wikipédia ne contient pas de catégorie souverain ou chef d’État !!!

Mais si veut extraire les informations par nationalité, par exemple Royaume de France :

```sparql
#Liste de souverains de France et de Navarre illustrés avec leur date de naissance et/ou de décès

SELECT ?human ?humanLabel ?dob ?dod ?isni ?picture
WHERE
{
	?human wdt:P31 wd:Q5
    ; wdt:P27 wd:Q70972 .
	?human wdt:P18 ?picture .
	OPTIONAL { ?human wdt:P569 ?dob . ?human wdt:P570 ?dod }.
    OPTIONAL { ?human wdt:P213 ?isni }.
	BIND(YEAR(?dob) as ?yob) . #if available: year
	BIND(YEAR(?dod) as ?yod) .
	SERVICE wikibase:label {
		bd:serviceParam wikibase:language "fr" .
	}
}
LIMIT 88
```

La requête ne rapporte que 88 individus !

Comment imaginer croiser avec fonction de monarque si peu nombreux à être renseignés ?

```sparql
SELECT ?human ?humanLabel ?dob ?dod ?isni ?picture
WHERE
{ ?human wdt:P31 wd:Q5 .
  {?human wdt:P39 wd:Q3439798 .} 
  UNION 
  {?human wdt:P39 wd:Q18384454 .}
  UNION 
  {?human wdt:P31 wd:Q22923081 .}

	?human wdt:P18 ?picture .
	OPTIONAL { ?human wdt:P569 ?dob . ?human wdt:P570 ?dod }.
    OPTIONAL { ?human wdt:P213 ?isni }.
	BIND(YEAR(?dob) as ?yob) . #if available: year
	BIND(YEAR(?dod) as ?yod) .
	SERVICE wikibase:label {
		bd:serviceParam wikibase:language "fr" .
	}
}
ORDER BY ?dob
LIMIT 88
```

```SPARQL
#Où est Anvers dans le monde ?
#defaultView:Map
SELECT DISTINCT ?settlement ?name ?coor
WHERE
{
  
   ?subclass_settlement wdt:P279+ wd:Q486972 .
   ?settlement wdt:P31 ?subclass_settlement ;
               wdt:P625 ?coor ;
                rdfs:label ?name .
   FILTER regex(?name, "Antwerp", "i")

}
```



## Références

https://gist.github.com/ColinMaudry/6fd6a5f610f0ac3e6696

https://www.wikidata.org/wiki/Wikidata:SPARQL_query_service

https://www.mediawiki.org/wiki/Wikidata_Query_Service/User_Manual
