---
title: "RDF, RDFS and Linked Data"
type: chapter
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - rdf
  - rdfs
  - linked-data
  - semantic-web
  - ontology
---
# RDF, RDFS and Linked Data

> [!goal]
> Model mergeable, globally identified statements; understand exactly what RDF and RDFS entail; and know when RDF is preferable to a property graph.

## 1. RDF’s core idea

RDF represents information as triples:

\[
(subject,\ predicate,\ object)
\]

Example:

```turtle
@prefix ex: <https://example.org/auto/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

ex:dealer-101 a ex:Dealer ;
    ex:legalName "North Star Motors" ;
    ex:inRegion ex:east-region ;
    ex:openedOn "2018-04-12"^^xsd:date .
```

A set of triples is an RDF graph. The graph abstraction supports decentralized identifiers and merging: two sources can make statements about the same IRI without agreeing on table layouts.

## 2. RDF terms

### IRI

An Internationalized Resource Identifier identifies a resource or vocabulary term. Prefer stable, dereferenceable HTTPS IRIs when publishing linked data. The IRI is an identifier, not necessarily the URL of a human web page, though content negotiation can provide machine and human representations.

### Literal

A literal has a lexical form plus datatype or language tag:

```turtle
"42"^^xsd:integer
"colour"@en-GB
```

The lexical form matters. Invalid lexical forms may be syntactically accepted by some parsers but not denote a valid datatype value.

### Blank node

A blank node denotes an existentially identified resource local to an RDF graph or dataset serialization context. It is not a globally stable identifier. Blank nodes are convenient for one-off structures but make reconciliation, updates and provenance harder. Use IRIs for entities you need to reference across systems or releases.

### Predicate

The predicate is an IRI. RDF edges are first-class vocabulary terms with a shared global name; unlike an LPG edge, a basic RDF predicate does not carry arbitrary properties directly.

## 3. Graphs and datasets

An RDF dataset contains:

- one default graph;
- zero or more named graphs identified by IRIs or blank nodes.

```trig
ex:source-a {
  ex:dealer-101 ex:hasManager ex:alice .
}
ex:source-b {
  ex:dealer-101 ex:hasManager ex:bob .
}
```

Named graphs group triples, but the RDF specifications do not impose one universal meaning such as provenance. Your application must state whether the graph name denotes a source, tenant, version, access scope or snapshot.

## 4. RDF 1.1 versus RDF 1.2 work

As of **5 November 2026**:

- RDF 1.1 remains the stable Recommendation family.
- RDF 1.2 Concepts reached a Candidate Recommendation Snapshot on 7 April 2026 and related documents continue on the Recommendation track.
- RDF 1.2 adds **triple terms** and directional language-tagged strings. A triple term can appear as the object of another triple, supporting statement-level descriptions without classic four-triple reification.

Treat draft-era interoperability carefully. Confirm that parser, store, query engine and serialization all support the same RDF 1.2 features. Keep a fallback representation for systems restricted to RDF 1.1.

## 5. Serializations

| Syntax | Best use | Notes |
|---|---|---|
| Turtle | human-authored RDF | prefixes, compact syntax |
| N-Triples | streaming/debugging | one triple per line, verbose |
| N-Quads | datasets/provenance exchange | adds graph label |
| TriG | human-readable datasets | Turtle plus named graphs |
| JSON-LD | web/API integration | context processing matters |
| RDF/XML | legacy/interchange | graph meaning differs from XML tree |

Serialization is not the data model. The same graph may have many syntactic forms and statement orders.

## 6. RDFS vocabulary

RDF Schema provides lightweight semantics:

- `rdfs:Class` and `rdf:Property`;
- `rdf:type`;
- `rdfs:subClassOf`;
- `rdfs:subPropertyOf`;
- `rdfs:domain` and `rdfs:range`;
- labels/comments and container-related vocabulary.

Example:

```turtle
ex:Dealer rdfs:subClassOf ex:Organization .
ex:premiumDealer rdfs:subClassOf ex:Dealer .
ex:inRegion rdfs:domain ex:Dealer ;
            rdfs:range ex:Region .
```

If `ex:d1 ex:inRegion ex:r1`, RDFS entails that `ex:d1` is a `Dealer` and `ex:r1` is a `Region`. Domain/range are inferential statements, not input-field validators.

## 7. RDFS entailment patterns

Important rules include:

- subclass transitivity;
- subproperty transitivity;
- type propagation through subclasses;
- statement propagation through subproperties;
- domain/range type inference.

RDFS cannot express class disjointness, cardinality, property inverses, unions, complements or many domain definitions. Use OWL when those meanings are essential, and SHACL when the requirement is data conformance.

## 8. Linked Data principles

A practical Linked Data approach is:

1. Use IRIs as names for things.
2. Use HTTP(S) IRIs so names can be looked up.
3. Return useful RDF and descriptions when an IRI is dereferenced.
4. Link to other IRIs to enable discovery.

Publishing linked data also requires licenses, versioning, provenance, content negotiation, availability and stable identifier governance.

## 9. Vocabulary reuse

Reuse established vocabularies when the semantics fit:

- RDF/RDFS/OWL for core semantics;
- SKOS for concept schemes;
- PROV-O for provenance;
- Dublin Core terms for general metadata;
- schema.org for broad web-facing terms;
- domain ontologies such as OBO resources for biomedicine.

Do not reuse a popular term whose intended semantics differ. A local property with a precise definition is better than a misleading external mapping.

## 10. Identity design

Decide separately:

- **identifier equality** — same string/IRI;
- **record co-reference** — two records describe one entity;
- **ontological identity** — substitutable in every statement;
- **business grouping** — same household, account family or legal group;
- **version identity** — same evolving entity across time.

`owl:sameAs` expresses the strongest identity. Prefer explicit mapping relations when evidence is uncertain or equivalence is contextual.

## 11. N-ary relations and statement metadata

Suppose a dealer receives a vehicle allocation of 20 units under a program during March. A single edge loses quantity, time and program identity. Introduce an allocation event:

```turtle
ex:allocation-778 a ex:Allocation ;
    ex:dealer ex:dealer-101 ;
    ex:vehicleLine ex:model-x ;
    ex:program ex:spring-program ;
    ex:quantity 20 ;
    ex:validDuring ex:march-2026 ;
    prov:wasDerivedFrom ex:source-file-44 .
```

This is usually clearer than attaching unrelated qualifiers to a timeless edge.

## 12. Lists, containers and collections

RDF collections use linked list cells (`rdf:first`, `rdf:rest`, `rdf:nil`). They are logically cumbersome for large ordered data. Use them for small closed lists required by ontology constructs, not as a general array representation. For operational sequences, use explicit position properties or an event model.

## 13. RDFLib laboratory

```python
from rdflib import Graph, Namespace, Literal, RDF, RDFS, XSD

EX = Namespace("https://example.org/auto/")
g = Graph()
g.bind("ex", EX)

g.add((EX["dealer-101"], RDF.type, EX.Dealer))
g.add((EX["dealer-101"], EX.legalName, Literal("North Star Motors")))
g.add((EX["dealer-101"], EX.openedOn,
       Literal("2018-04-12", datatype=XSD.date)))

g.add((EX.Dealer, RDFS.subClassOf, EX.Organization))

print(g.serialize(format="turtle"))
```

RDFLib supports parsing/serialization, datasets, SPARQL 1.1 and multiple stores. Restrict network/file access when processing untrusted RDF because parsers and queries may dereference external resources.

## 14. Modeling patterns

### Stable entity IRIs

Use opaque identifiers when names can change:

```text
https://example.org/id/dealer/7f36a1...
```

Keep labels as data. Avoid embedding current organization names or hierarchy paths in permanent identifiers.

### Class versus individual

A vehicle model can be modeled as an individual of `VehicleModel`, while each physical vehicle is an individual of `Vehicle`. Modeling the model as a class is possible but creates metamodeling complexity. Choose based on intended queries and reasoning.

### Measurement pattern

Do not store `ex:sales 42` without grain and unit. Model observation, metric, period, subject, value, unit and source.

### Role pattern

A person may bear a `ManagerRole` in an organization during an interval. Modeling `Manager` only as an immutable class loses context and time.

## 15. Common mistakes

- Using labels as identifiers.
- Treating blank-node IDs in serialized files as permanent.
- Assuming domain/range validates data.
- Using `owl:sameAs` for approximate matches.
- Collapsing events into timeless edges.
- Omitting units, time windows and grain from measurements.
- Mixing schema and instance namespaces without governance.
- Loading RDF/XML as though XML nesting defines semantics.
- Assuming named graphs automatically carry provenance semantics.

## Exercises

1. Convert a relational dealer/program/sales schema to RDF with stable IRIs.
2. Represent a changing manager assignment using an event/role node.
3. Write a graph in Turtle, JSON-LD and N-Quads; verify isomorphism.
4. Construct an RDFS graph and manually compute its closure.
5. Replace an unsafe `owl:sameAs` mapping with a provenance-qualified candidate match.
6. Compare RDF 1.1 reification, a statement node and an RDF 1.2 triple-term design.

## Primary sources

- RDF 1.2 Concepts and Abstract Data Model: https://www.w3.org/TR/rdf12-concepts/
- RDF 1.2 Primer: https://www.w3.org/TR/rdf12-primer/
- RDF 1.2 Schema: https://www.w3.org/TR/rdf12-schema/
- RDF 1.1 Concepts: https://www.w3.org/TR/rdf11-concepts/
- JSON-LD 1.1: https://www.w3.org/TR/json-ld11/
- RDFLib documentation: https://rdflib.readthedocs.io/en/latest/
- Aidan Hogan et al., *Knowledge Graphs*: https://kgbook.org/

## Next

Continue to [[06_SPARQL_Query_and_Federation]].
