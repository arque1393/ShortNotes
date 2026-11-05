---
tags: [project]
phase: 5
status: not-started
---
# P09 — Biomedical Drug-Repurposing KG

**Goal:** Predict drug–disease links on a biomedical KG and explain them with paths.

**Data:** PrimeKG or Hetionet.
**Stack:** PyG (R-GCN/HGT), PyKEEN, NBFNet/ULTRA, LLM for path explanation.

## Steps
- [ ] Explore schema (node/edge types), degree distributions
- [ ] **Leakage-safe split** (e.g., hold out diseases entirely)
- [ ] Models: KGE (RotatE/ComplEx), R-GCN/HGT, NBFNet, ULTRA zero-shot
- [ ] Metrics: MRR, Hits@k on held-out indications
- [ ] Path explanations (top paths drug → disease); LLM verbalisation with citations to KG edges
- [ ] Literature sanity-check top 10 novel predictions

**Done when:** rigorous split + explanations; discuss limitations honestly (no clinical claims).
Concepts: [[KG Embeddings]] · [[Message Passing and GNNs]] · [[GNN Explainability]]
