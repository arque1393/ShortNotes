---
title: "Courses and Video Lectures"
type: reference
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - courses
  - videos
  - youtube
  - learning-resources
---
# Courses and Video Lectures

> [!goal]
> Use lectures for guided intuition and demonstrations, while relying on standards, books and papers for authoritative claims.

## A. Complete structured courses

### OpenHPI - Knowledge Graphs: Foundations and Applications

[Course page](https://open.hpi.de/learn/knowledgegraphs2023)

**Instructor:** Harald Sack and collaborators. **Status:** self-paced; course page shows an update on 17 September 2026.

**Covers:** graph representation, Semantic Web, RDF, OWL, SPARQL, KGE, KG completion, language models, semantic/exploratory search and hands-on work.

**Use:** Primary guided course for Weeks 9-18 and an overview of later ML/application topics. Since you already know general ML, spend most effort on RDF/OWL/SPARQL and KG-specific sections.

### Stanford CS224W - Machine Learning with Graphs

[Current Fall 2026 course and public materials](https://web.stanford.edu/class/cs224w/)  
[Public 2021 syllabus/materials](https://snap.stanford.edu/class/cs224w-2021/)  
[Official 2021 YouTube playlist](https://www.youtube.com/playlist?list=PLoROMvodv4rPLKxIpqhjhPgdQy7imNkDn)

**Covers:** classical graph ML, embeddings, PageRank, GNNs, KG reasoning, influence and large-graph applications.

**Use:** Follow slides/assignments in the current offering; use the complete 2021 public videos for lecture explanations. Implement assignments rather than only watching.

### Neo4j GraphAcademy

[Course catalog](https://graphacademy.neo4j.com/courses)

**Recommended order:** Neo4j Fundamentals -> Cypher Fundamentals -> Graph Data Modeling Fundamentals -> Intermediate/Advanced Cypher -> Graph Data Science path -> GraphRAG/GenAI courses.

**Strength:** Current, hands-on product training in a browser.

**Caution:** Vendor training demonstrates one ecosystem. Compare with RDF/SPARQL, GQL, Gremlin and non-Neo4j systems.

### Protégé Short Course resources

[Official course page](https://protege.stanford.edu/short-courses)

**Covers:** ontology development, OWL 2, RDF, reasoning, querying, collaborative ontology work and real-world lessons. The site lists a June 23-25, 2026 Stanford course; future offerings vary.

**Use:** Follow topic list and public resources even without attending; practice every concept in your ontology.

### DeepLearning.AI - Agentic Knowledge Graph Construction

[Course page](https://www.deeplearning.ai/courses/agentic-knowledge-graph-construction)

**Covers:** multi-agent construction from structured/unstructured data.

**Use:** A practical supplement after you master schema, evidence, entity resolution and validation. Do not let an agent-generated graph bypass governance.

## B. High-value individual lectures and recent recordings

### MIT OCW - Architectures: Graphs

[Official OCW lecture](https://ocw.mit.edu/courses/6-7960-deep-learning-fall-2024/resources/mit6_7960f24_lec05_mp4/)  
[YouTube video, published 11 February 2026](https://www.youtube.com/watch?v=0niIwb37nF0)

Concise GNN/message-passing overview, connections to MLP/CNN architectures, and expressive limitations.

### KGC 2025 - Choosing an Ontology

[Recording page](https://watch.knowledgegraph.tech/kgc-2025/videos/day-1-classroom-215-choosing-an-ontology-720p)

A 1h45m practical workshop on ontology types/styles, benefits, upper ontologies and choosing multiple ontology families. Pair with an explicit architecture decision record.

### KGC 2025 - AI-Assisted Knowledge Graph Extraction From Text

[Recording page](https://watch.knowledgegraph.tech/videos/day-1-classroom-215-ai-assisted-knowledge-graph-extraction-from-text-720p)

A 1h54m tutorial on ontology-guided extraction and iterative KG building. Evaluate extraction claims against your gold set.

### KGC 2025 - From Research to Reality

[Recording page](https://watch.knowledgegraph.tech/kgc-2025/videos/day-4-auditorium-from-research-to-reality-made-with-clipchamp-720p)

Case study of on-device personal KG use, ontology and reasoning. Useful for product/architecture questions, not an independent benchmark.

### NODES AI 2026 - Agentic GraphRAG: Autonomous KG Construction and Adaptive Retrieval

[Recording page](https://neo4j.com/videos/nodes-ai-2026-agentic-graphrag-autonomous-knowledge-graph-construction-and-adaptive-retrieval/)

**Event date:** 15 April 2026. Demonstrates schema inference, multiple construction agents and vector/graph routing. Use as an implementation pattern; compare against GraphRAG benchmarks and simpler baselines.

### NODES 2025 - Ontology Creation with the Neo4j Data Modeling MCP Server

[YouTube](https://www.youtube.com/watch?v=rVsiZ8UXULg)  
[Neo4j page](https://neo4j.com/videos/ontology-creation-with-the-neo4j-data-modeling-mcp-server/)

Shows model-to-ontology workflow with an MCP server. Critically evaluate formal semantics and governance, because a generated LPG schema is not automatically an OWL ontology.

### NODES 2025 - Agentic GraphRAG: Multi-Agent Knowledge Graph

[Recording page](https://neo4j.com/videos/agnetic-graphrag-multi-agent-knowledge-graph/)

Demonstrates a multi-agent PDF/table-to-KG pipeline. Inspect provenance, error propagation and whether extra agents beat a fixed pipeline.

### NODES 2025 - Crafting an LPG Semantic Reasoner with Python and CDC

[Session information/recording link](https://confpad.io/conferences/nodes-2025/crafting-a-neo4j-knowledge-graph-semantic-reasoner-for-lpg-based-ontologies-with-python-and-cdc)

Useful for incremental reasoning and RDF/OWL-to-LPG rule translation. Check soundness/completeness claims for the supported rule subset.

### NODES 2025 archive

[Full on-demand archive](https://neo4j.com/video/nodes-2025/)

Filter for KG, GraphRAG, GDS, GNN and production talks. The archive includes more than 100 sessions, so choose by your current phase.

### Knowledge Graph Conference library

[KGC community/video links](https://www.knowledgegraph.tech/community)  
[KGC 2025 library](https://watch.knowledgegraph.tech/kgc-2025)

Some recordings/library access may require subscription. Prefer workshops with code, definitions and evaluation rather than trend-only panels.

## C. Documentation tutorials that function like courses

- [RDFLib documentation and examples](https://rdflib.readthedocs.io/)
- [Apache Jena tutorials](https://jena.apache.org/tutorials/)
- [PyG tutorials](https://pytorch-geometric.readthedocs.io/en/latest/get_started/colabs.html)
- [DGL tutorials](https://docs.dgl.ai/tutorials/blitz/index.html)
- [Neo4j GDS manual](https://neo4j.com/docs/graph-data-science/current/)
- [TinkerPop Gremlin recipes/reference](https://tinkerpop.apache.org/docs/current/reference/)

## D. Suggested viewing sequence

| Curriculum phase | Watch/course |
|---|---|
| Weeks 1-8 | MIT GNN lecture only as preview; focus on foundations |
| Weeks 9-18 | OpenHPI RDF/OWL/SPARQL; Protégé material; KGC ontology workshop |
| Weeks 19-28 | GraphAcademy modeling/Cypher; Jena/RDFLib docs; extraction workshop |
| Weeks 29-34 | CS224W classical graph lectures; GDS courses |
| Weeks 35-44 | CS224W GNN/KG lectures; MIT GNN; PyG/DGL tutorials |
| Weeks 45-52 | GraphRAG papers first, then NODES/KGC implementation talks |
| Research phase | conference talks only after reading the associated paper/artifact |

## E. Video-note method

For every lecture:

1. write the central claim before copying definitions;
2. pause and derive/implement the key equation or query;
3. record assumptions and missing baselines;
4. link to the corresponding chapter and paper;
5. create one test or counterexample;
6. tag as academic course, vendor implementation, case study or research talk.

> [!warning]
> Conference and vendor videos can be recent but are not necessarily peer reviewed. Recency is not evidence quality.
