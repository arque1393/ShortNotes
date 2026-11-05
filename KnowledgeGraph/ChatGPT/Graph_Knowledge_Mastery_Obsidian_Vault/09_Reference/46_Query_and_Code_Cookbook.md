---
title: "Query and Code Cookbook"
type: reference
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - cookbook
  - sparql
  - cypher
  - rdflib
  - pyg
  - testing
---
# Query and Code Cookbook

> [!abstract]
> Reusable patterns for the most common graph tasks. Treat every snippet as a starting point: pin versions, add tests, record assumptions, and profile against representative data before production use.

## 1. Reproducible project skeleton

```text
graph-project/
|-- README.md
|-- pyproject.toml
|-- uv.lock or requirements.lock
|-- data/
|   |-- raw/
|   |-- interim/
|   `-- processed/
|-- ontology/
|   |-- domain.ttl
|   `-- shapes.ttl
|-- queries/
|   |-- sparql/
|   `-- cypher/
|-- src/
|   |-- ingest/
|   |-- resolve/
|   |-- validate/
|   |-- retrieve/
|   `-- evaluate/
|-- tests/
|-- experiments/
|-- reports/
`-- configs/
```

Minimum principles:

1. Raw data is immutable.
2. Every transformation has a versioned configuration.
3. Generated identifiers are deterministic.
4. Validation precedes publication.
5. Evaluation data is isolated from tuning data.
6. Each experiment records code, data, ontology and model versions.

## 2. RDFLib: construct, parse and serialize RDF

```python
from __future__ import annotations

from rdflib import Graph, Literal, Namespace, RDF, RDFS, URIRef, XSD

EX = Namespace("https://example.org/kg/")
SCHEMA = Namespace("https://schema.org/")

g = Graph()
g.bind("ex", EX)
g.bind("schema", SCHEMA)

dealer = EX["dealer/D001"]
region = EX["region/East"]

g.add((dealer, RDF.type, EX.Dealer))
g.add((dealer, SCHEMA.name, Literal("Example Dealer", lang="en")))
g.add((dealer, EX.dealerCode, Literal("D001", datatype=XSD.string)))
g.add((dealer, EX.locatedIn, region))
g.add((region, RDF.type, EX.Region))
g.add((region, RDFS.label, Literal("East Region", lang="en")))

g.serialize("data/processed/dealers.ttl", format="turtle")
```

Parse defensively:

```python
from pathlib import Path
from rdflib import Graph

path = Path("data/processed/dealers.ttl")
g = Graph()
g.parse(path, format="turtle")
print(f"Loaded {len(g):,} triples")
```


In production, fail fast on parsing errors, verify expected namespaces, and record the source checksum.

## 3. Deterministic identifiers

Never use display labels as identifiers. A stable source key can be mapped to an IRI:

```python
from urllib.parse import quote

BASE = "https://example.org/kg/"

def iri_for(kind: str, source_key: str) -> str:
    clean_kind = quote(kind.strip(), safe="")
    clean_key = quote(source_key.strip(), safe="")
    return f"{BASE}{clean_kind}/{clean_key}"
```

For composite or sensitive identifiers, use a namespaced hash:

```python
import hashlib


def stable_hash(namespace: str, *parts: str) -> str:
    canonical = "\x1f".join([namespace, *(p.strip() for p in parts)])
    return hashlib.sha256(canonical.encode("utf-8")).hexdigest()
```

A hash does not automatically anonymize data. Small domains and linkable auxiliary data can enable re-identification.

## 4. RDF datasets and named graphs

Use named graphs when provenance, tenancy, source snapshots or access policies differ.

```python
from rdflib import Dataset, Namespace, RDF, URIRef

EX = Namespace("https://example.org/kg/")
ds = Dataset()

source_graph = ds.graph(URIRef("https://example.org/graph/source/crm/2026-11-05"))
source_graph.add((EX["dealer/D001"], RDF.type, EX.Dealer))

curated_graph = ds.graph(URIRef("https://example.org/graph/curated/current"))
curated_graph.add((EX["dealer/D001"], EX.status, EX.Active))
```

Model provenance at the level required by decisions:

- graph-level provenance for a source batch;
- statement-level provenance for disputed or independently changing assertions;
- derivation activity for computed facts;
- evidence spans for extracted text claims.

## 5. SPARQL query patterns

Assume:

```sparql
PREFIX ex: <https://example.org/kg/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
```

### 5.1 Typed selection

```sparql
SELECT ?dealer ?name ?region
WHERE {
  ?dealer a ex:Dealer ;
          ex:name ?name ;
          ex:locatedIn ?region .
}
ORDER BY LCASE(STR(?name))
```

### 5.2 OPTIONAL without accidental row loss

```sparql
SELECT ?dealer ?name ?manager
WHERE {
  ?dealer a ex:Dealer ; ex:name ?name .
  OPTIONAL { ?dealer ex:managedBy ?manager . }
}
```

A filter outside the `OPTIONAL` can remove unbound rows. Put a condition inside when absence must remain valid:

```sparql
OPTIONAL {
  ?dealer ex:managedBy ?manager .
  ?manager ex:active true .
}
```

### 5.3 Absence under open-world semantics

```sparql
SELECT ?dealer
WHERE {
  ?dealer a ex:Dealer .
  FILTER NOT EXISTS { ?dealer ex:managedBy ?manager }
}
```

This means the dataset has no matching assertion. It does not prove that no manager exists in reality.

### 5.4 Aggregation with stable grain

```sparql
SELECT ?region (COUNT(DISTINCT ?dealer) AS ?dealerCount)
WHERE {
  ?dealer a ex:Dealer ; ex:locatedIn ?region .
}
GROUP BY ?region
ORDER BY DESC(?dealerCount)
```

Before aggregation, write the intended row grain: one row per region, dealer, claim, event or interval.

### 5.5 Property paths

```sparql
SELECT DISTINCT ?ancestor
WHERE {
  ex:Part123 ex:partOf+ ?ancestor .
}
```

Use bounded paths when the business meaning has a maximum depth. Unbounded paths can be semantically vague and expensive.

### 5.6 CONSTRUCT a retrieval subgraph

```sparql
CONSTRUCT {
  ?dealer ex:locatedIn ?region .
  ?dealer ex:hasMetric ?metric .
  ?metric ex:metricType ?type ; ex:value ?value ; ex:period ?period .
}
WHERE {
  VALUES ?dealer { ex:dealer/D001 }
  ?dealer ex:locatedIn ?region ; ex:hasMetric ?metric .
  ?metric ex:metricType ?type ; ex:value ?value ; ex:period ?period .
  FILTER(?period >= "2026-01" && ?period <= "2026-10")
}
```

`CONSTRUCT` is useful for GraphRAG evidence packages because the output preserves connected structure.

### 5.7 Parameterization

Do not concatenate untrusted strings into SPARQL. Use prepared bindings where the client supports them, validate IRIs, and allow-list predicates and graph names. Language models should select from a constrained semantic catalog rather than invent arbitrary query fragments.

## 6. SPARQL Update and idempotency

```sparql
DELETE {
  GRAPH <https://example.org/graph/curated/current> {
    ex:dealer/D001 ex:status ?old .
  }
}
INSERT {
  GRAPH <https://example.org/graph/curated/current> {
    ex:dealer/D001 ex:status ex:Active .
  }
}
WHERE {
  OPTIONAL {
    GRAPH <https://example.org/graph/curated/current> {
      ex:dealer/D001 ex:status ?old .
    }
  }
}
```

Prefer replacing a source snapshot or upserting by deterministic identity over appending duplicate facts.

## 7. SHACL validation

A compact shape:

```turtle
@prefix ex: <https://example.org/kg/> .
@prefix sh: <http://www.w3.org/ns/shacl#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

ex:DealerShape
    a sh:NodeShape ;
    sh:targetClass ex:Dealer ;
    sh:property [
        sh:path ex:dealerCode ;
        sh:minCount 1 ;
        sh:maxCount 1 ;
        sh:datatype xsd:string ;
        sh:pattern "^[A-Z0-9-]+$" ;
    ] ;
    sh:property [
        sh:path ex:locatedIn ;
        sh:minCount 1 ;
        sh:class ex:Region ;
    ] .
```

Validate with pySHACL:

```python
from pathlib import Path
from pyshacl import validate

conforms, report_graph, report_text = validate(
    data_graph=str(Path("data/processed/dealers.ttl")),
    shacl_graph=str(Path("ontology/shapes.ttl")),
    inference="rdfs",
    abort_on_first=False,
    allow_infos=True,
    allow_warnings=True,
)

print(report_text)
if not conforms:
    raise SystemExit("SHACL validation failed")
```

Keep three shape profiles:

1. ingestion: minimal requirements for accepting a source batch;
2. publication: stronger requirements for curated data;
3. application: workload-specific constraints for an API or agent.

Do not confuse SHACL conformance with universal truth. It is validation against chosen constraints.

## 8. OWL with Owlready2

```python
from owlready2 import DataProperty, FunctionalProperty, ObjectProperty, Thing, get_ontology

onto = get_ontology("https://example.org/ontology/dealer.owl")

with onto:
    class Organization(Thing):
        pass

    class Dealer(Organization):
        pass

    class Region(Thing):
        pass

    class located_in(ObjectProperty):
        domain = [Dealer]
        range = [Region]

    class dealer_code(DataProperty, FunctionalProperty):
        domain = [Dealer]
        range = [str]

with onto:
    dealer = Dealer("D001")
    east = Region("East")
    dealer.located_in = [east]
    dealer.dealer_code = "D001"

onto.save(file="ontology/dealer.owl", format="rdfxml")
```

Reasoning requires a compatible Java reasoner or configured backend. Keep asserted and inferred graphs separable so you can explain where a fact came from and rebuild materialization.

## 9. Jena command-line workflow

Typical Apache Jena tools include RDF parsing/format conversion, SPARQL execution and Fuseki. Exact command names and options depend on the installed release, so check `--help` for the pinned version.

```bash
riot --validate data/processed/dealers.ttl
riot --output=JSONLD data/processed/dealers.ttl > data/processed/dealers.jsonld
arq --data=data/processed/dealers.ttl --query=queries/sparql/dealers.rq
```

For Fuseki, keep separate configuration for development, test and production. Do not expose an unrestricted update endpoint to agents or public clients.

## 10. Cypher schema and idempotent ingestion

### 10.1 Constraints first

```cypher
CREATE CONSTRAINT dealer_id IF NOT EXISTS
FOR (d:Dealer) REQUIRE d.id IS UNIQUE;

CREATE CONSTRAINT region_id IF NOT EXISTS
FOR (r:Region) REQUIRE r.id IS UNIQUE;
```

### 10.2 Deterministic upsert

```cypher
UNWIND $rows AS row
MERGE (d:Dealer {id: row.dealer_id})
SET d.name = row.dealer_name,
    d.updated_at = datetime(row.updated_at)
MERGE (r:Region {id: row.region_id})
MERGE (d)-[:LOCATED_IN]->(r);
```

`MERGE` the identity pattern only. Merging an entire mutable property map can create duplicates.

### 10.3 Query with explicit grain

```cypher
MATCH (d:Dealer)-[:LOCATED_IN]->(r:Region)
OPTIONAL MATCH (d)-[:HAS_METRIC]->(m:Metric {type: "sales"})
WHERE m.period >= date("2026-01-01") AND m.period < date("2026-11-01")
RETURN r.id AS region,
       count(DISTINCT d) AS dealers,
       sum(m.value) AS sales
ORDER BY sales DESC;
```

Check whether multiple metric nodes per dealer-period can multiply rows. Aggregate at the metric grain before joining to other one-to-many paths.

### 10.4 Controlled variable-length path

```cypher
MATCH p = (start:Part {id: $part_id})-[:PART_OF*1..8]->(ancestor:Assembly)
WHERE all(n IN nodes(p) WHERE n.active = true)
RETURN ancestor.id, length(p)
ORDER BY length(p);
```

Bound depth and relationship type. Avoid an unrestricted `[*]` over high-degree graphs.

### 10.5 Query plan inspection

```cypher
EXPLAIN
MATCH (d:Dealer {id: $dealer_id})-[:HAS_METRIC]->(m:Metric)
RETURN m;
```

Use `PROFILE` on safe test data or a controlled production workload. Inspect:

- index seek versus label scan;
- estimated versus actual cardinality;
- repeated expansion;
- eager materialization;
- memory-heavy sort/aggregation;
- cross products caused by disconnected patterns.

## 11. Temporal facts in property graphs

Represent a fact with validity and transaction time when corrections matter:

```cypher
CREATE (a:Dealer {id: "D001"})
CREATE (r:Region {id: "East"})
CREATE (a)-[:LOCATED_IN {
  valid_from: date("2026-01-01"),
  valid_to: null,
  recorded_at: datetime("2026-01-02T09:00:00Z"),
  source: "crm"
}]->(r);
```

As-of query:

```cypher
MATCH (d:Dealer {id: $id})-[rel:LOCATED_IN]->(r:Region)
WHERE rel.valid_from <= date($as_of)
  AND (rel.valid_to IS NULL OR date($as_of) < rel.valid_to)
RETURN r, rel;
```

For conflicting or richly attributed claims, model an assertion/event node rather than overloading an edge.

## 12. Gremlin traversal patterns

```groovy
g.V().hasLabel('Dealer').has('id', dealerId)
 .out('LOCATED_IN')
 .values('name')
```

Two-hop neighborhood with cycle protection:

```groovy
g.V().has('Dealer', 'id', dealerId)
 .repeat(bothE().otherV().simplePath())
 .times(2)
 .path()
```

Gremlin is traversal-oriented. Think in steps, traversers, barriers and side effects. Profile traversals and control fan-out.

## 13. NetworkX analytics

```python
import networkx as nx

G = nx.DiGraph()
G.add_edge("D001", "East", relation="LOCATED_IN")
G.add_edge("D001", "M001", relation="HAS_METRIC")

print(nx.number_of_nodes(G), nx.number_of_edges(G))
```

PageRank:

```python
scores = nx.pagerank(G, alpha=0.85)
```

Weakly connected components:

```python
components = list(nx.weakly_connected_components(G))
```

Shortest path on an unweighted graph:

```python
path = nx.shortest_path(G.to_undirected(), source="D001", target="East")
```

NetworkX is excellent for algorithms, prototypes and medium-size in-memory graphs. It is not a distributed graph database or a replacement for transactional storage.

## 14. PyTorch Geometric: node classification skeleton

```python
from __future__ import annotations

import torch
from torch import nn
from torch_geometric.nn import GCNConv


class GCN(nn.Module):
    def __init__(self, in_channels: int, hidden_channels: int, out_channels: int) -> None:
        super().__init__()
        self.conv1 = GCNConv(in_channels, hidden_channels)
        self.conv2 = GCNConv(hidden_channels, out_channels)

    def forward(self, x: torch.Tensor, edge_index: torch.Tensor) -> torch.Tensor:
        x = self.conv1(x, edge_index).relu()
        x = nn.functional.dropout(x, p=0.5, training=self.training)
        return self.conv2(x, edge_index)


model = GCN(dataset.num_features, 128, dataset.num_classes)
optimizer = torch.optim.AdamW(model.parameters(), lr=1e-3, weight_decay=1e-4)

for epoch in range(1, 201):
    model.train()
    optimizer.zero_grad()
    logits = model(data.x, data.edge_index)
    loss = nn.functional.cross_entropy(logits[data.train_mask], data.y[data.train_mask])
    loss.backward()
    optimizer.step()
```

Before interpreting performance, verify:

- whether validation/test nodes or edges leak through feature construction;
- whether the intended setting is transductive or inductive;
- whether labels are temporally available;
- whether a feature-only MLP baseline is competitive;
- whether graph rewiring, random features or shuffled edges change results.

## 15. Link prediction without false optimism

A minimal scoring loop is not enough. The candidate set and negative sampler define the task.

```python
from dataclasses import dataclass
import torch


@dataclass(frozen=True)
class TripleBatch:
    head: torch.Tensor
    relation: torch.Tensor
    tail: torch.Tensor


def translational_score(
    entity: torch.Tensor,
    relation: torch.Tensor,
    batch: TripleBatch,
) -> torch.Tensor:
    h = entity[batch.head]
    r = relation[batch.relation]
    t = entity[batch.tail]
    return -(h + r - t).norm(p=1, dim=-1)
```

Evaluation checklist:

- filtered ranking removes known true alternatives;
- negatives respect head/tail type constraints;
- time-aware tasks do not sample future-invalid entities;
- inverse and duplicate relations are audited;
- candidate coverage and calibration are reported;
- relation-wise metrics expose rare-relation failure.

See [[28_Graph_ML_Evaluation_Datasets_and_Benchmarks]].

## 16. Entity resolution pipeline

```python
from dataclasses import dataclass
from rapidfuzz.fuzz import ratio


@dataclass(frozen=True)
class EntityRecord:
    source: str
    source_id: str
    name: str
    postal_code: str | None


def normalize_name(value: str) -> str:
    return " ".join(value.casefold().strip().split())


def pair_features(left: EntityRecord, right: EntityRecord) -> dict[str, float]:
    name_score = ratio(normalize_name(left.name), normalize_name(right.name)) / 100.0
    postal_exact = float(
        left.postal_code is not None
        and right.postal_code is not None
        and left.postal_code == right.postal_code
    )
    return {"name_similarity": name_score, "postal_exact": postal_exact}
```

A production pipeline needs:

1. candidate blocking with measured recall;
2. pair features and calibrated match probability;
3. pair-to-cluster logic with consistency constraints;
4. human review for ambiguous/high-impact cases;
5. provenance for each merge;
6. reversible decisions and versioned golden records.

Never auto-merge solely on embedding similarity.

## 17. Typed retrieval plan for GraphRAG

Represent a retrieval request as a validated object:

```python
from dataclasses import dataclass
from datetime import date
from typing import Literal


@dataclass(frozen=True)
class RetrievalPlan:
    intent: Literal["lookup", "comparison", "path", "aggregate", "global_summary"]
    entity_ids: tuple[str, ...]
    relation_allowlist: tuple[str, ...]
    max_hops: int
    valid_on: date | None
    require_provenance: bool = True
```

Execution stages:

```text
question
  -> entity/intent resolution
  -> policy and scope check
  -> typed retrieval plan
  -> graph/vector/text tools
  -> evidence normalization
  -> claim-level generation
  -> citation/entailment checks
  -> answer or abstention
```

Do not allow the model to submit unrestricted query text directly to a privileged database. Use parameterized templates or a query validator and read-only role.

## 18. Claim-evidence representation

```python
from dataclasses import dataclass


@dataclass(frozen=True)
class EvidenceRef:
    source_id: str
    locator: str
    retrieved_at: str
    confidence: float | None = None


@dataclass(frozen=True)
class SupportedClaim:
    text: str
    evidence: tuple[EvidenceRef, ...]
    derivation: str  # asserted, inferred, computed, predicted, generated
```

At answer time, require every material factual claim to carry evidence or be marked as uncertainty/interpretation. Store the retrieval plan and tool outputs for audit.

## 19. Query and ontology tests

### 19.1 Golden query test

```python
EXPECTED = {
    "region": "East",
    "dealer_count": 42,
}

result = run_named_query("regional_dealer_count", parameters={"as_of": "2026-10-31"})
assert result == EXPECTED
```

### 19.2 Competency-question test

```text
CQ: Which active dealers had no valid manager assignment on 2026-10-31?
Given: fixture graph v3
Expected entities: D017, D031
Expected interpretation: absence from curated assignment graph under closed application profile
```

### 19.3 Metamorphic tests

Examples:

- renaming labels must not change identifier-based answers;
- adding an unrelated connected component must not change a scoped aggregate;
- duplicating source rows must not duplicate curated entities;
- reordering input files must not change output graph hashes;
- adding inferred superclass types must not delete explicit types;
- a future-dated event must not alter an earlier as-of query.

## 20. Performance experiment template

Record:

```yaml
system: neo4j
system_version: "<pin>"
dataset_snapshot: "<checksum>"
node_count: 0
edge_count: 0
query_id: Q-001
parameters_hash: "<hash>"
warmup_runs: 5
measured_runs: 30
cache_state: warm
concurrency: 1
p50_ms: 0
p95_ms: 0
p99_ms: 0
result_count: 0
plan_hash: "<hash>"
```

Latency without result correctness, workload definition and hardware context is not a benchmark.

## 21. Security defaults

- read-only credentials for retrieval;
- separate write pipeline and approval boundary;
- parameterized queries;
- relation, label and graph allow-lists;
- maximum depth, rows, time and memory;
- tenant and row-level filters applied before retrieval;
- provenance and policy checks on generated claims;
- secrets outside prompts and notebooks;
- audit log of plan, query, result and answer;
- adversarial tests for prompt injection in graph literals and source documents.

## 22. What to memorize versus look up

Memorize:

- graph/data grain and identity principles;
- open-world versus closed-world consequences;
- core SPARQL/Cypher matching and aggregation semantics;
- path fan-out risks;
- leakage patterns in graph ML;
- separation of asserted, inferred, computed and predicted facts.

Look up:

- release-specific syntax and configuration;
- optimizer hints;
- draft standards features;
- model hyperparameters;
- vendor-specific procedures;
- exact benchmark preprocessing.

## 23. Practice sequence

- [ ] Build one RDF graph and one property graph from the same five-table dataset.
- [ ] Express ten identical competency questions in SPARQL and Cypher.
- [ ] Add SHACL and database constraints; compare what each catches.
- [ ] Add provenance and an as-of query.
- [ ] Profile one path query and one aggregation.
- [ ] Implement a simple entity resolver and measure blocking recall.
- [ ] Run PageRank and community detection; explain whether results are useful.
- [ ] Train an MLP and GNN with leakage-safe splits.
- [ ] Build a typed GraphRAG retrieval plan and claim-evidence output.
- [ ] Add adversarial and metamorphic tests.

## Related notes

- [[05_RDF_RDFS_and_Linked_Data]]
- [[06_SPARQL_Query_and_Federation]]
- [[09_SHACL_SKOS_Rules_Provenance_and_Identity]]
- [[12_Property_Graphs_Cypher_GQL_and_Gremlin]]
- [[17_Entity_Resolution_and_Knowledge_Fusion]]
- [[24_Graph_Neural_Network_Foundations]]
- [[30_GraphRAG_and_Hybrid_Retrieval]]
- [[33_Safety_Evaluation_and_Production_Operations]]
