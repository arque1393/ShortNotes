---
tags: [project]
phase: 4
status: not-started
---
# P06 — GraphRAG Bake-off

**Goal:** Rigorous, cost-aware comparison of RAG strategies. This is your **portfolio centerpiece**.

**Data:** GraphRAG-Bench (or a subset), MultiHop-RAG, plus your own document set.
**Stack:** microsoft/graphrag, LightRAG, HippoRAG, neo4j-graphrag hybrid retriever, a reranker, RAGAS, Langfuse.

## Systems
- [ ] BM25
- [ ] Dense vector
- [ ] Hybrid + reranker (strong baseline!)
- [ ] Microsoft GraphRAG (local + global)
- [ ] LightRAG
- [ ] HippoRAG 2
- [ ] (optional) LazyGraphRAG-style / your own variant

## Evaluation
- [ ] Same generator LLM and token budget
- [ ] Stratify by question type (fact, multi-hop, summary, temporal)
- [ ] Accuracy/F1, faithfulness, citation accuracy
- [ ] Index cost, query cost, p50/p95 latency
- [ ] Bootstrap CIs; judge calibration on 100 human-labelled answers

**Done when:** a decision guide: "use graph method X when…, otherwise Y".
Concepts: [[GraphRAG Overview]] · [[Microsoft GraphRAG]] · [[LightRAG and HippoRAG]] · [[Evaluating GraphRAG]]
