<link rel="stylesheet" href="style.css">

<p align="left">
  <a href="index.md">
    <img src="assets/images/negative2nodeInverse_logo.png" alt="Home" style="height: 250px;">
  </a>
</p>

# Hands-On Activities

## 1. Entity Annotation
Look at this sample image from the Clinton Wright Collection.  
- Who can you identify?  
- What places, events, or organizations are depicted?  
[Open the image →](assets/images/photo-sample.jpg)

## 2. Modeling Scenario
You're given metadata for a local church picnic. How would you model:
- The event?
- People featured in the image?
- Their relationship (family, social, professional)?

## 3. SPARQL Challenge
Use our [example dataset](queries.md) and try this:
```sparql
SELECT ?person ?relation ?relatedPerson
WHERE {
  ?person a schema:Person .
  ?person agrelon:hasFamilyRelation ?relatedPerson .
  ?person rdfs:label ?name .
}

