---
tags: [project]
phase: 2
status: not-started
---
# P02 — Domain Ontology (50–150 classes)

**Goal:** A published, tested OWL 2 ontology for a domain you care about (supply chain, clinical trials, ESG, education…).

## Steps
- [ ] Write 25+ **competency questions**
- [ ] Search for reusable ontologies (LOV, BioPortal, schema.org, OBO)
- [ ] Model in Protégé using ≥3 ODPs (n-ary relation, part-of, time-indexed situation…)
- [ ] Align top classes to **BFO or gUFO**; map key terms to schema.org / Wikidata (`skos:exactMatch`)
- [ ] Add SHACL shapes for instance data
- [ ] Create 30–50 sample instances; run HermiT/ELK — zero unsatisfiable classes
- [ ] Turn CQs into SPARQL tests; all pass
- [ ] Run OOPS! and ROBOT `report`; fix issues
- [ ] Document with WIDOCO; publish on GitHub Pages with a w3id-style IRI

**Done when:** reasoner-consistent, CQ tests pass, docs published.
Concepts: [[Ontology Engineering Methodologies]] · [[OWL 2 and Profiles]] · [[SHACL and ShEx]] · [[Foundational and Domain Ontologies]]
