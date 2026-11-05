---
tags: [project]
phase: 4
status: not-started
---
# P08 — Self-correcting Text-to-Cypher / SPARQL Agent

**Goal:** NL questions → validated graph queries → answers, with measured execution accuracy.

**Data:** Neo4j Text2Cypher dataset / your P01 graph; LC-QuAD 2.0 or QALD for SPARQL.

## Steps
- [ ] Compact schema serialiser
- [ ] Exemplar store (few-shot retrieval)
- [ ] Generation → `EXPLAIN` validation → execution → self-correction loop (≤3)
- [ ] Ontology/schema constraint checker (labels, directions, domain/range)
- [ ] Guardrails: read-only, LIMIT, timeout
- [ ] Measure execution accuracy, validity rate, latency; ablate each component

**Done when:** ablation table shows the contribution of schema linking, few-shot and self-correction.
Concepts: [[Text-to-Cypher and Text-to-SPARQL]] · [[Property Graphs and Cypher]] · [[RDF and SPARQL]]
