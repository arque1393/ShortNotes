---
tags: [graph-ml, scalability]
phase: 3
status: not-started
---
# Scalable GNN Training

> [!summary]
> Full-batch GNNs don't fit large graphs in GPU memory because of **neighbourhood explosion**. Solutions: sample, partition, precompute, or distribute.

| Family | Methods | Idea |
|---|---|---|
| Node-wise sampling | **GraphSAGE**, PinSage | Fixed fan-out per layer (e.g., [15, 10]) |
| Layer-wise sampling | FastGCN, LADIES | Sample nodes per layer |
| Subgraph sampling | **Cluster-GCN**, **GraphSAINT** | Train on partitions / sampled subgraphs |
| Precomputation | **SIGN**, SGC | Precompute $\hat A^k X$; then train an MLP |
| Historical embeddings | GNNAutoScale | Cache stale embeddings of out-of-batch nodes |
| Distributed | DistDGL, **GraphStorm**, PyG distributed | Partition graph across machines |
| GPU analytics | cuGraph, WholeGraph | Fast sampling & feature storage |

```python
from torch_geometric.loader import NeighborLoader
loader = NeighborLoader(data, num_neighbors=[15, 10], batch_size=1024,
                        input_nodes=data.train_mask, shuffle=True)
for batch in loader:
    out = model(batch.x, batch.edge_index)[:batch.batch_size]   # seed nodes first
    loss = F.cross_entropy(out, batch.y[:batch.batch_size])
```

## Benchmarks
OGB `ogbn-products`, `ogbn-papers100M`, OGB-LSC (MAG240M, WikiKG90Mv2), IGB.

## My notes


## Self-test #flashcards/graph-ml
What is neighbourhood explosion?::The K-hop receptive field grows exponentially with depth, making full computation infeasible.
How does Cluster-GCN scale training?::Partitions the graph (e.g., METIS) and trains on subgraphs formed from clusters.
Why is SIGN fast?::It precomputes propagated features (ÂᵏX) once, then trains a simple MLP.
In PyG NeighborLoader, which rows of the output correspond to seed nodes?::The first batch.batch_size rows.
