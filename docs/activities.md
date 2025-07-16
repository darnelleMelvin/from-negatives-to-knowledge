<link rel="stylesheet" href="style.css">

<p align="left">
  <a href="https://darnellemelvin.github.io/from-negatives-to-knowledge">
    <img src="assets/images/negative2nodeInverse_logo.png" alt="Home" style="height: 250px;">
  </a>
</p>

# 🧠 Hands-On Activities

## 1. Entity Annotation
Look at this sample image from the Clinton Wright Collection.  

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
  <p><strong>Caption:</strong> Transcribed from attachment on the back of the photo: "Sands Hotel before 1962 left to right Dr. James B. McMillan, Dr. Charles I. West, Sammy Davis, Jr., Mons. James B. Empey, Pastor of St. Joan of Arc Catholic Church. Presenting an "Award of Merit and honorary fellowship" to Sammy Davis, Jr. and Will Mastin Trio from the George Washington Carver Memorial Institute of Washington, D. C. for outstanding contributions to the arts, humanities, and better race relations."

    
Sands Hotel and Casino: 3355 Las Vegas Boulevard South</p>
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

## 🗂 Part 2: What metadata can you extract?

Now that you've reviewed the caption, take a moment to think like a metadata creator. Based on what you've read, how might you model this information in a knowledge graph?

**Prompt:** What structured metadata can you identify from the caption?

Click each category below to reveal the example values:

<details>
<summary><strong>schema:Person</strong></summary>

- Dr. James B. McMillan  
- Dr. Charles I. West  
- Sammy Davis, Jr.  
- Mons. James B. Empey  
- Will Mastin  

</details>

<details>
<summary><strong>schema:Event</strong></summary>

- Award of Merit and honorary fellowship presentation  
- Event recognizing contributions to the arts, humanities, and race relations  

</details>

<details>
<summary><strong>schema:Organization</strong></summary>

- George Washington Carver Memorial Institute  
- St. Joan of Arc Catholic Church  

</details>

<details>
<summary><strong>schema:Place</strong></summary>

- Sands Hotel and Casino  
- 3355 Las Vegas Boulevard South  

</details>

<details>
<summary><strong>schema:Award / schema:Role</strong></summary>

- Outstanding contributions to the arts, humanities, and better race relations  
- Honorary fellowship  
- Award of Merit  

</details>

---

**💡 Try this:**  
Write out a few RDF triples (in Turtle or natural language) that describe this moment using what you know about Schema.org or SKOS.

> _Bonus challenge:_ Can you find a Wikidata Q-ID for any of the people, places, or organizations listed?



---

## 2. Modeling Scenario
You're given metadata for a local church picnic. How would you model:
- The event?
- People featured in the image?
- Their relationship (family, social, professional)?

---

## 3. SPARQL Challenge
Use our [example dataset](queries.md) and try this:
```sparql   
SELECT ?person ?relation ?relatedPerson
WHERE {
  ?person a schema:Person .
  ?person agrelon:hasFamilyRelation ?relatedPerson .
  ?person rdfs:label ?name .
}

---

<p style="text-align: right; margin-top: 2em;">
  <a href="https://special.library.unlv.edu/">
  <img src="assets/images/unlv_sca_logo.png" alt="UNLV Special Collections & Archives Logo" style="max-width: 200px;">
  </a>
</p>
