---
tags: [graph-ml, theory]
phase: 3
status: not-started
---
# Over-smoothing, Over-squashing & Heterophily

> [!summary]
> Deep GNNs fail in two distinct ways: **over-smoothing** (all node embeddings become alike) and **over-squashing** (information from far away gets compressed through bottlenecks). Plus **heterophily**, where neighbours are not similar.

## Over-smoothing
- Repeated averaging ≈ applying a low-pass filter → node states converge to the dominant eigenvector; **Dirichlet energy** $\sum_{(i,j)}\|h_i-h_j\|^2 \to 0$.
- Remedies: residual/skip connections, **Jumping Knowledge**, normalisation (PairNorm), **APPNP** (propagate with personalized PageRank: $Z^{(k+1)} = (1-\alpha)\hat A Z^{(k)} + \alpha H$), DropEdge, decoupling propagation from transformation.

## Over-squashing (Alon & Yahav 2021)
- Receptive field grows exponentially; fixed-size vectors must carry it → long-range dependencies lost.
- Measured via Jacobian sensitivity $\partial h_v^{(K)} / \partial x_u$; linked to **negative Ricci curvature** / bottleneck edges (Topping et al. 2022) and low Cheeger constant ([[Spectral Graph Theory]]).
- Remedies: **graph rewiring** (SDRF, FoSR), virtual/master nodes, fully adjacent last layer, [[Graph Transformers]].
- Benchmark: Long Range Graph Benchmark (LRGB).

## Heterophily
- Homophily ratio $h$ = fraction of edges joining same-label nodes. Low $h$ (e.g., fraud: fraudsters connect to victims) breaks GCN assumptions.
- Remedies: separate ego/neighbour embeddings (H2GCN), signed/learned propagation (GPR-GNN, FAGCN), higher-order neighbourhoods.

## My notes


## Self-test #flashcards/graph-ml
What is over-smoothing?::With depth, node representations converge and become indistinguishable (Dirichlet energy → 0).
What is over-squashing?::Exponentially growing receptive fields compressed into fixed-size vectors through bottlenecks, losing long-range information.
Graph property linked to over-squashing bottlenecks?::Negative (Ricci) curvature / low Cheeger constant.
How does APPNP fight over-smoothing?::It propagates with personalized PageRank, always teleporting back to the node's own features.
Why is heterophily relevant for fraud detection?::Fraudsters connect to dissimilar nodes (victims), violating the homophily assumption of standard GNNs.
