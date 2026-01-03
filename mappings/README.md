# SKOS Mappings

This directory contains SKOS (Simple Knowledge Organization System) mapping files for aligning the Kairos ontology with external industry standards like Schema.org and FIBO.

## Purpose

SKOS mappings enable:
- **Synonym Management**: Alternative labels for concepts (e.g., "Client", "Buyer" for "Customer")
- **Cross-Ontology Alignment**: Linking Kairos concepts to industry standards
- **Semantic Interoperability**: Consistent terminology across platforms
- **Search Enhancement**: Improving discoverability through alternative terms

## Files

- `schema-org.ttl` - Mappings to Schema.org vocabulary (e-commerce, general web)
- `fibo.ttl` - Mappings to Financial Industry Business Ontology (planned)

## SKOS Mapping Types

### Exact Match (`skos:exactMatch`)
**Use when:** Concepts are semantically identical with the same scope
```turtle
:CustomerConcept skos:exactMatch schema:Customer .
```
**Example:** Kairos `Customer` = Schema.org `Customer` (both represent buyers in commerce)

### Close Match (`skos:closeMatch`)
**Use when:** Concepts are similar but not identical; slight differences in scope or definition
```turtle
:CustomerConcept skos:closeMatch schema:Person, schema:Organization .
```
**Example:** Kairos `Customer` is close to Schema.org `Person`/`Organization` but more specific to commerce context

### Broader/Narrower (`skos:broader`, `skos:narrower`)
**Use when:** Establishing hierarchical relationships
```turtle
:ProductConcept skos:broader schema:Thing ;
                skos:narrower :PhysicalProductConcept, :DigitalProductConcept .
```
**Example:** `Product` is narrower than generic `Thing`, broader than `PhysicalProduct`

### Related (`skos:related`)
**Use when:** Concepts are associated but not hierarchically or equivalently
```turtle
:OrderConcept skos:related schema:Invoice, schema:Receipt .
```
**Example:** Orders are related to Invoices and Receipts but distinct concepts

## Best Practices

### 1. Preferred vs. Alternative Labels
```turtle
:CustomerConcept a skos:Concept ;
    skos:prefLabel "Customer"@en ;  # Official term
    skos:altLabel "Client"@en, "Buyer"@en, "Patron"@en .  # Synonyms
```
- **Use `prefLabel`** for the canonical term used in documentation
- **Use `altLabel`** for synonyms, industry jargon, regional variations

### 2. Language Tags
```turtle
skos:prefLabel "Customer"@en, "Client"@fr, "Kunde"@de .
```
- Always include language tags (`@en`, `@fr`, etc.)
- Supports multi-language systems (future scope)

### 3. Definitions and Notes
```turtle
:SupplierConcept a skos:Concept ;
    skos:definition "An organization that provides products or services."@en ;
    skos:note "Schema.org lacks a Supplier class; use Organization with role='supplier'."@en .
```
- **`definition`**: Formal, concise explanation of the concept
- **`note`**: Implementation guidance, context-specific advice

### 4. Examples
```turtle
:OrderConcept skos:example "Online shopping cart checkout, B2B purchase requisition."@en .
```
- Provide concrete use cases to clarify concept scope

## Validation

SKOS files are validated as part of the standard ontology pipeline:
```bash
python scripts/validate.py --ontology ontology-hub/mappings/schema-org.ttl
```

Validation checks:
- Turtle syntax correctness
- SKOS vocabulary usage
- Referenced URIs resolvable (future enhancement)

## Usage in Projections

SKOS mappings are used during artifact generation to:
1. **Azure AI Search**: Include altLabels as searchable synonyms
2. **Prompt Context**: Provide alternative terms for LLM context
3. **A2UI Protocol**: Map Kairos terms to consumer-facing labels
4. **Documentation**: Generate glossaries with synonyms

## Adding New Mappings

1. Create/edit `.ttl` file in this directory
2. Define SKOS concepts with appropriate mapping properties
3. Run validation: `python scripts/validate.py --all`
4. Commit to feature branch and create PR

## References

- [SKOS Specification](https://www.w3.org/TR/skos-reference/)
- [Schema.org Vocabulary](https://schema.org/)
- [FIBO Ontology](https://spec.edmcouncil.org/fibo/)

