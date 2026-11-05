---
title: "Graph Algorithms and Complexity"
type: chapter
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - foundations
  - graph-algorithms
  - complexity
---
# Graph Algorithms and Complexity

> [!goal]
> Select, implement and evaluate graph algorithms by their assumptions and workload—not by popularity.

## 1. Complexity on graphs

Use \(n=|V|\) and \(m=|E|\). Sparse real-world graphs often have \(m\ll n^2\), but hubs, skewed degree distributions and typed edges create practical costs not visible in big-O notation.

Complexity analysis should include:

- worst-case asymptotic cost;
- memory and data movement;
- random versus sequential access;
- frontier size and load imbalance;
- number of iterations until convergence;
- distributed communication;
- cost of graph projection and preprocessing.

A theoretically linear scan may be operationally expensive when it touches billions of properties or crosses machines.

## 2. Traversal and reachability

### Breadth-first search

BFS explores an unweighted graph by distance layers and runs in \(O(n+m)\). It gives shortest hop counts from a source.

```python
from collections import deque

def bfs(adj: dict[str, list[str]], source: str):
    distance = {source: 0}
    parent = {source: None}
    q = deque([source])
    while q:
        u = q.popleft()
        for v in adj.get(u, []):
            if v not in distance:
                distance[v] = distance[u] + 1
                parent[v] = u
                q.append(v)
    return distance, parent
```

### Depth-first search

DFS supports cycle detection, topological sorting, articulation/bridge algorithms and strongly connected components. Recursive implementations can overflow on large graphs; use an explicit stack when necessary.

### Bidirectional search

When a single source and target are known, searching from both ends can reduce explored states from roughly \(b^d\) to \(2b^{d/2}\), although directed/weighted/path-constrained cases require care.

## 3. Shortest paths

| Algorithm | Edge assumptions | Typical use |
|---|---|---|
| BFS | unweighted/equal cost | hop distance |
| Dijkstra | non-negative weights | routing/cost paths |
| Bellman–Ford | negative edges allowed | detect negative cycles |
| A* | admissible heuristic | goal-directed pathfinding |
| Floyd–Warshall | dense/smaller graph | all-pairs, \(O(n^3)\) |
| Johnson | sparse, possible negative edges | all-pairs via reweighting |

A path query in a database may enumerate all matching paths rather than compute only a cheapest path. Understand the language’s path mode and uniqueness semantics.

## 4. Components and ordering

- Union–find efficiently maintains components for incremental undirected edge additions.
- Kosaraju, Tarjan and Gabow find strongly connected components in linear time.
- A directed acyclic graph admits a topological order. Failure to produce one indicates a cycle, which may be a data issue or a legitimate feedback loop.
- Dynamic connectivity under deletions is much harder than under insertions.

## 5. Spanning trees, flows and matching

### Minimum spanning tree

Kruskal sorts edges and uses union–find; Prim grows from a frontier. An MST connects all nodes with minimum total edge weight but does not preserve all important paths or communities.

### Maximum flow and minimum cut

Flow networks model capacity-constrained movement. The max-flow/min-cut theorem connects the maximum feasible flow to the minimum capacity cut. Applications include assignment, segmentation and bottleneck analysis.

### Matching

Bipartite matching models one-to-one assignment such as candidates to positions or records to possible entities. Many entity-resolution systems need clustering rather than simple matching because several records can refer to one entity.

## 6. Centrality algorithms

### PageRank

Iterative power methods apply until convergence. Monitor residuals and dangling-node handling. Personalization changes the meaning materially.

### Betweenness

Brandes’ algorithm improves all-pairs dependency accumulation, but exact betweenness is still costly on large graphs. Approximation by source sampling must report uncertainty.

### Closeness/harmonic centrality

Disconnected graphs make classical closeness problematic. Harmonic centrality replaces unreachable inverse distances with zero.

## 7. Community detection

### Label propagation

Fast and scalable but unstable; tie-breaking and update order matter.

### Louvain and Leiden

Both optimize modularity-like objectives hierarchically. Leiden improves partition quality properties over Louvain, but results still depend on resolution, randomness and graph projection.

### Spectral clustering

Uses eigenvectors of graph Laplacians. It is mathematically interpretable but can be expensive and sensitive to chosen similarity/normalization.

### Stochastic block models

Treat community structure as a generative probabilistic model. They can represent assortative, disassortative and core–periphery patterns, unlike methods that equate communities with dense groups.

> [!warning]
> A community algorithm always returns a partition or hierarchy under its objective. It does not prove that a real social, business or ontological group exists.

## 8. Similarity and link heuristics

Local link predictors include:

\[
\text{CommonNeighbors}(u,v)=|N(u)\cap N(v)|
\]

\[
\text{Jaccard}(u,v)=\frac{|N(u)\cap N(v)|}{|N(u)\cup N(v)|}
\]

\[
\text{AdamicAdar}(u,v)=\sum_{z\in N(u)\cap N(v)}\frac{1}{\log d(z)}
\]

Preferential attachment uses \(d(u)d(v)\). These are useful baselines and often competitive. For typed or directed KGs, define relation-specific neighborhoods and avoid leaking the target relation.

## 9. Motifs, triangles and subgraph patterns

Motif analysis counts small patterns relative to a null model. Raw triangle counts mainly reflect degree and graph size. Subgraph isomorphism is computationally difficult in general; query optimizers rely on labels, indexes, selectivity and join ordering to avoid combinatorial explosion.

## 10. Graph sparsification, sampling and sketches

Large-graph work often requires approximation:

- node or edge sampling;
- random-walk sampling;
- neighborhood sampling for GNNs;
- reservoir sampling for streams;
- graph sparsification preserving cuts or spectra;
- Bloom filters and sketches for approximate membership/counts.

Sampling changes distributions. A random walk over-samples high-degree nodes unless corrected. Report the sampling design as part of the method.

## 11. Temporal and streaming algorithms

A static aggregate graph can invent paths that never existed at one time. Temporal reachability requires non-decreasing event times. Streaming systems may maintain approximate counts, windows, incremental PageRank or dynamic communities.

Distinguish:

- event time versus processing time;
- validity interval versus observation timestamp;
- snapshot queries versus time-respecting paths;
- append-only history versus corrections/deletions.

## 12. Distributed graph processing

Common abstractions include vertex-centric “think like a vertex,” edge-centric, GAS (gather–apply–scatter), linear algebra/GraphBLAS and dataflow systems. Performance is dominated by partitioning and communication when high-degree nodes cross workers.

Graphalytics uses BFS, PageRank, weakly connected components, label-propagation community detection, local clustering coefficient and single-source shortest paths as representative analytics kernels.

## 13. Algorithm selection by question

| Business/research question | First method | Required check |
|---|---|---|
| Can A influence B? | directed reachability | valid edge semantics and time |
| What is the cheapest route? | weighted shortest path | non-negative/cost definition |
| Which entities bridge groups? | betweenness + robustness | flow really follows shortest paths? |
| Which records form dense groups? | Leiden/SBM | compare resolution and null model |
| Which nodes are structurally similar? | role embeddings / automorphic features | similarity is not proximity |
| Which links are suspicious? | motif/rarity + supervised baseline | degree and sampling bias |
| What will connect next? | heuristics, KGE or GNN | temporal/leakage-safe split |
| What breaks the network? | articulation/cut/resilience simulation | model interventions explicitly |

## 14. Verification practice

For any algorithm:

1. Test on a tiny graph where the answer is known.
2. Test edge cases: empty graph, isolates, self-loops, parallel edges, disconnected components.
3. Compare at least two implementations or a reference output.
4. Measure sensitivity to direction, weights and projection.
5. Create a null/randomized graph preserving key marginals.
6. Report runtime, memory and approximation error—not only the score.

## Labs

### Lab A — Algorithm notebook

Implement BFS, DFS, Dijkstra, PageRank and connected components without a graph library. Compare with NetworkX on generated graphs.

### Lab B — Projection sensitivity

From a multi-relational domain graph, create four projections. Run community detection and centrality; quantify how rankings change.

### Lab C — Null models

Compare clustering and motif counts against Erdős–Rényi and degree-preserving randomized graphs. Explain what remains surprising.

### Lab D — Query-versus-algorithm

Implement the same reachability and shortest-path tasks in NetworkX, Cypher and SPARQL property paths. Compare semantics and execution behavior.

## Sources

- NetworkX algorithms reference: https://networkx.org/documentation/stable/reference/algorithms/
- LDBC Graphalytics: https://ldbcouncil.org/benchmarks/graphalytics/
- LDBC Social Network Benchmark: https://ldbcouncil.org/benchmarks/snb/
- Barabási, *Network Science*: https://www.networksciencebook.com/
- Neo4j Graph Data Science manual: https://neo4j.com/docs/graph-data-science/current/

## Next

Read [[03_Logic_Knowledge_Representation_and_Semantics]].
