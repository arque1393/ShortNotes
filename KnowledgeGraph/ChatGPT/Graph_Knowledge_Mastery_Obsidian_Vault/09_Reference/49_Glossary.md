---
title: "Detailed Graph Field Glossary"
aliases:
  - "Glossary"
type: reference
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - glossary
  - ontology
  - knowledge-graph
  - graph-ml
---
# Detailed Graph Field Glossary

> [!abstract]
> Precise working definitions across ontology, graph systems, analytics, graph ML and agentic AI. Many terms have community-specific meanings; the definition below states the intended meaning in this book.

## A

**ABox**  
The assertional component of a description-logic knowledge base: claims about individuals, such as `Dealer(D001)` or `locatedIn(D001, East)`. Contrast with TBox.

**Adjacency list**  
A graph representation storing, for each vertex, its neighboring vertices or incident edges. Efficient for sparse graphs and neighborhood traversal.

**Adjacency matrix**  
A matrix whose entry indicates whether, or with what weight, a pair of vertices is connected. Useful for algebraic graph methods but dense storage is expensive for sparse graphs.

**Agentic GraphRAG**  
A retrieval-generation architecture in which an agent decides when and how to use graph, text, vector, database and reasoning tools. The agent adds planning and control; it does not make graph evidence automatically correct.

**Alignment**  
The process or result of relating entities, classes or properties across schemas/ontologies, for example equivalence, subsumption or close mapping. Alignment assertions can be uncertain and context-dependent.

**Anonymous individual**  
An individual without a globally named IRI, often represented by a blank node in RDF. Its scope and identity are local to the graph/document semantics.

**Assertion**  
A stated claim in a graph. Keep it distinguishable from an inferred, computed or predicted claim.

**Assortativity**  
The tendency of vertices to connect to vertices with similar attributes, often measured using degree or categorical attributes.

**Axiom**  
A formal statement in an ontology or logical theory, such as subclass, disjointness, domain, range or property characteristics.

## B

**Bag semantics**  
Semantics in which duplicate solution rows are preserved. SPARQL and many query languages can produce duplicates unless `DISTINCT` or aggregation removes them.

**Betweenness centrality**  
A measure based on the fraction of shortest paths passing through a vertex or edge. It can identify structural brokers but is expensive and depends on path assumptions.

**Bitemporal model**  
A model recording both valid time, when a fact holds in the modeled world, and transaction time, when the system recorded or believed it.

**Blank node**  
An RDF term representing a resource without a globally named IRI in that graph. Blank nodes are existential-like identifiers, not ordinary strings and not automatically stable across serializations.

**Blocking**  
In entity resolution, candidate-generation rules that avoid comparing every record pair. Blocking recall limits the maximum recall of the complete matcher.

**Bridge**  
An edge whose removal increases the number of connected components in an undirected graph.

**Business glossary**  
A governed collection of business terms, definitions and ownership. It can inform an ontology but usually lacks formal axioms and machine reasoning semantics.

## C

**Canonical entity**  
The curated representation selected to integrate records believed to refer to the same real-world entity. It should retain source links and reversible merge history.

**Cardinality constraint**  
A restriction on how many values a property may or must have. OWL cardinalities express logical conditions; SHACL cardinalities validate graph data under selected targets.

**Centrality**  
A family of structural importance scores, including degree, closeness, betweenness, eigenvector centrality and PageRank. Importance always depends on graph and flow semantics.

**Class**  
A category of individuals. In OWL, a class denotes a set of individuals under an interpretation.

**Classification**  
In ontology reasoning, computing subclass relationships and the class hierarchy implied by axioms. In ML, predicting categorical labels; context must distinguish the meanings.

**Closed shape**  
A SHACL shape that rejects properties not explicitly permitted, subject to ignored-property rules. It introduces a local closed-world validation boundary.

**Closed-world assumption (CWA)**  
The assumption that facts not known to be true are false. Databases and application validation often use local CWA; OWL reasoning generally uses the open-world assumption.

**Clustering coefficient**  
A measure of how connected a node's neighbors are to one another, or the analogous global graph measure.

**Community detection**  
Algorithms that partition or group nodes based on dense internal connectivity or another structural objective. Communities are algorithm-dependent, not necessarily real social groups.

**Competency question (CQ)**  
A natural-language question the ontology/KG must be able to answer or support. CQs drive scope, modeling and tests.

**Concept scheme**  
In SKOS, a collection/context for concepts such as a taxonomy or thesaurus.

**Conformance**  
Satisfaction of a specification or validation profile. Conformance to syntax or SHACL does not prove factual truth.

**Connected component**  
A maximal set of vertices connected by paths. For directed graphs, distinguish weakly and strongly connected components.

**Consistency**  
In logic, absence of contradiction under the formal semantics. A consistent ontology can still contain factually wrong or incomplete data.

**Constraint**  
A condition data must satisfy in a chosen validation or storage context. Constraints differ from open-world logical axioms.

**Contextual embedding**  
A representation whose value depends on surrounding text or graph context, rather than a single fixed vector per entity.

**Coreference resolution**  
Determining which mentions in text refer to the same entity. It is related to but not identical with cross-source entity resolution.

**CRUD**  
Create, read, update and delete operations. Graph modeling must still define identity, history and relationship lifecycle under these operations.

**Cypher**  
A declarative property-graph query language based on graph pattern matching. Syntax and capabilities vary by version and implementation; it is related to but not identical with ISO GQL.

## D

**Data graph**  
In SHACL, the RDF graph being validated. More generally, a graph containing instance data rather than only schema/shape definitions.

**Data lineage**  
Traceability of data through sources, transformations and outputs. Provenance is the broader semantic account; lineage often emphasizes pipeline flow.

**Datatype property**  
An OWL property linking an individual to a literal/data value, such as a string, date or decimal.

**Degree**  
The number of incident edges. Directed graphs distinguish in-degree and out-degree; weighted degree sums edge weights.

**Degree distribution**  
The frequency distribution of node degrees. It influences sampling, algorithm behavior, robustness and GNN training.

**Description logic (DL)**  
A family of decidable knowledge-representation logics underlying OWL 2 DL. DLs define constructors, model-theoretic semantics and reasoning tasks.

**Directed acyclic graph (DAG)**  
A directed graph without directed cycles. Used for dependencies, workflows, causal structures and computation graphs.

**Disjointness**  
An axiom saying two classes or properties cannot share instances/pairs under the specified semantics. Disjointness enables error detection through inconsistency.

**Distant supervision**  
Creating weak training labels by aligning text with an existing knowledge base. It scales annotation but introduces false-positive and missing-label noise.

**Domain and range**  
In RDFS/OWL, axioms that can infer the subject/object types of a property assertion. They are not merely input-validation declarations.

## E

**Edge**  
A connection between vertices. It may be directed/undirected, typed, weighted, temporal or attributed.

**Edge classification**  
Predicting a label for an observed edge. It differs from link prediction, which predicts whether an edge should exist.

**Edge cut**  
A set of edges whose removal disconnects selected vertices or the graph. Relevant to resilience and flow.

**Edge feature**  
A value associated with an edge and used in queries or ML, such as amount, timestamp, confidence or relation type.

**Eigenvector centrality**  
A score in which a node is important when connected to important nodes. It depends on spectral properties and can behave poorly in some directed/disconnected graphs.

**Embedding**  
A learned or computed vector representation of entities, relations, nodes, edges or graphs. Similarity in embedding space is model-dependent evidence, not identity or entailment.

**Entailment**  
A statement is entailed when it must be true in every interpretation satisfying the premises under a specified semantics.

**Entailment regime**  
The formal inference semantics assumed while answering queries, such as simple RDF, RDF, RDFS or an OWL-related regime.

**Entity**  
Something treated as having identity in the domain: a person, organization, place, event, document, product or abstract concept.

**Entity linking**  
Mapping a mention, usually in text, to a known entity identifier in a knowledge base.

**Entity resolution (ER)**  
Determining which records or identifiers across sources refer to the same real-world entity, followed by controlled clustering/fusion.

**Event node**  
A node representing an occurrence or process, often used to model time, participants, roles and provenance for n-ary relations.

**Existential restriction**  
An OWL/DL restriction such as `hasPart some Engine`, meaning every instance of the class has at least one `hasPart` value belonging to `Engine`, including possibly unnamed values.

**Explainability**  
The ability to provide useful reasons for a result. A graph path can aid explanation but is not automatically a causal or faithful explanation of a model.

## F

**Fact grain**  
The exact level represented by one assertion/row/event, such as one dealer-month-metric. Grain errors cause duplicates and invalid aggregation.

**Federated query**  
A query whose subparts execute against multiple endpoints/sources. It introduces latency, availability, trust, privacy and source-capability challenges.

**Filtered ranking**  
In knowledge-graph link-prediction evaluation, removing other known true triples from corrupt candidate rankings so the model is not penalized for ranking a valid alternative.

**First-order logic (FOL)**  
A formal language over individuals, predicates, functions and quantifiers. OWL/DLs use restricted fragments to retain decidability.

**Foundation model for graphs**  
An emerging term for a broadly pretrained model intended to transfer across graph tasks, domains or graphs. Definitions and evidence of generality are still evolving.

**Functional property**  
An OWL property characteristic meaning each subject has at most one value under the semantics. Two asserted values may imply equality rather than produce a conventional validation error.

## G

**GNN (graph neural network)**  
A neural model that propagates/aggregates information over graph structure or otherwise uses graph inductive bias.

**Golden record**  
A curated representation of an entity formed from multiple source records. It must preserve provenance and should not hide source disagreement.

**Graph**  
A mathematical structure of vertices and edges. Variants include directed, weighted, typed, temporal, multilayer and hypergraphs.

**Graph algorithm**  
A deterministic or randomized procedure operating on graph structure, such as BFS, PageRank, components or community detection.

**Graph analytics**  
Use of structural algorithms and statistics to describe, rank, partition or find patterns in graphs.

**Graph database**  
A database designed to store/query graph structures and relationships. It may use RDF or a property-graph model.

**Graph data science (GDS)**  
An end-to-end process using graph projection, algorithms, features, ML, evaluation and operationalization to solve data-science problems.

**Graph isomorphism**  
A bijection between vertex sets preserving adjacency (and labels/types when applicable). It formalizes structural equivalence.

**Graph kernel**  
A similarity function between graphs or nodes based on substructures such as walks, paths or Weisfeiler-Lehman patterns.

**Graph mining**  
Discovery of patterns such as frequent subgraphs, motifs, communities, anomalies or association structures.

**Graph neural message passing**  
A framework where nodes update representations using messages derived from neighbors/edges over repeated layers.

**Graph projection**  
A workload-specific graph derived from canonical data by selecting, transforming or aggregating node/edge types and properties.

**Graph query language**  
A language for matching/traversing/updating graphs, such as SPARQL, Cypher, GQL or Gremlin, each with different data and execution semantics.

**GraphRAG**  
Retrieval-augmented generation using graph-derived structure or graph queries to select and organize evidence. Architectures vary widely; the name alone does not specify construction, retrieval or evaluation.

**Gremlin**  
Apache TinkerPop's graph traversal language and virtual machine, expressed as a sequence of traversal steps.

**Ground truth**  
Reference labels used for evaluation. Ground truth may contain annotation uncertainty or coverage limits and should have provenance/adjudication.

## H

**Heterogeneous graph**  
A graph containing multiple node and/or edge types, often with type-specific features and semantics.

**Hierarchy**  
An ordering such as subclass, broader/narrower, part-whole or organizational reporting. Different hierarchy relations must not be conflated.

**Homophily**  
The tendency of connected nodes to share labels/features. Many GNN assumptions work best under homophily, but real graphs can be heterophilous.

**Hyperedge**  
An edge relating more than two vertices simultaneously. A hypergraph directly models such relations; ordinary graphs often reify them as event/relation nodes.

**Hypergraph**  
A graph generalization in which each edge can connect any number of vertices.

## I

**Identifier**  
A value intended to distinguish a resource in a scope. Stable graph systems separate identifiers from mutable labels.

**Identity link**  
An assertion that two identifiers refer to the same or closely corresponding entity. Strong equivalence such as `owl:sameAs` has substantial logical consequences.

**Inductive learning**  
Learning that generalizes to new nodes, edges or graphs not present in training. Contrast with transductive learning over a fixed graph.

**Inference**  
Deriving conclusions from premises using logical rules, deterministic algorithms or statistical models. Always name which kind.

**Information extraction (IE)**  
Transforming unstructured/semi-structured content into entities, relations, events, attributes and evidence.

**Instance**  
A particular member of a class, such as a specific dealer or document.

**Inverse property**  
A relation whose arguments reverse another relation, for example `hasPart` and `partOf`.

**IRI**  
Internationalized Resource Identifier. RDF uses IRIs to globally name resources and predicates.

## J

**Join**  
Combining solution bindings/rows on shared variables or keys. Graph pattern matching often compiles into joins plus traversal/index operations.

**JSON-LD**  
A JSON-based Linked Data serialization with contexts that map JSON terms to IRIs and define value interpretation.

## K

**Knowledge base (KB)**  
A repository of formalized knowledge, often including facts and rules/axioms. Some communities use KB and KG interchangeably.

**Knowledge graph (KG)**  
A graph-based representation of identified entities and semantically interpreted relationships, normally with types, provenance and governance. No single universal definition covers all communities.

**Knowledge graph completion (KGC)**  
Predicting missing plausible facts, commonly via link prediction. Predictions must not be stored as verified truth without validation/provenance.

**Knowledge organization system (KOS)**  
A taxonomy, thesaurus, classification scheme or subject-heading system. SKOS is designed to represent many KOS structures.

## L

**Label propagation**  
An algorithm spreading labels through graph neighborhoods. It can be used for community detection or semi-supervised classification; semantics depend on the variant.

**Labeled property graph (LPG)**  
A graph model with nodes/relationships carrying labels/types and key-value properties. Exact formal behavior varies by system and standard profile.

**Language tag**  
Metadata on an RDF string indicating natural language, such as `"car"@en`. RDF 1.2 also develops directional language-tagged strings.

**Leakage**  
Information from validation/test/future labels entering training or features. Graphs create special leakage through topology, reverse edges, duplicated entities and temporal neighborhoods.

**Linked Data**  
Principles for naming resources with HTTP IRIs, making them dereferenceable, returning useful RDF and linking to other resources.

**Link prediction**  
Predicting whether a relation exists or should exist between nodes. Evaluation depends strongly on negative sampling and candidate eligibility.

**Literal**  
An RDF value such as a string, number or date with datatype and possibly language metadata.

## M

**Materialization**  
Precomputing and storing inferred/derived facts. It improves some reads but complicates updates, provenance and storage.

**Message passing neural network (MPNN)**  
A general GNN framework where messages are computed along edges, aggregated at nodes and used to update representations.

**Metapath**  
A sequence of node/edge types in a heterogeneous graph, such as Author-Paper-Venue-Paper-Author, used to define typed connectivity.

**Metric closure**  
A graph containing shortest-path distances between all relevant vertex pairs; not to be confused with closed-world semantics.

**Motif**  
A small recurring graph pattern, often evaluated against a null model to determine overrepresentation.

**Multigraph**  
A graph allowing multiple edges between the same pair of vertices.

**Multilayer graph**  
A graph representing multiple relation layers, contexts or networks with possible inter-layer connections.

## N

**Named graph**  
A graph associated with a name inside an RDF dataset. It is often used for source, tenant, snapshot or context grouping, but RDF semantics do not automatically assign provenance meaning to the name.

**Negative sampling**  
Generating presumed non-edges/false triples for training or evaluation. Poor sampling can make a task unrealistically easy or mark unknown positives as negatives.

**Neighborhood**  
The set of vertices/edges around a node, often limited by direction, type, time or hop count.

**Neuro-symbolic AI**  
Systems combining neural/statistical learning with symbolic structures, constraints, logic or programs. The integration can occur in data, architecture, objective, inference or verification.

**Node classification**  
Predicting a label for a node using features and possibly graph structure.

**Node embedding**  
A vector representation of a node learned from topology, attributes or both.

**Node shape**  
A SHACL shape whose focus is a node and whose constraints apply to that node.

**Normalization**  
In data engineering, standardizing representations; in graph ML, rescaling adjacency/features; in databases, decomposing schema to reduce redundancy. State the intended meaning.

## O

**Object property**  
An OWL property linking individuals to individuals.

**Observation**  
A record of measuring/estimating a property under a procedure and context. It should not be confused with the enduring property or its current truth.

**Ontology**  
An explicit, formal specification of a shared conceptualization: concepts, relations, constraints/axioms and intended meanings.

**Ontology alignment**  
Finding and representing correspondences between ontologies or their terms.

**Ontology commitment**  
The modeling choices about what kinds of entities and distinctions the ontology asserts exist or matter.

**Ontology design pattern (ODP)**  
A reusable solution to a recurring ontology modeling problem, analogous to software design patterns but grounded in semantic commitments.

**Ontology engineering**  
The lifecycle of requirements, conceptualization, reuse, formalization, implementation, testing, publication, governance and evolution of ontologies.

**Ontology learning**  
Automatic/semi-automatic acquisition of ontology elements from data or text. Learned candidates require expert/governance review.

**Open-world assumption (OWA)**  
Absence of a statement does not imply its negation. Standard OWL semantics are open-world.

**Over-smoothing**  
A GNN phenomenon where node representations become too similar across layers, reducing discriminability.

**Over-squashing**  
Compression of exponentially growing distant information into fixed-size representations, limiting long-range message passing.

## P

**PageRank**  
A random-walk-based centrality score with damping/teleportation. Its interpretation depends on edge direction, weights and the meaning of flow.

**Path**  
A sequence of adjacent vertices/edges. Query languages differ on whether paths are simple, trails, walks, bounded or returned as first-class values.

**Path query**  
A query expressing connectivity through one or more relationship steps, often with type/direction constraints.

**Predicate**  
In RDF, the IRI in the middle of a triple. In logic, a relation/property interpreted over individuals.

**Probabilistic knowledge graph**  
A KG whose assertions or rules include uncertainty. Confidence scores require a defined probabilistic meaning and combination model.

**Property graph**  
A graph model where nodes/edges can have properties and types/labels. ISO GQL provides a standardized property-graph query framework, while implementations differ.

**Property path**  
In SPARQL, a regular-expression-like path expression over predicates and direction, enabling reachability patterns.

**Provenance**  
Information about the origin, derivation, agents, activities and evidence associated with data or claims.

## Q

**Qualified relation**  
A pattern that represents a relation through an intermediate assertion/event node so it can carry roles, time, provenance or other qualifiers.

**Query planning**  
Choosing an execution strategy, including access paths, join order, traversal direction and intermediate materialization.

**Query rewriting**  
Transforming a query using schema/ontology axioms or optimization rules, for example expanding a query to account for subclasses.

## R

**RDF**  
The Resource Description Framework, a graph data model based on triples and datasets, with formal semantics and Web identifiers.

**RDF dataset**  
A default RDF graph plus zero or more named graphs.

**RDF reification**  
The standard RDF vocabulary for describing a statement as a resource. It does not by itself assert the reified triple and can be verbose.

**RDFS**  
RDF Schema, a vocabulary and semantics for classes, properties, subclass/subproperty, domain and range.

**Reasoner**  
Software that computes logical consequences, consistency, classification or realization under a formal semantics.

**Recall@K**  
The proportion of relevant items appearing in the top K results. In graph retrieval, define the evidence unit and gold coverage carefully.

**Relation extraction**  
Identifying semantic relations between entity mentions, often from text. It can be sentence-level, document-level or cross-document.

**Relational inductive bias**  
A modeling bias that computation should respect entities and their relations, sharing functions across graph structure.

**Restriction**  
An OWL class expression constraining property values, such as existential, universal, value or cardinality restrictions.

**Retrieval-augmented generation (RAG)**  
A system that retrieves external evidence and conditions generation on it. Retrieval improves access but does not guarantee grounded use or factuality.

**Rule**  
An if-then derivation or constraint pattern. Its semantics depends on the rule language, negation, closure and conflict policy.

## S

**Schema**  
A structural model defining allowed/expected data organization. In semantic systems, distinguish database schema, RDF vocabulary, ontology and validation shapes.

**Semantic layer**  
A governed conceptual/query layer connecting business meanings to physical data. It may use ontologies, metrics models, mappings and APIs.

**Semantic similarity**  
A score for meaning-relatedness derived from text, ontology distance or embeddings. Similarity is not identity or logical equivalence.

**Semantic Web**  
Standards and practices for machine-processable linked data and formal vocabularies on the Web, including RDF, SPARQL and OWL.

**Shape**  
In SHACL, a set of constraints/targets used to validate focus nodes or property values.

**Shortest path**  
A path minimizing edge count or total weight. It is meaningful only when weight and admissible-path semantics match the domain.

**SKOS**  
The Simple Knowledge Organization System, an RDF model for concept schemes, labels, broader/narrower/related links and mappings.

**SPARQL**  
The W3C query/update/protocol family for RDF graphs and datasets.

**Statement-level provenance**  
Provenance attached to an individual assertion rather than only a file or named graph.

**Strongly connected component (SCC)**  
A maximal directed subgraph in which every vertex is reachable from every other vertex.

**Subgraph**  
A graph formed from subsets of vertices and edges. Retrieval subgraphs should preserve source/context needed to interpret claims.

**Subclass**  
A class whose every instance is also an instance of another class. It is an `is-a` relation, not part-whole or broader-topic by default.

**Subproperty**  
A property whose every pair is also a pair of another property.

**Symmetric property**  
A relation where `R(a,b)` entails `R(b,a)`, such as a properly modeled `isSiblingOf` relation.

## T

**TBox**  
The terminological component of a description-logic knowledge base: classes, properties and general axioms. Contrast with ABox.

**Taxonomy**  
A controlled classification hierarchy. A taxonomy is usually less expressive than a formal ontology.

**Temporal graph**  
A graph whose nodes, edges or events change over time. Snapshot, interval and event-stream models answer different questions.

**Temporal knowledge graph (TKG)**  
A multi-relational KG with time associated with facts/events, often used for time-aware reasoning and link prediction.

**Topological sort**  
A linear ordering of a DAG in which every directed edge goes from earlier to later. Used for dependency scheduling.

**Transductive learning**  
Learning over a fixed set of nodes where unlabeled test-node structure may be visible during training, while labels are hidden.

**Transitive property**  
A relation where `R(a,b)` and `R(b,c)` entail `R(a,c)`. Do not declare transitivity for relations that only seem loosely chainable.

**Triple**  
An RDF statement with subject, predicate and object.

**Triple term**  
In RDF 1.2, a triple used as an RDF term in another triple's object position. It supports statement annotation patterns but does not define complete provenance by itself.

**Triple store**  
A database optimized for RDF triples/datasets and SPARQL, often with optional reasoning and full-text/geospatial features.

## U

**Unbound variable**  
A SPARQL solution variable with no value in a particular result mapping, often due to `OPTIONAL` or union branches. It differs from SQL `NULL`.

**Universal restriction**  
An OWL restriction such as `hasPart only EnginePart`, constraining all known/possible property values under open-world semantics; it does not assert that any value exists.

**Upper ontology**  
A domain-independent ontology of high-level categories such as object, process, quality, role, time and space, intended to support consistent domain modeling.

**URI/URL/IRI**  
A URI identifies a resource; a URL is a locator form; an IRI extends identifiers to a broader character set. RDF uses IRIs.

## V

**Validation**  
Checking data against declared conditions. Validation results depend on the selected graph, targets, inference and constraint language.

**Validity time**  
The period during which a fact holds in the modeled domain, as opposed to when the database recorded it.

**Vector database**  
A system indexing embeddings for similarity search. It complements but does not encode explicit graph/path semantics by itself.

**Vertex**  
A graph node.

**Vocabulary**  
A set of named terms used to describe data. A vocabulary may have minimal formal semantics; an ontology normally adds explicit conceptual commitments and axioms.

## W

**Walk**  
A sequence of adjacent vertices/edges that may repeat vertices and edges. A trail forbids repeated edges; a simple path forbids repeated vertices.

**Weakly connected component (WCC)**  
A connected component obtained after ignoring edge direction in a directed graph.

**Weisfeiler-Lehman (WL) test**  
An iterative graph-refinement procedure used to study graph isomorphism and GNN expressive power.

**World model**  
An internal representation of entities, state, dynamics and action effects used for prediction/planning. A KG/ontology can supply part of a world model but may omit uncertainty and dynamics.

## X-Y-Z

**Zero-shot graph transfer**  
Applying a graph model to tasks/domains/graphs without task-specific labeled training. Claims require careful checks for shared vocabularies, pretraining overlap and prompt leakage.

## High-risk confusions

| Do not confuse | Why |
|---|---|
| taxonomy and ontology | A taxonomy is mainly classification; an ontology can encode richer relations and axioms. |
| schema and ontology | A storage schema constrains representation; an ontology specifies domain meaning under formal semantics. |
| missing and false | Under open-world semantics, missing generally means unknown. |
| domain/range and input validation | RDFS/OWL domain/range can infer types; they do not simply reject values. |
| functional property and SHACL `maxCount 1` | OWL may infer equality; SHACL reports a conformance violation. |
| similarity and identity | Similar entities are not necessarily the same entity. |
| graph path and explanation | A path is evidence of connectivity, not necessarily causality or model faithfulness. |
| confidence and probability | A model score is not calibrated probability unless defined and validated as such. |
| KGE completion and logical entailment | KGE ranks plausible triples; it does not prove them. |
| GraphRAG and KGQA | GraphRAG may build/retrieve corpus graphs; KGQA often queries an existing structured KG. |
| community and ground-truth group | A community is an optimization result dependent on objective/resolution. |
| temporal graph and bitemporal database | A temporal graph can model event time; bitemporality explicitly separates valid and transaction time. |
| generated claim and source claim | A generated synthesis must link back to evidence and distinguish interpretation. |

## Related notes

- [[03_Glossary_of_Graph_Fields]] - compact field map
- [[03_Logic_Knowledge_Representation_and_Semantics]]
- [[05_RDF_RDFS_and_Linked_Data]]
- [[07_Description_Logics_and_OWL_2]]
- [[12_Property_Graphs_Cypher_GQL_and_Gremlin]]
- [[20_Network_Science_and_Graph_Analytics]]
- [[23_Knowledge_Graph_Embeddings_and_Link_Prediction]]
- [[24_Graph_Neural_Network_Foundations]]
- [[30_GraphRAG_and_Hybrid_Retrieval]]
