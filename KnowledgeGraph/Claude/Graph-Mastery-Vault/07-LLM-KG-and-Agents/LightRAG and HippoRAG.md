---
tags: [llm-kg, graphrag]
phase: 4
status: not-started
---
# LightRAG & HippoRAG

> [!summary]
> Two lighter index-based GraphRAG designs: **LightRAG** = dual-level keyword retrieval over an entity graph with incremental updates; **HippoRAG** = hippocampus-inspired memory using **Personalized PageRank** over an open-IE KG.

## LightRAG (Guo et al., arXiv 2410.05779)
- Extract entities & relations per chunk → graph + key-value profiles.
- Query → LLM extracts **low-level keywords** (specific entities) and **high-level keywords** (themes).
- Low-level → match entities; high-level → match relations/themes; expand one-hop neighbours.
- **Incremental update:** union new subgraphs without rebuilding communities.

## HippoRAG (NeurIPS 2024) → HippoRAG 2 (ICML 2025, arXiv 2502.14802)
- Offline: open IE triples from passages → KG; add **synonym edges** via embedding similarity.
- Online: query entities → seed nodes → **PPR** over the KG → rank passages by node probabilities ([[Centrality Measures]]).
- HippoRAG 2 adds **passage nodes** in the graph, query-to-triple matching and LLM "recognition memory" filtering. Reports ~7-point average improvement on associativity (multi-hop) tasks vs standard RAG without losing factual-memory performance (self-reported).

## Compare
| | MS GraphRAG | LightRAG | HippoRAG 2 |
|---|---|---|---|
| Graph | Entities + communities | Entities + relations | Open-IE triples + passages + synonyms |
| Core retrieval | Community map-reduce / local | Dual-level keywords | PPR |
| Best at | Global sensemaking | Cheap general use, updates | Multi-hop associative QA |
| Index cost | High | Medium | Medium |

## My notes


## Self-test #flashcards/llm-kg
What graph algorithm is HippoRAG's retrieval engine?::Personalized PageRank seeded with query entities.
What are LightRAG's two keyword levels?::Low-level (specific entities) and high-level (broad themes/relations).
What did HippoRAG 2 add to the graph?::Passage nodes (plus query-to-triple matching and recognition-memory filtering).
