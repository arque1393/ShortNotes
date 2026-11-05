---
title: "Portfolio and Research Projects"
type: chapter
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - projects
  - portfolio
  - research
  - architecture
---
# Portfolio and Research Projects

> [!goal]
> Build a sequence of increasingly ambitious systems in which each project proves a distinct layer of graph expertise.

## Project selection rules

- Reuse one or two anchor domains so the KG and evaluation assets compound.
- Every project includes a non-graph or simpler baseline.
- Every generated/inferred fact has status and provenance.
- Freeze a dataset version and release a data card.
- Measure correctness, systems behavior and failure modes.
- Prefer a complete small system over an untestable massive prototype.

## Project 1 - Tested domain ontology

**Level:** foundation, 2-3 weeks.

**Problem:** Convert ambiguous domain language into an explicit, testable conceptual model.

**Architecture:** Protégé + OWL 2 profile + reasoner + SHACL + SPARQL CQ tests + CI.

**Deliverables:** ORSD; 40+ terms with definitions; 25 CQs; examples/counterexamples; modular ontology; shapes; regression tests; HTML/documentation; governance and release notes.

**Metrics:** CQ pass rate; unsatisfiable classes; SHACL precision on fixtures; expert agreement; competency coverage.

**Publishable direction:** Compare ontology design patterns or LLM-assisted ontology proposals against expert/test outcomes.

## Project 2 - Dual RDF and property-graph knowledge platform

**Level:** graph engineering, 3-4 weeks.

**Problem:** Determine whether semantic integration and operational traversal require different projections.

**Architecture:** source data -> canonical mappings -> RDF store/OWL/SHACL -> LPG projection/Neo4j -> API.

**Deliverables:** mapping contract; deterministic IDs; 20 SPARQL and 20 Cypher queries; semantic-equivalence tests; query plans; architecture decision record.

**Metrics:** result equivalence, information loss, latency, update cost, developer effort.

**Publishable direction:** Workload-aware automatic RDF/LPG projection and semantic preservation tests.

## Project 3 - Evidence-first document-to-KG pipeline

**Level:** KG construction, 4-6 weeks.

**Problem:** Extract entities, events and temporal claims from documents without treating model output as truth.

**Architecture:** parser/OCR -> structured chunks -> constrained extractor -> entity linker -> candidate claim graph -> SHACL/rules -> review -> verified KG.

**Datasets:** a legal corpus, technical manuals, program documents, scientific abstracts, or an openly licensed benchmark.

**Metrics:** mention, relation/event and linking P/R/F1; evidence-span accuracy; calibration; review workload; CQ answer quality.

**Deliverables:** annotation guide; gold set; pipeline; review UI/report; error taxonomy; model/data cards.

**Publishable direction:** Ontology-guided extraction, calibrated claim promotion or multimodal table/prose fusion.

## Project 4 - Entity resolution and conflict-aware fusion

**Level:** KG engineering/research, 3-5 weeks.

**Problem:** Consolidate noisy records while avoiding catastrophic false merges.

**Architecture:** normalization -> multi-strategy blocking -> pair model -> constrained clustering -> reversible identity graph -> claim fusion.

**Metrics:** blocking recall; pair/cluster metrics; cost-weighted errors; downstream CQ quality; reviewer minutes per 1,000 records.

**Deliverables:** crosswalk; merge/split history; conflict representation; review protocol; incident drill.

**Publishable direction:** Graph-neighborhood evidence without self-reinforcing errors; consequence-aware review selection.

## Project 5 - Network intelligence case study

**Level:** graph analytics, 3-4 weeks.

**Problem:** Discover structure that changes an operational or scientific decision.

**Architecture:** temporal graph projection -> descriptive profile -> centrality/community/core/motif -> null models -> decision report.

**Datasets:** OGB/citation, LDBC synthetic social data, Wikidata subset, open transport, fraud-like synthetic, or domain-safe internal data.

**Metrics:** stability, null-model significance, temporal robustness, decision utility.

**Deliverables:** notebook/report; reproducible data pipeline; limitations; visualization; stakeholder summary.

**Publishable direction:** Stability-aware graph analytics under incomplete/sampled graphs.

## Project 6 - Leakage-resistant KG completion benchmark

**Level:** graph ML, 4-5 weeks.

**Problem:** Compare KGE models under realistic entity, relation and temporal generalization.

**Architecture:** benchmark harness + PyKEEN/custom models + rule/path baselines + type constraints.

**Datasets:** FB15k-237/WN18RR for sanity plus OGB/domain KG for realism.

**Metrics:** filtered MRR/Hits@K; relation slices; calibration; unseen-entity/relation; runtime; candidate review utility.

**Deliverables:** split generator; negative sampler; models; error analysis; reproducibility package.

**Publishable direction:** Better realistic negatives, relation-disjoint evaluation or ontology-constrained calibration.

## Project 7 - Heterogeneous temporal GNN system

**Level:** advanced graph ML, 5-7 weeks.

**Problem:** Predict future risk/link/outcome using multiple entity and relation types.

**Architecture:** point-in-time graph builder -> feature store -> MLP/graph-feature baselines -> R-GCN/HGT/TGN-like model -> batch/online scoring.

**Metrics:** PR-AUC/ranking at capacity; calibration; seen/unseen nodes; relation/degree/time slices; update latency; cost.

**Deliverables:** temporal dataset card; four baselines; ablations; monitoring plan.

**Publishable direction:** Cold start, delayed labels, temporal memory consistency or heterophily.

## Project 8 - Neuro-symbolic decision system

**Level:** advanced research, 4-6 weeks.

**Problem:** Combine noisy learned predictions with hard domain constraints and inspectable derivations.

**Architecture:** neural candidate predictor -> candidate claim state -> rule/OWL/SHACL validator -> proof/evidence -> decision API.

**Metrics:** predictive quality; hard/soft violation; coverage/abstention; proof validity; robustness to wrong/missing axioms.

**Deliverables:** symbolic-only, neural-only and hybrid comparison; constraint ablations; counterexample suite.

**Publishable direction:** Learning when to trust/relax ontology constraints; proof-carrying predictions.

## Project 9 - GraphRAG benchmark, not demo

**Level:** LLM/KG, 4-6 weeks.

**Problem:** Determine exactly which question types benefit from graph retrieval.

**Architecture:** BM25 + vector + fusion + exact query + entity/path/PPR graph retrieval + community summaries + router.

**Dataset:** 100-300 evidence-labeled questions across factual, multi-hop, global, temporal and unanswerable categories.

**Metrics:** evidence recall/NDCG; answer correctness/faithfulness; citation P/R; index/query cost; p95 latency.

**Deliverables:** benchmark harness; controlled generator; ablations; error taxonomy; deployment decision matrix.

**Publishable direction:** Query-type routing, graph quality sensitivity, incremental updates or cost-aware retrieval.

## Project 10 - Ontology-grounded agent with safe tools

**Level:** agentic AI, 5-7 weeks.

**Problem:** Build an agent that plans over explicit types and constraints, executes authorized tools and produces auditable answers/actions.

**Architecture:** entity resolver -> ontology/schema retriever -> typed planner -> policy validator -> read/write separated tools -> evidence graph -> claim verifier.

**Metrics:** task success; plan validity; tool/parameter accuracy; unauthorized/invalid action rate; recovery; citations; cost.

**Deliverables:** tool ontology; 100 scenarios; red-team suite; traces; canary/rollback plan; comparison to prompt-only agent.

**Publishable direction:** Typed planning, ontology-version robustness, verification-guided replanning or minimal proof contexts.

## Project 11 - Knowledge graph research copilot

**Level:** capstone, 8-12 weeks.

**Problem:** Help a researcher map a literature field, trace claims, reproduce experiments and discover gaps.

**Architecture:** paper parser -> citation/claim/method/dataset graph -> ontology -> vector + graph retrieval -> agent tools -> experiment/artifact graph.

**Features:** claim-to-evidence links; paper comparison; dataset/model lineage; contradiction detection; research-gap queries; reproducibility checklist.

**Metrics:** claim extraction; evidence retrieval; comparison correctness; researcher time saved; hallucination/citation rate; coverage.

**Publishable direction:** Scientific claim graphs, contradiction-aware retrieval, reproducibility prediction or graph-guided hypothesis generation.

## Project 12 - Domain digital knowledge twin

**Level:** capstone/research platform, 8-16 weeks.

**Problem:** Maintain a temporally valid, provenance-rich model of entities, events, policies and decisions for one real domain.

**Architecture:** batch/stream sources -> canonical ontology/KG -> temporal/provenance layer -> analytics/ML -> GraphRAG/agent -> governance and observability.

**Required qualities:** bitemporal facts; reversible identity; quality SLA; access policy; model and ontology versions; incident response; decision feedback.

**Metrics:** data freshness/quality; CQ coverage; model utility; agent safety; operational cost; stakeholder outcomes.

**Publishable direction:** Co-evolution of ontology, KG, predictive models and agents under changing policy/data.

## Project documentation template

Every repository contains:

```text
README.md
architecture/
data/README.md and DATA_CARD.md
ontology/ or schema/
src/
tests/
experiments/
reports/
model_card.md (when ML)
threat_model.md (when agent/user data)
reproducibility.md
LICENSE
```

## Portfolio presentation

For each project, create:

1. one-sentence problem and why relationships/semantics matter;
2. architecture diagram;
3. 3-5 design decisions and rejected alternatives;
4. quantitative result with baseline;
5. one important failure;
6. demo or screenshots;
7. reproducibility command;
8. next research question.

A portfolio that shows diagnosis and tradeoffs is stronger than twelve polished screenshots.
