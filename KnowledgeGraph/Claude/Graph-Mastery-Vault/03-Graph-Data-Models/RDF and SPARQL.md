---
tags: [data-models, rdf, sparql, semantic-web]
phase: 1
status: not-started
---
# RDF, RDFS & SPARQL

> [!summary]
> **RDF** represents knowledge as triples *(subject, predicate, object)* with global **IRIs**, so data from anywhere can be merged. **RDFS** adds lightweight schema semantics. **SPARQL** queries it.

## RDF basics
- Terms: **IRIs** (`<http://example.org/alice>`), **literals** (`"Alice"@en`, `"42"^^xsd:integer`), **blank nodes** (`_:b1`, anonymous).
- Graph = set of triples. **Dataset** = default graph + **named graphs** (quads) → provenance, versioning.
- Serialisations: **Turtle**, N-Triples, TriG, JSON-LD, RDF/XML.
- **RDF 1.2 / "RDF-star"** (in progress at W3C): triple terms for statement-level annotations (like edge properties).

```turtle
@prefix ex:   <http://example.org/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix xsd:  <http://www.w3.org/2001/XMLSchema#> .

ex:alice a ex:Person ;
    ex:name "Alice"@en ;
    ex:worksFor ex:acme ;
    ex:born "1990-05-01"^^xsd:date .
ex:Employee rdfs:subClassOf ex:Person .
ex:worksFor rdfs:domain ex:Employee ; rdfs:range ex:Organization .
```

## RDFS entailment (key rules)
- `rdfs:subClassOf` is transitive; instances propagate up: `x a C`, `C ⊑ D` ⇒ `x a D`.
- `rdfs:domain`/`rdfs:range` **infer types** (they do not validate!). Above, Alice is inferred to be an `ex:Employee`, and Acme an `ex:Organization`.

## SPARQL 1.1
```sparql
PREFIX ex: <http://example.org/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

# Basic graph pattern + OPTIONAL + FILTER
SELECT ?person ?name ?org WHERE {
  ?person a ex:Person ; ex:name ?name .
  OPTIONAL { ?person ex:worksFor ?org }
  FILTER(lang(?name) = "en")
}

# Property paths: all (transitive) superclasses
SELECT ?super WHERE { ex:Employee rdfs:subClassOf+ ?super }

# Aggregation
SELECT ?org (COUNT(?p) AS ?n) WHERE { ?p ex:worksFor ?org } GROUP BY ?org ORDER BY DESC(?n)
```
Other forms: `ASK`, `CONSTRUCT` (build new graph), `DESCRIBE`, `SERVICE` (federation), SPARQL UPDATE (`INSERT/DELETE`).

### Wikidata practice
```sparql
# House cats on Wikidata (P31 = instance of, Q146 = house cat)
SELECT ?item ?itemLabel WHERE {
  ?item wdt:P31 wd:Q146 .
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
} LIMIT 20
```

## Tools
Apache Jena / Fuseki, Ontotext GraphDB, Stardog, RDFox, Oxigraph, `rdflib` (Python), Wikidata Query Service.

## Connections
- [[Property Graph vs RDF]] · [[OWL 2 and Profiles]] · [[SHACL and ShEx]] · [[SKOS]]

## My notes


## Self-test #flashcards/data-models
Three kinds of RDF terms?::IRIs, literals, blank nodes.
What do rdfs:domain and rdfs:range do?::They infer types of subjects/objects; they do not validate.
SPARQL syntax for transitive closure of subClassOf?::rdfs:subClassOf+ (one or more) or * (zero or more) property paths.
What are named graphs used for?::Grouping triples to record provenance, context, or versions (datasets of quads).
Which SPARQL keyword enables federated queries?::SERVICE
