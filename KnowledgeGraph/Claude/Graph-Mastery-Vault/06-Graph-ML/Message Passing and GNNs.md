---
tags: [graph-ml, gnn]
phase: 3
status: not-started
---
# Message Passing & Core GNNs

> [!summary]
> A GNN layer updates each node from its own state and an **aggregation of neighbour messages**. Stacking $K$ layers gives a $K$-hop receptive field. Parameters are shared → inductive, uses features.

## General MPNN
$$h_v^{(k)} = \mathrm{UPDATE}^{(k)}\Big(h_v^{(k-1)},\ \bigoplus_{u\in N(v)} \mathrm{MSG}^{(k)}(h_u^{(k-1)}, h_v^{(k-1)}, e_{uv})\Big)$$
$\bigoplus$ must be **permutation invariant** (sum, mean, max, attention).

## Canonical layers
| Model | Update rule |
|---|---|
| **GCN** (Kipf & Welling 2017) | $H' = \sigma(\hat A H W)$, $\hat A = \tilde D^{-1/2}(A+I)\tilde D^{-1/2}$ |
| **GraphSAGE** (2017) | $h_v' = \sigma\big(W[h_v \,\|\, \mathrm{AGG}(\{h_u\})]\big)$ + neighbour sampling → inductive |
| **GAT** (2018) | $\alpha_{vu} = \mathrm{softmax}_u(\mathrm{LeakyReLU}(a^\top[Wh_v\|Wh_u]))$, $h_v' = \sigma(\sum_u \alpha_{vu}Wh_u)$ (GATv2 fixes static attention) |
| **GIN** (2019) | $h_v' = \mathrm{MLP}\big((1+\epsilon)h_v + \sum_u h_u\big)$ — maximally expressive MPNN |
| R-GCN | Relation-specific weights $W_r$ (+ basis decomposition) for KGs |
| HGT / HAN | Heterogeneous graphs (type-aware attention) |

## Tasks & heads
- **Node** classification/regression → per-node head
- **Link** prediction → decoder on $(h_u, h_v)$
- **Graph** classification → **readout** (sum/mean/attention pooling, DiffPool, SAGPool)

## PyG example
```python
import torch, torch.nn.functional as F
from torch_geometric.datasets import Planetoid
from torch_geometric.nn import GCNConv
data = Planetoid(root="data", name="Cora")[0]

class GCN(torch.nn.Module):
    def __init__(self, i, h, o):
        super().__init__(); self.c1 = GCNConv(i, h); self.c2 = GCNConv(h, o)
    def forward(self, x, ei):
        x = F.dropout(F.relu(self.c1(x, ei)), p=0.5, training=self.training)
        return self.c2(x, ei)

model = GCN(data.num_features, 64, 7)
opt = torch.optim.Adam(model.parameters(), lr=0.01, weight_decay=5e-4)
for epoch in range(200):
    model.train(); opt.zero_grad()
    loss = F.cross_entropy(model(data.x, data.edge_index)[data.train_mask], data.y[data.train_mask])
    loss.backward(); opt.step()
```

## Honest baselines (always run)
MLP on features · label propagation · Correct & Smooth (C&S) · SIGN. They often come close to GNNs.

## My notes


## Self-test #flashcards/graph-ml
Why must GNN aggregation be permutation invariant?::Neighbours have no canonical order; output must not depend on ordering.
GCN propagation rule?::H' = σ(D̃^-1/2 (A+I) D̃^-1/2 H W)
What makes GraphSAGE inductive?::It learns aggregator functions (shared weights) with neighbour sampling, so it can embed unseen nodes.
GIN update rule?::h' = MLP((1+ε)·h_v + Σ_u h_u)
What does R-GCN add?::Relation-type-specific weight matrices for multi-relational graphs.
Name two simple baselines that often rival GNNs.::Label propagation / Correct & Smooth and an MLP on node features.
