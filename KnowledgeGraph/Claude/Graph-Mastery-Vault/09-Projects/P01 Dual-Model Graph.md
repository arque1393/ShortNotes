---
tags: [project]
phase: 1
status: not-started
---
# P01 — Dual-Model Graph (LPG + RDF)

**Goal:** Model one dataset in both Neo4j and an RDF store; prove fluency in Cypher, SPARQL and graph algorithms.

**Data:** MovieLens, OpenAlex subset, or a Wikidata extract.
**Stack:** Neo4j + GDS, Apache Jena Fuseki or GraphDB Free, NetworkX, Python.

## Steps
- [ ] Design LPG model (diagram) and an RDF/RDFS vocabulary for the same domain
- [ ] Load into Neo4j (`LOAD CSV` / Python driver) with constraints
- [ ] Convert to Turtle and load into Fuseki
- [ ] Write the **same 10 questions** in Cypher and SPARQL (incl. aggregation, optional, variable-length/property paths)
- [ ] Run PageRank, Louvain/Leiden, node similarity in GDS; interpret results
- [ ] Reproduce one algorithm in NetworkX and compare
- [ ] README: modelling decisions, LPG vs RDF reflections ([[Property Graph vs RDF]])

**Done when:** queries return identical answers in both systems; write-up explains trade-offs.
Concepts: [[Property Graphs and Cypher]] · [[RDF and SPARQL]] · [[Centrality Measures]] · [[Community Detection]]
