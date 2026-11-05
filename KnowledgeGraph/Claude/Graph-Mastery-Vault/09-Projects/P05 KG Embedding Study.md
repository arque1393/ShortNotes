---
tags: [project]
phase: 3
status: not-started
---
# P05 — KG Embedding Study

**Goal:** Reproduce and compare KGE models; test zero-shot transfer with ULTRA on your own KG.

**Data:** FB15k-237, WN18RR, CoDEx; plus your KG from P03.
**Stack:** PyKEEN, ULTRA repo.

## Steps
- [ ] Train TransE, DistMult, ComplEx, RotatE, TuckER with PyKEEN (filtered MRR, Hits@1/3/10)
- [ ] Hyper-parameter sensitivity on one model (shows why tuning matters)
- [ ] Relation-pattern analysis: per-relation MRR for symmetric vs antisymmetric vs compositional relations
- [ ] Run **ULTRA** zero-shot on CoDEx and on your own KG; compare with trained models
- [ ] Inspect predicted missing links on your KG — manually verify top 50

**Done when:** report linking theory (relation patterns) to observed results.
Concepts: [[KG Embeddings]] · [[Graph Foundation Models]] · [[KG Quality and Refinement]]
