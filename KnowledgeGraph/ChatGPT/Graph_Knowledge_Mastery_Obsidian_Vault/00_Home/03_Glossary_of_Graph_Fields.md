---
title: "Glossary of Graph Fields"
type: chapter
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - glossary
  - knowledge-graph
  - ontology
---
# Glossary of Graph Fields

This chapter separates terms that are often collapsed into “graph technology.” The expanded alphabetical glossary is in [[49_Glossary]].

## Core representations

**Graph**  
A mathematical structure \(G=(V,E)\) with vertices and edges. Variants may be directed, weighted, typed, attributed, temporal, multi-relational, multiplex, probabilistic or hypergraphic.

**Labeled property graph (LPG)**  
A graph model in which nodes and relationships can have labels/types and key–value properties. It is natural for traversal-centric applications and is used by Cypher/GQL-style systems.

**RDF graph**  
A set of subject–predicate–object triples using IRIs, blank nodes, literals and, in RDF 1.2 work, triple terms. RDF is designed for global identifiers, mergeability and formal semantics.

**RDF dataset**  
A default graph plus zero or more named graphs. Named graphs are commonly used for context, source, tenancy or version grouping, but their exact application semantics must be specified.

**Hypergraph**  
A graph in which one hyperedge can connect more than two vertices. It directly represents n-ary relations, though an ordinary graph can often reify the relation as a node.

**Multigraph**  
A graph allowing multiple edges between the same pair of vertices. This matters when each relationship event has its own identity, time or provenance.

## Knowledge organization

**Controlled vocabulary**  
An approved set of terms. It may include labels and identifiers but need not contain formal relations or axioms.

**Taxonomy**  
A hierarchical classification, usually broader/narrower or superclass/subclass. A taxonomy does not by itself define rich logical semantics.

**Thesaurus**  
A controlled vocabulary with preferred terms, synonyms and associative or hierarchical relations. SKOS is a common representation model.

**Schema**  
A structural contract for data: types, properties, allowed shapes and constraints. A schema may be syntactic, logical, validation-oriented or database-specific.

**Ontology**  
An explicit specification of a conceptualization: classes, relations, individuals, definitions and axioms that state intended meaning. Ontologies range from lightweight vocabularies to expressive logical theories.

**Upper/top-level ontology**  
A domain-neutral ontology of general categories such as object, process, quality, role, time and space. Examples include BFO, DOLCE and SUMO. Adopting one creates commitments and should solve an integration need, not serve as decoration.

**Knowledge graph (KG)**  
A graph-based knowledge system representing entities or concepts and their relations, normally with identifiers, types, contextual metadata and intended interpretation. There is no single universally accepted formal definition; state your data model and semantics.

## Logic and semantics

**Interpretation/model**  
A mathematical assignment that gives symbols a meaning. A theory is satisfiable if at least one model makes all of its statements true.

**Entailment**  
A statement is entailed when it is true in every model of the premises. Entailment is stronger than “the query engine happened to return it.”

**Description logic (DL)**  
A family of decidable knowledge-representation logics balancing expressivity and computational properties. OWL 2 DL is grounded in description-logic research.

**Open-world assumption (OWA)**  
Absence of a statement does not imply falsity. This is appropriate for incomplete, distributed knowledge, but it surprises developers accustomed to database completeness.

**Closed-world assumption (CWA)**  
What cannot be derived from the database is treated as false for the current task. Many application validation and operational queries use a local closed world.

**Unique-name assumption (UNA)**  
Different names denote different entities. OWL does not generally assume this; database systems often behave as though identifiers are unique.

**Reasoning**  
Deriving logical consequences, checking consistency, classifying concepts, answering queries under an entailment regime, or applying rules. “Reasoning” is also used loosely for LLM chain-of-thought; keep symbolic and generative meanings separate.

**Validation**  
Checking whether data conforms to a declared shape or business rule. A failed SHACL constraint says the graph violates a data contract; it does not necessarily mean the world is logically inconsistent.

## Construction and quality

**Entity linking**  
Mapping a mention in text or data to an entity identifier in a KG.

**Entity resolution**  
Deciding which records or mentions refer to the same real-world entity. It includes candidate generation, matching, clustering and often human review.

**Knowledge fusion**  
Combining statements from multiple sources while resolving identity, conflicts, provenance, confidence and temporal scope.

**Provenance**  
Information about origin, derivation, responsibility and processing history. Provenance may attach to entities, records, statements, named graphs or activities.

**Ontology alignment**  
Finding correspondences between entities in different ontologies: equivalence, subsumption or other mappings. Alignment is uncertain and context-sensitive; `owl:sameAs` is often too strong.

## Analytics and learning

**Graph analytics / network science**  
Descriptive and inferential methods that use topology: paths, components, centrality, communities, motifs, diffusion, resilience and similarity.

**Graph data science (GDS)**  
A workflow discipline combining graph projection, algorithms, feature engineering, ML, evaluation and operationalization.

**Knowledge-graph embedding (KGE)**  
Learning vector or geometric representations for entities and relations, commonly for link prediction, ranking or similarity. An embedding is a statistical approximation, not an ontology.

**Graph neural network (GNN)**  
A neural architecture that updates node, edge or graph representations by aggregating information over graph neighborhoods or related structures.

**Heterogeneous GNN**  
A GNN that models multiple node and edge types, usually with type-specific parameters or attention.

**Graph transformer**  
A transformer adapted to graph structure through structural encodings, constrained attention, positional signals or hybrid message passing.

**Graph foundation model (GFM)**  
An emerging class of models pretrained for transfer across graph tasks, datasets or domains. Claims of “foundation” vary; evaluate actual generalization scope rather than the label.

**Neuro-symbolic AI**  
Systems combining learned representations with explicit symbolic structures, logic, constraints or programs. The key research issue is not merely connecting two components, but achieving useful learning, guarantees and explanations end to end.

## LLM and agentic systems

**Vector RAG**  
Retrieval-augmented generation in which chunks are typically retrieved by dense/sparse similarity. It is strong for local semantic relevance but does not directly encode multi-hop relations.

**GraphRAG**  
A family of systems that construct or use graph structure to retrieve, organize or summarize evidence for an LLM. It may mean entity-graph traversal, community summaries, graph-indexed chunks or hybrid vector–graph retrieval; always specify the architecture.

**Ontology-grounded agent**  
An agent whose planning, tool inputs, memory types, validation or permissions are constrained by an ontology/schema. Grounding can improve consistency and auditability but does not guarantee correct planning.

**Graph memory**  
A persistent graph of experiences, entities, events, decisions, evidence and relationships used by an agent. Good graph memory requires temporal semantics, identity control, deletion, provenance and retrieval evaluation.

## Systems

**OLTP graph workload**  
Concurrent transactional reads and writes, often with bounded neighborhood traversals and consistency requirements.

**OLAP graph workload**  
Large scans or iterative algorithms over substantial portions of a graph, such as PageRank or connected components.

**Query plan**  
The physical execution strategy chosen for a declarative query: starting points, indexes, joins, expansions, filters and operators. Graph queries can explode when branching factors and path semantics are underestimated.

**Graph projection**  
A task-specific view of source data containing selected nodes, relationships, direction, weights and properties. Most graph analytics and GNN results are properties of the projection, not of an abstract “true graph.”
