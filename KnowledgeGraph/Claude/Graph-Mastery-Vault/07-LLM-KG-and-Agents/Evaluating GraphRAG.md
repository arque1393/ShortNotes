---
tags: [llm-kg, evaluation, research]
phase: 4
status: not-started
---
# Evaluating GraphRAG (your signature skill)

> [!summary]
> Most GraphRAG claims are weakly evaluated (LLM-as-judge on "comprehensiveness", few baselines, no cost). Rigorous evaluation is both a **job skill** and an **open research area**.

## What to measure
| Layer | Metrics |
|---|---|
| KG construction | triple precision (sampled), recall vs gold, duplicates, schema violations |
| Retrieval | evidence recall@k, path correctness, context precision, # tokens |
| Generation | exact match / F1 (factoid), faithfulness/groundedness, citation accuracy, LLM-judge with **calibration against human labels** |
| Cost | index $ and time, query $ and p50/p95 latency, update cost |
| Robustness | noisy/incomplete KG, adversarial docs, temporal drift |

## Protocol checklist
- [ ] Baselines: BM25, dense, **hybrid + reranker**, long-context LLM, RAPTOR
- [ ] Same LLM, same token budget across methods
- [ ] Question types stratified: fact, multi-hop, comparison, summarisation, temporal
- [ ] Multiple seeds / bootstrap 95% CIs; significance tests
- [ ] Judge bias checks (position swap, length bias)
- [ ] Ablations: graph vs no graph, communities vs none, PPR vs BFS
- [ ] Report failures qualitatively

## Benchmarks
GraphRAG-Bench (Xiang et al., ICLR 2026; 4 task levels), MultiHop-RAG, HotpotQA, 2WikiMultiHopQA, MuSiQue; memory: LOCOMO, LongMemEval. Systematic comparisons: arXiv 2502.11371, 2503.04338.

## Tools
RAGAS, DeepEval, TruLens, Langfuse/Phoenix tracing.

## My notes


## Self-test #flashcards/llm-kg
Strongest non-graph baseline to include?::Hybrid (BM25 + dense) retrieval with a reranker under the same LLM and token budget.
Why calibrate LLM-as-judge?::Judges have position/length/self-preference biases; agreement with human labels must be checked.
Four cost metrics to report for GraphRAG?::Indexing cost/time, query cost, latency (p50/p95), update cost.
