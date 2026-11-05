---
tags: [data-models]
phase: 1
status: not-started
---
# Property Graph vs RDF

> [!summary]
> Not a war — two tools. LPG is optimised for **traversal and app development**; RDF for **global identity, semantics, integration and reasoning**.

| Dimension | RDF / Semantic Web | Labelled Property Graph |
|---|---|---|
| Unit | Triple (+ named graph) | Node / relationship with properties |
| Identity | Global IRIs | Local internal IDs |
| Edge properties | Reification, named graphs, RDF 1.2 triple terms | Native |
| Schema | RDFS/OWL (inference), SHACL (validation) | Constraints/indexes; PG-Schema emerging |
| Semantics | Formal model theory | Mostly operational |
| Query | SPARQL (W3C) | Cypher/openCypher, **GQL (ISO)**, Gremlin |
| Reasoning | Built in (RDFS, OWL RL, rules) | Usually application-level |
| Interop | Linked data, standards everywhere | Vendor-specific import/export |
| Sweet spot | Data integration, publishing, life sciences, government, ontologies | Fraud, recommendations, network ops, GraphRAG apps |

## Bridges
- **Neo4j neosemantics (n10s):** import/export RDF, use ontologies and SHACL on Neo4j.
- **Amazon Neptune:** supports both models in one service.
- Many teams model with an **ontology** (OWL/SKOS) and **store** as LPG for applications.

> [!tip] Interview answer
> "I choose based on whether the main problem is *meaning and integration* (RDF) or *connected-data computation and apps* (LPG) — and I can map between them."

## My notes


## Self-test #flashcards/data-models
Main identity difference between RDF and LPG?::RDF uses global IRIs; LPG uses local database IDs.
How does RDF handle edge properties?::Via reification, named graphs, or RDF 1.2 triple terms (RDF-star).
Neo4j plugin for RDF/ontology interop?::neosemantics (n10s).
