---
tags: [foundations, graph-theory]
phase: 0
status: not-started
---
# Graph Theory Essentials

> [!summary]
> A graph $G=(V,E)$ is a set of nodes and edges. Almost everything later — PageRank, GNNs, SPARQL property paths — is an operation on this object or its matrix form.

## Core definitions
- **Directed / undirected**, **weighted**, **multigraph** (parallel edges — KGs are directed labelled multigraphs), **simple graph**.
- **Degree** $k_i$; in-/out-degree for digraphs. **Handshake lemma:** $\sum_i k_i = 2|E|$.
- **Walk** (vertices may repeat) ⊃ **trail** (no repeated edges) ⊃ **path** (no repeated vertices).
- **Connected component**; for digraphs: *weakly* vs *strongly* connected.
- **Tree** = connected acyclic graph, $|E|=|V|-1$. **DAG** = directed acyclic → topological sort.
- **Bipartite** = 2-colourable ⇔ no odd cycle (user–item graphs, recommendation).
- **Clique**, **k-core** (max subgraph with min degree ≥ k), **triangle**.
- **Graph isomorphism** — no known polynomial algorithm in general (quasi-polynomial, Babai 2015); matters for [[GNN Expressivity and WL]].

## Matrix representations
- **Adjacency** $A_{ij}=1$ if edge $i\to j$. **Degree** $D=\mathrm{diag}(k_i)$.
- **Incidence** $B \in \{0,\pm1\}^{|V|\times|E|}$; then $L = BB^\top$ (oriented).
- **Key fact:** $(A^k)_{ij}$ = number of walks of length $k$ from $i$ to $j$. Triangles $= \tfrac{1}{6}\mathrm{tr}(A^3)$ (undirected).
- Storage: adjacency list $O(|V|+|E|)$, CSR/COO sparse formats (PyG uses COO `edge_index` of shape `[2, E]`).

## Traversals & complexity
| Algorithm | Use | Complexity |
|---|---|---|
| BFS | Unweighted shortest paths, k-hop neighbourhoods | $O(V+E)$ |
| DFS | Components, cycles, topological sort | $O(V+E)$ |
| Dijkstra (binary heap) | Non-negative weighted SP | $O((V+E)\log V)$ |
| Bellman–Ford | Negative weights | $O(VE)$ |
| Tarjan / Kosaraju | Strongly connected components | $O(V+E)$ |

```python
from collections import deque
def bfs(adj, s):
    dist = {s: 0}; q = deque([s])
    while q:
        u = q.popleft()
        for v in adj[u]:
            if v not in dist:
                dist[v] = dist[u] + 1; q.append(v)
    return dist
```

## Exercises
- [ ] Prove the handshake lemma; derive that the number of odd-degree vertices is even.
- [ ] Count triangles in the karate club graph with $\mathrm{tr}(A^3)/6$ and compare with `nx.triangles`.
- [ ] Implement topological sort with DFS and with Kahn's algorithm.

## Connections
- → [[Spectral Graph Theory]] (matrices → eigenvalues)
- → [[Path Finding and Similarity]], [[Centrality Measures]]
- → [[Message Passing and GNNs]] (neighbourhood aggregation = sparse matrix multiply)

## Resources
- Newman, *Networks*, ch. 6
- West, *Introduction to Graph Theory* (for proofs)

## My notes


## Self-test #flashcards/foundations
What does $(A^k)_{ij}$ count?::The number of walks of length k from node i to node j.
A graph is bipartite if and only if…::It contains no odd-length cycle.
Formula for triangles in an undirected graph via A?::tr(A³)/6
Time complexity of BFS?::O(V + E)
What is a k-core?::The maximal subgraph in which every node has degree at least k.
