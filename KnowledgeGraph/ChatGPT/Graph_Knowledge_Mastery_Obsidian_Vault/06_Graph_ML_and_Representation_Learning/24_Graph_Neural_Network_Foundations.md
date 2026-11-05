---
title: "Graph Neural Network Foundations"
type: chapter
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - gnn
  - message-passing
  - graphsage
  - gcn
  - gat
---
# Graph Neural Network Foundations

> [!goal]
> Derive message passing, understand its expressive and optimization limits, and implement leakage-safe node, edge and graph prediction.

## 1. Relational inductive bias

A GNN assumes a node's representation can be computed from its features and structured neighborhood using permutation-equivariant operations. For graph-level output, pooling should be permutation invariant.

A general message-passing layer is:

$$m_v^{(k)}=\text{AGG}^{(k)}\{\psi^{(k)}(h_v^{(k-1)},h_u^{(k-1)},e_{uv}) : u\in\mathcal{N}(v)\},$$

$$h_v^{(k)}=\phi^{(k)}(h_v^{(k-1)},m_v^{(k)}).$$

After $K$ layers, a node normally sees a $K$-hop receptive field.

## 2. GCN

A common GCN layer is

$$H^{(k+1)}=\sigma(\tilde{D}^{-1/2}\tilde{A}\tilde{D}^{-1/2}H^{(k)}W^{(k)}),$$

where $\tilde{A}=A+I$. It performs normalized neighbor smoothing followed by a linear transformation.

Strength: simple and effective under homophily. Limit: transductive full-batch origin, over-smoothing and poor fit for some heterophilous/typed graphs.

## 3. GraphSAGE

GraphSAGE samples and aggregates neighbors, enabling inductive inference from features:

$$h_v^{(k)}=\sigma(W^{(k)}[h_v^{(k-1)}\|\text{AGG}(\{h_u^{(k-1)}\})]).$$

Mean, pool and LSTM-style aggregators exist. Sampling controls scale but introduces variance and can miss rare important neighbors.

## 4. GAT

Graph Attention Networks learn neighbor weights:

$$\alpha_{vu}=\text{softmax}_{u\in\mathcal{N}(v)}(a(Wh_v,Wh_u)).$$

Attention improves adaptivity but is not automatically an explanation. Coefficients can be unstable or weakly related to causal importance.

## 5. GIN and expressivity

Graph Isomorphism Networks use sum aggregation and MLPs, matching the distinguishing power of the 1-dimensional Weisfeiler-Lehman test under conditions:

$$h_v^{(k)}=\text{MLP}^{(k)}((1+\epsilon)h_v^{(k-1)}+\sum_{u\in\mathcal{N}(v)}h_u^{(k-1)}).$$

Standard message-passing GNNs cannot distinguish some non-isomorphic graphs. Positional encodings, higher-order methods, subgraph GNNs and transformers can increase expressivity at computational cost.

## 6. Tasks

### Node prediction

Encode nodes, then classify/regress each target. Use temporal/grouped splits and separate transductive from inductive performance.

### Link prediction

Encode endpoint nodes and score with dot product, MLP or relation-specific decoder. Remove target edges from message passing where necessary and use realistic negatives.

### Graph prediction

Pool node representations using sum/mean/max, attention or hierarchical pooling, then predict graph properties. Splits should reflect scaffold/domain/time rather than random near-duplicate graphs.

## 7. Failure modes

### Over-smoothing

Repeated aggregation makes node representations too similar. Mitigate with residual/initial connections, normalization, decoupled propagation or limited depth.

### Over-squashing

Exponentially growing distant information is compressed into fixed-size vectors. Curvature/bottleneck structure, rewiring, positional encodings and global attention may help.

### Neighborhood explosion

Sampling $s$ neighbors over $K$ layers can approach $s^K$. Use layer-wise sampling, subgraph sampling, clustering or precomputation.

### Heterophily

Neighbors may have different labels/roles. Use architectures preserving self/neighbor channels, signed/high-order information, relation types or nonlocal similarity.

### Oversensitivity and shortcut learning

Models may exploit degree, duplicate features, target leakage or dataset artifacts. Include degree-only and feature-only baselines and perturbation tests.

## 8. PyTorch Geometric example

```python
import torch
from torch_geometric.nn import SAGEConv

class GraphSAGE(torch.nn.Module):
    def __init__(self, in_dim: int, hidden: int, out_dim: int):
        super().__init__()
        self.conv1 = SAGEConv(in_dim, hidden)
        self.conv2 = SAGEConv(hidden, out_dim)

    def forward(self, x, edge_index):
        x = self.conv1(x, edge_index).relu()
        x = torch.nn.functional.dropout(x, p=0.3, training=self.training)
        return self.conv2(x, edge_index)
```

A usable training system also needs split masks, neighbor loaders for scale, metrics, checkpointing, reproducibility and leakage controls.

## 9. Scaling strategies

- neighbor sampling: GraphSAGE-style mini-batches;
- layer-wise sampling: sample nodes per layer;
- cluster/subgraph batching: Cluster-GCN, GraphSAINT-like ideas;
- feature/embedding caching;
- precomputed propagation: decouple diffusion and MLP;
- distributed partitioning;
- mixed precision and compiled kernels;
- sparse matrix operations.

Benchmark accuracy and systems behavior together. Sampling changes the statistical estimator.

## 10. Interpretability

Methods include gradient/feature attribution, mask optimization, subgraph extraction and counterfactual edge/feature changes. Evaluate explanations for faithfulness, stability, sparsity and domain validity. Avoid displaying an attractive neighborhood without testing whether it drives the prediction.

## 11. Experimental protocol

- graph and feature construction documented;
- point-in-time or grouped split;
- feature-only, graph-only and simple graph-feature baselines;
- hyperparameter budget equalized;
- multiple seeds;
- accuracy plus calibration and system metrics;
- ablate edges, features, relation types and depth;
- inspect performance by degree/component/subgroup;
- test unseen nodes where deployment requires it.

## 12. Laboratory

Implement GCN, GraphSAGE, GAT and GIN on one OGB task. Compare against an MLP and label/structural baselines. Test:

- feature-only and topology-only;
- depth 1-8 for smoothing;
- neighbor-sampling sensitivity;
- degree-stratified accuracy;
- edge perturbation;
- runtime/memory.

Write a failure analysis, not only a leaderboard table.

## Mastery checklist

- [ ] I can derive message passing and normalization.
- [ ] I understand 1-WL-level limits.
- [ ] I diagnose smoothing, squashing, explosion and heterophily.
- [ ] Splits and message-passing edges avoid leakage.
- [ ] I compare against feature-only and simple graph baselines.

## Sources and next reading

- William Hamilton, *Graph Representation Learning* ([free author PDF](https://www.cs.mcgill.ca/~wlh/grl_book/))
- [Stanford CS224W](https://web.stanford.edu/class/cs224w/)
- [PyTorch Geometric documentation](https://pytorch-geometric.readthedocs.io/)
- [DGL documentation](https://www.dgl.ai/)
- [[25_Relational_Heterogeneous_and_Temporal_GNNs]]
