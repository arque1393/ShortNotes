---
tags: [network-science, gds, link-prediction]
phase: 1
status: not-started
---
# Link Prediction Heuristics

> [!summary]
> Predict missing or future edges. Simple heuristics are **strong baselines** that many GNN papers fail to beat fairly — always include them.

## Classic scores for pair $(x,y)$
| Score | Formula |
|---|---|
| Common neighbours | $|N(x)\cap N(y)|$ |
| Jaccard | $\frac{|N(x)\cap N(y)|}{|N(x)\cup N(y)|}$ |
| Adamic–Adar | $\sum_{z\in N(x)\cap N(y)} \frac{1}{\log k_z}$ |
| Resource allocation | $\sum_{z\in N(x)\cap N(y)} \frac{1}{k_z}$ |
| Preferential attachment | $k_x \cdot k_y$ |
| Katz | $\sum_{l=1}^{\infty}\beta^l (A^l)_{xy}$ |
| PPR / SimRank | Global, random-walk based |

## Learned approaches
- Embedding + decoder: [[Node Embeddings]] → dot product / Hadamard + classifier.
- GNN link prediction: GAE/VGAE; **SEAL** (subgraph classification + labeling trick); **NBFNet**; NCN/NCNC (neighbour-aware).
- KG link prediction → [[KG Embeddings]].

## Evaluation pitfalls
> [!warning]
> - **Leakage:** remove test edges from the graph before computing features/embeddings.
> - **Negative sampling** strategy changes results drastically; use hard negatives.
> - **Temporal split** for evolving graphs, not random split.
> - Report **Hits@K / MRR** (ranking) rather than only AUC (inflated by easy negatives).

## Code
```python
import networkx as nx
G = nx.karate_club_graph()
preds = nx.adamic_adar_index(G, [(0, 33), (5, 16)])
print(list(preds))
```

## My notes


## Self-test #flashcards/network-science
Adamic–Adar formula?::Σ over common neighbours z of 1 / log(degree(z)).
Why is AUC often misleading for link prediction?::Random negatives are too easy; ranking metrics like Hits@K/MRR with hard negatives are more informative.
What is the "labeling trick" (SEAL)?::Label nodes by their distance to the target pair so the GNN can distinguish the target link's structural role.
Most important evaluation rule for link prediction features?::Remove test edges before computing features/embeddings to avoid leakage.
