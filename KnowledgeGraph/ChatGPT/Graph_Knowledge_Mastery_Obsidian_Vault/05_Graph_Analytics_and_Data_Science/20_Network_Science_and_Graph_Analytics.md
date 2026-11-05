---
title: "Network Science and Graph Analytics"
type: chapter
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - network-science
  - centrality
  - community-detection
  - graph-analytics
---
# Network Science and Graph Analytics

> [!goal]
> Describe, compare and explain graph structure without turning every correlation or centrality score into a causal story.

## 1. Analysis starts with graph semantics

Before computing an algorithm, write:

- what a node represents;
- what each edge type means;
- direction, weight, sign and multiplicity;
- observation window and missingness;
- whether edges are opportunities, events, affinities or inferred links;
- the unit of analysis;
- the action a result may influence.

The same PageRank implementation means different things on hyperlinks, payments, citations and organizational communication.

## 2. Basic structural profile

For $G=(V,E)$ measure:

- $|V|$, $|E|$ and density;
- connected/weakly/strongly connected components;
- degree and weighted-degree distributions;
- isolates, leaves and hubs;
- self-loops and parallel edges;
- reciprocity in directed graphs;
- assortativity;
- clustering/transitivity;
- path-length and diameter estimates;
- type and temporal coverage.

For an undirected simple graph, density is

$$\rho=\frac{2|E|}{|V|(|V|-1)}.$$

Most real large graphs are sparse, but local regions can be dense. Report distributions and quantiles rather than only averages.

## 3. Degree and heavy tails

Degree $k_v$ counts incident edges. Weighted degree/strength sums weights. In directed graphs, separate in-degree and out-degree.

A log-log line is not evidence of a power law. Fit competing distributions, estimate the lower cutoff, use goodness-of-fit tests and report uncertainty. Heavy-tailed degree affects sampling, robustness, ML evaluation and distributed performance.

## 4. Paths and reachability

- BFS gives unweighted shortest paths.
- Dijkstra requires nonnegative weights.
- Bellman-Ford permits negative edges but detects negative cycles.
- A* uses an admissible heuristic.
- all-pairs methods include Floyd-Warshall and repeated single-source algorithms.

A path weight must represent a composable cost. Similarity or probability may need transformation. For probabilities along independent edges, negative log converts products to sums; independence must be justified.

## 5. Centrality is a family of hypotheses

| Measure | Operational interpretation | Main caution |
|---|---|---|
| Degree | Local activity/opportunity | Rewards raw volume |
| Betweenness | Lies on many shortest paths | Assumes shortest-path flow; expensive/unstable |
| Closeness | Small distance to others | Disconnected graphs require variants |
| Harmonic | Reciprocal distances | Still depends on path semantics |
| Eigenvector | Connected to important nodes | Localization and sign/direction issues |
| PageRank | Stationary visit probability with teleportation | Sensitive to direction, damping and graph construction |
| HITS | Hub/authority mutual reinforcement | Query/subgraph dependent |
| k-core | Embedded in recursively dense region | Not influence by itself |

Centrality is not importance in the abstract. Validate against a domain outcome and compare rankings under perturbation.

### PageRank

$$\mathbf{r}=\alpha P^T\mathbf{r}+(1-\alpha)\mathbf{v},$$

where $P$ is a transition matrix, $\alpha$ the continuation probability and $\mathbf{v}$ a teleportation distribution. Personalized PageRank changes $\mathbf{v}$ to focus on seed nodes.

## 6. Triangles, clustering and motifs

Local clustering coefficient for an undirected node $v$ is the fraction of neighbor pairs connected. Global transitivity compares closed triplets to all connected triplets.

Motifs are small subgraph patterns compared with a null model. A motif is meaningful only relative to a defensible randomized baseline that preserves relevant properties such as degree sequence or type counts.

## 7. Community detection

A community is not a universal object. Algorithms optimize different definitions.

### Modularity methods

Louvain and Leiden seek partitions with more within-community edges than a null model. Leiden improves connectivity properties of communities. Risks include resolution limits, stochastic variation and over-interpreting algorithmic clusters as social groups.

### Flow methods

Infomap compresses random-walk flow. It is useful when communities retain movement.

### Label propagation

Fast and scalable, but unstable and weakly objective-driven.

### Spectral clustering

Uses eigenstructure of Laplacian/adjacency matrices. Effective when geometry matches assumptions; sensitive to chosen number of clusters and scaling.

### Stochastic block models

A generative model in which connection probabilities depend on latent blocks. It can identify assortative, disassortative and core-periphery structure and supports statistical model comparison.

Run multiple seeds, report stability and compare to simple baselines.

## 8. Cohesion, roles and core-periphery

- connected components identify reachability groups;
- biconnected components and articulation points identify structural fragility;
- bridges connect regions;
- k-core/k-shell measures recursive cohesion;
- k-truss uses triangle support;
- structural equivalence compares similar neighbors;
- regular equivalence compares similar roles.

A broker can have low degree but high bridge value. A hub can sit inside one community with low brokerage.

## 9. Similarity and link signals

Local scores:

- common neighbors;
- Jaccard;
- Adamic-Adar;
- resource allocation;
- preferential attachment.

Global/learned scores include Katz, personalized PageRank, embeddings and GNNs. Use time-respecting evaluation; random edge deletion often leaks future structure.

## 10. Diffusion and cascades

Models include independent cascade, linear threshold, susceptible-infected-recovered variants and random walks. Parameters and interventions are domain assumptions, not properties inferred from topology alone.

Influence maximization is submodular under some diffusion models, enabling greedy approximation guarantees. Those guarantees disappear when model assumptions change.

## 11. Null models and statistical discipline

Compare an observed statistic to graphs preserving selected properties:

- Erdos-Renyi size/density;
- configuration model degree sequence;
- degree-preserving edge swaps;
- temporal randomization;
- bipartite/type-preserving randomization;
- stochastic block models.

Multiple hypothesis testing matters when scanning many motifs or communities. Network dependence violates naive independent-observation assumptions.

## 12. Temporal and sampling bias

Graph measurements depend on the observation window. Crawling, API limits, missing private edges and snowball sampling bias degree and centrality. Report graph construction and coverage alongside every result.

## 13. Laboratory

Analyze one directed weighted temporal graph with NetworkX and a scalable system. Produce:

- structural profile and degree-tail analysis;
- five centralities with rank-correlation/stability;
- three community approaches with stability and quality measures;
- bridge/core analysis;
- temporal snapshots;
- at least two null-model comparisons;
- a one-page statement of what cannot be inferred.

## Mastery checklist

- [ ] Every algorithm has a stated structural hypothesis.
- [ ] I report distributions, uncertainty and construction bias.
- [ ] I distinguish association, diffusion model and causation.
- [ ] Communities are tested for stability and usefulness.
- [ ] I compare against relevant null models.

## Sources and next reading

- [Network Science by Albert-Laszlo Barabasi](https://networksciencebook.com/)
- Mark Newman, *Networks*, 2nd edition
- [NetworkX algorithms](https://networkx.org/documentation/stable/reference/algorithms/)
- [[21_Graph_Data_Science_Workflows]]
- [[22_Graph_Algorithm_Selection_Guide]]
