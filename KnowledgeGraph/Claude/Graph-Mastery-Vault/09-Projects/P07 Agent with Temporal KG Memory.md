---
tags: [project]
phase: 4
status: not-started
---
# P07 — Agent with Temporal KG Memory (over MCP)

**Goal:** A conversational agent whose long-term memory is a bi-temporal KG, exposed via MCP with safe writes.

**Stack:** Graphiti or Mem0 (graph mode) on Neo4j/FalkorDB, LangGraph, MCP SDK.

## Steps
- [ ] Memory schema: episodes, entities, facts with `valid_from/valid_to`, `created_at/expired_at`
- [ ] Ingest conversations → extract facts → resolve entities → invalidate contradictions
- [ ] Retrieval: hybrid (semantic + BM25 + graph expansion) with time filter ("as of")
- [ ] MCP server: `get_schema`, `search_memory`, `read_query` (read-only), `add_fact` (approval-gated)
- [ ] Evaluate on LongMemEval / LOCOMO subsets + your own knowledge-update tests
- [ ] Compare: no memory vs vector memory vs graph memory

**Done when:** demo + metrics showing correct handling of updated facts.
Concepts: [[Agent Memory as Knowledge Graphs]] · [[MCP and Graph Tools]] · [[Entity Resolution]]
