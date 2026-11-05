---
tags: [llm-kg, reasoning, kgqa]
phase: 4
status: not-started
---
# Reasoning on Graphs: ToG, RoG, GNN-RAG, SubgraphRAG

> [!summary]
> Instead of retrieving once, let the LLM (or a GNN) **navigate** the KG: explore paths, prune, and reason step by step with traceable evidence.

| Method | Mechanism | Training? |
|---|---|---|
| **Think-on-Graph (ToG)** (arXiv 2307.07697) | LLM as agent doing **beam search** over KG relations/entities, deciding when enough evidence | Training-free |
| **ToG-2** (ICLR 2025) | Alternates KG exploration and document retrieval (KG×text) | Training-free |
| ToG-3 (2025) | Multi-agent, evolving heterogeneous graph index | — |
| **RoG** (ICLR 2024) | **Plan** relation paths with a fine-tuned LLM → retrieve instances → reason | Instruction-tuned planner |
| **GNN-RAG** | GNN retrieves answer candidates + shortest paths → verbalised for LLM | GNN trained |
| **SubgraphRAG** (ICLR 2025) | Lightweight MLP + directional distance encoding scores triples → subgraph for LLM | Light training |
| KG-Agent, StructGPT | Tool-using agents with KG interfaces | Varies |

## Benchmarks (KGQA)
WebQSP, CWQ (ComplexWebQuestions), GrailQA, MetaQA, Mintaka; LC-QuAD 2.0 & QALD for SPARQL.

## Design questions
- Who decides the next hop — LLM (flexible, costly) or GNN/scorer (cheap)?
- How to prune exponential path space? (beam width, relation pruning)
- How to stop? (sufficiency check)
- Faithfulness: does the answer actually follow from the retrieved path?

## My notes


## Self-test #flashcards/llm-kg
How does Think-on-Graph explore the KG?::The LLM performs iterative beam search over relations/entities, pruning and checking sufficiency.
RoG's three steps?::Plan relation paths (fine-tuned LLM), retrieve path instances from the KG, reason over them.
What does ToG-2 add over ToG?::Tight coupling of KG exploration with document (text) retrieval.
Name two KGQA benchmarks.::WebQSP and CWQ (also GrailQA, MetaQA).
