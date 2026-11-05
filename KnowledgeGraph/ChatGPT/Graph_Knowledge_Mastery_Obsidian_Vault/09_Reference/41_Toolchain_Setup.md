---
title: "Toolchain Setup"
type: reference
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - toolchain
  - setup
  - python
  - neo4j
  - rdf
  - gnn
---
# Toolchain Setup

> [!goal]
> Create a versioned, reproducible workstation for ontology, RDF, property graphs, analytics, graph ML and agent experiments.

## 1. Installation principles

- Use isolated environments; never install research packages into system Python.
- Pin exact versions in project lockfiles; this note records the November 2026 landscape, not a permanent version guarantee.
- Keep data, code, configuration and results separately versioned.
- Use containers for services and reproducibility, but understand native installation for debugging.
- Record CPU/GPU, CUDA, OS and database versions in every experiment.
- Start with one tool per layer; add alternatives only for a concrete comparison.

## 2. Recommended stack

| Layer | Minimum choice | Add when needed |
|---|---|---|
| Language/env | Python 3.11-3.13, `uv` or Conda | Java 21 for Jena/ROBOT tools |
| RDF | RDFLib 7.6.x | Apache Jena 6.2/Fuseki; Oxigraph/GraphDB |
| Ontology | Protégé 5.6.9 | WebProtégé, Owlready2 0.52, OWLAPI |
| Validation | pySHACL 0.40.x | Jena SHACL/vendor engine |
| Property graph | Neo4j Desktop/Community | TinkerPop/Gremlin provider |
| Classical graph | NetworkX 3.7 | igraph, graph-tool, GraphBLAS |
| Graph ML | PyTorch + PyG 2.9 | DGL, PyKEEN |
| Experiment | pytest, MLflow/W&B optional | DVC/lakeFS when data needs it |
| Agent/RAG | your chosen orchestration library | keep core graph interfaces framework-neutral |
| Quality | Ruff, mypy/pyright, pre-commit | security/dependency scanners |

Current official references:

- [RDFLib 7.6.0 release](https://github.com/RDFLib/rdflib/releases)
- [Apache Jena 6.2.0 downloads](https://jena.apache.org/download/)
- [NetworkX 3.7 documentation](https://networkx.org/documentation/stable/)
- [Owlready2 0.52](https://owlready2.readthedocs.io/)
- [Protégé 5.6.9](https://protege.stanford.edu/software/)
- [pySHACL releases](https://github.com/RDFLib/pySHACL/releases)
- [PyG documentation](https://pytorch-geometric.readthedocs.io/)
- [DGL documentation](https://www.dgl.ai/)

## 3. Repository layout

```text
graph-mastery/
  README.md
  pyproject.toml
  uv.lock                 # or environment.yml/poetry.lock
  .env.example
  Makefile
  docker-compose.yml
  configs/
  data/
    raw/                  # immutable; normally not committed
    interim/
    processed/
    README.md
  ontology/
    src/
    shapes/
    mappings/
    examples/
    tests/
  src/
    ingestion/
    entity_resolution/
    graph/
    ml/
    rag/
    agents/
  queries/
    sparql/
    cypher/
  tests/
  experiments/
    manifests/
    configs/
  results/
    raw/
    reports/
  notebooks/             # exploration, not production logic
  docs/
```

## 4. Python environment

### Option A: `uv`

```bash
uv init
uv python pin 3.12
uv add rdflib pyshacl owlready2 networkx pandas numpy scipy scikit-learn
uv add torch torch-geometric
uv add --dev pytest ruff mypy pre-commit jupyterlab
uv lock
```

Install PyTorch/PyG against the appropriate CPU/CUDA build using their official selectors. Do not blindly copy an old CUDA command.

### Option B: Conda

```bash
conda create -n graph-mastery python=3.12 -y
conda activate graph-mastery
python -m pip install --upgrade pip
pip install rdflib pyshacl owlready2 networkx pandas numpy scipy scikit-learn
pip install torch torch-geometric
pip install pytest ruff mypy jupyterlab
```

Export both human-readable and explicit environment records.

## 5. Java tools

Jena 6 requires Java 21 or later. Verify:

```bash
java -version
```

Download Apache Jena/Fuseki from the official release page and verify signatures/checksums. Add the binary folder to `PATH` or run Fuseki in a container.

## 6. Neo4j

### Desktop

Neo4j Desktop is convenient on Windows and bundles a suitable JDK for its DBMS. Create a local project, database and a separate least-privilege user for applications.

### Container example

```yaml
services:
  neo4j:
    image: neo4j:2026.10
    ports:
      - "7474:7474"
      - "7687:7687"
    environment:
      NEO4J_AUTH: "neo4j/change-this-password"
    volumes:
      - neo4j_data:/data
      - ./plugins:/plugins
volumes:
  neo4j_data:
```

Pin a version compatible with the GDS/plugin versions you actually use. Never expose Bolt/HTTP publicly with default credentials.

### Smoke test

```cypher
CREATE CONSTRAINT person_id IF NOT EXISTS
FOR (p:Person) REQUIRE p.id IS UNIQUE;
MERGE (a:Person {id:'a'}) SET a.name='Ada'
MERGE (b:Person {id:'b'}) SET b.name='Grace'
MERGE (a)-[:KNOWS {since:2026}]->(b);
MATCH (a:Person)-[r:KNOWS]->(b) RETURN a.name, r.since, b.name;
```

## 7. RDFLib smoke test

```python
from rdflib import Graph, Namespace, Literal, RDF

EX = Namespace("https://example.org/")
g = Graph()
g.bind("ex", EX)
g.add((EX.ada, RDF.type, EX.Person))
g.add((EX.ada, EX.name, Literal("Ada")))

rows = g.query("""
PREFIX ex: <https://example.org/>
SELECT ?name WHERE { ex:ada ex:name ?name }
""")
assert [str(row.name) for row in rows] == ["Ada"]
print(g.serialize(format="turtle"))
```

## 8. SHACL smoke test

```python
from pyshacl import validate
from rdflib import Graph

data = Graph().parse("ontology/examples/data.ttl")
shapes = Graph().parse("ontology/shapes/shapes.ttl")
conforms, report_graph, report_text = validate(
    data_graph=data,
    shacl_graph=shapes,
    inference="rdfs",
    abort_on_first=False,
)
print(report_text)
assert conforms
```

## 9. Protégé workflow

1. Create separate ontology source and generated/release files.
2. Set a stable base IRI.
3. Add labels and definitions before complex axioms.
4. Configure HermiT or another compatible reasoner.
5. Keep example individuals in a separate module when possible.
6. Export Turtle for readable diffs.
7. Run automated CI tests outside the UI.

Do not commit temporary lock/session files.

## 10. Jena/Fuseki smoke test

Start Fuseki with a test dataset, then run `curl` or a SPARQL client against `/query`. Keep separate datasets for development, tests and production-like experiments. Verify update permissions independently from query permissions.

## 11. NetworkX smoke test

```python
import networkx as nx

G = nx.DiGraph()
G.add_weighted_edges_from([("a", "b", 1.0), ("b", "c", 2.0)])
assert nx.shortest_path(G, "a", "c", weight="weight") == ["a", "b", "c"]
print(nx.pagerank(G))
```

NetworkX favors clarity and rich algorithms, not massive graph performance. Move to scalable systems only after confirming semantics on a smaller graph.

## 12. PyG smoke test

```python
import torch
from torch_geometric.data import Data
from torch_geometric.nn import GCNConv

x = torch.tensor([[1.0], [0.0], [1.0]])
edge_index = torch.tensor([[0, 1, 1, 2], [1, 0, 2, 1]])
data = Data(x=x, edge_index=edge_index)

layer = GCNConv(1, 4)
out = layer(data.x, data.edge_index)
assert out.shape == (3, 4)
```

## 13. Reproducibility configuration

Record:

```yaml
experiment_id: exp-2026-001
code_commit: <git-sha>
data_version: <checksum-or-tag>
ontology_version: 0.2.0
mapping_version: 0.4.1
graph_snapshot: 2026-11-05T00:00:00Z
seed: 42
hardware: <cpu-gpu-memory>
software_lock: uv.lock
```

Set random seeds, but do not promise perfect determinism across GPU/library versions. Record repeated runs.

## 14. CI pipeline

Minimum stages:

1. lint/type check;
2. unit tests;
3. parse ontology/RDF;
4. reasoner/consistency tests;
5. SHACL tests;
6. SPARQL/Cypher expected-result tests;
7. tiny ML smoke test;
8. build documentation/artifacts;
9. dependency/security checks.

Large benchmarks run on schedule or manual workflow, not every commit.

## 15. Secrets and data

- `.env` is ignored; commit `.env.example` only.
- Use a secret manager in deployed environments.
- Never commit customer/proprietary data, tokens or database dumps.
- Create synthetic/open fixtures reproducing the schema and failure.
- Check licenses before distributing datasets/models.

## 16. Setup completion checklist

- [ ] Clean environment can install from lockfile.
- [ ] RDFLib/SPARQL smoke test passes.
- [ ] Protégé opens ontology and reasoner works.
- [ ] SHACL test passes and a bad fixture fails.
- [ ] Neo4j query and constraint work.
- [ ] NetworkX algorithm test works.
- [ ] PyG forward pass works.
- [ ] CI runs all small tests.
- [ ] Experiment manifest records versions.
- [ ] Backup/restore of local graph stores is tested.
