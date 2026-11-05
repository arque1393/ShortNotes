---
tags: [project]
phase: 2
status: not-started
---
# P03 — Text → KG Pipeline (classic vs LLM)

**Goal:** Build two pipelines from documents to KG and compare them quantitatively.

**Data:** News articles, SEC EDGAR filings, or PubMed abstracts (≈500–2,000 docs).
**Stack:** spaCy / GLiNER, ReFinED or alias-table linking, Splink, LLM with structured outputs, neo4j-graphrag or LangChain, pySHACL.

## Steps
- [ ] Use ontology from [[P02 Domain Ontology]] (or a small schema) as target
- [ ] **Pipeline A (classic):** NER → RE (rules/supervised) → entity linking → ER
- [ ] **Pipeline B (LLM):** ontology-guided structured extraction with evidence spans
- [ ] Shared post-processing: normalisation, ER, SHACL validation, provenance
- [ ] Hand-label **200 triples** as gold sample
- [ ] Report precision, recall, duplicate rate, schema-violation rate, $ and time per 1k docs
- [ ] Error analysis: 20 failure cases per pipeline

**Done when:** a table comparing A vs B with honest error analysis.
Concepts: [[KG Construction Pipeline]] · [[Information Extraction and Entity Linking]] · [[Entity Resolution]] · [[LLM-based KG Construction]]
