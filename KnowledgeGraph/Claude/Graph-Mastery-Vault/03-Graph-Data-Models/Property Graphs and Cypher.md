---
tags: [data-models, cypher, neo4j]
phase: 1
status: not-started
---
# Property Graphs & Cypher

> [!summary]
> **Labelled property graph (LPG):** nodes with labels and key–value properties; directed, typed relationships that can also carry properties. Cypher queries graphs with ASCII-art patterns `(a)-[:R]->(b)`.

## Model
- Node: `(:Person {name:'Alice', born:1990})` — can have multiple labels.
- Relationship: `-[:WORKS_AT {since:2020}]->` — exactly one type, always directed (can be queried undirected).
- No global IDs/schema standard by default → add **constraints** and **indexes**.

## Essential Cypher
```cypher
// Create with constraint
CREATE CONSTRAINT person_id IF NOT EXISTS FOR (p:Person) REQUIRE p.id IS UNIQUE;

// Idempotent upsert
MERGE (p:Person {id: 'p1'}) SET p.name = 'Alice';
MERGE (c:Company {id: 'c1'}) SET c.name = 'Acme';
MATCH (p:Person {id:'p1'}), (c:Company {id:'c1'})
MERGE (p)-[:WORKS_AT {since: 2020}]->(c);

// Pattern + aggregation
MATCH (p:Person)-[:WORKS_AT]->(c:Company)
RETURN c.name, count(p) AS employees ORDER BY employees DESC;

// Variable-length paths (friends of friends up to 3 hops)
MATCH (a:Person {name:'Alice'})-[:KNOWS*1..3]-(x)
RETURN DISTINCT x.name;

// OPTIONAL MATCH = left outer join
MATCH (p:Person) OPTIONAL MATCH (p)-[:OWNS]->(car:Car)
RETURN p.name, collect(car.model) AS cars;

// Pipelining with WITH
MATCH (p:Person)-[:KNOWS]-(f)
WITH p, count(f) AS deg WHERE deg > 10
RETURN p.name, deg;

// Bulk import
LOAD CSV WITH HEADERS FROM 'file:///people.csv' AS row
MERGE (:Person {id: row.id, name: row.name});
```

## Modelling heuristics
| Question | Usually → |
|---|---|
| Is it a thing you traverse through / query by? | **Node** |
| Is it a connection with meaning? | **Relationship** (specific types: `:PURCHASED` not `:RELATED_TO`) |
| Is it a simple attribute you filter on? | **Property** |
| Relationship needs relationships of its own (n-ary)? | **Reify** into an intermediate node (e.g., `:Employment`) |
| Versioning / time? | Time properties on relationships, or event nodes |

> [!warning] Pitfalls
> - `MERGE` on a full pattern creates duplicates if part of it exists — `MERGE` nodes first, then the relationship.
> - Unbounded `*` paths explode; always set an upper bound.
> - Super-nodes (millions of edges) kill traversals — model around them.
> - Cypher match semantics: **relationship isomorphism** (no relationship repeated within one MATCH pattern).

## Connections
- Algorithms: [[Centrality Measures]], [[Community Detection]]
- [[Text-to-Cypher and Text-to-SPARQL]]
- [[Graph Query Languages]] (GQL standard grew out of Cypher)

## Resources
- Neo4j GraphAcademy (free) · Cypher Manual · APOC docs

## My notes


## Self-test #flashcards/data-models
What does MERGE do in Cypher?::Matches a pattern if it exists, otherwise creates it (upsert).
How do you model an n-ary relationship in a property graph?::Reify it as an intermediate node connected to all participants.
What is WITH used for in Cypher?::Pipelining — passing/aggregating intermediate results to the next query part (like a subquery boundary).
Cypher's match semantics regarding relationships?::Relationship isomorphism — the same relationship cannot appear twice in one pattern match.
What is a super-node and why is it a problem?::A node with an extremely high degree; traversals through it become very expensive.
