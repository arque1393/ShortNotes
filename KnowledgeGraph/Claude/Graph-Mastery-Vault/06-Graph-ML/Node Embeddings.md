---
tags: [graph-ml, embeddings]
phase: 3
status: not-started
---
# Shallow Node Embeddings

> [!summary]
> Learn a vector $z_v$ per node so that **similarity in embedding space ≈ similarity in the graph** (co-occurrence on random walks, neighbourhood overlap). Encoder = lookup table.

## Encoder–decoder view (Hamilton)
- Encoder: $\mathrm{ENC}(v) = Z[v]$
- Decoder: $\mathrm{DEC}(z_u, z_v) = z_u^\top z_v$
- Loss: make decoder match a similarity $S[u,v]$ (adjacency, k-hop, random-walk co-occurrence)

## Methods
| Method | Similarity notion | Key idea |
|---|---|---|
| Laplacian eigenmaps | Adjacency | Spectral, $\min \sum A_{uv}\|z_u-z_v\|^2$ |
| **DeepWalk** (2014) | Random-walk co-occurrence | Uniform walks + skip-gram with negative sampling |
| **node2vec** (2016) | Biased walks | Return param $p$, in-out param $q$: BFS-like (structural equivalence) vs DFS-like (homophily) |
| **LINE** (2015) | 1st- and 2nd-order proximity | Scales to large graphs |
| NetMF (2018) | — | Shows DeepWalk/LINE ≈ implicit matrix factorisation |

## Limitations
- **Transductive:** can't embed unseen nodes without retraining
- **No node features** used
- $O(|V|d)$ parameters, no parameter sharing → motivates [[Message Passing and GNNs]]

## Code (PyG)
```python
import torch
from torch_geometric.nn import Node2Vec
model = Node2Vec(data.edge_index, embedding_dim=128, walk_length=20,
                 context_size=10, walks_per_node=10, p=1.0, q=0.5,
                 num_negative_samples=1, sparse=True)
loader = model.loader(batch_size=128, shuffle=True)
opt = torch.optim.SparseAdam(list(model.parameters()), lr=0.01)
for pos_rw, neg_rw in loader:
    opt.zero_grad(); loss = model.loss(pos_rw, neg_rw); loss.backward(); opt.step()
```

## My notes


## Self-test #flashcards/graph-ml
What do node2vec's p and q control?::p = return probability to previous node; q = in-out parameter (low q → DFS-like exploration, high q → BFS-like).
Main limitations of shallow embeddings?::Transductive, ignore node features, no parameter sharing (O(|V|·d) parameters).
What did NetMF show?::DeepWalk/LINE implicitly factorise a specific matrix derived from random-walk co-occurrence.
DeepWalk = random walks + ?::Skip-gram (word2vec) with negative sampling.
