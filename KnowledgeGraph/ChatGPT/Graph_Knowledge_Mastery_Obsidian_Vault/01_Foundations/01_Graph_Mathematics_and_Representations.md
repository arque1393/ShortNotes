---
title: "Graph Mathematics and Representations"
type: chapter
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - foundations
  - graph-theory
  - mathematics
---
# Graph Mathematics and Representations

> [!goal]
> Develop enough graph mathematics to reason about semantics, algorithms, system cost and machine-learning behavior—not merely to recognize terminology.

## 1. Graph objects

A simple graph is \(G=(V,E)\). In a directed graph, \(E\subseteq V\times V\); in an undirected graph, an edge is an unordered pair. Real knowledge graphs usually need more structure:

\[
G=(V,E,\tau_V,\tau_E,X_V,X_E,T,P)
\]

where \(\tau\) assigns types, \(X\) assigns attributes/features, \(T\) carries time and \(P\) may represent provenance or probabilities. This notation is not a standard; it forces you to state what information the graph actually contains.

### Important variants

| Variant | Distinguishing feature | Typical use |
|---|---|---|
| Directed | edge has source and target | citations, ownership, dependencies |
| Weighted | edge has cost/strength | distance, traffic, confidence |
| Multigraph | parallel edges allowed | repeated events, multiple relation instances |
| Bipartite | vertices split into two sets | user–item recommendation, entity–document graphs |
| Heterogeneous | multiple node/edge types | enterprise KGs, biomedical networks |
| Temporal | vertices/edges have validity or event time | transactions, organizational history |
| Multiplex | same nodes connected through layers | social, communication and financial ties |
| Hypergraph | one edge joins many vertices | reactions, teams, n-ary facts |

## 2. Paths, walks and reachability

A **walk** may repeat vertices and edges. A **trail** does not repeat edges. A **path** normally does not repeat vertices. A **cycle** returns to its start. Be precise because query languages use different path semantics and may return many repeated-edge walks unless constrained.

For unweighted graphs, shortest-path distance \(d(u,v)\) is the minimum number of edges. For weighted graphs it is the minimum sum of costs, provided the algorithm’s assumptions hold. Dijkstra requires non-negative weights; Bellman–Ford handles negative edges and can detect a reachable negative cycle.

The branching factor is decisive. A depth-\(k\) traversal with average branching \(b\) can examine roughly \(1+b+\cdots+b^k\) states before pruning. “Only five hops” can be enormous.

## 3. Degree and local structure

For a directed graph:

- \(d^+(v)\): out-degree;
- \(d^-(v)\): in-degree;
- weighted degree/strength: sum of incident weights.

Degree is not automatically importance. A high-degree account may be a hub, a data-integration artifact, a generic category, a duplicated entity or an ingestion error.

A local clustering coefficient for an undirected simple graph is commonly:

\[
C_v = \frac{2T_v}{d_v(d_v-1)}
\]

where \(T_v\) is the number of triangles containing \(v\). The formula must be adapted for directed, weighted or multi-relational graphs.

## 4. Matrix representations

Let \(n=|V|\).

### Adjacency matrix

\(A_{ij}=1\) when an edge exists from \(i\) to \(j\), or the edge weight for weighted graphs. Dense storage is \(O(n^2)\); real KGs are usually sparse, so compressed sparse row/column formats are central.

### Degree matrix and Laplacian

For an undirected graph, \(D\) is diagonal with \(D_{ii}=d_i\). The combinatorial Laplacian is:

\[
L=D-A
\]

Common normalized forms are:

\[
L_{sym}=I-D^{-1/2}AD^{-1/2}, \qquad L_{rw}=I-D^{-1}A
\]

The Laplacian connects graph structure to diffusion, cuts, smoothness and spectral methods. For a signal \(x\) on nodes:

\[
x^T L x = \frac{1}{2}\sum_{i,j} A_{ij}(x_i-x_j)^2
\]

so small energy means adjacent nodes have similar signal values. GCN-style propagation exploits a related smoothness bias; this helps under homophily and can hurt under heterophily.

### Incidence matrix

An incidence matrix relates vertices to edges. It is useful for flows, cycle spaces, hypergraph generalizations and topological methods.

## 5. Random walks and stationary behavior

For a row-normalized transition matrix \(P=D^{-1}A\), a distribution evolves as \(\pi_{t+1}=\pi_tP\). A stationary distribution satisfies \(\pi=\pi P\). For a connected, non-bipartite undirected graph, the stationary probability of a node is proportional to degree.

PageRank modifies the walk with restart/teleportation:

\[
p = \alpha P^T p + (1-\alpha)v
\]

where \(v\) is a teleport or personalization distribution. PageRank is therefore not “universal importance”; it is importance under a particular stochastic process and graph projection.

## 6. Connectivity and components

- **Connected component**: maximal connected subgraph in an undirected graph.
- **Weakly connected component**: connected after ignoring direction.
- **Strongly connected component**: every pair is mutually reachable respecting direction.
- **Articulation point/bridge**: removal increases the number of components.
- **k-core**: maximal subgraph in which each node has degree at least \(k\) within the subgraph.

These concepts help discover isolated data, cyclic dependencies, resilient cores and integration defects.

## 7. Centrality families

| Measure | Question encoded | Common failure |
|---|---|---|
| Degree | Who has many direct ties? | confounds duplicates/generic nodes with importance |
| Closeness | Who is near everyone? | unstable/disconnected graphs; direction matters |
| Betweenness | Who lies on shortest paths? | shortest paths may not model actual flow |
| Eigenvector | Who connects to important nodes? | localization around dense hubs |
| PageRank | Who receives probability under a random surfer? | arbitrary edge projection/teleport assumptions |
| Harmonic | Who is close while tolerating disconnection? | still depends on shortest-path semantics |

Do not rank entities before writing the process that the score is supposed to approximate.

## 8. Communities and cuts

A graph partition groups nodes so that within-group connectivity is high relative to between-group connectivity. **Modularity** compares observed within-community edges against a degree-preserving null model. It has a resolution limit and can produce different partitions across runs.

Communities are algorithmic summaries, not discovered ontological classes. A community of dealers with similar operational links does not mean they instantiate a natural category.

## 9. Homophily, heterophily and assortativity

**Homophily** means linked nodes tend to share attributes or labels. **Heterophily** means useful links often connect unlike nodes. Many message-passing GNNs assume local smoothness; heterophilous relations may require relation-aware, signed, higher-order or feature-preserving architectures.

Assortativity measures mixing by degree or attributes. A high value can result from the data-collection process rather than a domain mechanism.

## 10. Multi-relational and knowledge graphs

A KG triple is often written \((h,r,t)\), but this hides context. A fact may need:

\[
(h,r,t,\text{valid-time},\text{transaction-time},\text{source},\text{confidence},\text{scope})
\]

Binary edges can represent n-ary relations by introducing an event/statement node. For example, a `Sale` node can connect dealer, vehicle, customer, date, price and campaign. This often preserves identity and provenance better than six unrelated binary facts.

## 11. Graph equivalence and isomorphism

Two graphs are isomorphic if a bijection between vertices preserves adjacency. Graph isomorphism is different from ontology equivalence or entity identity. Two differently labeled graph structures may be isomorphic but refer to entirely different domains.

Automorphisms are structure-preserving permutations of a graph onto itself. They create indistinguishable structural positions and help explain limitations of message-passing GNNs.

## 12. A minimal Python laboratory

```python
import networkx as nx

G = nx.MultiDiGraph()
G.add_node("dealer:101", kind="Dealer")
G.add_node("region:east", kind="Region")
G.add_edge("dealer:101", "region:east", key="membership-2026",
           relation="IN_REGION", valid_from="2026-01-01")

print(G.in_degree("region:east"))
print(list(nx.weakly_connected_components(G)))
```

For algorithms, explicitly project a simple graph:

```python
H = nx.DiGraph()
for u, v, data in G.edges(data=True):
    if data["relation"] == "IN_REGION":
        H.add_edge(u, v)
```

The projection is a modeling decision. Record it.

## 13. Problem-solving checklist

Before any algorithm or ML model, write:

- What constitutes a node?
- Does an edge denote a type-level relation, a specific event, similarity or evidence?
- Is direction meaningful?
- Are parallel edges collapsed? If so, how?
- Are weights costs, strengths, counts, probabilities or confidences?
- Which time is represented?
- Are missing edges negative, unknown or unobserved?
- Which projection will the algorithm actually see?

## Exercises

1. Model a dealer–vehicle allocation domain in three ways: direct edges, event nodes and a hypergraph. Compare query simplicity and provenance.
2. Construct a graph where degree, betweenness and PageRank rank the top node differently. Explain each ranking.
3. Show a five-hop traversal whose state space explodes despite only 1,000 nodes.
4. Compute \(x^TLx\) for two node signals and explain which one is smoother.
5. Create a heterophilous graph and explain why neighbor averaging destroys class information.
6. Identify whether ten business questions require reachability, shortest path, set joins, aggregation, temporal ordering or logical entailment.

## Sources and further reading

- Albert-László Barabási, *Network Science* (open textbook): https://www.networksciencebook.com/
- William L. Hamilton, *Graph Representation Learning* (open prepublication book): https://www.cs.mcgill.ca/~wlh/grl_book/
- NetworkX documentation: https://networkx.org/documentation/stable/
- LDBC Graphalytics algorithms: https://ldbcouncil.org/benchmarks/graphalytics/algorithms/

## Next

Continue to [[02_Graph_Algorithms_and_Complexity]].
