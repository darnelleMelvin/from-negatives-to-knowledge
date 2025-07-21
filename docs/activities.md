<link rel="stylesheet" href="style.css">

<p align="left">
  <a href="https://darnellemelvin.github.io/from-negatives-to-knowledge">
    <img src="assets/images/negative2nodeInverse_logo.png" alt="Home" style="height: 250px;">
  </a>
</p>

# 🧠 Hands-On Activities

## Activity 1. Entity Annotation
Look at this sample image from the Marie and James B. McMillan Photograph Collection (PH-00334).  

## 👀 Who can you identify?

<div style="text-align: center; margin-bottom: 1em;">
  <img id="activityImage" src="assets/images/ohr000452.jpg" alt="Historic Westside photo" style="max-width: 90%; border: 1px solid #ccc; border-radius: 8px;">
</div>

<div style="text-align: center; margin-bottom: 2em;">
  <button id="showButton" onclick="showCaption()" style="padding: 10px 20px; font-size: 1em; background-color: #810100; color: white; border: none; border-radius: 5px; cursor: pointer;">
    Show Caption
  </button>

  <button id="hideButton" onclick="hideCaption()" style="display: none; padding: 10px 20px; font-size: 1em; background-color: #555; color: white; border: none; border-radius: 5px; cursor: pointer;">
    Hide Caption
  </button>
</div>

<div id="captionBox" style="display: none; text-align: center; background: #f9f9f9; padding: 1em; border: 1px solid #ccc; border-radius: 8px; max-width: 80%; margin: auto;">
  <p><strong>Caption</strong>: Transcribed from attachment on the back of the photo: "Sands Hotel before 1962 left to right Dr. James B. McMillan, Dr. Charles I. West, Sammy Davis, Jr., Mons. James B. Empey, Pastor of St. Joan of Arc Catholic Church. Presenting an "Award of Merit and honorary fellowship" to Sammy Davis, Jr. and Will Mastin Trio from the George Washington Carver Memorial Institute of Washington, D. C. for outstanding contributions to the arts, humanities, and better race relations."

    
Sands Hotel and Casino: 3355 Las Vegas Boulevard South</p> 

<p><strong>Citation</strong>: ohr000452. Marie and James B. McMillan Photograph Collection, 1900-1994. PH-00334. Special Collections and Archives, University Libraries, University of Nevada, Las Vegas. Las Vegas, Nevada. <a href="http://n2t.net/ark:/62930/d1959g30x" target="_blank">http://n2t.net/ark:/62930/d1959g30x</a></p>
</div>

<script>
  function showCaption() {
    document.getElementById('captionBox').style.display = 'block';
    document.getElementById('showButton').style.display = 'none';
    document.getElementById('hideButton').style.display = 'inline-block';
  }

  function hideCaption() {
    document.getElementById('captionBox').style.display = 'none';
    document.getElementById('showButton').style.display = 'inline-block';
    document.getElementById('hideButton').style.display = 'none';
  }
</script>

---

### 🗂 Part B: Mapping Concepts to Classes

Now that you’ve reviewed the caption, let’s examine how key entities in the photo can be represented using <a href="https://schema.org/docs/full.html" target="_blank">Schema.org classes</a>.  

**Prompt:** Read the caption and explore how each of the following Schema.org classes applies to people, groups, organizations, and places mentioned.

Click each class below to reveal the corresponding values:

<details>
<summary><strong>schema:Person</strong></summary>

<ul>
  <li>Dr. James B. McMillan</li>
  <li>Dr. Charles I. West</li>
  <li>Sammy Davis, Jr.</li>
  <li>Mons. James B. Empey</li>
</ul>
</details>

<details>
<summary><strong>schema:PerformingGroup</strong></summary>

<ul>
  <li>Will Mastin Trio</li>
</ul>
</details>

<details>
<summary><strong>schema:Organization</strong></summary>

<ul>
  <li>George Washington Carver Memorial Institute</li>
  <li>St. Joan of Arc Catholic Church</li>
</ul>
</details>

<details>
<summary><strong>schema:Place</strong></summary>

<ul>
  <li>Sands Hotel and Casino (3355 Las Vegas Boulevard South)</li>
</ul>
</details>

---

**💡 Try this:**  
Using <strong>Part B: Mapping Concepts to Classes</strong> as a reference, complete the RDF triple statement by replacing the square brackets with an schema.org class.  

<textarea rows="10" style="width:100%; font-family: monospace;">
@prefix schema: <http://schema.org/> .
@prefix ex: <http://example.org/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
@prefix wd: <https://www.wikidata.org/entity/> .  
  
ex:stJoanOfArcCathChurch a [REPLACE WITH A SCHEMA CLASS HERE] ;
    schema:name "St. Joan of Arc Catholic Church"@en .

    
</textarea>

> _Bonus challenge:_ Can you find a Wikidata Q-ID or a uri from a name authority file for any of the people, places, or organizations listed?



---

## Activity 2. Modeling Scenario and Writing RDF
Understanding how to express structured metadata in RDF is key to building your knowledge graph. Below is an example using real entities from the project.

### 📄 RDF Triple Structure in Turtle Syntax

```turtle
@prefix schema: <http://schema.org/> .
@prefix skos: <http://www.w3.org/2004/02/skos/core#> .
@prefix agrelon: <https://d-nb.info/standards/elementset/agrelon#> .
@prefix unl: <https://special.library.unlv.edu/taxonomy/term/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

unl:16527 a skos:Concept ;
    a schema:Person ;
    skos:prefLabel "West, Charles I., 1908-1984"@en ;
    skos:note "American doctor, civil rights activist, and newspaper publisher."@en ;
    skos:inScheme unl: ;
    schema:name "Charles I. West"@en ;
    schema:givenName "Charles"@en ;
    schema:additionalName "I."@en ;
    schema:familyName "West"@en ;
    schema:birthDate "1908-09-27"^^xsd:date ;    
    schema:birthPlace <https://sws.geonames.org/4138106/> ;
    schema:deathDate "1984-10"^^xsd:date ;
    schema:deathPlace <https://sws.geonames.org/7174241/> ;
    schema:hasOccupation <http://id.loc.gov/authorities/subjects/sh85026385> ;
    schema:hasOccupation <http://id.loc.gov/authorities/subjects/sh85101610> ;
    schema:alumniOf unl:26371 ;
    schema:alumniOf unl:26372 ;
    schema:founder unl:13280 ;
    agrelon:HasSpouse unl:27781 ;
    agrelon:hasChild unl:17559 ;
    agrelon:HasColleague unl:15502 ;
    agrelon:HasColleague unl:15811 ;
    agrelon:HasColleague unl:16510 ;
    agrelon:HasColleague unl:1758 ;
    agrelon:HasColleague unl:17776 ;
    agrelon:HasColleague unl:6025 ;
    skos:exactMatch <http://id.loc.gov/authorities/names/no2019080699> ;
    skos:closeMatch <http://www.wikidata.org/entity/Q105758712> ;
    rdfs:seeAlso <http://n2t.net/ark:/62930/f13t22> .
```
This example uses Schema.org, SKOS, and Agrelon vocabularies to model relationships and biographical metadata. The unl: prefix represents local identifiers from the UNLV taxonomy.  

### 🧾 Explanation of RDF Predicates and Selected Triple Components

| **Triple Component**                  | **Description**                                                                 |
|--------------------------------------|---------------------------------------------------------------------------------|
| `a skos:Concept`                     | Declares the resource as a SKOS concept, allowing it to function in a controlled vocabulary or thesaurus. |
| `a schema:Person`                    | Declares the resource as a person class using Schema.org.                       |
| `skos:prefLabel`                     | The preferred label or name of the person, formatted for use in SKOS vocabularies. |
| `skos:note`                          | A brief biographical note or description.                                       |
| `skos:inScheme unl:`                | Indicates this term belongs to the UNLV controlled vocabulary. |
| `schema:name`                        | The name of the item (in direct order), combining given, middle, and family names. |
| `schema:givenName`                   | The person’s first name.                                                       |
| `schema:additionalName`              | The person’s middle name or initial.                                           |
| `schema:familyName`                  | The person’s last name or family name.                                         |
| `schema:birthDate`                   | The person’s birthdate in ISO format using the XML Schema datatype.           |
| `schema:birthPlace`                  | URI referring to the person’s place of birth.                |
| `schema:deathDate`                   | The person’s deathdate in ISO format using the XML Schema datatype.          |
| `schema:deathPlace`                  | URI referring to the person’s place of death.                                 |
| `schema:hasOccupation`               | Links to one or more occupation terms using controlled subject vocabularies (e.g., LCSH). |
| `schema:alumniOf`                    | Indicates the person attended (graduated from) the institution identified by the URI. |
| `schema:founder`                     | Indicates the person founded the organization or entity identified by the URI. |
| `agrelon:HasSpouse unl:27781`        | Relationship link to a spouse entity.                                          |
| `agrelon:hasChild unl:17559`         | Relationship link to a child entity.                                           |
| `agrelon:HasColleague`              | Indicates professional relationships with identified colleagues.               |
| `skos:exactMatch`                    | Links to a matching external authority record (e.g., Library of Congress).     |
| `skos:closeMatch`                    | Links to a closely matching external authority record (e.g., Wikidata, Dbpedia). |
| `rdfs:seeAlso`                       | Further information about the subject resource, typically linking to related web or archival content. |

---

### 💡 Part B: Building on Classes from Activity 1  

Using the example URIs and classes below, write RDF statements to describe each entity. For each one:

* Use the `a` keyword to assign the appropriate schema: class as its <a href="https://www.w3.org/TR/rdf-schema/#ch_type" target="_blank">`rdf:type`</a>
  
* Add an <a href="http://www.w3.org/2004/02/skos/core#prefLabel" target="_blank">`skos:prefLabel`</a> to provide a human-readable name  

* Add a <a href="http://www.w3.org/2004/02/skos/core#note" target="_blank">`skos:note`</a> to briefly describe the entity


| Entity                                      | URI                                                   | Class (click on Class to explore their properties)                                                                                           |
| ------------------------------------------- | -----------------------------------------------------------------------------------------------------------------------  | ------------------------------------------------------------------------- |
| Sammy Davis, Jr.                            | <a href="https://special.library.unlv.edu/taxonomy/term/3454" target="_blank">https://special.library.unlv.edu/taxonomy/term/3454</a>    | <a href="https://schema.org/Person" target="_blank">`schema:Person`</a>                   |
| Will Mastin Trio                            | <a href="https://special.library.unlv.edu/taxonomy/term/9834" target="_blank">https://special.library.unlv.edu/taxonomy/term/9834</a>    | <a href="https://schema.org/PerformingGroup" target="_blank">`schema:PerformingGroup`</a> |
| Mons. James B. Empey                        | <a href="https://special.library.unlv.edu/taxonomy/term/28078" target="_blank">https://special.library.unlv.edu/taxonomy/term/28078</a>  | <a href="https://schema.org/Person" target="_blank">`schema:Person`</a>                   |
| St. Joan of Arc Catholic Church             | <a href="https://special.library.unlv.edu/taxonomy/term/28100" target="_blank">https://special.library.unlv.edu/taxonomy/term/28100</a>  | <a href="https://schema.org/Organization" target="_blank">`schema:Organization`</a>   |
| Sands Hotel & Casino                        | <a href="https://special.library.unlv.edu/taxonomy/term/11258" target="_blank">https://special.library.unlv.edu/taxonomy/term/11258</a>  | <a href="https://schema.org/Place" target="_blank">`schema:Place`</a>                     |

<textarea rows="10" style="width:100%; font-family: monospace;">
@prefix skos: <http://www.w3.org/2004/02/skos/core#> .
@prefix unl: <https://special.library.unlv.edu/taxonomy/term/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
@prefix schema: <http://schema.org/> .
@prefix agrelon: <https://d-nb.info/standards/elementset/agrelon#> .  

</textarea>

**💡 Try This:**
Use the following entities to write your own RDF triples (**SEE OUR PROJECT <a href="https://darnellemelvin.github.io/from-negatives-to-knowledge/classes.html" target="_blank">CLASS & PROPERTY DOCUMENTATION</a>**):  

<a href="https://special.library.unlv.edu/taxonomy/term/13280" target="_blank">`unl:13280`</a> Las Vegas voice  

<a href="https://special.library.unlv.edu/taxonomy/term/17776" target="_blank">`unl:17776`</a> Clinton Wright  

<a href="https://special.library.unlv.edu/taxonomy/term/27746" target="_blank">`unl:27746`</a> Arkansas Agricultural, Mechanical, and Normal College 

<a href="https://special.library.unlv.edu/taxonomy/term/16527" target="_blank">`unl:16527`</a> Dr. Charles I. West

**Focus on:**

* Assigning the correct class using `a` (short for <a href="https://www.w3.org/TR/rdf-schema/#ch_type" target="_blank">`rdf:type`</a>)

* Using <a href="https://www.w3.org/2009/08/skos-reference/skos.html#prefLabel" target="_blank">`skos:prefLabel`</a> and <a href="https://schema.org/name" target="_blank">`schema:name`</a> for the labels

* Using <a href="https://www.w3.org/2009/08/skos-reference/skos.html#note" target="_blank">`skos:note`</a> for a description

* Describing relationships using properties like <a href="https://schema.org/memberOf" target="_blank">`schema:memberOf`</a>, <a href="https://schema.org/member" target="_blank">`schema:member`</a>, <a href="https://schema.org/alumniOf" target="_blank">`schema:alumniOf`</a>, <a href="https://schema.org/alumni" target="_blank">`schema:alumni`</a>, <a href="https://d-nb.info/standards/elementset/agrelon#hasEmployer" target="_blank">`agrelon:hasEmployer`</a>, <a href="https://d-nb.info/standards/elementset/agrelon#hasEmployee" target="_blank">`agrelon:hasEmployee`</a>, or <a href="https://schema.org/affiliation" target="_blank">`schema:affiliation`</a>

* Linking entities to external name authority files via <a href="https://www.w3.org/2009/08/skos-reference/skos.html#closeMatch" target="_blank">`skos:closeMatch`</a> or <a href="https://www.w3.org/2009/08/skos-reference/skos.html#exactMatch" target="_blank">`skos:exactMatch` 

--- 

