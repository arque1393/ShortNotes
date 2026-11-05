---
tags: [llm-kg, agents, memory]
phase: 4
status: not-started
---
# Agent Memory as Knowledge Graphs

> [!summary]
> Long-running agents need memory that **accumulates, updates and resolves contradictions** over time. A **temporal KG** stores entities, facts with validity intervals, and links back to the episodes they came from.

## Memory types (cognitive analogy)
- **Working** — context window
- **Episodic** — what happened (conversation turns, events)
- **Semantic** — distilled facts (user prefers X; Alice works at Acme)
- **Procedural** — how to do things (skills, tools)

## Why graphs?
Entity-centric retrieval, multi-hop recall ("my manager's project deadline"), explicit contradiction handling, provenance, time.

## Bi-temporal modelling
Each fact edge carries:
- `valid_from` / `valid_to` — when true **in the world**
- `created_at` / `expired_at` — when the system **learned/invalidated** it
New contradicting fact ⇒ **invalidate** old edge (set `valid_to`), don't delete → history queries work.

## Systems
| System | Highlights |
|---|---|
| **Graphiti / Zep** (arXiv 2501.13956) | Episode, semantic-entity and community subgraphs; bi-temporal edges; hybrid semantic + BM25 + graph search. Reports 94.8% vs 93.4% (MemGPT) on DMR, up to 18.5% accuracy gain + 90% lower latency on LongMemEval (self-reported) |
| **Mem0 / Mem0g** (arXiv 2504.19413) | Extract → update (ADD/UPDATE/DELETE/NOOP); graph variant on Neo4j with conflict invalidation; ~2% over base Mem0 on LOCOMO (self-reported, 10 conversations) |
| Cognee | ECL pipelines (extract, cognify, load) into graph + vectors |
| mcp-neo4j-memory | Simple KG memory exposed as MCP tools |
| Letta (MemGPT) | Tiered memory, non-graph contrast |

## Benchmarks
LOCOMO, LongMemEval, DMR — all small/young; statistical soundness is debated → research opportunity.

## Design checklist
- [ ] Entity resolution across sessions
- [ ] Contradiction detection & invalidation policy
- [ ] Time-aware retrieval ("as of" queries)
- [ ] Forgetting / user deletion (privacy, GDPR)
- [ ] Provenance to source episode

## My notes


## Self-test #flashcards/llm-kg
What are the two time dimensions in bi-temporal memory?::Valid time (when true in the world) and transaction time (when recorded/invalidated in the system).
How does Graphiti handle a contradicting new fact?::It invalidates the old edge by setting its validity end time instead of deleting it.
Name three agent-memory benchmarks.::LOCOMO, LongMemEval, DMR.
Four memory types in agents?::Working, episodic, semantic, procedural.
