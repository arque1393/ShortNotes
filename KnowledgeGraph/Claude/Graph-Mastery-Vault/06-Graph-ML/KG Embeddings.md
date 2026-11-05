---
tags: [graph-ml, kge, link-prediction]
phase: 3
status: not-started
---
# Knowledge Graph Embeddings (KGE)

> [!summary]
> Embed entities and relations so a **scoring function** $f(h,r,t)$ ranks true triples above false ones → used for KG completion, link prediction, entity similarity.

## Scoring functions
| Model | Score $f(h,r,t)$ | Space |
|---|---|---|
| **TransE** | $-\|h + r - t\|$ | $\mathbb{R}^d$ |
| TransH / TransR | Project onto relation hyperplane/space first | |
| **RotatE** | $-\|h \circ r - t\|$, $|r_i|=1$ (rotation) | $\mathbb{C}^d$ |
| RESCAL | $h^\top M_r t$ | full matrix per relation |
| **DistMult** | $\langle h, r, t\rangle = \sum_i h_i r_i t_i$ | diagonal $M_r$ |
| **ComplEx** | $\mathrm{Re}(\langle h, r, \bar t\rangle)$ | $\mathbb{C}^d$ |
| TuckER | $\mathcal{W}\times_1 h \times_2 r \times_3 t$ | Tucker decomposition |
| ConvE | 2D convolution over reshaped $[h;r]$ | neural |
| R-GCN / CompGCN | GNN encoder + KGE decoder | message passing |
| **NBFNet** | Path-based (Bellman–Ford GNN) | inductive |
| **ULTRA** | Relation graph + NBFNet; zero-shot across KGs | foundation model → [[Graph Foundation Models]] |

## Relation patterns (what can each model represent?)
| Pattern | Example | TransE | DistMult | ComplEx | RotatE |
|---|---|---|---|---|---|
| Symmetry | marriedTo | ✗ | ✓ | ✓ | ✓ |
| Antisymmetry | parentOf | ✓ | ✗ | ✓ | ✓ |
| Inversion | hasPart / partOf | ✓ | ✗ | ✓ | ✓ |
| Composition | brother∘father = uncle | ✓ | ✗ | ✗ | ✓ |

## Training
- Negative sampling (corrupt head/tail), **self-adversarial** sampling (RotatE)
- Losses: margin ranking, logistic, BCE / 1-N scoring (ConvE-style, very strong)
- Regularisation (N3 for ComplEx), large batch, careful hyper-parameter tuning (Ruffinelli et al. 2020: old models are competitive when tuned!)

## Evaluation
- Rank true $t$ against all entities for $(h,r,?)$ (and head side).
- **Filtered** setting: remove other known-true triples from the candidates.
- Metrics: **MRR**, **Hits@1/3/10**.
- Datasets: FB15k-237 and WN18RR (fixed **test leakage** via inverse relations in FB15k/WN18), CoDEx, YAGO3-10, ogbl-wikikg2.

## Code (PyKEEN)
```python
from pykeen.pipeline import pipeline
result = pipeline(dataset="FB15k237", model="RotatE",
                  training_kwargs=dict(num_epochs=100), random_seed=42)
print(result.metric_results.get_metric("both.realistic.inverse_harmonic_mean_rank"))  # MRR
```

## My notes


## Self-test #flashcards/graph-ml
TransE scoring function?::−‖h + r − t‖ (translation in embedding space).
Why can't DistMult model antisymmetric relations?::Its score ⟨h,r,t⟩ is symmetric in h and t.
Which KGE model represents relations as rotations in complex space?::RotatE
What is the filtered evaluation setting?::Removing other known-true triples from the ranking candidates before computing rank.
Why were FB15k-237 and WN18RR created?::To remove test leakage through inverse relations in FB15k and WN18.
Which model performs zero-shot link prediction on unseen KGs?::ULTRA
