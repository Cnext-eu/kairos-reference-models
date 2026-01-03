# Reference Models

This folder contains external ontologies and standards used by the Kairos Core Ontology.

---

## Folder Structure

### 📚 authoritative-ontologies

**What:** Official RDF/OWL ontologies published by standards bodies or authorities.

**Characteristics:**
- Published as RDF/OWL by the original authority
- Stable namespaces controlled by the publisher
- Clear versioning and licensing
- Imported as-is (no semantic reinterpretation)

**Examples:**
- FIBO (Financial Industry Business Ontology)
- W3C vocabularies (SKOS, Dublin Core, etc.)
- ISO/UN vocabularies in RDF format

**Usage:** Read-only reference; semantics owned by the publisher.

---

### 🔧 derived-ontologies

**What:** RDF/OWL representations we create by interpreting non-RDF standards and documentation.

**Characteristics:**
- Our interpretation of source material (PDFs, XSD, specs)
- We own the RDF modeling choices
- Requires careful provenance tracking
- May evolve as interpretations improve

**Examples:**
- EN 16931 invoice model (derived from specification)
- SAF-T expressed as OWL/SKOS
- ISO 20022 concepts from message schemas
- Industry standards without official RDF publication

**Usage:** Hub-curated models; explicit provenance and disclaimers required.

---

## Provenance Guidelines

All ontologies should include clear metadata:

- **Authoritative:** Use `dcterms:publisher`, `dcterms:source`
- **Derived:** Use `prov:wasDerivedFrom`, `dcterms:creator`, include disclaimer in `skos:note`

---

## File Naming

- Use clear version indicators in filenames
- Store original source documentation alongside RDF files
- Maintain CHANGELOG for derived ontologies
