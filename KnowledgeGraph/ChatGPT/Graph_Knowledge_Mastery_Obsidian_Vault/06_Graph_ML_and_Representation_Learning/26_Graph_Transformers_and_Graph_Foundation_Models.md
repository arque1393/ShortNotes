---
title: "Graph Transformers and Graph Foundation Models"
type: chapter
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - graph-transformer
  - graph-foundation-model
  - pretraining
  - emerging-research
---
# Graph Transformers and Graph Foundation Models

> [!goal]
> Understand how attention is adapted to graphs, what cross-graph pretraining must solve, and why graph foundation models remain an emerging research program rather than a settled recipe.

## 1. Why transformers for graphs?

Local message passing has limited receptive fields and can over-squash distant information. Global attention can connect any pair of nodes, but a graph has no natural token order and full attention costs $O(n^2)$.

A graph transformer must encode:

- node/edge types and features;
- adjacency/local structure;
- relative position or distance;
- graph-level identity;
- permutation equivariance/invariance;
- scalability.

## 2. Structural and positional encodings

Common encodings:

- shortest-path distance;
- edge/path features;
- Laplacian eigenvectors/eigenvalues;
- random-walk structural encodings;
- centrality/degree;
- anchor distances;
- subgraph/motif encodings;
- relation/type embeddings.

Laplacian eigenvectors have sign and basis ambiguity, especially with repeated eigenvalues. Encodings can leak graph size/domain or be expensive to compute.

## 3. Architecture families

### Full global attention

Every node attends to every other node with structural biases. Expressive but quadratic.

### Local-plus-global hybrids

GPS-style architectures combine message passing with global transformer blocks. Local edges encode inductive bias; global attention carries long-range information.

### Sparse/linear attention

Use selected tokens, landmarks, neighborhoods or kernel approximations. Scalability improves, but structural coverage and approximation error must be tested.

### Sequence serialization

Convert walks, paths, trees or graph tokens into sequences processed by a transformer. Ordering/serialization can introduce bias; multiple randomizations or equivariant designs may help.

## 4. Pretraining objectives

- masked node/edge/attribute prediction;
- contrastive graph/subgraph learning;
- context prediction;
- link/relation prediction;
- denoising/reconstruction;
- graph-to-text and text-to-graph alignment;
- generative graph modeling;
- multi-task supervised pretraining.

Pretraining succeeds only if the task and domain share transferable structure. An easy proxy loss can learn graph IDs or degree shortcuts.

## 5. What makes a graph foundation model?

A useful definition requires broad transfer across tasks, graphs or domains with efficient adaptation. Claimed scopes differ:

- domain-specific: many molecular or recommendation tasks;
- task-general within a graph family;
- cross-domain graph transfer;
- KG foundation models transferring to new entities and relations;
- graph-language multimodal models.

Always ask: **what is new at test time?** New nodes, labels, graphs, relation vocabularies, domains or tasks are progressively harder.

## 6. Core research obstacles

### Structural alignment

Graphs have no shared node vocabulary or ordering. Two domains can have different schemas and meanings even if topology looks similar.

### Heterogeneity

Feature spaces, relation types and labels differ. A universal tokenizer for graphs is unsolved.

### Negative transfer

Pretraining on structurally dominant domains can hurt specialized domains.

### Scale

Huge graphs require sampling, partitioning and compressed attention; pretraining cost and carbon/resource reporting matter.

### Evaluation

Benchmarks may not test true transfer. Fine-tuning on most target data is not zero-shot generalization.

### Semantics

Structural equivalence can confuse relations with different meanings. Text/ontology grounding can help but introduces language-model biases.

## 7. Knowledge-graph foundation models

KGFMs seek transfer to unseen entities and, more challengingly, unseen relations/KGs. Approaches use:

- relation-equivariant message passing;
- structural tokens and subgraphs;
- random-walk sequence models;
- textual relation/entity descriptions;
- meta-learning and in-context examples.

Flock, accepted at ICLR 2026, uses sampled random walks and probabilistic node-relation equivariance for zero-shot KG link prediction. It is a notable current result, not proof that one KGFM generalizes across all semantic domains.

## 8. Graph-language models

Patterns include:

- LLM generates/reads graph serializations;
- GNN encodes graph and projects into LLM tokens;
- LLM text embeddings initialize graph models;
- joint contrastive alignment;
- LLM acts as planner while graph tools execute;
- graph structure augments retrieval and memory.

Compare against text-only, graph-only and simple late-fusion baselines. Many gains come from richer text or retrieval rather than graph reasoning.

## 9. Evaluation protocol

A credible GFM study reports:

- pretraining graphs and licenses;
- overlap/near-duplicate analysis with targets;
- exact zero/few/full-shot setting;
- unseen node/relation/domain/task definition;
- adaptation parameter count and compute;
- task-specific strong baselines;
- scaling curves and uncertainty;
- negative transfer cases;
- robustness to node permutation/schema renaming;
- cost, latency and memory.

## 10. Research directions

- schema/ontology-aware graph tokenization;
- universal relational positional encodings;
- cross-domain transfer theory;
- continual graph pretraining without forgetting;
- uncertainty and abstention;
- explainable and rule-compatible GFMs;
- privacy-preserving pretraining;
- benchmark suites for genuine graph transfer;
- combining graph simulators, causal structure and language.

## 11. Laboratory

Choose three graph domains with different schemas. Pretrain a modest graph encoder on two and adapt to the third. Compare:

- from-scratch task model;
- pretrained GNN/transformer;
- text-only encoder;
- simple structural features;
- graph-language fusion.

Evaluate few-shot curves, permutation robustness and negative transfer. Do not call it a foundation model unless transfer scope is explicit.

## Mastery checklist

- [ ] I understand positional/structural encoding assumptions.
- [ ] I can distinguish local, global and serialized architectures.
- [ ] I define the exact generalization axis.
- [ ] I test data overlap and negative transfer.
- [ ] I treat GFM claims as emerging evidence, not settled capability.

## Sources and next reading

- [GraphGPS](https://arxiv.org/abs/2205.12454)
- [Graphormer](https://arxiv.org/abs/2106.05234)
- [Graph Foundation Models: A Comprehensive Survey (2025)](https://arxiv.org/abs/2505.15116)
- [Flock, ICLR 2026](https://proceedings.iclr.cc/paper_files/paper/2026/hash/3ddbd473456a57e3cafb1ee51ddf8ff6-Abstract-Conference.html)
- [[29_Knowledge_Graph_and_LLM_Integration]]
