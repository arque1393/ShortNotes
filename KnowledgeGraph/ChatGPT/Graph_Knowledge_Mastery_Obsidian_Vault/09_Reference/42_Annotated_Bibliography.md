---
title: "Annotated Bibliography"
type: reference
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - books
  - bibliography
  - reading-list
  - reference
---
# Annotated Bibliography

> [!goal]
> Use a prioritized reading spine. Read books for coherent mental models, standards for exact semantics, papers for claims, and documentation for current implementation behavior.

## Tier 0 - the core spine

### 1. Hogan et al. - *Knowledge Graphs*

[Free official HTML](https://kgbook.org/)

**Why:** The best single compact academic overview of graph data models, schema, identity, construction, enrichment, quality and applications. It connects symbolic and statistical KG topics.

**Read:** Entire book once; revisit construction, quality and enrichment during projects.

**Limitation:** Published before the current GraphRAG/agent wave; supplement with [[44_Papers_by_Topic]].

### 2. Allemang, Hendler and Gandon - *Semantic Web for the Working Ontologist*, 3rd ed.

[ACM book page](https://doi.org/10.1145/3382097)

**Why:** Practical conceptual modeling with RDF, RDFS and OWL; excellent for understanding why the standards are designed as they are.

**Read:** Alongside your first ontology, not as passive theory.

### 3. Hitzler, Krotzsch and Rudolph - *Foundations of Semantic Web Technologies*

[Official companion site](https://www.semantic-web-book.org/)

**Why:** More formal treatment of logic, semantics, RDF(S), OWL and rules. Use when you need exactness beyond practitioner descriptions.

**Read:** Logic/semantics chapters during Weeks 7-14; work exercises.

### 4. Hamilton - *Graph Representation Learning*

[Free author pre-publication PDF](https://www.cs.mcgill.ca/~wlh/grl_book/)

**Why:** Coherent introduction to embeddings, KGs, GNNs, theory and generative graph models.

**Read:** Chapters 2-7 before chasing modern architectures.

### 5. Barabasi - *Network Science*

[Free official online book](https://networksciencebook.com/)

**Why:** Intuitive and visual network-science foundation with datasets/slides.

**Pair with:** Newman's more rigorous *Networks* and your own null-model experiments.

## Tier 1 - deepen each track

### Kejriwal, Knoblock and Szekely - *Knowledge Graphs: Fundamentals, Techniques, and Applications*

[MIT Press](https://mitpress.mit.edu/9780262045094/knowledge-graphs/)

**Best for:** A broader, longer KG engineering/application treatment, especially construction and practical systems.

### Newman - *Networks*, 2nd ed.

**Best for:** Rigorous network models, measures, community structure, spreading and statistical treatment.

### Easley and Kleinberg - *Networks, Crowds, and Markets*

[Free official draft](https://www.cs.cornell.edu/home/kleinber/networks-book/)

**Best for:** Connections among networks, game theory, markets, information cascades and social phenomena.

### Robinson, Webber and Eifrem - *Graph Databases*, 2nd ed.

[O'Reilly page](https://www.oreilly.com/library/view/graph-databases-2nd/9781491930885/)

**Best for:** Property-graph modeling and application intuition. Treat vendor-specific advice as one ecosystem view; verify current Cypher/GQL behavior in docs.

### Arp, Smith and Spear - *Building Ontologies with Basic Formal Ontology*

[MIT Press](https://mitpress.mit.edu/9780262527811/building-ontologies-with-basic-formal-ontology/)

**Best for:** Applied ontology and upper-ontology discipline, especially scientific/biomedical domains.

### Baader et al. - *The Description Logic Handbook*

**Best for:** Formal DL foundations, reasoning algorithms and complexity. Use selectively rather than cover-to-cover.

### Christen - *Data Matching*

**Best for:** Record linkage/entity resolution pipeline, blocking, similarity, classification and evaluation.

### Koller and Friedman - *Probabilistic Graphical Models*

**Best for:** Bayesian/Markov networks and structured probability. It is not a KG book; use to prevent conceptual mixing.

### Pearl, Glymour and Jewell - *Causal Inference in Statistics: A Primer*

**Best for:** Causal DAGs, interventions and adjustment. Essential when graph analytics claims become causal.

## Tier 2 - engineering and special topics

### Akhtar - *Practical Graph Data Science with Neo4j*

Use for tool-oriented practice, but always tie recipes to [[20_Network_Science_and_Graph_Analytics]] and current GDS docs.

### Noy and McGuinness - *Ontology Development 101*

[Stanford guide](https://protege.stanford.edu/publications/ontology_development/ontology101.pdf)

Short, classic workflow for scope, reuse, terms, hierarchy, properties and instances. Supplement with modern testing/governance.

### NeOn Methodology

[NeOn methodology resources](http://neon-project.org/)

Useful for collaborative/networked ontology engineering, reuse and lifecycle scenarios.

### OBO Foundry principles

[Official principles](https://obofoundry.org/principles/fp-000-summary.html)

Important for interoperable ontology governance, especially life sciences. Learn the principles even outside biomedicine.

### W3C and ISO specifications

Use [[48_Current_Standards_Status_2026]]. Specifications are the authoritative source for semantics; books and tutorials simplify.

## Reading order by goal

### Ontology/semantic engineer

1. Hogan overview;
2. *Working Ontologist*;
3. Ontology Development 101;
4. OWL 2 and SHACL standards;
5. *Foundations of Semantic Web Technologies*;
6. upper ontology/BFO or domain methodology;
7. reasoner/testing papers.

### KG platform engineer

1. Hogan;
2. graph database book + Cypher/GQL docs;
3. RDF/SPARQL specs;
4. data matching;
5. database/query optimization papers;
6. governance/provenance/security.

### Graph data scientist

1. Barabasi;
2. Newman;
3. CS224W/Hamilton;
4. GDS/system docs;
5. null models/statistical network papers;
6. domain causal literature.

### Graph ML researcher

1. Hamilton;
2. seminal GNN/KGE papers in [[44_Papers_by_Topic]];
3. expressivity/scalability/evaluation papers;
4. OGB and realistic domain benchmarks;
5. graph transformers/GFMs only after diagnostics.

### KG + LLM/agent researcher

1. Hogan + ontology spine;
2. retrieval and KGQA foundations;
3. GraphRAG surveys/benchmarks;
4. typed tool/planning/security work;
5. reproduction before architectural novelty.

## How to annotate a book

For each chapter record:

- five concepts in your own words;
- one worked example in your anchor domain;
- one assumption or limitation;
- one implementation task;
- links to relevant papers/standards;
- three questions you still cannot answer.

Do not copy passages. Build a personal conceptual index using `[[wiki links]]`.
