---
title: "Graph Mastery Progress Dashboard"
type: dashboard
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - dashboard
  - progress
  - roadmap
---
# Graph Mastery Progress Dashboard

> [!goal]
> Track evidence of mastery, not time spent. A chapter is complete only when you can explain the ideas, implement the central methods and diagnose a failure without copying a tutorial.

## Current cycle

| Field | Value |
|---|---|
| Start date | |
| Current week | |
| Current chapter | |
| Current lab | |
| Current project | |
| Research theme | |
| Weekly deep-work target | 12-18 hours |

## Completion legend

- [ ] not started
- [/] reading/implementing
- [x] mastery evidence produced

Obsidian may render `[/]` according to your theme; the raw Markdown remains portable.

## Part I - Foundations

- [ ] [[01_Graph_Mathematics_and_Representations]]
- [ ] [[02_Graph_Algorithms_and_Complexity]]
- [ ] [[03_Logic_Knowledge_Representation_and_Semantics]]
- [ ] [[04_Uncertainty_Causality_and_Probabilistic_Graphs]]

**Gate artifact:** implement a typed graph library, benchmark BFS/Dijkstra/components and write a two-page explanation of OWA, CWA and entailment.

## Part II - Semantic Web and ontology

- [ ] [[05_RDF_RDFS_and_Linked_Data]]
- [ ] [[06_SPARQL_Query_and_Federation]]
- [ ] [[07_Description_Logics_and_OWL_2]]
- [ ] [[08_Ontology_Engineering_Methodology]]
- [ ] [[09_SHACL_SKOS_Rules_Provenance_and_Identity]]
- [ ] [[10_Upper_Ontologies_and_Design_Patterns]]
- [ ] [[11_Reasoners_and_Semantic_System_Architecture]]

**Gate artifact:** a versioned ontology with at least 20 tested competency questions, SHACL profiles, example data, reasoner checks and documentation.

## Part III - Graph databases and systems

- [ ] [[12_Property_Graphs_Cypher_GQL_and_Gremlin]]
- [ ] [[13_Graph_Database_Internals_and_Distributed_Systems]]
- [ ] [[14_RDF_vs_Property_Graphs_and_Interoperability]]

**Gate artifact:** load the same domain into RDF and property-graph systems, express equivalent workloads, inspect query plans and write an ADR for the chosen architecture.

## Part IV - KG construction and quality

- [ ] [[15_KG_Construction_from_Structured_Data]]
- [ ] [[16_KG_Construction_from_Text_and_Multimodal_Data]]
- [ ] [[17_Entity_Resolution_and_Knowledge_Fusion]]
- [ ] [[18_KG_Quality_Governance_and_Evolution]]
- [ ] [[19_Temporal_Spatial_Probabilistic_and_Hyper_KGs]]

**Gate artifact:** a repeatable KG pipeline with deterministic identity, provenance, ER evaluation, temporal facts, quality dashboard and reversible corrections.

## Part V - Graph analytics and data science

- [ ] [[20_Network_Science_and_Graph_Analytics]]
- [ ] [[21_Graph_Data_Science_Workflows]]
- [ ] [[22_Graph_Algorithm_Selection_Guide]]

**Gate artifact:** one decision-focused graph analysis with null models, sensitivity analysis, non-graph baseline and a clear statement of what is not causal.

## Part VI - Graph ML

- [ ] [[23_Knowledge_Graph_Embeddings_and_Link_Prediction]]
- [ ] [[24_Graph_Neural_Network_Foundations]]
- [ ] [[25_Relational_Heterogeneous_and_Temporal_GNNs]]
- [ ] [[26_Graph_Transformers_and_Graph_Foundation_Models]]
- [ ] [[27_Neuro_Symbolic_AI_and_Logical_Learning]]
- [ ] [[28_Graph_ML_Evaluation_Datasets_and_Benchmarks]]

**Gate artifact:** reproduce one KGE and one GNN result with leakage-safe splits, strong baselines, multiple seeds, ablations and relation/degree/time slices.

## Part VII - LLMs, GraphRAG and agents

- [ ] [[29_Knowledge_Graph_and_LLM_Integration]]
- [ ] [[30_GraphRAG_and_Hybrid_Retrieval]]
- [ ] [[31_Ontology_Grounded_Agents]]
- [ ] [[32_Graph_Memory_Planning_and_Multi_Agent_Systems]]
- [ ] [[33_Safety_Evaluation_and_Production_Operations]]

**Gate artifact:** a hybrid agent that routes among exact graph query, vector/text retrieval and rules; every material claim has evidence and the system has adversarial, authorization, cost and latency tests.

## Part VIII - Research execution

- [ ] [[34_12_to_18_Month_Curriculum]]
- [ ] [[35_First_30_60_90_Days]]
- [ ] [[36_Labs_and_Exercises]]
- [ ] [[37_Portfolio_and_Research_Projects]]
- [ ] [[38_Research_Frontiers_and_Open_Problems]]
- [ ] [[39_Paper_Reading_Reproduction_and_Writing]]
- [ ] [[40_Career_and_Research_Positioning]]

## Reference readiness

- [ ] [[41_Toolchain_Setup]]
- [ ] [[42_Annotated_Bibliography]]
- [ ] [[43_Courses_and_Video_Lectures]]
- [ ] [[44_Papers_by_Topic]]
- [ ] [[45_Datasets_and_Benchmarks_Catalog]]
- [ ] [[46_Query_and_Code_Cookbook]]
- [ ] [[47_Decision_Trees_for_Graph_Problems]]
- [ ] [[48_Current_Standards_Status_2026]]
- [ ] [[49_Glossary]]

## Weekly evidence scorecard

Score 0 (none), 1 (partial), or 2 (strong).

| Dimension | Score | Evidence link |
|---|---:|---|
| Conceptual explanation | | |
| Formal reasoning/query | | |
| Implementation | | |
| Evaluation/failure analysis | | |
| Reproducibility | | |
| Communication/teaching | | |

A week is successful at 8/12 or higher with at least one working artifact.

## Lab tracker

| Lab | Status | Result | Experiment note |
|---|---|---|---|
| L01 | not started | | |
| L02 | not started | | |
| L03 | not started | | |

Continue from [[36_Labs_and_Exercises]].

## Project tracker

| Project | Stage | Main risk | Next milestone | Evidence |
|---|---|---|---|---|
| P1 | idea | | | |
| P2 | idea | | | |
| P3 | idea | | | |

Use [[Template - Project README]], [[Template - Architecture Decision Record]] and [[Template - Failure Analysis]].

## Paper queue

| Priority | Paper | Why now | Status | Note |
|---:|---|---|---|---|
| 1 | | | unread | |

Use [[Template - Paper Note]].

## Research question queue

| ID | Question | Evidence gap | Smallest experiment | Status |
|---|---|---|---|---|
| RQ-001 | | | | idea |

## Monthly retrospective

1. Which graph-specific skill now changes the quality of my solutions?
2. Where am I using complexity without demonstrated benefit?
3. Which assumption failed most often: identity, semantics, time, retrieval, topology or evaluation?
4. What is my strongest reproducible artifact?
5. Which result could become a technical article, open-source contribution or paper?
6. What should I stop studying temporarily?

## Optional Dataview query

The vault works without community plugins. With Dataview enabled, copied study/experiment notes can be summarized using properties such as `type`, `status`, `project` and `created`:

```dataview
TABLE status, project, created
FROM ""
WHERE type = "experiment"
SORT created DESC
```

```dataview
TABLE year, venue, status, rating
FROM ""
WHERE type = "paper-note"
SORT year DESC
```

## Next action

- [ ] Open [[35_First_30_60_90_Days]] and complete Day 1.
- [ ] Copy [[Template - Weekly Review]] into your working-notes folder.
- [ ] Select one lab and create an [[Template - Experiment Note|experiment note]].
