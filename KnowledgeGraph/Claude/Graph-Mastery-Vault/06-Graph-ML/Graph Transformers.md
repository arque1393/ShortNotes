---
tags: [graph-ml, transformers]
phase: 3
status: not-started
---
# Graph Transformers

> [!summary]
> Let every node attend to every node (global receptive field, no over-squashing), but **inject graph structure** via positional/structural encodings and attention biases.

## Key models
| Model | How structure enters |
|---|---|
| GT (Dwivedi & Bresson 2020) | Laplacian eigenvector PE, attention restricted to neighbours |
| SAN | Learned spectral attention over full graph |
| **Graphormer** (2021) | Centrality encoding (degree), spatial encoding (shortest-path distance as attention bias), edge encoding |
| **GraphGPS** (2022) | Each layer = local MPNN + global attention + PE/SE → general recipe |
| Exphormer | Sparse attention via expander graphs + virtual nodes → linear-ish cost |
| NodeFormer / SGFormer | Scalable kernelised / simplified attention for large graphs |

## Trade-offs
- Full attention: $O(N^2)$ → fine for molecules, hard for million-node graphs.
- Need good PEs (sign/basis ambiguity of eigenvectors → SignNet/BasisNet).
- Empirically strong on long-range tasks (LRGB, molecules); well-tuned MPNNs remain competitive elsewhere — an open debate.

## My notes


## Self-test #flashcards/graph-ml
What three encodings does Graphormer use?::Centrality (degree) encoding, spatial encoding (shortest-path distance bias), and edge encoding.
GraphGPS layer structure?::Local message passing + global attention + positional/structural encodings.
Main cost problem of graph transformers?::Full attention is O(N²) in the number of nodes.
