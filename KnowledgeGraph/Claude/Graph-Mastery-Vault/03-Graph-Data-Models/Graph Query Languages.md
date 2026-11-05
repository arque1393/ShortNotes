---
tags: [data-models, query-languages]
phase: 1
status: not-started
---
# Graph Query Languages: GQL, SQL/PGQ, openCypher, Gremlin, SPARQL

> [!summary]
> **GQL (ISO/IEC 39075:2024)** is the first ISO database language since SQL, heavily influenced by Cypher. **SQL/PGQ** (SQL:2023) adds graph pattern matching inside SQL. Learn Cypher → GQL is a short step.

## Comparison
| Language | Style | Data model | Where |
|---|---|---|---|
| Cypher / openCypher | Declarative pattern | LPG | Neo4j, Memgraph, FalkorDB, Neptune, AGE |
| **GQL** | Declarative pattern (ISO) | LPG | Growing vendor adoption (e.g., Spanner Graph) |
| SQL/PGQ | `GRAPH_TABLE(... MATCH ...)` in SQL | Property graph views over tables | Relational DBs |
| Gremlin | Imperative traversal (TinkerPop) | LPG | Neptune, JanusGraph, Cosmos DB |
| SPARQL | Declarative triple patterns | RDF | All triple stores |

## Same query four ways — "names of Alice's friends"
```cypher
MATCH (:Person {name:'Alice'})-[:KNOWS]->(f) RETURN f.name
```
```groovy
g.V().has('Person','name','Alice').out('KNOWS').values('name')
```
```sparql
SELECT ?n WHERE { ?a ex:name "Alice" ; ex:knows ?f . ?f ex:name ?n }
```
```sql
SELECT f_name FROM GRAPH_TABLE (social
  MATCH (a IS Person WHERE a.name = 'Alice') -[IS KNOWS]-> (f IS Person)
  COLUMNS (f.name AS f_name))
```

## Concepts worth knowing for research
- **Path semantics:** walks vs trails vs simple paths; homomorphism vs isomorphism matching.
- **Regular path queries (RPQs)** and their complexity.
- Angles et al., "Foundations of Modern Query Languages for Graph Databases" (ACM CSUR 2017).

> [!tip] Engineering advice
> Keep application queries in openCypher/GQL-compatible syntax and behind a repository layer so you can switch engines (lesson from KùzuDB being archived in Oct 2025).

## My notes


## Self-test #flashcards/data-models
What is GQL?::ISO/IEC 39075:2024, the standard property-graph query language.
What does SQL/PGQ add?::Graph pattern matching over property-graph views inside SQL (GRAPH_TABLE … MATCH).
Gremlin is declarative or imperative?::Imperative traversal language (Apache TinkerPop).
What is a regular path query?::A query asking for node pairs connected by a path whose label sequence matches a regular expression.
