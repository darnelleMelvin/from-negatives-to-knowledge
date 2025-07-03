<p align="left">
  <a href="https://darnellemelvin.github.io/from-negatives-to-knowledge">
    <img src="assets/images/negative2nodeInverse_logo.png" alt="Home" style="height: 250px;">
  </a>
</p>

<link rel="stylesheet" href="style.css">

# 📊 SPARQL Queries

---

### 🔍 Query #1: Graph of People from WikiProject African Diaspora

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

**[▶️ Run this query on Wikidata Query Service](https://query.wikidata.org/#CONSTRUCT%20%7B%0A%20%20%3Fitem%20a%20skos%3AConcept%2Cschema%3APerson%20.%0A%20%20%3Fitem%20skos%3AprefLabel%20%3FitemLabel%20.%0A%20%20%3Fitem%20skos%3Adefinition%20%3Fdescription%20.%0A%20%20%3Fitem%20schema%3AbirthDate%20%3FdateOfBirth%20.%0A%20%20%3Fitem%20schema%3AdeathDate%20%3FdateOfDeath%20.%0A%20%20%3Fitem%20schema%3AbirthPlace%20%3FplaceOfBirth%20.%0A%20%20%3Fitem%20schema%3Aoccupation%20%3Foccupation%20.%0A%20%20%3Foccupation%20a%20skos%3AConcept%2Cschema%3AOccupation%20.%0A%20%20%3Foccupation%20skos%3AprefLabel%20%3FoccupationLabel%20.%0A%20%20%3Foccupation%20schema%3Adescription%20%3Foccupation_description%20.%0A%20%20%3FplaceOfBirth%20a%20skos%3AConcept%2Cschema%3APlace%20.%0A%20%20%3FplaceOfBirth%20skos%3AprefLabel%20%3FplaceOfBirthLabel%20.%0A%20%20%3FplaceOfBirth%20schema%3Adescription%20%3FplaceOfBirth_description%20.%0A%7D%0AWHERE%20%7B%0A%20%20%3Fitem%20wdt%3AP5008%20wd%3AQ15304953%20%3B%0A%20%20%20%20wdt%3AP31%20wd%3AQ5%20%3B%0A%20%20%20%20wdt%3AP31%20%3FinstanceOf%20.%0A%20%20%3Fitem%20schema%3Adescription%20%3Fdescription%20.%0A%20%20FILTER%20(LANG(%3Fdescription)%20%3D%20%22en%22)%0A%20%20%3Fitem%20wdt%3AP106%20%3Foccupation%20.%0A%20%20%3Foccupation%20rdfs%3Alabel%20%3FoccupationLabel%20.%0A%20%20FILTER%20(LANG(%3FoccupationLabel)%20%3D%20%22en%22)%0A%20%20%3Foccupation%20schema%3Adescription%20%3Foccupation_description%20.%0A%20%20FILTER%20(LANG(%3Foccupation_description)%20%3D%20%22en%22)%0A%20%20%3Fitem%20wdt%3AP569%20%3FdateOfBirth%20.%0A%20%20OPTIONAL%20%7B%3Fitem%20wdt%3AP570%20%3FdateOfDeath%7D%20.%0A%20%20%3Fitem%20wdt%3AP19%20%3FplaceOfBirth%20.%0A%20%20%3FplaceOfBirth%20rdfs%3Alabel%20%3FplaceOfBirthLabel%20.%0A%20%20FILTER%20(LANG(%3FplaceOfBirthLabel)%20%3D%20%22en%22)%0A%20%20%3FplaceOfBirth%20schema%3Adescription%20%3FplaceOfBirth_description%20.%0A%20%20FILTER%20(LANG(%3FplaceOfBirth_description)%20%3D%20%22en%22)%0A%7D%20LIMIT%201)**
