---
title: "First 30, 60 and 90 Days"
type: chapter
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - 30-60-90
  - action-plan
  - roadmap
  - onboarding
---
# First 30, 60 and 90 Days

> [!goal]
> Convert ambition into a concrete first quarter with daily artifacts, early feedback and no dependency gaps.

## Day 0: create the workspace

- Clone/copy this vault into Obsidian.
- Create a Git repository with `notes/`, `labs/`, `data/`, `src/`, `tests/`, `experiments/`, `reports/`.
- Copy [[Template - Weekly Review]], [[Template - Paper Note]] and [[Template - Experiment Note]].
- Select one anchor domain: automotive/dealer coaching, legal research, scientific literature or another domain you can access ethically.
- Write 20 competency questions: 8 factual, 4 multi-hop, 3 temporal, 2 aggregate, 2 explanatory, 1 unanswerable.

## Days 1-7: field map and graph fundamentals

### Day 1

Read [[00_Graph_Field_Mastery_Home]] and [[03_Glossary_of_Graph_Fields]]. Write a one-page answer to: "Why does this problem need a graph?"

### Day 2

Read graph representations in [[01_Graph_Mathematics_and_Representations]]. Implement adjacency list, edge list, matrix and CSR conversions.

### Day 3

Implement BFS/DFS, connected components and topological sorting. Add unit tests for disconnected graphs, self-loops and directed cycles.

### Day 4

Implement Dijkstra and compare with NetworkX. Create a counterexample showing why negative edges break Dijkstra.

### Day 5

Derive PageRank and implement power iteration. Compare convergence at three damping values.

### Day 6

Read [[03_Logic_Knowledge_Representation_and_Semantics]]. Write examples separating truth, entailment, validation, absence and contradiction.

### Day 7

Teach back the field map in a ten-minute recording. Complete a weekly review and fix unclear explanations.

## Days 8-14: RDF and SPARQL

- Model 50-100 domain entities in Turtle.
- Use stable IRIs, labels, datatypes and named graphs.
- Parse and query with RDFLib.
- Write 15 SPARQL queries covering joins, `OPTIONAL`, `FILTER`, `UNION`, aggregation and property paths.
- Add expected-result tests.
- Model one statement with time and provenance using an event/assertion pattern.
- Write a note comparing RDF graph, RDF dataset and property graph.

**Day-14 checkpoint:** From an empty repository, you can create and query a small RDF KG without copying a tutorial.

## Days 15-21: ontology engineering

- Draft an Ontology Requirements Specification with scope, stakeholders and CQs.
- Build the core taxonomy and relations in Protégé.
- Add textual definitions, examples and counterexamples.
- Add high-confidence disjointness and restrictions.
- Run a reasoner and inspect explanations.
- Create at least 10 SHACL shapes.
- Add test fixtures that must pass and fail.

Use [[08_Ontology_Engineering_Methodology]], [[07_Description_Logics_and_OWL_2]] and [[09_SHACL_SKOS_Rules_Provenance_and_Identity]].

**Day-21 checkpoint:** Ontology v0.1 is consistent; every term exists for a CQ, integration requirement or explicit reuse goal.

## Days 22-30: property graph and first mini-project

- Load equivalent data into Neo4j.
- Write uniqueness constraints and idempotent `MERGE` ingestion.
- Write 15 Cypher queries, including a bounded path, aggregation and update.
- Profile three queries and record plans.
- Compare five CQs in SPARQL and Cypher.
- Publish Mini-Project A: "One domain, two graph models."

### Day-30 deliverables

- [ ] Field map and study log;
- [ ] tested graph algorithms repository;
- [ ] RDF dataset and SPARQL suite;
- [ ] OWL ontology + SHACL + reasoner tests;
- [ ] Neo4j model + Cypher suite;
- [ ] RDF-vs-LPG architecture note;
- [ ] 5-minute demo video;
- [ ] list of 10 knowledge gaps.

## Days 31-45: construction and identity

### Week 5: structured data pipeline

- Ingest PostgreSQL/CSV/API data into a raw layer.
- Define deterministic identifiers and mappings.
- Store source-record provenance and batch versions.
- Implement incremental replay and deletion/end-dating.
- Reconcile source counts and keys.

### Week 6: text extraction

- Select 100-200 documents.
- Define an extraction schema and annotate 30-50 documents.
- Implement schema-constrained extraction with evidence spans.
- Evaluate mention, relation/event and temporal fields separately.
- Store candidate claims, not accepted facts.

### Days 43-45: identity

- Normalize and block candidate entities.
- Build deterministic and supervised/probabilistic matching baselines.
- Evaluate blocking recall and pair metrics.

## Days 46-60: quality, analytics and Project 1 release

### Week 7

- Add SHACL/business quality gates.
- Build provenance and freshness metrics.
- Test ontology/mapping changes with CI.
- Run an entity merge/split incident drill.

### Week 8

- Profile topology with NetworkX/Neo4j GDS.
- Compare PageRank, betweenness, k-core and Leiden communities.
- Test ranking/community stability across seeds and edge perturbations.
- Write limitations and null-model comparison.

### Day-60 deliverables

- [ ] replayable structured/text KG pipeline;
- [ ] entity-resolution evaluation;
- [ ] quality dashboard/report;
- [ ] graph analytics notebook with stability tests;
- [ ] Project 1 public-quality README and architecture diagram;
- [ ] one 8-12 page technical report;
- [ ] 12 paper notes and literature graph.

> [!checkpoint] Day 60
> You are no longer only learning syntax. You can construct, validate and analyze a small governed KG and explain where its facts came from.

## Days 61-75: KGE and GNN foundations

### Week 9: KGE

- Use a domain dataset or FB15k-237/WN18RR.
- Train TransE, DistMult and ComplEx.
- Implement filtered ranking and type-constrained negatives.
- Report per-relation MRR/Hits and investigate 50 errors.
- Add a rule/path baseline.

### Week 10: GNN

- Implement GCN and GraphSAGE in PyG.
- Add MLP, degree and label-propagation baselines.
- Use grouped or temporal splits.
- Measure degree-stratified performance and feature/topology ablations.

### Days 73-75

Read one seminal GNN paper and one modern evaluation/foundation-model paper using [[39_Paper_Reading_Reproduction_and_Writing]]. Reproduce one table or figure.

## Days 76-90: GraphRAG and ontology-grounded agent

### Week 11: retrieval benchmark

Implement:

- BM25;
- dense vector retrieval;
- reciprocal-rank fusion;
- entity-neighborhood graph retrieval;
- exact SPARQL/Cypher route.

Create 50 questions across fact, multi-hop, global and temporal categories. Label source evidence.

### Week 12: agent

- Define typed tool schemas and permissions.
- Resolve entities and retrieve ontology/schema subgraphs.
- Generate an intermediate plan before queries.
- Validate query AST and bound paths/results.
- Return claim-level citations.
- Add unanswerable, unauthorized and prompt-injection tests.

### Day-90 deliverables

- [ ] KGE benchmark with leakage analysis;
- [ ] GNN benchmark with strong baselines;
- [ ] hybrid retrieval/GraphRAG benchmark;
- [ ] ontology-grounded, read-only agent;
- [ ] adversarial and policy test suite;
- [ ] portfolio page linking all artifacts;
- [ ] selected research cluster and 25-paper map;
- [ ] next 6-month plan using [[34_12_to_18_Month_Curriculum]].

## Rules for the first 90 days

1. Use one anchor domain so concepts accumulate instead of resetting.
2. Keep raw data and provenance; never edit source truth in-place.
3. Add a non-graph baseline to every ML/retrieval experiment.
4. Use expected outputs and tests from the first week.
5. Read standards/papers, but build weekly.
6. Publish negative results and failure cases.
7. Do not start graph foundation-model research before you can diagnose simple graph leakage and query semantics.
8. At least once per week, explain a concept without notes.

## Your Day-90 self-assessment

Score 0-3:

| Skill | 0 | 1 | 2 | 3 |
|---|---|---|---|---|
| Formal semantics | none | definitions | working ontology | reasoner/debug mastery |
| Graph systems | none | query syntax | profiled pipeline | operational tradeoffs |
| KG engineering | none | static graph | replayable provenance | governed lifecycle |
| Analytics | none | algorithm use | assumptions/stability | decision impact |
| Graph ML | none | library run | leakage-safe comparison | reproduction/extension |
| Agentic graph AI | none | prompt demo | typed evidence tools | secure evaluated system |
| Research | none | paper summaries | reproduction | novel controlled claim |

Any score below 2 becomes the next quarter's first dependency.
