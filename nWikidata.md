# nWikidata

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

