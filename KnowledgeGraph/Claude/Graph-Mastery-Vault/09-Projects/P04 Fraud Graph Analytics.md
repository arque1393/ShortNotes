---
tags: [project]
phase: 3
status: not-started
---
# P04 — Fraud / AML Graph Analytics

**Goal:** Show the value ladder: rules → graph features → embeddings → GNN.

**Data:** Elliptic (Bitcoin), IBM AML synthetic transactions, or PaySim.
**Stack:** Neo4j GDS, PyG, (optional) cuGraph, Streamlit/Bloom for an investigator UI.

## Steps
- [ ] Baseline: tabular model (XGBoost) on transaction features
- [ ] Add graph features: degree, PageRank, betweenness, WCC size, Louvain/Leiden community, triangle count
- [ ] Add node2vec / FastRP embeddings
- [ ] Train GraphSAGE / GAT; handle **class imbalance** and **heterophily**
- [ ] Temporal split (train past → test future)
- [ ] Metrics: PR-AUC, recall@k (investigation budget)
- [ ] Explain flagged cases with GNNExplainer + community visualisation
- [ ] Simple investigation UI

**Done when:** ablation table shows the marginal value of each graph layer.
Concepts: [[Centrality Measures]] · [[Community Detection]] · [[Message Passing and GNNs]] · [[Oversmoothing and Oversquashing]] · [[GNN Explainability]]
