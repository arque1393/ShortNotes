---
tags: [graph-ml, gfm, research]
phase: 3
status: not-started
---
# Graph Foundation Models (GFMs)

> [!summary]
> Models pre-trained on broad graph data that **transfer to new graphs and tasks** with little or no training. The hottest graph-ML research area in 2025–2026; KG reasoning has the most convincing results so far.

## Why it's hard
1. **No shared vocabulary:** node features differ in meaning/dimension across graphs; relation types differ across KGs.
2. **Structural diversity:** social vs molecular vs road networks; homophily vs heterophily.
3. **Task diversity:** node, link, graph-level.

## Approaches
| Approach | Examples | Idea |
|---|---|---|
| Graph-native, relation-agnostic | **ULTRA** (ICLR 2024), UltraQuery | Learn over a "graph of relations" + NBFNet → zero-shot on unseen KGs (<200k params, 57 KGs) |
| Feature-agnostic node classification | GraphAny | Combine LinearGNN predictions with learned attention |
| Text-unified | OFA (One-for-All), text-attributed graphs | Describe nodes/edges in natural language → shared LM embedding space |
| LLM as predictor | GraphGPT, LLaGA, InstructGLM | Graph tokens/descriptions into an LLM |
| In-context graph learning | PRODIGY | Prompt graphs with examples |
| Relational DB foundation models | Relational Transformer, RelBench | Tables as temporal heterogeneous graphs |

## Surveys
- Wang et al., "Graph Foundation Models: A Comprehensive Survey" (arXiv 2505.15116)
- Liu et al., "Graph Foundation Models: Concepts, Opportunities and Challenges" (IEEE TPAMI 2025)
- Position: "Graph Foundation Models Are Already Here" (ICML 2024)

## Open questions → [[Open Problems]]
Scaling laws for graphs? What is a graph "token"? GNN vs LLM backbone? Benchmarks that test true transfer?

## My notes


## Self-test #flashcards/graph-ml
Biggest obstacle to graph foundation models?::No shared feature/relation vocabulary across graphs (plus structural and task diversity).
How does ULTRA generalise to unseen KGs?::It builds a graph of relations and learns relative relation representations, so it doesn't need KG-specific embeddings.
What does OFA (One-for-All) use to unify graphs?::Natural-language descriptions of nodes/edges embedded by a language model.
