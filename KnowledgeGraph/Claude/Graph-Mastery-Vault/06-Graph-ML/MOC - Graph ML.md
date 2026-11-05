---
tags: [moc]
phase: 3
---
# MOC — Phase 3: Graph Machine Learning

> [!abstract] Goal
> Understand graph representation learning from shallow embeddings to graph foundation models — theory (expressivity, over-squashing) **and** practice (PyG, PyKEEN, scaling).

## Notes (order)
1. [[Node Embeddings]]
2. [[KG Embeddings]]
3. [[Message Passing and GNNs]]
4. [[GNN Expressivity and WL]]
5. [[Oversmoothing and Oversquashing]]
6. [[Graph Transformers]]
7. [[Scalable GNN Training]]
8. [[Temporal Graph Learning]]
9. [[GNN Explainability]]
10. [[Graph Foundation Models]]

## Core course
**Stanford CS224W** (Leskovec) — do every Colab. Lectures on YouTube; site: web.stanford.edu/class/cs224w

## Reading
- Hamilton, *Graph Representation Learning* (free PDF) — read cover to cover
- Bronstein et al., *Geometric Deep Learning* (arXiv 2104.13478)
- Wu et al. (eds.), *Graph Neural Networks: Foundations, Frontiers, and Applications*
- Marzullo et al., *Graph Machine Learning* 2nd ed. (Packt 2025)

## Milestones
- [ ] Reproduce GCN, GraphSAGE, GAT, GIN on `ogbn-arxiv` vs MLP + label propagation baselines
- [ ] 2–3 page derivation: GCN from spectral filtering + WL bound
- [ ] [[P05 KG Embedding Study]], [[P04 Fraud Graph Analytics]]
