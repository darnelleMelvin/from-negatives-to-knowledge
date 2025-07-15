<link rel="stylesheet" href="style.css">

<p align="left">
  <a href="https://darnellemelvin.github.io/from-negatives-to-knowledge">
    <img src="assets/images/negative2nodeInverse_logo.png" alt="Home" style="height: 250px;">
  </a>
</p>

# Data Modeling

This page provides an overview of how entities, relationships, and vocabulary terms are modeled in the knowledge graph supporting *From Negatives to Knowledge*. Modeling decisions help align local metadata with widely adopted vocabularies such as `schema.org`, `skos`, `GeoNames`, and `lcsh`.

---

## 🖼️ Visualizing Modeling Decisions

Below are conceptual diagrams showing how key entity types are modeled and linked to external vocabularies:

### 📌 1. `schema:Person` Modeling Decisions

<p align="center">
  <img src="assets/images/dataModel_schemaPerson.jpg" alt="Data model for schema:Person" style="max-width: 100%; border: 1px solid #ccc; border-radius: 8px;">
</p>

A diagram showing how a `schema:Person` is modeled using properties like `birthDate`, `occupation`, and connections to external sources.

---

### 📌 2. `schema:Organization` Modeling Decisions

<p align="center">
  <img src="assets/images/dataModel_schemaOrg.jpg" alt="Data model for schema:Organization" style="max-width: 100%; border: 1px solid #ccc; border-radius: 8px;">
</p>

This diagram models various types of organizations—such as schools, churches, and businesses—using appropriate `schema:Organization` subclasses and descriptive properties.

---

### 📌 3. `unl:` Modeling Decisions (Node-to-Node Linking) 

<p align="center">
  <img src="assets/images/dataModel_unlNode2Node.jpg" alt="unl: Node Linkage Model" style="max-width: 100%; border: 1px solid #ccc; border-radius: 8px;">
</p>

This conceptual graphic shows how one `unl:` node is connected to another `unl:` node using semantic relationships drawn from vocabularies such as `agrelon:` and `schema:`. These links capture real-world relationships like affiliation, employment, or organizational roles within the graph.

---

<p style="text-align: right; margin-top: 2em;">
  <a href="https://special.library.unlv.edu/">
    <img src="assets/images/unlv_sca_logo.png" alt="UNLV Special Collections & Archives Logo" style="max-width: 200px;">
  </a>
</p>
