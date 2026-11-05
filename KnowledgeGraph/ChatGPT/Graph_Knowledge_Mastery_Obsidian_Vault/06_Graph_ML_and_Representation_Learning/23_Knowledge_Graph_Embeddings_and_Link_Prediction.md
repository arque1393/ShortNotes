---
title: "Knowledge Graph Embeddings and Link Prediction"
type: chapter
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - knowledge-graph-embedding
  - link-prediction
  - representation-learning
  - kge
---
# Knowledge Graph Embeddings and Link Prediction

> [!goal]
> Understand KGE model families, train/evaluate them without leakage, and decide when a score is useful despite not being logical proof.

## 1. Task formulation

A KG contains triples $(h,r,t)$. A KGE model maps entities and relations to vectors and defines a score $f(h,r,t)$, where higher plausibility should correspond to true or useful triples.

Common tasks:

- tail prediction $(h,r,?)$;
- head prediction $(?,r,t)$;
- relation prediction $(h,?,t)$;
- triple classification;
- entity alignment;
- ranking candidates for human review.

KGE scores estimate patterns in observed data. They do not establish truth, causality or OWL entailment.

## 2. Model families

### Translational

**TransE** seeks $\mathbf{h}+\mathbf{r}\approx\mathbf{t}$.

$$f=-\|\mathbf{h}+\mathbf{r}-\mathbf{t}\|.$$

Simple and scalable; weak for some one-to-many, symmetry and complex relation patterns. TransH/TransR/RotatE-style models increase expressiveness.

### Bilinear/tensor factorization

**DistMult** scores a tri-linear product and is symmetric in head/tail for a relation, limiting asymmetric relations.

$$f=\langle\mathbf{h},\mathbf{r},\mathbf{t}\rangle.$$

**ComplEx** uses complex embeddings and can represent asymmetry. **RESCAL** uses full relation matrices but is parameter-heavy. **TuckER** factorizes a shared core tensor.

### Geometric and box/cone models

Rotations represent compositional patterns; hyperbolic embeddings suit hierarchy; boxes/cones model sets and partial order. Select based on relation patterns, not novelty.

### Neural and graph-based

Convolutional scoring, relation-aware GNNs and path encoders combine entity features/topology with triple scoring. They may support inductive entities better than pure lookup embeddings.

## 3. Relation patterns

Test models against:

- symmetry/antisymmetry;
- inverse relations;
- composition;
- hierarchy/subsumption;
- one-to-one, one-to-many and many-to-many;
- temporal qualifiers;
- n-ary context.

A model can rank well overall while failing a critical relation type. Report per-relation and arity-stratified performance.

## 4. Training objectives

Typical losses compare positive triples to corrupted negatives:

$$\mathcal{L}=-\log\sigma(f(h,r,t))-\sum_{i}\log\sigma(-f(h_i',r,t_i')).$$

Options include margin ranking, logistic/BCE, softmax and self-adversarial negative sampling.

### Negative sampling problem

A corrupted triple may be unobserved but true. Improve with:

- type/domain-range constrained negatives;
- filtered known positives;
- temporal validity;
- hard-negative mining;
- adversarial sampling;
- relation-specific strategies.

Do not evaluate on the same negatives used to tune heuristics.

## 5. Transductive versus inductive

Classic KGE assigns a learned vector to each entity, so unseen entities cannot be represented directly. Inductive approaches derive representations from attributes, text, neighborhoods or relation structures.

Define the deployment setting:

- new edges among known entities;
- new entities with known relation types;
- new relation types;
- entirely new KGs/domains;
- zero/few-shot transfer.

The last two motivate current KG foundation-model research but remain substantially harder.

## 6. Evaluation

For each test triple, rank the true entity against candidates. Standard metrics:

- mean reciprocal rank (MRR);
- Hits@K;
- mean rank, usually less robust;
- PR-AUC/ROC-AUC for explicit binary settings;
- calibration and utility for thresholded decisions.

**Filtered evaluation** removes other known true triples from corrupt candidates. It still assumes the KG's observed positives approximate truth and can overstate performance when many truths are missing.

### Leakage traps

- inverse/redundant relations crossing splits;
- test facts encoded through reciprocal edges;
- random split of temporal facts;
- entity aliases duplicated across splits;
- text descriptions containing the target relation;
- negative candidates that violate obvious type constraints;
- benchmark artifacts such as those exposed in WN18/FB15k.

Use WN18RR and FB15k-237 rather than their leakage-prone predecessors for basic comparison, while recognizing their remaining limitations.

## 7. Rule and ontology integration

Use ontology constraints to:

- generate type-correct negatives;
- regularize subsumption/disjointness;
- filter impossible predictions;
- explain candidates with paths/rules;
- combine symbolic entailment and learned ranking.

Do not force uncertain domain assumptions as hard constraints. Separate logical impossibility from low empirical probability.

## 8. Temporal and qualified KGs

For $(h,r,t,\tau)$, models may encode timestamps, intervals or event sequences. Qualified/n-ary facts require hyper-relational models, statement nodes or qualifier-aware encoders.

Evaluation must respect time and avoid using future graph structure. Report seen/unseen entity and relation subsets separately.

## 9. Practical library workflow

Useful libraries include PyKEEN, DGL-KE and custom PyTorch/PyG implementations. A strong experiment includes:

- exact split and reciprocal-edge policy;
- type constraints;
- negative sampler;
- seed/hyperparameter search budget;
- parameter count and runtime;
- simple frequency/path baselines;
- per-relation results;
- confidence intervals;
- top prediction error review.

## 10. When KGE is appropriate

Use KGE for scalable candidate ranking, recommendations, similarity, feature learning and completion hypotheses. Prefer rules/queries when answers must follow explicit semantics. Prefer retrieval/text encoders when entity descriptions dominate and topology is weak. Consider a hybrid for human-verified candidate generation.

## 11. Laboratory

On FB15k-237 or a domain KG, compare TransE, DistMult, ComplEx, RotatE and a rule/path baseline. Add:

- type-constrained negatives;
- temporal or relation-disjoint split if available;
- per-relation analysis;
- filtered and sampled-realistic evaluation;
- calibration of top-k candidates;
- human inspection of 100 high-confidence errors.

Then add one ontology-derived constraint and measure both benefit and failure.

## Mastery checklist

- [ ] I can derive the score and limitation of major KGE families.
- [ ] I define transductive/inductive/unseen-relation settings explicitly.
- [ ] My negatives and splits match deployment.
- [ ] I report per-relation results and strong baselines.
- [ ] I never call a KGE score a proof.

## Sources and next reading

- [Knowledge Graph Embedding survey](https://arxiv.org/abs/2002.00388)
- [PyKEEN documentation](https://pykeen.readthedocs.io/)
- [OGB link prediction datasets](https://ogb.stanford.edu/docs/linkprop/)
- [[25_Relational_Heterogeneous_and_Temporal_GNNs]]
- [[27_Neuro_Symbolic_AI_and_Logical_Learning]]
