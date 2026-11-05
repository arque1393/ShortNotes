---
tags: [data-models, databases, tools]
phase: 1
status: not-started
---
# Graph Databases Landscape (2026)

> [!summary]
> Pick by **data model, scale, workload (OLTP traversal vs OLAP analytics), reasoning needs and governance**. The landscape is volatile — design for portability.

| Engine | Model / language | Notes |
|---|---|---|
| **Neo4j** | LPG / Cypher | Market leader; GDS library, vector index, GenAI tooling, official MCP server |
| Amazon Neptune | LPG + RDF / openCypher, Gremlin, SPARQL | Managed; Neptune Analytics (in-memory algorithms, vectors) |
| TigerGraph | LPG / GSQL | Distributed, deep-link analytics |
| Memgraph | LPG / Cypher | In-memory, streaming |
| FalkorDB | LPG / Cypher | GraphBLAS-based (RedisGraph successor), GraphRAG focus |
| ArangoDB | Multi-model / AQL | Docs + graph |
| Apache AGE | Cypher on PostgreSQL | Graph inside Postgres |
| Google Spanner Graph | GQL | Cloud-scale, GQL early adopter |
| Kùzu | Embedded, Cypher | **Archived Oct 2025**; community forks exist |
| Ontotext GraphDB | RDF / SPARQL | OWL 2 RL reasoning |
| Stardog | RDF / SPARQL | Virtualisation, reasoning, enterprise KG |
| RDFox | RDF / Datalog | Fast incremental materialisation |
| Apache Jena/Fuseki, Oxigraph | RDF | Open source |
| TypeDB | Own type system / TypeQL | Strongly typed, rules |

## Choosing checklist
- [ ] Need standards-based integration & reasoning? → RDF store
- [ ] Need app-centric traversal + rich algorithms? → LPG (Neo4j/Memgraph/TigerGraph)
- [ ] Embedded / local-first agent memory? → evaluate FalkorDB, Kùzu forks, SQLite-based options
- [ ] Analytics only? → in-memory: NetworkX/igraph/cuGraph, Neo4j GDS, Neptune Analytics
- [ ] Licence, governance, managed offering, ecosystem (GraphRAG, MCP)?

## My notes


## Self-test #flashcards/data-models
Which RDF store is known for fast incremental Datalog materialisation?::RDFox
Graph DB that runs Cypher inside PostgreSQL?::Apache AGE
Which Neo4j library provides graph algorithms?::Graph Data Science (GDS).
