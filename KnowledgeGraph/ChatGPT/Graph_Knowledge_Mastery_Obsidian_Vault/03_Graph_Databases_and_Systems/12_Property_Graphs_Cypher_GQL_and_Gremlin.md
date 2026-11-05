---
title: "Property Graphs, Cypher, GQL and Gremlin"
type: chapter
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - property-graph
  - cypher
  - gql
  - gremlin
  - graph-database
---
# Property Graphs, Cypher, GQL and Gremlin

> [!goal]
> Model and query property graphs fluently, understand the declarative-versus-traversal distinction, and know what the GQL standard changes.

## 1. The property-graph model

A property graph contains:

- **nodes** representing identifiable things;
- **relationships/edges** connecting nodes, normally directed and typed;
- **labels** or types attached to nodes;
- **properties** attached to nodes and relationships;
- implementation-specific identifiers and schema constraints.

A compact mathematical view is

$$G=(V,E,\lambda_V,\lambda_E,P_V,P_E),$$

where $V$ and $E$ are nodes and edges, $\lambda$ assigns labels/types, and $P$ assigns key-value properties.

Unlike a plain graph, an edge can carry business facts. A `SOLD` edge can include `date`, `quantity`, `channel`, and `sourceBatch`. This makes relationship-centric domains natural, but it also creates modeling choices: should a sale be an edge or a `SaleEvent` node?

> [!important] Edge or node?
> Use an edge when the relation is simple, binary, and has no independent lifecycle. Promote it to a node when it needs participants beyond two, multiple timestamps, its own identity, provenance, versioning, access control, or links to other facts.

## 2. Modeling discipline

Model for questions and invariants, not visual attractiveness.

| Decision | Prefer node | Prefer property | Prefer relationship |
|---|---|---|---|
| Has identity/lifecycle | Yes | No | Sometimes |
| Independently queried | Yes | Rarely | Yes |
| Connects entities | Sometimes | No | Yes |
| Atomic scalar | No | Yes | No |
| Repeated or multi-valued | Often | Carefully | Often |
| Requires provenance | Often | With metadata pattern | Edge properties or assertion node |

Avoid:

- mega-nodes with hundreds of unrelated properties;
- generic `RELATED_TO` edges that erase domain meaning;
- storing comma-separated lists in one property;
- duplicating the same fact as edge and property without a synchronization rule;
- using display labels as stable identifiers;
- unbounded paths in online queries without controls.

## 3. Cypher mental model

Cypher is a declarative pattern-matching language. A query describes graph patterns and transformations; the engine selects physical operators.

```cypher
MATCH (d:Dealer)-[:LOCATED_IN]->(r:Region)
MATCH (d)-[s:SOLD]->(m:VehicleModel)
WHERE s.saleDate >= date('2026-10-01')
WITH r, m, sum(s.quantity) AS units
WHERE units >= 50
RETURN r.code AS region, m.name AS model, units
ORDER BY units DESC;
```

Read it as a pipeline:

1. bind dealer-region patterns;
2. expand to sales and models;
3. filter by time;
4. aggregate by region and model;
5. filter groups;
6. project and sort.

Core clauses:

- `MATCH`, `OPTIONAL MATCH`;
- `WHERE`;
- `WITH` as projection, grouping and pipeline boundary;
- `RETURN`;
- `UNWIND` for lists to rows;
- `CREATE`, `MERGE`, `SET`, `REMOVE`, `DELETE`;
- `CALL` for subqueries and procedures;
- path patterns and quantified path patterns.

### `MERGE` is not magic upsert

`MERGE` guarantees a pattern exists according to the pattern and transaction isolation. It does not automatically know your business key.

```cypher
CREATE CONSTRAINT dealer_code_unique IF NOT EXISTS
FOR (d:Dealer) REQUIRE d.code IS UNIQUE;

UNWIND $rows AS row
MERGE (d:Dealer {code: row.dealerCode})
ON CREATE SET d.createdAt = datetime()
SET d.name = row.dealerName,
    d.updatedAt = datetime();
```

Create uniqueness constraints before concurrent ingestion. Otherwise logically duplicate nodes can be created.

## 4. Path semantics

A path is an alternating sequence of nodes and relationships. Questions that sound similar can have different semantics:

- reachability: does any path exist?
- shortest path by hop count;
- least-cost path by weights;
- simple path: no repeated node;
- trail: no repeated edge;
- walk: repetition permitted;
- all matching paths, which may explode combinatorially.

```cypher
MATCH p = SHORTEST 1
  (a:Dealer {code:$a})-[:SIMILAR_TO|IN_REGION]-+
  (b:Dealer {code:$b})
RETURN length(p), p;
```

Never assume a query language's default path uniqueness. Check the exact version and operator semantics.

## 5. Query performance reasoning

Performance is dominated by:

- starting cardinality;
- index/constraint availability;
- expansion degree;
- selectivity of predicates;
- path length and uniqueness semantics;
- intermediate row multiplication;
- aggregation and sorting volume;
- memory pressure and remote communication.

Use `EXPLAIN` before execution and `PROFILE` on controlled data. Look for label scans where an index seek is expected, accidental Cartesian products, high estimated-versus-actual cardinality error, repeated expansions, eager materialization, and late filters.

```cypher
PROFILE
MATCH (d:Dealer {code:$dealer})-[:HAS_SALES_OBSERVATION]->(o)
WHERE o.period >= $from AND o.period < $to
RETURN o
ORDER BY o.period;
```

A useful rewrite rule is: **anchor selectively, filter early when semantics permit, aggregate before fan-out, and return only required fields.**

## 6. GQL

ISO/IEC 39075:2024 defines GQL, the first international standard specifically for property-graph data and querying. It covers graph types, graph creation and maintenance, pattern matching, paths, expressions and data modification. Technical Corrigendum 1 was published in July 2026.

GQL is important for conceptual portability, but standardization does not make every product feature interchangeable. Vendors differ in supported subsets, extensions, transaction behavior, indexing, procedures and graph algorithms.

Study GQL at three levels:

1. **model**: property graphs and graph types;
2. **language semantics**: pattern variables, path modes, matching, null/missing behavior;
3. **implementation mapping**: which GQL features your database supports and how they perform.

Authoritative references:

- [ISO/IEC 39075:2024 GQL](https://www.iso.org/standard/76120.html)
- [GQL Technical Corrigendum 1:2026](https://www.iso.org/standard/93701.html)
- [GQL Standards overview](https://www.gqlstandards.org/)

## 7. Gremlin

Gremlin, from Apache TinkerPop, is a graph traversal language expressed as a chain of steps. It is functional/data-flow oriented and can target multiple TinkerPop-enabled graph systems.

```groovy
g.V().hasLabel('Dealer').has('code', dealerCode).
  outE('SOLD').has('saleDate', gte(fromDate)).
  group().
    by(inV().values('name')).
    by(values('quantity').sum())
```

A traversal consists of traversers carrying objects, path history, side effects, sacks and bulk. Steps are broadly:

- map: transform each traverser;
- flatMap: emit zero or more values;
- filter: retain/discard;
- sideEffect: observe or mutate without changing the traversed object;
- barrier: coordinate/aggregate traversers;
- branch: choose paths.

Gremlin can be written in language variants such as Python, Java and JavaScript, but server/provider support varies. TinkerPop 3.8.2 is the current stable line as of September 2026.

## 8. Cypher versus Gremlin versus GQL

| Dimension | Cypher | Gremlin | GQL |
|---|---|---|---|
| Primary style | Declarative pattern query | Composable traversal | Standardized declarative graph language |
| Portability | Broad but dialect-dependent | Provider ecosystem | Standard target; implementation coverage varies |
| Learning strength | Readable graph patterns | Explicit traversal control | Formal cross-vendor semantics |
| Typical risk | Hidden row explosion | Imperative-looking hard-to-optimize traversals | Assuming unsupported standard features |
| Best study outcome | Query and profile production property graphs | Understand traversal algebra and provider portability | Reason about common language semantics |

Do not choose solely by syntax. Choose a database based on workload, consistency, deployment, scale, ecosystem and operational constraints; then master its query language.

## 9. Laboratory

Build the same 50,000-entity domain graph twice:

1. Neo4j with Cypher;
2. a TinkerPop-enabled system or Gremlin Server.

Implement:

- idempotent ingestion;
- uniqueness constraints;
- one-hop and multi-hop queries;
- weighted shortest path;
- community-oriented aggregation;
- update and deletion;
- query-plan inspection.

Record latency at p50/p95, result correctness, query readability, portability gaps and operational complexity.

## 10. Mastery checklist

- [ ] I can justify node-versus-edge modeling.
- [ ] I can explain rows, bindings and cardinality through a Cypher pipeline.
- [ ] I can state the exact path semantics I need.
- [ ] I can profile and repair a query with row explosion.
- [ ] I understand the role and limits of GQL standardization.
- [ ] I can express the same traversal in Cypher and Gremlin.

## Sources and next reading

- [Neo4j Cypher Manual, current Cypher 25](https://neo4j.com/docs/cypher-manual/current/)
- [Apache TinkerPop 3.8.2 documentation](https://tinkerpop.apache.org/docs/current/reference/)
- [Graph Databases, 2nd ed.](https://www.oreilly.com/library/view/graph-databases-2nd/9781491930885/)
- [[13_Graph_Database_Internals_and_Distributed_Systems]]
- [[14_RDF_vs_Property_Graphs_and_Interoperability]]
