---
title: "Datasets and Benchmarks Catalog"
type: reference
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - datasets
  - benchmarks
  - evaluation
  - catalog
---
# Datasets and Benchmarks Catalog

> [!goal]
> Select datasets and benchmarks by the generalization claim, data construction and license - not by popularity alone.

## 1. Knowledge graphs and link prediction

| Dataset | Typical use | Split/metric | Main cautions |
|---|---|---|---|
| FB15k-237 | KGE sanity/benchmark | MRR, Hits@K | Derived from Freebase; limited domain and common benchmark overfitting |
| WN18RR | Lexical KG completion | MRR, Hits@K | Relation patterns and lexical structure; not representative of enterprise KGs |
| YAGO3-10 | KG completion | MRR/Hits | Popular entities and relation skew |
| NELL-995 | Rule/path reasoning | query-specific | Construction artifacts and old KB snapshot |
| OGB `ogbl-wikikg2` | large KG completion | temporal split, MRR | Large transductive setting; inspect negative evaluation |
| OGB `ogbl-biokg` | biomedical heterogeneous KG | MRR | random split; domain-specific types |
| ICEWS variants | temporal KG | time-aware ranking | preprocessing/split conventions differ across papers |
| GDELT variants | temporal events | ranking | noisy event extraction and huge scale |

Use [OGB link property datasets](https://ogb.stanford.edu/docs/linkprop/) for official loaders/evaluators.

## 2. Node prediction and general graph ML

| Dataset | Task | Why useful | Caution |
|---|---|---|---|
| `ogbn-arxiv` | paper subject classification | chronological split | text embeddings/features and citation biases |
| `ogbn-products` | product category | large graph | split tied to sales rank, transductive |
| `ogbn-mag` | heterogeneous paper venue | typed large graph | single target type and time split |
| `ogbn-papers100M` | huge node classification | systems scale | heavy compute/storage |
| Cora/Citeseer/PubMed | teaching | quick experiments | too small/overused for strong claims |
| Reddit/Flickr/Yelp variants | inductive node tasks | sampling/scaling | exact preprocessing varies |

Official catalog: [OGB node property prediction](https://ogb.stanford.edu/docs/nodeprop/).

## 3. Graph-level prediction

| Dataset | Domain/task | Split recommendation |
|---|---|---|
| `ogbg-molhiv` | molecule property | scaffold split |
| `ogbg-molpcba` | multi-task molecule | scaffold split, AP |
| `ogbg-code2` | code graph -> tokens | project-aware split |
| ZINC | molecular regression | standard split, but synthetic benchmark behavior |
| QM9 | molecular quantum properties | assess 3D/feature assumptions |
| TUDatasets | many small graph datasets | teaching/legacy comparison; watch tiny size |

Official catalog: [OGB graph property prediction](https://ogb.stanford.edu/docs/graphprop/).

## 4. Heterogeneous and temporal graphs

- OGB-MAG: heterogeneous academic graph.
- DBLP/ACM/IMDB heterogeneous variants: common for metapath/HAN studies; preprocessing differs and may make tasks easy.
- TGB (Temporal Graph Benchmark): standardized temporal graph tasks; check latest versions and negative sampler.
- JODIE/Wikipedia/Reddit/MOOC/LastFM temporal event datasets: useful for TGN/TGAT reproduction; inspect event definitions and leakage.
- ICEWS/GDELT: temporal multi-relational KGs.

Prefer rolling time evaluation and new-node slices.

## 5. Network science/open graphs

- [SNAP datasets](https://snap.stanford.edu/data/): social, citation, web, communication and temporal networks.
- [KONECT](http://konect.cc/): broad network collection with metadata.
- [Network Repository](https://networkrepository.com/): many graph datasets and statistics.
- [Wikidata dumps](https://www.wikidata.org/wiki/Wikidata:Database_download): massive open KG; requires careful truthy/full statement selection.
- [DBpedia](https://www.dbpedia.org/resources/): RDF derived from Wikipedia.
- [YAGO](https://yago-knowledge.org/): taxonomy-aligned open KG.
- [OpenAlex](https://openalex.org/): scholarly graph/metadata with API/snapshots.

Check licenses and snapshot dates. A convenient API may not permit redistribution of derived data.

## 6. Entity resolution

- Magellan/DeepMatcher benchmark sets (Amazon-Google, DBLP-ACM, DBLP-Scholar, Walmart-Amazon, etc.): useful baseline sets but often small and clean relative to production.
- WDC product matching datasets: larger Web-derived product matching.
- OAEI instance matching tracks: ontology/KG alignment and identity tasks.
- Synthetic corruption from a clean entity table: useful only when corruption resembles the target source.

Evaluate blocking recall, pair and cluster metrics, and entity-disjoint splits.

## 7. Information extraction and KG construction

- DocRED: document-level relation extraction.
- TACRED/Re-TACRED: relation extraction; label noise and sentence-level limits.
- SciERC: scientific entities/relations/coreference.
- ACE/ERE: entities, relations and events, often licensed/restricted.
- FewRel: few-shot relation classification; constructed setting.
- Wikidata/DBpedia distant supervision: scalable but noisy.
- domain corpora such as biomedical benchmarks: select based on ontology and licensing.

For your own domain, annotate a smaller high-quality gold set with evidence spans and adjudication.

## 8. KGQA and multi-hop QA

- WebQSP: questions over Freebase; commonly used in KGQA.
- ComplexWebQuestions (CWQ): compositional questions; inherited construction artifacts.
- GrailQA: compositional/generalization splits.
- MetaQA: synthetic multi-hop movie questions; useful diagnostics, not realism.
- HotpotQA, 2WikiMultiHopQA, MuSiQue: text multi-hop retrieval/QA, often used in GraphRAG.
- NarrativeQA: long-document sense-making.
- Natural Questions/PopQA: factual retrieval.

GraphRAG evaluation needs evidence labels and question-type stratification, not only answer matching.

## 9. GraphRAG benchmarks

- [GraphRAG-Bench / When to use Graphs in RAG](https://github.com/GraphRAG-Bench/GraphRAG-Benchmark): stages from fact retrieval to complex/global tasks; accepted ICLR 2026.
- HippoRAG evaluation suite: factual, associative and sense-making datasets; inspect exact corpus and LLM settings.
- Microsoft GraphRAG examples: useful methodology demos, not a universal benchmark.
- Your domain benchmark: required for production because graph quality and question mix dominate.

Include BM25, vector, fusion, exact query, simple graph and oracle-evidence baselines.

## 10. Graph database/system benchmarks

### Graph Data Council (formerly LDBC)

[Benchmark catalog](https://ldbcouncil.org/benchmarks/)

- Social Network Benchmark (SNB): interactive/BI graph workloads.
- FinBench: distributed transactional financial graph workload.
- Graphalytics: BFS, PageRank, WCC, label propagation, local clustering and SSSP with reference outputs.
- LSQB: labeled subgraph query workload.
- Semantic Publishing Benchmark: RDF/SPARQL workload.

### RDF/SPARQL

- WatDiv: workload diversity and selectivity for RDF stores.
- Berlin SPARQL Benchmark (BSBM): e-commerce-inspired SPARQL workload.
- SP2Bench: DBLP-inspired SPARQL benchmark.
- LUBM: university ontology/reasoning benchmark; useful but synthetic and old.

Do not compare systems using only a vendor-selected query. Use validated standard workloads plus your application workload.

## 11. Ontology benchmarks/resources

- OAEI tracks: ontology alignment and instance matching.
- BioPortal and OBO Foundry ontologies: reuse/alignment studies; obey licenses/governance.
- LOV (Linked Open Vocabularies): vocabulary discovery.
- Ontology Pitfall Scanner (OOPS!) examples: quality education, not a complete correctness oracle.

## 12. Dataset selection checklist

- [ ] Does the graph represent the deployment semantics?
- [ ] Is the split aligned with the generalization claim?
- [ ] Could inverse edges, duplicate entities or future topology leak?
- [ ] Are negatives realistic and type/time eligible?
- [ ] Is graph construction documented and reproducible?
- [ ] Are licenses and privacy compatible with release/use?
- [ ] Are rare types/relations represented?
- [ ] Is there a strong non-graph baseline?
- [ ] Can results transfer beyond this benchmark?
- [ ] Is a data card available or will you write one?

Use [[Template - Dataset Card]] before experiments.
