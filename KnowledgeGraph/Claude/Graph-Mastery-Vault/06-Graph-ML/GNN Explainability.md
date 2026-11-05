---
tags: [graph-ml, xai, trust]
phase: 3
status: not-started
---
# GNN Explainability & Trust

> [!summary]
> Explain *which subgraph and features* drove a GNN prediction. Critical in fraud, healthcare, finance — and a natural fit with KG paths for human-readable explanations.

## Methods
| Method | Idea |
|---|---|
| Gradient/saliency | Gradients w.r.t. edges/features |
| **GNNExplainer** (2019) | Optimise soft edge + feature masks maximising mutual information with prediction, with sparsity regularisation |
| PGExplainer | Learn a parametric mask generator → explains many instances fast |
| **SubgraphX** | Monte Carlo tree search over subgraphs, scored with Shapley values |
| Counterfactual (CF-GNNExplainer) | Minimal edge deletions that flip the prediction |
| Path-based | Explain link predictions with KG paths (NBFNet, rule-based) |

## Evaluating explanations
Fidelity+ / Fidelity− (drop in prediction when removing/keeping the explanation), sparsity, stability; synthetic ground-truth benchmarks (BA-Shapes).

## Related trust topics
Uncertainty (conformalized GNNs), robustness to adversarial edge perturbations, fairness, privacy (DP-GNNs).

Survey: Yuan et al., "Explainability in Graph Neural Networks: A Taxonomic Survey" (TPAMI 2022).

## My notes


## Self-test #flashcards/graph-ml
What does GNNExplainer optimise?::Sparse soft masks over edges and features that preserve the prediction (maximising mutual information).
SubgraphX scores subgraphs using…?::Shapley values, searched with Monte Carlo tree search.
What does fidelity measure?::How much the prediction changes when the explanation is removed or kept alone.
