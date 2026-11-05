---
tags: [network-science, gds, algorithms]
phase: 1
status: not-started
---
# Centrality Measures

> [!summary]
> Centrality = "importance", but each measure defines importance differently. Choosing the right one is a modelling decision.

| Measure | Formula / idea | Good for | Cost |
|---|---|---|---|
| Degree | $k_i$ | Local popularity | $O(E)$ |
| Closeness | $\frac{n-1}{\sum_j d(i,j)}$ | Fast spreaders | $O(VE)$ |
| Harmonic | $\sum_{j\ne i} 1/d(i,j)$ | Closeness for disconnected graphs | $O(VE)$ |
| Betweenness | $\sum_{s\ne i\ne t}\frac{\sigma_{st}(i)}{\sigma_{st}}$ | Brokers, bottlenecks, money mules | $O(VE)$ Brandes |
| Eigenvector | $Ax = \lambda_1 x$ | Connected to important nodes | iterative |
| Katz | $x = \sum_{l\ge1}\beta^l A^l \mathbf{1}$ | Eigenvector for DAGs | iterative |
| **PageRank** | $PR_i = \frac{1-d}{N} + d\sum_{j\to i}\frac{PR_j}{k^{out}_j}$ | Directed importance, ranking | iterative |
| **Personalized PageRank** | Teleport only to seed set $S$ | Relevance to a query → **HippoRAG** retrieval, recommendations | iterative |
| HITS | Hubs & authorities | Web, citations | iterative |

## PageRank as a Markov chain
$\mathbf{r} = d\, P^\top \mathbf{r} + (1-d)\,\mathbf{v}$, with $P=D^{-1}A$, damping $d\approx0.85$, teleport vector $\mathbf{v}$ (uniform = PageRank; one-hot/seeds = PPR). Stationary distribution of a random surfer.

## Neo4j GDS example
```cypher
CALL gds.graph.project('social', 'Person', 'KNOWS');

CALL gds.pageRank.stream('social', {dampingFactor: 0.85})
YIELD nodeId, score
RETURN gds.util.asNode(nodeId).name AS name, score
ORDER BY score DESC LIMIT 10;

CALL gds.betweenness.stream('social')
YIELD nodeId, score
RETURN gds.util.asNode(nodeId).name AS name, score
ORDER BY score DESC LIMIT 10;
```

## Pitfalls
> [!warning]
> - Betweenness on huge graphs: use sampling approximation.
> - PageRank on graphs with dangling nodes needs proper handling.
> - Centralities are highly correlated with degree in many graphs — always compare against degree as a baseline.

## Connections
- PPR → [[LightRAG and HippoRAG]], APPNP in [[Oversmoothing and Oversquashing]]
- Centrality features → [[P04 Fraud Graph Analytics]]

## My notes


## Self-test #flashcards/network-science
Which centrality identifies brokers / bottlenecks?::Betweenness centrality.
Algorithm for exact betweenness in O(VE)?::Brandes' algorithm.
PageRank vs Personalized PageRank?::PPR teleports only to a seed set instead of uniformly, measuring relevance to those seeds.
Typical PageRank damping factor?::0.85
Which retrieval method uses PPR over an open-IE KG?::HippoRAG / HippoRAG 2.
