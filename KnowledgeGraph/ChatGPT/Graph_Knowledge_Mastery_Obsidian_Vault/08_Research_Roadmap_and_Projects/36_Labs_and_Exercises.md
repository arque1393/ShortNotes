---
title: "Labs and Exercises"
type: chapter
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - labs
  - exercises
  - practice
  - assessment
---
# Labs and Exercises

> [!goal]
> Use a graded laboratory sequence to turn concepts into reusable implementation and research skill.

## How to use the labs

Each lab has four evidence levels:

- **L1 - correct**: passes functional tests;
- **L2 - explained**: assumptions and complexity documented;
- **L3 - evaluated**: compared with baselines and stress cases;
- **L4 - research-ready**: reproducible artifact, error analysis and extension question.

Do not progress by completing only L1.

## Foundation labs

### Lab 1 - graph representation invariants

Implement edge list, adjacency list, adjacency matrix, CSR and COO conversions for directed/undirected multigraphs. Test node order, duplicate edges, self-loops and weights.

**Deliverable:** library + property-based tests + memory/time comparison.

### Lab 2 - traversal and path semantics

Implement BFS, DFS, Dijkstra, Bellman-Ford and A*. Construct counterexamples for negative edges, inconsistent heuristics and all-path explosion.

**Research extension:** benchmark path queries against a graph database query planner.

### Lab 3 - random walks and PageRank

Implement power iteration, personalized PageRank and dangling-node handling. Study convergence, teleportation and hub sensitivity.

### Lab 4 - graph spectra

Compute adjacency/Laplacian eigenvalues for synthetic graphs. Connect spectral gap to mixing/connectivity and test perturbation sensitivity.

### Lab 5 - logic model/countermodel

Translate natural-language rules into FOL/DL fragments. For each claimed entailment, produce proof intuition or countermodel.

## Semantic Web and ontology labs

### Lab 6 - RDF model and serialization

Create a 500-triple dataset in Turtle, JSON-LD, N-Triples and TriG. Round-trip and compare blank-node/canonicalization behavior.

### Lab 7 - SPARQL query suite

Write 40 queries covering basic graph patterns, optional, negation, aggregation, subqueries, property paths, construct and updates. Build expected-result tests.

### Lab 8 - OWL classification

Create necessary and sufficient class definitions, disjointness, inverse/transitive properties and chains. Predict classifications before running a reasoner; inspect surprises.

### Lab 9 - ontology debugging

Deliberately introduce unsatisfiable classes and unintended equivalences. Use explanation tools to find minimal causes.

### Lab 10 - SHACL versus OWL

Represent five requirements in OWL and SHACL. Explain why entailment and validation differ. Test closed shapes, qualified counts and SPARQL constraints.

### Lab 11 - ontology engineering sprint

Run expert interviews or simulate them from documents. Produce ORSD, CQs, definitions, patterns, ontology, tests, release notes and governance.

## Graph database and KG engineering labs

### Lab 12 - Cypher and Gremlin equivalence

Express 20 traversals in both languages. Compare readability, path semantics, plans and portability.

### Lab 13 - query-plan repair

Create five intentionally slow graph queries: missing anchor, Cartesian product, unbounded path, late aggregation and hub explosion. Profile and repair each.

### Lab 14 - dual model

Implement one domain in RDF and LPG. Define mapping and test ten semantically equivalent questions. Record information lost.

### Lab 15 - incremental KG ingestion

Implement snapshot + CDC/event replay, idempotency, watermark, late events, tombstones and rollback. Corrupt a batch and recover.

### Lab 16 - evidence-preserving extraction

Extract entities/events from prose and tables. Store source coordinates, uncertainty and claim status. Evaluate each stage.

### Lab 17 - entity resolution

Measure blocking recall, pair metrics and cluster metrics. Inject common-name collisions and temporal contradictions. Build a review UI or report.

### Lab 18 - KG quality incident

Inject unit, identity, temporal, provenance, authorization and ontology errors. Detect, quarantine, repair and write a postmortem.

## Analytics labs

### Lab 19 - centrality robustness

Run degree, PageRank, harmonic, betweenness and k-core. Compare rank correlation after edge sampling, hub removal and time-window changes.

### Lab 20 - community detection

Compare Leiden/Louvain, Infomap, label propagation and SBM on synthetic planted partitions and real data. Measure stability and resolution behavior.

### Lab 21 - motifs and null models

Count motifs and compare with degree-preserving random graphs. Correct for multiple testing and discuss sampling bias.

### Lab 22 - graph feature value

Predict an outcome using tabular-only, structural-only and combined features with point-in-time correctness. Quantify incremental utility.

## Graph ML labs

### Lab 23 - shallow embeddings

Implement random-walk embedding or use a library. Evaluate node classification/link prediction, compare with degree and spectral baselines.

### Lab 24 - KGE families

Train TransE, DistMult, ComplEx and RotatE. Diagnose relation patterns, negatives, inverse leakage and calibration.

### Lab 25 - GCN from scratch

Implement normalized propagation using sparse PyTorch operations. Match PyG on a small graph and test gradients.

### Lab 26 - GraphSAGE sampling

Measure accuracy, variance, memory and latency for different fanouts. Identify when sampling misses rare edges.

### Lab 27 - GNN diagnostic suite

Use synthetic tasks for WL expressivity, over-smoothing, over-squashing, heterophily and long-range dependencies.

### Lab 28 - heterogeneous graph

Compare collapsed homogeneous GCN, metapath features, R-GCN and HGT. Evaluate rare relation types.

### Lab 29 - temporal graph

Build rolling-window link prediction. Ensure all sampling/features are past-only. Test late event and cold-start behavior.

### Lab 30 - graph transformer

Replicate a small GraphGPS/Graphormer-style model. Ablate positional encodings and global attention.

### Lab 31 - neuro-symbolic constraints

Add soft and hard ontology constraints to a predictor. Measure accuracy, violation, coverage and failure when an axiom is wrong.

## GraphRAG and agent labs

### Lab 32 - retrieval baseline harness

Implement BM25, dense retrieval and fusion over one corpus. Create evidence-labeled questions before adding graph methods.

### Lab 33 - graph retrieval

Implement entity neighborhood, path and personalized PageRank retrieval. Measure evidence recall, latency and hub bias.

### Lab 34 - community GraphRAG

Construct communities and summaries. Evaluate broad synthesis and verify every summary claim against source passages.

### Lab 35 - NL-to-query with validation

Generate SPARQL/Cypher through a typed plan. Parse AST, allowlist operations, set limits and compare result-set accuracy.

### Lab 36 - ontology-grounded tool agent

Build typed actions with preconditions/effects. Compare prompt-only and validator-backed agents on valid/invalid goals.

### Lab 37 - graph memory

Implement episodic and semantic memories, consolidation, temporal supersession and deletion propagation. Test stale-memory failures.

### Lab 38 - multi-agent graph

Represent tasks, artifacts and claims in a coordination graph. Compare against a single agent and fixed pipeline.

### Lab 39 - red team

Attack through prompt injection, poisoned edges, alias collision, unauthorized queries, unbounded paths and false citations. Measure attack success before/after controls.

## Research labs

### Lab 40 - paper claim audit

For one paper, map each headline claim to dataset, metric, baseline and evidence. Identify at least five untested assumptions.

### Lab 41 - exact reproduction

Recreate one table/figure from a graph paper with a clean environment. Document every deviation.

### Lab 42 - robustness extension

Add one realistic split, baseline or perturbation that tests the paper's main claim. Pre-register expected outcomes.

### Lab 43 - negative result report

Write a rigorous report where the proposed graph method does not outperform a simpler baseline. Explain conditions and value.

### Lab 44 - artifact review

Give your repository to another person or fresh container. Track setup failures, undocumented dependencies and result differences.

## Suggested grading rubric

| Dimension | Weight |
|---|---:|
| Correctness and tests | 25% |
| Semantic/problem formulation | 20% |
| Baselines and evaluation | 20% |
| Error/failure analysis | 15% |
| Reproducibility | 10% |
| Communication and documentation | 10% |

Use [[Template - Experiment Note]] for every lab and link the results from a dashboard note.
