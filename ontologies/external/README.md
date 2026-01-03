# External Reference Ontologies

This directory contains external ontologies imported by Kairos ontologies.

## Structure

### Authoritative-Ontologies/
Official reference ontologies from industry standards bodies:

- **FIBO/** - Financial Industry Business Ontology (FIBO Q3 2025)
  - 300+ ontology files from EDM Council
  - Covers: Foundations, Business Entities, Contracts, Legal, etc.
  - Source: https://spec.edmcouncil.org/fibo/

### Derived-Ontologies/ (Future)
Our RDF interpretations of non-RDF industry standards.

## Import Resolution

The [catalog-v001.xml](../../catalog-v001.xml) file maps FIBO URIs to local files:

`xml
<uri name="https://spec.edmcouncil.org/fibo/ontology/FND/AgentsAndPeople/Agents/"
     uri="ontologies/external/Authoritative-Ontologies/FIBO/..."/>
`

This enables offline development and consistent import resolution.
