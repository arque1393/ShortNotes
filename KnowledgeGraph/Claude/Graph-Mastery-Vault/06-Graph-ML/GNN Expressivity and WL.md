---
tags: [graph-ml, theory]
phase: 3
status: not-started
---
# GNN Expressivity & the Weisfeiler–Leman Test

> [!summary]
> Message-passing GNNs can distinguish **at most** the graphs that the 1-WL colour-refinement test distinguishes (Xu et al. 2019; Morris et al. 2019). GIN reaches that bound.

## 1-WL colour refinement
1. Give every node the same colour.
2. Repeat: new colour = HASH(own colour, **multiset** of neighbour colours).
3. Stop when stable. Different colour histograms ⇒ non-isomorphic. Same ⇒ *maybe* isomorphic.

MPNN = "neural, soft version" of this. To match 1-WL the aggregation must be **injective on multisets** → **sum** (not mean/max) + MLP ⇒ **GIN**.

## What 1-WL (and MPNNs) cannot do
- Distinguish **regular graphs** of same degree and size (e.g., two triangles vs a 6-cycle — every node has degree 2).
- Count cycles/cliques in general; detect some substructures.
- Mean aggregation can't distinguish multisets with the same distribution ({a,b} vs {a,a,b,b}); max can't count.

## Going beyond 1-WL
| Approach | Idea |
|---|---|
| k-WL / k-GNNs | Colour k-tuples (more powerful, $O(n^k)$) |
| Random node features | Break symmetry (probabilistic) |
| **Positional/structural encodings** | Laplacian eigenvectors (LapPE), random-walk SE (RWSE) |
| Subgraph GNNs | Run GNN on node-deleted/marked subgraphs |
| Substructure counts | Add cycle/clique counts as features (GSN) |
| Graph transformers + PE | [[Graph Transformers]] |

## Key reading
- Xu, Hu, Leskovec, Jegelka, "How Powerful are GNNs?" ICLR 2019
- Morris et al., "Weisfeiler and Leman Go Neural" AAAI 2019; "…Go Machine Learning: The Story so Far" JMLR 2023

## My notes


## Self-test #flashcards/graph-ml
Upper bound on the distinguishing power of message-passing GNNs?::The 1-WL (colour refinement) test.
Which aggregator is needed for 1-WL expressivity and why?::Sum — it is injective on multisets (with MLPs), unlike mean or max.
Classic pair 1-WL can't distinguish?::Two disjoint triangles vs a 6-cycle (both 2-regular on 6 nodes).
Two ways to exceed 1-WL?::Positional/structural encodings (e.g., Laplacian eigenvectors, RWSE) or higher-order/subgraph GNNs (also random features).
