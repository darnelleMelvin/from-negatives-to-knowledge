<p align="left">
  <a href="https://darnellemelvin.github.io/from-negatives-to-knowledge">
    <img src="assets/images/negative2nodeInverse_logo.png" alt="Home" style="height: 250px;">
  </a>
</p>

<link rel="stylesheet" href="style.css">

# 📊 SPARQL Queries

Explore queries contributed by and inspired by UNLV Wikimedians and Wikidata editors, focusing on the African Diaspora and broader community-linked topics. These examples progress from basic lookups to advanced graph patterns.

---

### 🔍 Query #1: What *types* of things have UNLV Wikimedians contributed to?

This query looks at all items connected to the [UNLV Wikimedians Projects](https://www.wikidata.org/wiki/Q100202113) and returns what types of entities they are (`instance of`, `P31`).

```sparql
SELECT DISTINCT ?instanceOfLabel ?instanceOf
WHERE
{
 ?resource wdt:P5008 wd:Q100202113 ;
     wdt:P31 ?instanceOf .
 SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
}ORDER BY ASC(?instanceOfLabel)

```

<strong><a href="https://query.wikidata.org/#SELECT%20DISTINCT%20%3FinstanceOfLabel%20%3FinstanceOf%0AWHERE%20%7B%0A%20%20%3Fresource%20wdt%3AP5008%20wd%3AQ100202113%20%3B%0A%20%20%20%20%20%20%20%20wdt%3AP31%20%3FinstanceOf%20.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%7D%0AORDER%20BY%20ASC(%3FinstanceOfLabel)" target="_blank">▶️ Run this query on Wikidata</a></strong>

---

### 🧮 Query #2: What properties are used in UNLV Wikimedians' contributions?

This query identifies which Wikidata properties (`P###`) are used across the group’s contributions and returns both the property and its English label.

```sparql
SELECT DISTINCT ?property ?propertyLabel
WHERE
{
 ?resource wdt:P5008 wd:Q100202113 .
 ?resource ?prop ?value .
 ?property wikibase:directClaim ?prop .
 SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
}ORDER BY ?propertyLabel

```
<strong><a href="https://query.wikidata.org/#SELECT%20DISTINCT%20%3Fproperty%20%3FpropertyLabel%0AWHERE%20%7B%0A%20%20%3Fitem%20wdt%3AP5008%20wd%3AQ100202113%20.%0A%20%20%3Fitem%20%3Fprop%20%3Fvalue%20.%0A%20%20%3Fproperty%20wikibase%3AdirectClaim%20%3Fprop%20.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%7D%0AORDER%20BY%20%3FpropertyLabel" target="_blank" rel="noopener noreferrer">▶️ Run this query on Wikidata</a></strong>

---

### 🗺️ Query #3: Map by Type (instance of)
This adds a map visualization layer for contributions to Wikidata by the UNLV Wikimedians group, grouped by what type of entity they are.  

```sparql
#defaultView:Map
SELECT DISTINCT ?resource ?resourceLabel ?coord ?layerLabel
WHERE
{
 ?resource wdt:P5008 wd:Q100202113 ;
     wdt:P31 ?type ;
     wdt:P625 ?coord .
 BIND(?type AS ?layer)
 SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
}ORDER BY ASC(?layerLabel)
```

<strong><a href="https://query.wikidata.org/#SELECT%20DISTINCT%20%3Fitem%20%3FitemLabel%20%3Fcoord%20%3FtypeLabel%0AWHERE%20%7B%0A%20%20%3Fitem%20wdt%3AP5008%20wd%3AQ100202113%20%3B%0A%20%20%20%20%20%20%20%20wdt%3AP31%20%3Ftype%20%3B%0A%20%20%20%20%20%20%20%20wdt%3AP625%20%3Fcoord%20.%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22%20%7D%0A%7D" target="_blank" rel="noopener noreferrer">▶️ Run this query with Map view</a></strong>

---

### 🔍 Query #4: Graph of People from WikiProject African Diaspora

This `CONSTRUCT` query builds a graph of individuals associated with the [WikiProject African diaspora (Q15304953)](https://www.wikidata.org/wiki/Q15304953). It includes their place of birth, date of birth/death, and occupation using `schema.org` and `skos` vocabularies.

```sparql
CONSTRUCT {
  ?item a skos:Concept, schema:Person .
  ?item skos:prefLabel ?itemLabel .
  ?item skos:definition ?description .
  ?item schema:birthDate ?dateOfBirth .
  ?item schema:deathDate ?dateOfDeath .
  ?item schema:birthPlace ?placeOfBirth .
  ?item schema:occupation ?occupation .

  ?occupation a skos:Concept, schema:Occupation .
  ?occupation skos:prefLabel ?occupationLabel .
  ?occupation schema:description ?occupation_description .

  ?placeOfBirth a skos:Concept, schema:Place .
  ?placeOfBirth skos:prefLabel ?placeOfBirthLabel .
  ?placeOfBirth schema:description ?placeOfBirth_description .
}
WHERE {
  ?item wdt:P5008 wd:Q15304953 ;
        wdt:P31 wd:Q5 ;
        wdt:P31 ?instanceOf .
  ?item schema:description ?description .
  FILTER (LANG(?description) = "en")

  ?item wdt:P106 ?occupation .
  ?occupation rdfs:label ?occupationLabel .
  FILTER (LANG(?occupationLabel) = "en")
  ?occupation schema:description ?occupation_description .
  FILTER (LANG(?occupation_description) = "en")

  ?item wdt:P569 ?dateOfBirth .
  OPTIONAL { ?item wdt:P570 ?dateOfDeath }

  ?item wdt:P19 ?placeOfBirth .
  ?placeOfBirth rdfs:label ?placeOfBirthLabel .
  FILTER (LANG(?placeOfBirthLabel) = "en")
  ?placeOfBirth schema:description ?placeOfBirth_description .
  FILTER (LANG(?placeOfBirth_description) = "en")
}
LIMIT 100
```

<strong><a href="https://query.wikidata.org/#CONSTRUCT%20%7B%0A%20%20%3Fitem%20a%20skos%3AConcept%2Cschema%3APerson%20.%0A%20%20%3Fitem%20skos%3AprefLabel%20%3FitemLabel%20.%0A%20%20%3Fitem%20skos%3Adefinition%20%3Fdescription%20.%0A%20%20%3Fitem%20schema%3AbirthDate%20%3FdateOfBirth%20.%0A%20%20%3Fitem%20schema%3AdeathDate%20%3FdateOfDeath%20.%0A%20%20%3Fitem%20schema%3AbirthPlace%20%3FplaceOfBirth%20.%0A%20%20%3Fitem%20schema%3Aoccupation%20%3Foccupation%20.%0A%20%20%3Foccupation%20a%20skos%3AConcept%2Cschema%3AOccupation%20.%0A%20%20%3Foccupation%20skos%3AprefLabel%20%3FoccupationLabel%20.%0A%20%20%3Foccupation%20schema%3Adescription%20%3Foccupation_description%20.%0A%20%20%3FplaceOfBirth%20a%20skos%3AConcept%2Cschema%3APlace%20.%0A%20%20%3FplaceOfBirth%20skos%3AprefLabel%20%3FplaceOfBirthLabel%20.%0A%20%20%3FplaceOfBirth%20schema%3Adescription%20%3FplaceOfBirth_description%20.%0A%7D%0AWHERE%20%7B%0A%20%20%3Fitem%20wdt%3AP5008%20wd%3AQ15304953%20%3B%0A%20%20%20%20wdt%3AP31%20wd%3AQ5%20%3B%0A%20%20%20%20wdt%3AP31%20%3FinstanceOf%20.%0A%20%20%3Fitem%20schema%3Adescription%20%3Fdescription%20.%0A%20%20FILTER%20(LANG(%3Fdescription)%20%3D%20%22en%22)%0A%20%20%3Fitem%20wdt%3AP106%20%3Foccupation%20.%0A%20%20%3Foccupation%20rdfs%3Alabel%20%3FoccupationLabel%20.%0A%20%20FILTER%20(LANG(%3FoccupationLabel)%20%3D%20%22en%22)%0A%20%20%3Foccupation%20schema%3Adescription%20%3Foccupation_description%20.%0A%20%20FILTER%20(LANG(%3Foccupation_description)%20%3D%20%22en%22)%0A%20%20%3Fitem%20wdt%3AP569%20%3FdateOfBirth%20.%0A%20%20OPTIONAL%20%7B%3Fitem%20wdt%3AP570%20%3FdateOfDeath%7D%20.%0A%20%20%3Fitem%20wdt%3AP19%20%3FplaceOfBirth%20.%0A%20%20%3FplaceOfBirth%20rdfs%3Alabel%20%3FplaceOfBirthLabel%20.%0A%20%20FILTER%20(LANG(%3FplaceOfBirthLabel)%20%3D%20%22en%22)%0A%20%20%3FplaceOfBirth%20schema%3Adescription%20%3FplaceOfBirth_description%20.%0A%20%20FILTER%20(LANG(%3FplaceOfBirth_description)%20%3D%20%22en%22)%0A%7D%20LIMIT%20100" target="_blank">▶️ Run this graph query</a></strong>
