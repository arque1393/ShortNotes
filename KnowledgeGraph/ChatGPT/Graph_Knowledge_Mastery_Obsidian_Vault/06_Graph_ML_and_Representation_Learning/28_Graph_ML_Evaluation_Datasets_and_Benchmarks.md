---
title: "Graph ML Evaluation, Datasets and Benchmarks"
type: chapter
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - evaluation
  - benchmark
  - dataset
  - reproducibility
  - graph-ml
---
# Graph ML Evaluation, Datasets and Benchmarks

> [!goal]
> Design evaluations that measure deployment-relevant generalization rather than benchmark familiarity or structural leakage.

## 1. Define the generalization claim

Graph ML settings include:

- transductive: test nodes share one graph with training nodes;
- inductive-node: new nodes in a known domain;
- inductive-graph: unseen graphs;
- temporal: future nodes/edges/events;
- relation/domain transfer;
- zero/few-shot task transfer.

State the claim before choosing a dataset or split.

## 2. Split leakage unique to graphs

Even with disjoint labels, information flows through edges. Common leakage:

- future edges present during historical prediction;
- target edge retained in message passing;
- reciprocal/inverse relation in training;
- same entity/near duplicate in train and test;
- graph-level duplicates/scaffolds across split;
- normalization/statistics fit on full graph;
- negative samples that are trivially impossible;
- labels encoded in node IDs, types or source process;
- test neighborhoods used during unsupervised pretraining without disclosure.

Create each split's graph and features from the information available at its decision time.

## 3. Metrics by task

### Node/graph classification

Accuracy for balanced multiclass; macro-F1 for class imbalance; ROC-AUC or PR-AUC depending prevalence; calibration; subgroup metrics.

### Link/KG prediction

MRR, Hits@K, ranking utility, filtered policy, negative-sampling policy and calibration. Report per relation and degree.

### Ranking/recommendation

NDCG@K, MAP, recall@K, precision@K, coverage, novelty and decision utility.

### Regression

MAE/RMSE, calibration intervals, rank correlation and domain-specific tolerance.

### Clustering/community

Internal quality plus stability and external labels only when they truly represent communities. Modularity alone is not ground truth.

### Systems

Training/inference time, throughput, peak memory, preprocessing, communication, energy/resource and cost.

## 4. Baseline ladder

- constant/frequency/popularity;
- feature-only MLP or gradient boosting;
- topology-only degree/heuristics;
- label propagation where legitimate;
- classical graph features + simple model;
- shallow embedding;
- canonical GNN/KGE;
- proposed model.

Equalize data, tuning budget and compute reporting. A weak baseline invalidates a sophisticated comparison.

## 5. Statistical reporting

- multiple random seeds;
- mean, standard deviation and confidence intervals;
- paired tests or bootstrap over appropriate units;
- multiple-comparison correction when many models/tasks;
- effect size, not only p-value;
- learning curves and sensitivity;
- failure counts and variance across time/domains.

Graph observations are dependent, so naive per-node confidence intervals may be misleading. Resample graphs, time blocks or clusters where appropriate.

## 6. Dataset families

### OGB

The Open Graph Benchmark provides standardized loaders, splits and evaluators for node, link and graph property prediction. It includes large datasets such as `ogbn-papers100M` and KG completion datasets such as `ogbl-wikikg2`.

### Knowledge-graph benchmarks

- FB15k-237;
- WN18RR;
- YAGO3-10;
- NELL variants;
- OGB `ogbl-wikikg2` and `ogbl-biokg`;
- temporal ICEWS/GDELT variants.

Document licenses, construction artifacts, inverse relations and whether entities/text overlap with pretrained LLM corpora.

### Molecules and proteins

OGB molecule tasks, ZINC, QM9 and domain datasets. Use scaffold or time splits where chemical generalization is intended.

### Citation/social/product graphs

Cora/Citeseer/PubMed are useful for teaching but too small and overused for strong modern claims. Prefer realistic OGB or domain datasets with temporal splits.

## 7. Graph-system benchmarks

Do not confuse ML benchmarks with database benchmarks.

- LDBC Social Network Benchmark: transactional/analytical graph workloads;
- LDBC/Graph Data Council FinBench: financial transactional workload;
- Graphalytics: BFS, PageRank, WCC, label propagation, local clustering coefficient and SSSP;
- WatDiv: diverse RDF/SPARQL workload;
- Berlin SPARQL Benchmark and other RDF suites.

Use reference outputs and benchmark fair-use rules. Add application-specific workloads without presenting vendor-biased microbenchmarks as universal truth.

## 8. Dataset documentation

A graph dataset card should include:

- entity/edge definitions;
- source and collection process;
- temporal range and cutoff;
- missingness/sampling;
- node/edge counts by type;
- degree/component distributions;
- labels and annotation process;
- split generation;
- known leakage/artifacts;
- privacy/licensing;
- intended/prohibited use;
- update/version history.

Use [[Template - Dataset Card]].

## 9. Reproducibility checklist

- [ ] exact data version/checksums;
- [ ] preprocessing/projection code;
- [ ] split files and seed;
- [ ] model and parameter count;
- [ ] search space/budget;
- [ ] environment lockfile/container;
- [ ] hardware and runtime;
- [ ] checkpoint and evaluation code;
- [ ] negative sampler/filter policy;
- [ ] repeated-run raw metrics;
- [ ] license and data-access instructions;
- [ ] ablations and failed configurations.

## 10. Stress and robustness tests

- edge/node deletion and noisy features;
- hub removal and degree shift;
- unseen relation/entity types;
- temporal drift;
- adversarial or injected edges;
- missing modalities;
- subgroup/source shift;
- graph size scaling;
- ontology/schema version change;
- calibration under abstention.

## 11. Benchmark saturation and research value

Small gains on saturated datasets may reflect tuning noise. Strong research evaluates a clear hypothesis across multiple relevant settings, explains failures and releases artifacts. Prefer a smaller controlled claim over a universal claim unsupported by transfer tests.

## 12. Laboratory

Create a benchmark harness that evaluates one heuristic, one conventional model, one KGE/GNN and one proposed hybrid on:

- random split (for contrast only);
- grouped/entity-disjoint split;
- temporal split;
- corrupted/shifted test set.

Report predictive, calibration and systems metrics plus a data card. Explain how conclusions change by split.

## Mastery checklist

- [ ] My split exactly matches the generalization claim.
- [ ] Full-graph preprocessing cannot see forbidden future/test data.
- [ ] Baselines, tuning budgets and system costs are fair.
- [ ] I report uncertainty and meaningful slices.
- [ ] Dataset artifacts and licenses are documented.

## Sources and next reading

- [Open Graph Benchmark](https://ogb.stanford.edu/)
- [Graph Data Council benchmarks](https://ldbcouncil.org/benchmarks/)
- [Graphalytics](https://ldbcouncil.org/benchmarks/graphalytics/)
- [Papers with Code graph benchmarks](https://paperswithcode.com/area/graphs)
- [[39_Paper_Reading_Reproduction_and_Writing]]
