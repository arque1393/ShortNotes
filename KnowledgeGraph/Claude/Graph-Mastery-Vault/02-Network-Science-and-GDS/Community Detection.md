---
tags: [network-science, gds, algorithms]
phase: 1
status: not-started
---
# Community Detection

> [!summary]
> Find groups of nodes more densely connected internally than externally. Core to fraud rings, customer segmentation — and to **Microsoft GraphRAG's global search** (hierarchical Leiden).

## Modularity
$$Q = \frac{1}{2m}\sum_{ij}\left[A_{ij} - \frac{k_i k_j}{2m}\right]\delta(c_i, c_j)$$
- Compares edges inside communities with the configuration-model expectation.
- **Resolution limit:** modularity maximisation can't detect communities smaller than ~$\sqrt{m}$ → use resolution parameter $\gamma$.
- Maximising $Q$ is NP-hard → heuristics.

## Algorithms
| Algorithm | Idea | Notes |
|---|---|---|
| **Louvain** | (1) local moves of nodes to neighbour communities maximising ΔQ; (2) aggregate communities into super-nodes; repeat | Fast; can create **badly connected** communities |
| **Leiden** (Traag et al. 2019) | Adds a **refinement** phase | Guarantees connected communities; faster & better; default choice |
| Label propagation | Nodes adopt majority neighbour label | Very fast, non-deterministic |
| Infomap | Minimises description length of random walks (map equation) | Good for flow/directed graphs |
| SBM inference | Fit stochastic block model (e.g., `graph-tool`) | Principled, statistical |
| WCC / SCC | Connected components | Always run first! |
| Clique percolation | Overlapping communities | |

## Evaluation
- With ground truth: **NMI**, **ARI**.
- Without: modularity, conductance, coverage; and *domain sanity checks*.

## Code
```python
import igraph as ig, leidenalg as la
g = ig.Graph.Famous("Zachary")
part = la.find_partition(g, la.ModularityVertexPartition)
print(part.modularity, len(part))
```
```cypher
CALL gds.leiden.stream('social', {includeIntermediateCommunities: true})
YIELD nodeId, communityId, intermediateCommunityIds
RETURN communityId, count(*) AS size ORDER BY size DESC;
```

## Connections
- [[Microsoft GraphRAG]] community reports
- [[Spectral Graph Theory]] (spectral clustering)
- [[Random Graph Models]] (SBM, configuration model)

## My notes


## Self-test #flashcards/network-science
What problem of Louvain does Leiden fix?::Louvain can produce badly connected or even disconnected communities; Leiden's refinement guarantees connected ones.
What is the resolution limit of modularity?::Modularity maximisation cannot resolve communities smaller than roughly √m edges.
Two metrics to compare a partition to ground truth?::NMI and ARI.
Which community algorithm does Microsoft GraphRAG use?::Hierarchical Leiden.
Infomap optimises what?::The map equation — description length of a random walk on the partition.
