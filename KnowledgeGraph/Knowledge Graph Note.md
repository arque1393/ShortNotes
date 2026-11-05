# From Graph Fundamentals to the Research Frontier: A Roadmap for Knowledge Graphs, Ontologies, Graph Data Science, Graph ML and Agentic GraphRAG (2026 Edition)

With your background, you can reach expert level in about 15–24 months across five phases. Two parallel tracks run through it. The symbolic track goes graph data → RDF/OWL/ontologies → KG construction. The statistical track goes network science → graph algorithms → GNNs/KG embeddings → graph foundation models. The tracks meet at the 2025–2026 frontier: GraphRAG, graph-structured agent memory and neuro-symbolic reasoning. That is where the open problems are richest and the evidence is still thin.

## TL;DR

- **Path:** about 2–3 months on graph foundations (graph theory, network science, Cypher/GQL, RDF/SPARQL), about 3 months on ontologies and KG construction, about 3 months on graph ML (CS224W + Hamilton + PyG/PyKEEN), about 3 months on LLM+KG systems (GraphRAG, text-to-Cypher, Graphiti/Zep-style memory, MCP), then 6–12 months specializing toward research. Ship one portfolio project per phase.
- **Core reading:** Hogan et al. _Knowledge Graphs_ (free at kgbook.org); Allemang/Hendler/Gandon _Semantic Web for the Working Ontologist_ (3rd ed., 2020); Barabási _Network Science_; Hamilton _Graph Representation Learning_ (free PDF); Bronstein et al. _Geometric Deep Learning_; Pan et al. "Unifying LLMs and KGs: A Roadmap" (arXiv 2306.08302, IEEE TKDE 2024); Bratanič & Hane _Essential GraphRAG_ (Manning, 2025); Negro et al. _Knowledge Graphs and LLMs in Action_ (Manning, 2025).
- **Where to do research:** the most defensible 2026 niches are:
    1. rigorous evaluation of when graphs actually help RAG (GraphRAG-Bench, ICLR 2026, shows GraphRAG does not always beat vanilla RAG);
    2. temporal and bi-temporal KGs as agent memory;
    3. LLM ontology learning and ontology-grounded extraction;
    4. graph foundation models that transfer across graphs (ULTRA-style);
    5. neuro-symbolic reasoning with faithfulness guarantees.

---

## 1. Key Findings (the 2025–2026 landscape)

1. **The main application frontier is now "LLM + graph."** The Pan et al. roadmap (arXiv 2306.08302, IEEE TKDE 2024) defines three paradigms: KG-enhanced LLMs, LLM-augmented KGs, and synergized LLM+KG. Almost every 2025–2026 system fits one of them: GraphRAG, HippoRAG 2, Graphiti/Zep, Mem0g, Think-on-Graph 2.0. Use this taxonomy as your mental map.
    
2. **GraphRAG works, but it is over-hyped, and evaluation is the bottleneck.** GraphRAG-Bench ("When to use Graphs in RAG", Xiang et al., arXiv 2506.05690, ICLR 2026) has 4,076 questions across four task levels: fact retrieval, complex reasoning, contextual summarization and creative generation. The authors built it because "recent studies report that GraphRAG frequently underperforms vanilla RAG on many real-world tasks." Graphs win on multi-hop and cross-document reasoning, but not everywhere. On the medical contextual-summarization task, reranked vanilla RAG scored 65.75% answer accuracy against 63.08% for HippoRAG 2. Decide "graph or not" empirically for each workload.
    
3. **Cost was GraphRAG's biggest weakness, and Microsoft's own follow-ups address it.** The release sequence was GraphRAG (Feb 2024), DRIFT search (Oct 31, 2024), LazyGraphRAG (Nov 25, 2024) and GraphRAG 1.0 (Dec 2024). Microsoft's November 2024 LazyGraphRAG blog post tested it on 5,590 AP news articles with 50 local and 50 global queries. It reports three things:
    
    - indexing cost equals vector RAG and is 0.1% of full GraphRAG;
    - "for 4% of the query cost of GraphRAG global search, LazyGraphRAG significantly outperforms all competing methods" on both local and global queries;
    - answer quality comparable to global search at "more than 700× lower query cost."
    
    These figures come from secondary summaries of the post. Both GraphRAG and LazyGraphRAG are now available through Microsoft Discovery on Azure.
    
4. **Agent memory has become a graph problem.**
    
    - **Zep's Graphiti** (arXiv 2501.13956, Jan 2025) is a temporally aware KG in which contradicted facts are invalidated rather than deleted. It reports 94.8% vs. 93.4% for MemGPT on Deep Memory Retrieval, and up to 18.5% higher accuracy with 90% lower latency on LongMemEval.
    - **Mem0** (arXiv 2504.19413, Apr 2025) reports that its Neo4j-based graph variant, Mem0g, scores "around 2% higher overall score than the base configuration." It also reports 26% higher LLM-as-a-Judge scores than OpenAI's memory and 91% lower p95 latency than full-context.
    - **HippoRAG 2** (ICML 2025, arXiv 2502.14802) runs Personalized PageRank over an open-IE KG. The paper reports "an average 7 point improvement over standard RAG in associativity tasks while showing no deterioration and even slight improvements in factual memory and sense-making tasks." Its average F1 is 59.8, against 57.0 for NV-Embed-v2.
    
    The authors or vendors reported all of these numbers themselves, on small benchmarks; Mem0's LOCOMO evaluation uses only 10 conversations. Treat them as directional.
    
5. **Graph query languages now have an ISO standard.** GQL (ISO/IEC 39075:2024) was published on 12 April 2024 by the same committee that maintains SQL (JTC1 SC32 WG3). Neo4j describes it as "a peer language to SQL and the first new ISO database language since 1987." SQL/PGQ (part of SQL:2023) adds graph pattern matching to SQL. GQL draws heavily on Cypher/openCypher, so learning Cypher first is the right investment.
    
6. **The graph-database vendor landscape is volatile, so plan for switching costs.** KùzuDB, a popular embedded analytical graph DB, was archived on GitHub on 10 October 2025 (last stable release 0.11.3). Community forks such as LadybugDB exist. Press reports (AppleInsider, heise, Feb 2026) say Apple disclosed the purchase in the EU's list of significant acquisitions: "Apple, through a subsidiary, will acquire all shares and hire select employees of Kuzu." BetaKit, cited secondhand, puts the deal at 9 October 2025 and about 10 staff. The EU filing itself was not checked. Lesson: build behind an abstraction layer (openCypher/GQL or a repository pattern) so you can swap engines.
    
7. **MCP is now the standard way to connect graphs to agents.** Neo4j ships an official MCP server (neo4j/mcp) with schema introspection, read-cypher, write-cypher and list-gds-procedures. It also maintains a Labs family: mcp-neo4j-cypher, mcp-neo4j-memory, mcp-neo4j-data-modeling and an Aura manager. The first Labs MCP server appeared in December 2024.
    
8. **Graph foundation models (GFMs) are the hottest graph-ML research area, and KG reasoning has the most convincing results.** ULTRA (Galkin et al., ICLR 2024, arXiv 2310.04562) is a single pre-trained model that runs zero-shot on any multi-relational graph. Across "57 different KGs... the zero-shot inductive inference performance of a single pre-trained ULTRA model on unseen graphs of various sizes is often on par or better than strong baselines trained on specific graphs." It does this with fewer than 200k parameters. UltraQuery extends it to zero-shot complex logical queries. Key surveys:
    
    - Wang et al., "Graph Foundation Models: A Comprehensive Survey" (arXiv 2505.15116; condensed KDD 2025 version);
    - Liu et al., "Graph Foundation Models: Concepts, Opportunities and Challenges" (IEEE TPAMI 47(6), 2025).
9. **LLM ontology learning is becoming a benchmarked subfield.** The LLMs4OL challenge (TIB Hannover, at ISWC) has run three editions:
    
    - 2024: 14 teams, 21 subtasks over WordNet, GeoNames and UMLS;
    - 2025: added a text2onto task. The overview concludes that LLMs "contribute meaningfully to ontology learning, but no single approach suffices." Hybrid pipelines won: commercial LLMs plus domain-tuned models, RAG and ensembles;
    - 2026: under way.
10. **New, field-defining venues exist.** For KG researchers, the natural home is TGDK (Transactions on Graph Data and Knowledge, Dagstuhl). It launched in 2023 as Diamond Open Access, free for readers and authors, with founding EiCs Aidan Hogan, Ian Horrocks, Andreas Hotho and Lalana Kagal. For graph-ML researchers, it is LoG (Learning on Graphs Conference), founded in 2022 with a focus on review quality.
    

---

## 2. How the six fields connect (your mental model)

Picture a layered stack with two tracks that meet at the top.

- **L0 Math:** graph theory, linear algebra (Laplacians, spectra), logic, probability (PGMs, causal graphs), optimization.
- **L1 Data models & storage:** RDF/RDFS vs property graphs; SPARQL, Cypher, GQL, Gremlin; triple stores and graph DBs.
- **L2:**
    - symbolic: KG construction (IE, NER, RE, entity linking, R2RML);
    - statistical: network science (degree distributions, small-world, scale-free, spreading).
- **L3:**
    - symbolic: ontologies (OWL 2, SKOS, BFO/DOLCE/gUFO, ODPs);
    - statistical: graph data science (centrality, communities, paths, link prediction).
- **L4:**
    - symbolic: reasoning (DL reasoners, rules, SHACL validation);
    - statistical: graph ML (GNNs, KG embeddings, graph transformers, GFMs).
    - The two connect through neuro-symbolic methods.
- **L5 Applications:** agentic AI: GraphRAG, agent memory, KGQA, MCP tools, ontology-grounded agents, multi-agent shared KGs.

Bridges you should be able to explain fluently:

- **Ontology → KG construction:** the ontology is the target schema for extraction. Ontology-guided LLM extraction is the 2025–2026 best practice for clean KGs.
- **KG → KG embeddings → link prediction:** statistical refinement of a symbolic artifact.
- **Network science → graph data science → GNNs:** centrality and community features serve both as baselines and as GNN inputs. PageRank is the retrieval engine in HippoRAG. Leiden communities are the backbone of Microsoft GraphRAG's global search.
- **Spectral graph theory → GCN:** GCN is a first-order approximation of spectral filtering on the normalized Laplacian, the same object used in graph signal processing.
- **Description-logic reasoning ↔ LLM reasoning:** neuro-symbolic AI tries to get the soundness of the first with the coverage of the second.

---

## 3. Phased Roadmap

Time estimates assume about 15–20 focused hours a week. Your math/ML background lets you compress the ML-heavy phases. The semantic-web phases are where most ML engineers are weakest, so do not skip them.

### Phase 0: Calibration (1–2 weeks)

- **Graph theory:** paths, connectivity, trees, bipartite graphs, matchings, flows, graph isomorphism (it matters for WL/GNN expressivity).
- **Linear algebra on graphs:** adjacency, degree, normalized Laplacian, random-walk matrix, spectrum, Fiedler vector.
- **Logic:** propositional and first-order logic; interpretations, entailment, decidability. This is the prerequisite for description logics.
- **Reading:** opening chapters of Newman _Networks_ (2nd ed.); Hamilton _Graph Representation Learning_ ch. 2.
- **Milestone:** implement BFS/DFS, Dijkstra, PageRank (power iteration) and spectral clustering from scratch in NumPy.

### Phase 1: Graph data, network science and both data models (8–12 weeks)

**Topics:**

1. **Network science:** Erdős–Rényi, Watts–Strogatz, Barabási–Albert, assortativity, clustering, motifs, robustness, spreading.
2. **Graph algorithms:**
    - centrality: degree, betweenness, closeness, eigenvector, PageRank, HITS;
    - communities: Louvain, Leiden, label propagation, Infomap, modularity and its resolution limit;
    - paths: Dijkstra, A*, Yen's k-shortest;
    - similarity and link-prediction heuristics: Jaccard, Adamic–Adar, resource allocation, Katz;
    - structure: components, triangles, k-core.
3. **Property graphs and Cypher:** MATCH patterns, variable-length paths, APOC, indexes and constraints, modeling choices (node vs. property vs. relationship), bulk import.
4. **GQL/openCypher/Gremlin:** standard GQL semantics; enough Gremlin to read TinkerPop/Neptune code.
5. **The RDF stack:** IRIs, triples, named graphs, Turtle/JSON-LD, RDFS, SPARQL 1.1 (property paths, federation, UPDATE). Track RDF 1.2/SPARQL 1.2 ("RDF-star" statement annotations).
6. **Property graphs vs. RDF:** they differ in identity, edge properties, schema, reasoning, standards and ecosystem.

**Tools:** Neo4j (Desktop/Aura Free) with the Graph Data Science library, NetworkX, igraph, Apache Jena/Fuseki or GraphDB Free, Wikidata Query Service.

**Reading:**

- Barabási, _Network Science_ (free at networksciencebook.com);
- Newman, _Networks_;
- Needham & Hodler, _Graph Algorithms_ (O'Reilly, 2019);
- Bratanič, _Graph Algorithms for Data Science_ (Manning, 2024);
- Barrasa & Webber, _Building Knowledge Graphs: A Practitioner's Guide_ (O'Reilly, 2023);
- Hogan et al., _Knowledge Graphs_, ch. 1–3 (free HTML at https://kgbook.org/).

**Courses:** Neo4j GraphAcademy (free): Fundamentals, Cypher, Data Modeling, Importing, GDS (https://graphacademy.neo4j.com/).

**Milestones:**

- Pass the free **Neo4j Certified Professional** exam (80 questions, 60 minutes, 80% to pass, open book).
- Build Project 1 (§7) and write the same 10 queries in both Cypher and SPARQL.

### Phase 2: Knowledge representation, ontologies and KG construction (10–14 weeks)

**Topics:**

1. **Description logics:** ALC up to SROIQ(D) (≈ OWL 2 DL); TBox/ABox; tableau reasoning; complexity; the open-world and unique-name assumptions (why OWL is not a database constraint language).
2. **OWL 2 profiles:**
    - EL: large biomedical ontologies, polynomial classification (ELK);
    - QL: ontology-based data access via query rewriting;
    - RL: rule-based materialization (RDFox, GraphDB).
3. **SKOS** for taxonomies and thesauri. Most enterprise "ontologies" are really SKOS taxonomies.
4. **Validation:** SHACL (closed-world shapes) and ShEx. Use SHACL for constraints and OWL for inference.
5. **Reasoners:**
    - HermiT and Pellet/Openllet (OWL 2 DL);
    - ELK (EL, very fast);
    - Konclude;
    - RDFox (incremental Datalog materialization);
    - the built-in reasoning in Stardog and GraphDB.
6. **Methodologies:** METHONTOLOGY, NeOn (reuse and re-engineering scenarios), competency questions, ontology design patterns (ODPs) and eXtreme Design, modular ontologies (MOMo), ontology testing.
7. **Foundational and domain ontologies:**
    - foundational: BFO (ISO/IEC 21838-2), DOLCE (ISO/IEC 21838-3), gUFO (lightweight OWL implementation of UFO/OntoUML);
    - web: schema.org;
    - domain: FIBO (finance), SNOMED CT (clinical, OWL EL), Gene Ontology and the OBO Foundry;
    - general-purpose vocabularies: PROV-O, OWL-Time, GeoSPARQL.
8. **Linked data:** Berners-Lee's four principles; the pitfalls of owl:sameAs. Wikidata is a statement graph with qualifiers, references and ranks, closer to a property graph than to plain RDF. DBpedia extracts Wikipedia infoboxes. YAGO 4/4.5 is typed with schema.org and cleaned with SHACL.
9. **Ontology matching:** string, structural and embedding-based matchers (LogMap, AgreementMakerLight, BERTMap) and LLM-based matchers. The yearly benchmark campaign is OAEI, held with the Ontology Matching workshop at ISWC.
10. **The KG construction pipeline:**
    - structured sources: R2RML/RML (YARRRML), virtual KGs (Ontop);
    - text: NER, relation extraction (supervised, distant, open IE), coreference, entity linking (Wikidata/UMLS), entity resolution (blocking + matching; Splink, Dedupe, Senzing), provenance;
    - LLM-based: ontology-guided structured-output extraction (Neo4j LLM Graph Builder, neo4j-graphrag `SimpleKGPipeline`, LangChain `LLMGraphTransformer`, LlamaIndex `PropertyGraphIndex`).
11. **Quality and refinement:** accuracy, completeness and consistency (Paulheim's refinement survey); error detection; rule mining (AMIE, AnyBURL); embedding-based completion.

**Tools:** Protégé (with HermiT/ELK/Pellet plugins), ROBOT, pySHACL, rdflib, owlready2, Ontop, RMLMapper/Morph-KGC, GraphDB, Stardog, RDFox, spaCy, GLiNER, ReFinED.

**Reading:**

- Allemang, Hendler & Gandon, _Semantic Web for the Working Ontologist_ (3rd ed., ACM Books, 2020);
- Hitzler, Krötzsch & Rudolph, _Foundations of Semantic Web Technologies_ (CRC, 2009), for formal rigor;
- Baader, Horrocks, Lutz & Sattler, _An Introduction to Description Logic_ (CUP, 2017);
- Keet, _An Introduction to Ontology Engineering_ (free);
- Kejriwal, Knoblock & Szekely, _Knowledge Graphs: Fundamentals, Techniques, and Applications_ (MIT Press, 2021; 568 pp., 130 exercises), the best textbook on IE, entity resolution and completion;
- Hitzler et al. (eds.), _Ontology Engineering with Ontology Design Patterns_ (IOS Press, 2016);
- Labra Gayo et al., _Validating RDF Data_ (free online).

**Courses and videos:** openHPI "Knowledge Graphs – Foundations and Applications" (Harald Sack); Stanford CS520 Knowledge Graphs seminar talks; Ontotext webinars; Neo4j's "Going Meta" livestream (Jesús Barrasa: ontologies, RDF and SHACL on Neo4j via neosemantics/n10s).

**Milestones:**

- Project 2: a published OWL 2 ontology (50–150 classes) with competency questions, ODPs, SHACL shapes and reasoner checks.
- Project 3: a text→KG pipeline with precision/recall measured on a hand-labeled sample.

### Phase 3: Graph Machine Learning (10–14 weeks)

**Topics:**

1. **Shallow embeddings:** DeepWalk, node2vec, LINE; the matrix-factorization view (NetMF); limits (transductive only, no features).
2. **KG embeddings:**
    - translational: TransE, TransH, TransR, RotatE;
    - bilinear: RESCAL, DistMult, ComplEx, TuckER;
    - neural: ConvE, R-GCN, CompGCN;
    - path/rule-based: NBFNet, AnyBURL;
    - evaluation pitfalls: filtered MRR/Hits@k, test leakage (why FB15k-237 and WN18RR replaced FB15k and WN18), inductive KG completion.
3. **GNN core:** MPNN, GCN, GraphSAGE, GAT/GATv2, GIN; pooling; heterogeneous GNNs (R-GCN, HAN, HGT).
4. **Spectral methods and graph signal processing:** graph Fourier transform, ChebNet, GCN as a low-pass filter, APPNP/personalized-PageRank propagation.
5. **Theory:** the WL test and GIN; the k-WL hierarchy and higher-order/subgraph GNNs; positional and structural encodings; over-smoothing; over-squashing (Alon & Yahav; Topping et al. curvature rewiring); heterophily.
6. **Graph transformers:** Graphormer, SAN, GraphGPS, Exphormer.
7. **Temporal graphs:**
    - models: EvolveGCN, TGN, TGAT, JODIE, DyRep, GraphMixer, DyGFormer;
    - temporal KG reasoning: RE-NET, xERTE, TLogic;
    - benchmarks: TGB / TGB 2.0.
8. **Geometric deep learning:** Bronstein, Bruna, Cohen & Veličković (arXiv 2104.13478), with symmetry/equivariance as the unifying principle; E(n)-equivariant GNNs.
9. **Scalability:**
    - sampling: GraphSAGE, FastGCN, Cluster-GCN, GraphSAINT;
    - precomputation: SIGN;
    - distributed training: DistDGL, GraphStorm;
    - GPU: RAPIDS cuGraph / nx-cugraph.
10. **Self-supervised and generative models:** DGI, GraphCL, GRACE, GraphMAE; GraphRNN, GCPN, DiGress.
11. **Relational deep learning:** relational databases treated as temporal heterogeneous graphs (RelBench, Relational Transformer). This is now part of CS224W.
12. **Trust:** GNNExplainer, PGExplainer, SubgraphX; conformalized GNNs; robustness and fairness.

**Tools:** PyTorch Geometric, DGL, PyKEEN, GraphStorm, Spektral, TorchDrug, OGB loaders, cuGraph.

**Reading:**

- Hamilton, _Graph Representation Learning_ (Morgan & Claypool, 2020; free PDF at https://www.cs.mcgill.ca/~wlh/grl_book/), read cover to cover;
- Wu, Cui, Pei & Zhao (eds.), _Graph Neural Networks: Foundations, Frontiers, and Applications_ (Springer, 2022);
- Ma & Tang, _Deep Learning on Graphs_ (CUP, 2021);
- Marzullo, Deusebio & Stamile, _Graph Machine Learning_, 2nd ed. (Packt, July 2025), with new LLM and temporal-graph chapters and PyG/DGL examples;
- Bronstein et al., _Geometric Deep Learning_ (arXiv 2104.13478);
- Ortega, _Introduction to Graph Signal Processing_ (CUP, 2022).

**Courses:**

- **Stanford CS224W** (Jure Leskovec; https://web.stanford.edu/class/cs224w/; 2021 lectures on YouTube). The current syllabus covers embeddings, GNNs and their design space, heterogeneous graphs, KG reasoning, relational deep learning/RelBench, graph transformers, generative models, PRODIGY in-context learning and conformalized GNNs. Do every Colab and homework.
- The Geometric Deep Learning course (Bronstein et al.) on YouTube.
- The CS224W Medium publication of PyG tutorials.

**Milestones:**

- Reproduce GCN, GraphSAGE, GAT and GIN on ogbn-arxiv and ogbn-products against honest baselines (MLP, label propagation, C&S).
- Project 5: train KGEs with PyKEEN.
- Write a 2–3 page note deriving GCN from spectral filtering and explaining the WL bound.
- Optional: the free **Neo4j Graph Data Science Certification** (now 50 questions, 60 minutes, 80% to pass).

### Phase 4: LLM + KG systems, GraphRAG and agentic graphs (10–14 weeks)

**Topics:**

1. **Pan et al.'s three paradigms** as the frame for everything below.
2. **GraphRAG families:**
    - **Knowledge-based** (retrieve over an existing KG): KG-RAG, KAPING, G-Retriever, SubgraphRAG.
    - **Index-based** (build a graph from documents):
        - Microsoft GraphRAG (Edge et al., arXiv 2404.16130): LLM extraction → Leiden hierarchical communities → community summaries → local/global/DRIFT search;
        - LightRAG (arXiv 2410.05779): dual-level retrieval, incremental updates;
        - HippoRAG / HippoRAG 2: Personalized PageRank memory;
        - LazyGraphRAG;
        - RAPTOR as a baseline.
    - **Hybrid** (vector + graph + keyword): the Neo4j GraphRAG Python retrievers (VectorCypher, HybridCypher, Text2Cypher).
3. **Reasoning on graphs:**
    - Think-on-Graph (arXiv 2307.07697): beam search over the KG with the LLM as agent;
    - Think-on-Graph 2.0 (ICLR 2025): alternates graph retrieval and document retrieval, training-free; reports SOTA on 6 of 7 knowledge-intensive datasets with GPT-3.5;
    - Think-on-Graph 3.0 (multi-agent, 2025);
    - Reasoning on Graphs (RoG, ICLR 2024): plan relation paths, then retrieve;
    - also GNN-RAG, KG-Agent, StructGPT.
4. **Text-to-Cypher/SPARQL:** schema linking, exemplar retrieval, self-correction from execution feedback. KGQA benchmarks: WebQSP, CWQ, MetaQA, LC-QuAD 2.0, QALD, GrailQA.
5. **LLM-based KG construction:** schema in the prompt + structured output + SHACL validation; embedding plus LLM adjudication for entity resolution; incremental updates; provenance back to source chunks.
6. **Agent memory as KGs:**
    - Graphiti/Zep: bi-temporal (valid time + transaction time), episode/entity/community subgraphs, hybrid semantic/BM25/graph search;
    - Mem0/Mem0g: triplets on Neo4j with conflict invalidation;
    - Cognee: extract–cognify–load pipelines;
    - Letta/MemGPT and A-MEM as non-graph contrasts.
    - Benchmarks: LOCOMO, LongMemEval, DMR.
7. **Ontology-grounded and neuro-symbolic agents:** ontologies as tool schemas and guardrails; SHACL as an output validator; reasoners as verifiers; semantic layers for grounding text-to-SQL/Cypher; a shared KG as the "blackboard" for multiple agents.
8. **MCP:**
    - Neo4j: the official neo4j/mcp server and the Labs servers;
    - Google MCP Toolbox for Databases;
    - community servers for other DBs;
    - safety: read-only modes, timeouts, token limits, write-approval gates.
9. **Evaluation:**
    - retrieval: evidence recall@k, path faithfulness;
    - generation: RAGAS-style faithfulness, calibrated LLM-as-judge;
    - cost: index-build cost, query cost and latency;
    - benchmarks: GraphRAG-Bench, MultiHop-RAG, HotpotQA/2Wiki/MuSiQue;
    - studies: "RAG vs. GraphRAG: A Systematic Evaluation" (arXiv 2502.11371), unified-framework analysis (arXiv 2503.04338).

**Tools:** microsoft/graphrag, LightRAG, HippoRAG, neo4j-graphrag, LangChain/LangGraph, LlamaIndex, Graphiti, Mem0, Cognee, FalkorDB GraphRAG SDK, MCP SDKs, RAGAS/DeepEval, Langfuse/Phoenix.

**Reading:**

- Pan et al. roadmap;
- Bratanič & Hane, _Essential GraphRAG_ (Manning, Sept 2025, 176 pp.): vector and hybrid search, text-to-Cypher, agentic RAG, LLM KG construction, Microsoft GraphRAG, evaluation;
- Negro, Kus, Futia & Montagna, _Knowledge Graphs and LLMs in Action_ (Manning, Nov 2025, 472 pp.): KG modeling, KGs from ontologies and text via LLMs, GNN node classification/link prediction, KG-powered RAG, NL KGQA, a LangGraph QA agent;
- the GraphRAG surveys and the memory papers in §6.

**Courses and videos:** GraphAcademy's GenAI track; DeepLearning.AI short courses with Neo4j (Knowledge Graphs for RAG; Agentic Knowledge Graph Construction); Neo4j NODES recordings and "Going Meta"; Microsoft Research GraphRAG talks; the KGC talk archive; Tomaž Bratanič's blog; Zep and Cognee engineering talks.

**Milestones:**

- Project 6: a GraphRAG bake-off with a written evaluation.
- Project 7: an agent with temporal KG memory, served over MCP.
- One reproducible public blog post.

### Phase 5: Research frontier (6–12+ months, ongoing)

1. Read the must-read list (§6). Then read two years of proceedings in your niche: ISWC/ESWC + TGDK for KG work; LoG + NeurIPS/ICLR/ICML for graph ML; ACL/EMNLP/KDD/WWW for LLM+KG.
2. Pick one niche from §8 and reproduce 2–3 recent papers end to end.
3. Mine the gap between claimed and reproduced behavior (cost, robustness, temporal drift, schema sensitivity). It is the cheapest source of publishable insight.
4. Start with workshops and challenges before main tracks:
    - workshops at ISWC/ESWC, NeurIPS/ICLR graph workshops, and LoG;
    - challenges: LLMs4OL, OAEI, OGB-LSC, TGB leaderboards.
5. Release artifacts. Resource papers at ISWC/ESWC and TGDK special issues are a proven way in.

Targets: a workshop paper within about 6 months of starting Phase 5, and a main-track submission within about 12.

---

## 4. Field-by-field quick reference

**4.1 Ontology & Semantic Web**

- **Standards:** RDF 1.1 (1.2 in progress), RDFS, OWL 2 (DL/EL/QL/RL), SKOS, SHACL, ShEx, SPARQL 1.1, R2RML/RML, PROV-O, JSON-LD.
- **Reasoners:** HermiT, Pellet, ELK, Konclude, RDFox.
- **LLM-assisted ontology generation:** the LLMs4OL paper (ISWC 2023) and challenges (2024–2026). Competency-question prompting (Ontogenia, "Memoryless CQbyCQ") can beat novice human modelers, but the output still needs manual refinement. OntoChat-style conversational engineering. A _Semantic Web_ journal systematic review of LLMs for ontology engineering.

**4.2 Knowledge Graphs: graph databases (2026 status)**

- **Neo4j:** market leader; Cypher, GDS, vector index, GenAI tooling, MCP.
- **Amazon Neptune:** openCypher, Gremlin and SPARQL. Neptune Analytics adds in-memory algorithms, vector search and a NetworkX backend.
- **TigerGraph:** distributed, GSQL, deep-link analytics.
- **Stardog:** RDF KG, virtualization, reasoning.
- **Ontotext GraphDB:** RDF with OWL 2 RL reasoning.
- **Memgraph:** in-memory, Cypher, streaming.
- **Kùzu:** embedded columnar Cypher DB, archived 10 Oct 2025.
- **ArangoDB:** multi-model, AQL.
- **FalkorDB:** GraphBLAS-based successor to RedisGraph, aimed at GraphRAG/agents.
- **Also:** Google Spanner Graph (GQL), Apache AGE, ArcadeDB, TypeDB, MillenniumDB.

Other KG topics:

- **Enterprise KG / data fabric / semantic layer:** KGs as the integration layer across silos. Juan Sequeda's research on KG-grounded text-to-SQL accuracy is a key reference.
- **Temporal and multimodal KGs:** ICEWS, GDELT, Wikidata qualifiers, bi-temporal modeling, MMKG benchmarks.
- **Public KGs:** Wikidata, DBpedia, YAGO, Hetionet, PrimeKG, SPOKE, UMLS, OpenAlex, ORKG.

**4.3 Agentic AI + KG**

- **Systems:** GraphRAG (+ DRIFT, LazyGraphRAG, incremental `update`), LightRAG, HippoRAG 2, LinearRAG (PolyU, relation-free, Oct 2025), ToG/ToG-2/ToG-3, RoG, GNN-RAG, SubgraphRAG ("Simple is Effective", ICLR 2025).
- **Memory:** Graphiti/Zep, Mem0g, Cognee, mcp-neo4j-memory, G-Memory for multi-agent systems.
- **Neuro-symbolic:** Neural LP, DRUM, Logic Tensor Networks, DeepProbLog/Scallop, LLM-plus-verifier loops, ontology-constrained decoding.

**4.4 Graph Data Science**

- **Leiden vs. Louvain:** Leiden (Traag et al., 2019) fixes Louvain's badly connected communities.
- **Scale:** Neo4j GDS / Aura Graph Analytics, NetworkX + nx-cugraph, igraph, cuGraph, GraphFrames/GraphX, Neptune Analytics, TigerGraph, GraphBLAS.
- **Visualization:** Gephi, Neo4j Bloom/Explore, Cytoscape, G.V(), Graphistry, sigma.js/Cosmograph.
- **Use cases:** fraud/AML rings, recommendation (PinSage), supply-chain multi-tier risk, identity resolution/customer 360, cybersecurity attack graphs, IT root-cause analysis, drug repurposing.

**4.5 Graph ML canon**

- **Classic models:** DeepWalk (2014), LINE (2015), node2vec (2016), GCN (2017), GraphSAGE (2017), MPNN (2017), GAT (2018), R-GCN (2018), GIN (2019).
- **KG embeddings:** TransE (2013), DistMult (2015), ComplEx (2016), RotatE (2019), TuckER (2019).
- **Scaling and architectures:** Cluster-GCN (2019), GraphSAINT (2020), NBFNet (2021), GraphGPS (2022), ULTRA (2024).
- **Benchmarks:** OGB (2020), OGB-LSC (2021), TGB (2023), TGB 2.0 (2024).
- **Graph foundation models:** GraphAny, OpenGraph, AnyGraph, OFA, SAMGPT and BRIDGE (2025), Relational Transformer; the position paper "Graph Foundation Models Are Already Here" (ICML 2024).
- **LLM+GNN:**
    - LLM-as-enhancer: text-attributed graphs;
    - LLM-as-predictor: GraphGPT;
    - GNN-as-retriever: GNN-RAG, G-Retriever;
    - LLM-on-graph benchmarks: GraphArena, NLGraph.

**4.6 Related fields**

- **Causal graphs:** SCMs, do-calculus, PC/GES/NOTEARS discovery.
- **PGMs:** belief propagation is the ancestor of message passing.
- **Hypergraphs and topological deep learning:** HGNN, simplicial/cell complexes, sheaf NNs; Hajij et al. (arXiv 2206.00606); Papamarkou et al. (ICML 2024); TopoX/TopoBench.
- **Graph signal processing:** Shuman et al. (2013); Ortega et al. (Proc. IEEE, 2018).
- **KBQA:** semantic parsing vs. retrieval-based approaches.
- **GNN explainability:** GNNExplainer, SubgraphX, the Yuan et al. survey.
- **Graph recommenders:** LightGCN, NGCF, KGAT; GFMs for recommendation (survey arXiv 2502.08346).
- **Scientific KGs:** Hetionet, PrimeKG, TxGNN-style drug repurposing, equivariant molecular GNNs, ORKG.

---

## 5. Books, mapped to phases

|Phase|Book|Why|
|---|---|---|
|0–1|Newman, _Networks_ (2nd ed., OUP 2018)|Rigorous network theory|
|1|Barabási, _Network Science_ (CUP 2016; free online)|Intuition for network phenomena|
|1|Needham & Hodler, _Graph Algorithms_ (O'Reilly 2019)|Practical algorithms|
|1|Bratanič, _Graph Algorithms for Data Science_ (Manning 2024)|Modern GDS with Neo4j|
|1|Barrasa & Webber, _Building Knowledge Graphs_ (O'Reilly 2023)|Practitioner KG on property graphs|
|1–2|Hogan et al., _Knowledge Graphs_ (2021; free at kgbook.org)|The canonical KG text|
|2|Allemang, Hendler & Gandon, _Semantic Web for the Working Ontologist_ (3rd ed., ACM Books 2020)|RDF/RDFS/OWL modeling|
|2|Hitzler, Krötzsch & Rudolph, _Foundations of Semantic Web Technologies_ (CRC 2009)|Formal semantics|
|2|Baader et al., _An Introduction to Description Logic_ (CUP 2017)|DL theory|
|2|Keet, _An Introduction to Ontology Engineering_ (free)|Methodology|
|2|Kejriwal, Knoblock & Szekely, _Knowledge Graphs: Fundamentals, Techniques, and Applications_ (MIT Press 2021)|Construction, ER, completion|
|3|Hamilton, _Graph Representation Learning_ (2020; free PDF)|Concise GRL theory|
|3|Wu, Cui, Pei & Zhao (eds.), _Graph Neural Networks: Foundations, Frontiers, and Applications_ (Springer 2022)|Breadth reference|
|3|Ma & Tang, _Deep Learning on Graphs_ (CUP 2021)|Textbook|
|3|Marzullo, Deusebio & Stamile, _Graph Machine Learning_ (2nd ed., Packt 2025)|Hands-on PyG/DGL, LLMs, temporal|
|3|Bronstein et al., _Geometric Deep Learning_ (arXiv 2104.13478)|Unifying theory|
|3|Ortega, _Introduction to Graph Signal Processing_ (CUP 2022)|Spectral foundations|
|4|Bratanič & Hane, _Essential GraphRAG_ (Manning 2025)|Production GraphRAG|
|4|Negro, Kus, Futia & Montagna, _Knowledge Graphs and LLMs in Action_ (Manning 2025)|End-to-end KG + LLM|
|4|Negro, _Graph-Powered Machine Learning_ (Manning 2021)|Applied graph ML|
|5|Koller & Friedman, _Probabilistic Graphical Models_ (MIT 2009)|PGMs|
|5|Pearl, _Causality_ (2009); Peters, Janzing & Schölkopf, _Elements of Causal Inference_ (2017, free)|Causal graphs|

---

## 6. Must-read papers and surveys

**KG and semantic web**

- Hogan et al., "Knowledge Graphs," ACM Computing Surveys 54(4), 2021 (arXiv 2003.02320).
- Paulheim, "Knowledge Graph Refinement: A Survey," Semantic Web journal, 2017.
- Ji et al., "A Survey on Knowledge Graphs," IEEE TNNLS 2021 (arXiv 2002.00388).
- Biswas et al., "Knowledge Graph Embeddings: Open Challenges and Opportunities," TGDK 1(1), 2023.
- Angles et al., "Foundations of Modern Query Languages for Graph Databases," ACM CSUR 2017; "PG-Schema," SIGMOD 2023.
- Babaei Giglou, D'Souza & Auer, "LLMs4OL," ISWC 2023, plus the 2024 and 2025 challenge overviews.

**Graph ML**

- Bronstein et al., "Geometric Deep Learning" (arXiv 2104.13478).
- Wu et al., "A Comprehensive Survey on GNNs," IEEE TNNLS 2021.
- Xu et al., "How Powerful are GNNs?" ICLR 2019.
- Morris et al., "Weisfeiler and Leman Go Neural," AAAI 2019, and "...go Machine Learning: The Story so Far," JMLR 2023.
- Alon & Yahav (over-squashing), ICLR 2021; Topping et al. (curvature), ICLR 2022.
- Rampášek et al., GraphGPS, NeurIPS 2022.
- Hu et al., OGB (arXiv 2005.00687); Huang et al., TGB (NeurIPS 2023).
- Galkin et al., ULTRA (ICLR 2024) and UltraQuery (arXiv 2404.07198).
- Wang et al., GFM survey (arXiv 2505.15116); Liu et al., GFM survey (IEEE TPAMI 2025).
- "Deep Graph Learning will stall without Network Science" (arXiv 2502.01177), a contrarian position paper.

**LLM + KG / GraphRAG / agents**

- Pan et al. roadmap (arXiv 2306.08302; IEEE TKDE 2024).
- Edge et al., GraphRAG (arXiv 2404.16130).
- Guo et al., LightRAG (arXiv 2410.05779).
- Gutiérrez et al., HippoRAG (NeurIPS 2024) and HippoRAG 2 (ICML 2025, arXiv 2502.14802).
- Think-on-Graph (arXiv 2307.07697); Think-on-Graph 2.0 (ICLR 2025, arXiv 2407.10805).
- Luo et al., RoG (ICLR 2024).
- Surveys: Peng et al. (arXiv 2408.08921); Zhang et al. (arXiv 2501.13958, with a knowledge-/index-/hybrid-based taxonomy and the Awesome-GraphRAG repo); Han et al. (arXiv 2501.00309).
- Xiang et al., GraphRAG-Bench (arXiv 2506.05690; ICLR 2026); arXiv 2502.11371; arXiv 2503.04338.
- Rasmussen et al., Zep (arXiv 2501.13956); Chhikara et al., Mem0 (arXiv 2504.19413).
- Li, Miao & Li, SubgraphRAG (ICLR 2025).

---

## 7. Project ladder (beginner → research-level)

Every project should end with a GitHub repo, a README covering architecture and evaluation, and a short write-up.

|#|Project|Phase|Stack|Data|
|---|---|---|---|---|
|1|Dual-model graph: the same data in Neo4j and RDF; 10 identical Cypher/SPARQL queries; GDS PageRank, Louvain, similarity|1|Neo4j+GDS, Jena/GraphDB, NetworkX|MovieLens, OpenAlex, Wikidata|
|2|Domain ontology: ODPs, alignment to BFO/gUFO + schema.org, SHACL, reasoner tests, published with WIDOCO docs|2|Protégé, ROBOT, pySHACL, HermiT/ELK|Your domain (supply chain, trials, ESG)|
|3|Text→KG: NER + RE + linking + ER + provenance, P/R on 200 labeled triples, then head-to-head against an LLM ontology-guided pipeline|2/4|spaCy/GLiNER, ReFinED, Splink, neo4j-graphrag|News, SEC EDGAR, PubMed|
|4|Fraud/AML analytics: communities + centrality + embeddings + GNN, with an investigation UI|1/3|Neo4j GDS, PyG, cuGraph|Elliptic, IBM AML, PaySim|
|5|KGE study: TransE/RotatE/ComplEx/TuckER/NBFNet + ULTRA zero-shot, including on your own KG|3|PyKEEN, ULTRA|FB15k-237, WN18RR, CoDEx|
|6|GraphRAG bake-off: vector vs. hybrid vs. MS GraphRAG vs. LazyGraphRAG-style vs. LightRAG vs. HippoRAG 2, reporting quality, index cost, query cost and latency|4|graphrag, LightRAG, HippoRAG, RAGAS|GraphRAG-Bench, MultiHop-RAG, your docs|
|7|Agent with temporal KG memory over MCP (read-only + approval-gated writes)|4|Graphiti/Mem0, LangGraph, Neo4j MCP|LongMemEval, LOCOMO|
|8|Self-correcting text-to-Cypher/SPARQL with ontology constraints, scored on execution accuracy|4|Neo4j Text2Cypher data|LC-QuAD 2.0, QALD, WebQSP|
|9|Biomedical drug-repurposing KG: KGE + GNN link prediction + LLM path explanations, with leakage-safe splits|3/5|PyG, PyKEEN|PrimeKG, Hetionet|
|10|Temporal graph learning: TGN/DyGFormer vs. simple baselines; temporal KG forecasting|3/5|PyG, TGB|TGB, ICEWS, GDELT|
|11|Research project, one of: (a) KG-schema sensitivity of GraphRAG; (b) a bi-temporal memory benchmark with knowledge-update and contradiction tests; (c) LLM ontology learning with reasoner-in-the-loop repair, entered in LLMs4OL; (d) GFM transfer from public KGs to enterprise KGs|5|All|Public + own|

**Product ideas:**

- KG-grounded enterprise Q&A with citations
- regulatory-change tracker on a temporal KG
- supplier-risk graph
- clinical-trial matching
- entity-resolution service
- vertical agent-memory layer
- ontology-authoring copilot with SHACL/reasoner validation

**Key repos:** pyg-team/pytorch_geometric, dmlc/dgl, pykeen/pykeen, DeepGraphLearning/ULTRA, microsoft/graphrag, HKUDS/LightRAG, OSU-NLP-Group/HippoRAG, getzep/graphiti, mem0ai/mem0, topoteretes/cognee, neo4j/neo4j-graphrag-python, neo4j/mcp, neo4j-contrib/mcp-neo4j, DEEP-PolyU/Awesome-GraphRAG, GraphRAG-Bench/GraphRAG-Benchmark.

---

## 8. Open research problems (2025–2026)

1. **The science of GraphRAG evaluation.** Open questions: when graphs help, why, and at what cost; contamination; LLM-as-judge bias in the "comprehensiveness/diversity" metrics GraphRAG papers use; cost-normalized comparison; sensitivity to KG schema. A TGDK 2025 paper already studies "GraphRAG on Technical Documents – Impact of Knowledge Graph Schema."
2. **Robust GraphRAG over imperfect, LLM-extracted KGs.** Retrieval drift, hallucination detection and online KG repair.
3. **Bi-temporal KGs for agent memory.** Formal invalidation semantics, correct knowledge updates, forgetting/erasure, and statistically sound memory benchmarks.
4. **LLM ontology learning beyond taxonomies.** Axiom learning, reasoner-in-the-loop repair, alignment to foundational ontologies.
5. **Neuro-symbolic reasoning with guarantees.** Faithful reasoning paths, ontology-constrained decoding, verifiable text-to-query.
6. **Graph foundation models.** What is the "vocabulary" of graphs? Open topics: cross-domain transfer, text-free GFMs, scaling laws, heterophily, and whether the backbone should be an LLM or a GNN.
7. **Scalability.** Billion-edge training; incremental GraphRAG indexing (EraRAG, LightRAG, GraphRAG `update`); linear-cost graph retrieval (LinearRAG).
8. **Expressivity vs. trainability.** Over-squashing remedies, and whether graph transformers really beat well-tuned MPNNs.
9. **Temporal graph learning evaluation.** Negative-sampling and batching pitfalls; temporal KG forecasting.
10. **Relational deep learning on enterprise databases** (RelBench).
11. **Trust:** path-based explanations, prompt injection through graph content in MCP tools, differential privacy.
12. **Multi-agent shared knowledge:** consistency, provenance and conflict resolution.

**Recommended first niche:** combine 1 with 3, or 1 with 4. Both play to your GenAI/agentic background, need modest compute, have public code to reproduce, and attract both semantic-web venues (ISWC/ESWC/TGDK) and NLP/ML venues (ACL/EMNLP/ICLR).

---

## 9. Courses, channels and talk archives

- **Stanford CS224W:**
    - https://web.stanford.edu/class/cs224w/
    - 2021 lectures on YouTube
    - Stanford Online XCS224W (paid, 10 weeks)
- **Stanford CS520 Knowledge Graphs:** seminar talks.
- **Neo4j GraphAcademy:** free courses and certifications.
- **Neo4j YouTube:** NODES, Going Meta, GenAI livestreams.
- **Geometric Deep Learning course** (Bronstein, Bruna, Cohen, Veličković) on YouTube.
- **openHPI:** "Knowledge Graphs – Foundations and Applications."
- **Vendor webinars:** Ontotext, Stardog and TigerGraph.
- **Conference talk archives:** KGC (The Knowledge Graph Conference, New York), ISWC/ESWC keynotes and tutorials.
- **LoG recordings:** LoG 2025 keynotes were Aditi Krishnapriyan, Haggai Maron, Melanie Weber and Michael Galkin.
- **Microsoft Research:** the GraphRAG blog and talks.
- **DeepLearning.AI × Neo4j:** short courses.
- **AWS:** Neptune/GraphStorm sessions and TinkerPop livestreams.

---

## 10. Venues

**Journals:**

- _Journal of Web Semantics_
- _Semantic Web_ (IOS Press)
- **TGDK** (Dagstuhl, Diamond OA). Special issues include "Trends in Graph Data and Knowledge" (vol. 1), "Resources for Graph Data and Knowledge" (vol. 2(2)) and "Data Management for (Knowledge) Graphs" (vol. 4(2), Sept 2026).
- _IEEE TKDE_, _TNNLS_, _TPAMI_, _JMLR_, _TMLR_
- _ACM Computing Surveys_
- _Knowledge-Based Systems_
- _Journal of Biomedical Semantics_
- _Network Science_

**Conferences:**

- **Semantic web/KG:** ISWC, ESWC, K-CAP, SEMANTiCS, KR, DL workshop, OM/OAEI, KGC (industry).
- **Graph ML:** LoG, NeurIPS, ICML, ICLR and their graph workshops.
- **Mining/web:** KDD, WWW, CIKM, WSDM, ICDM, RecSys.
- **AI/NLP:** AAAI, IJCAI, ACL, EMNLP, NAACL.
- **Databases:** SIGMOD, VLDB, ICDE, GRADES-NDA.
- **Network science:** NetSci, Complex Networks.

---

## 11. People, labs, communities, newsletters

**Graph ML:** Jure Leskovec, Michael Bronstein, Petar Veličković, William L. Hamilton, Michael Galkin, Jian Tang, Zhaocheng Zhu, Haggai Maron, Christopher Morris, Stefanie Jegelka, Xavier Bresson, Pietro Liò, Bryan Perozzi, Yanfang Ye & Nitesh Chawla (GFMs), Chuan Shi, Ingo Scholtes.

**KG / semantic web:** Aidan Hogan, Ian Horrocks, Uli Sattler, Pascal Hitzler, Axel Polleres, Heiko Paulheim, Steffen Staab, Natasha Noy, Denny Vrandečić, Juan Sequeda, Jeff Z. Pan, Harald Sack, Sören Auer & Jennifer D'Souza (TIB), Ernesto Jiménez-Ruiz, Giancarlo Guizzardi.

**LLM+KG / GraphRAG / memory:** Shirui Pan & Linhao Luo, Yu Su (OSU), Chao Huang (HKU), Xiao Huang (PolyU), Jonathan Larson & Darren Edge (MSR), Jian Guo (IDEA), Daniel Chalef (Zep), Tomaž Bratanič and Jesús Barrasa (Neo4j).

**Labs:** Stanford SNAP, Oxford, Mila, Google DeepMind/Research, Microsoft Research, Amazon (GraphStorm), TIB Hannover, FIZ Karlsruhe/KIT, U. Mannheim, U. Chile/IMFD, OSU NLP, HKU Data Intelligence Lab, PolyU DEEP Lab, Notre Dame.

**Communities:** LoG Slack and meetups, PyG Slack, the Neo4j forum and Discord, W3C community groups, OBO Foundry, the Wikidata community, ISWC/ESWC doctoral consortia.

**Newsletters, blogs and podcasts:**

- Michael Galkin's annual "Graph & Geometric ML in 202X" posts
- Michael Bronstein's essays
- the Neo4j Developer Blog
- Tomaž Bratanič's blog
- gdotv's "The Weekly Edge"
- the Ontotext blog
- Kurt Cagle's "The Cagle Report"
- Juan Sequeda's "Catalog & Cocktails" podcast
- Paco Nathan's writing on KGs and entity resolution
- the CS224W Medium publication
- the Awesome-GraphRAG and Awesome-Foundation-Models-on-Graphs lists

---

## 12. Certifications and career paths

**Certifications** are useful signals, but they do not replace a portfolio.

- **Neo4j Certified Professional:** free; 80 questions in 60 minutes; 80% to pass; open book; unlimited retakes.
- **Neo4j Graph Data Science Certification:** free; now 50 questions in 60 minutes (previously 40); 80% to pass.
- **Others:**
    - AWS certifications that touch Neptune;
    - TigerGraph courses;
    - Stardog and Ontotext training;
    - Stanford XCS224W (graded transcript);
    - the openHPI KG certificate.

**Career paths:**

1. **KG Engineer / Ontologist** (pharma, finance/FIBO, publishing, government).
2. **Graph Data Scientist** (fraud/AML, recommendations, supply chain).
3. **GraphRAG / AI Engineer**, the fastest-growing path (GraphRAG, text-to-Cypher, memory, MCP, evaluation).
4. **Graph ML Research Scientist** (big-tech labs, drug discovery, materials).
5. **Semantic / Data Fabric Architect.**
6. **Founder** (vertical KG products, memory layers, evaluation tools, ontology copilots).
7. **Academic researcher.** TGDK, ISWC and LoG are welcoming first venues.

---

## 13. Recommendations

1. **Use property graphs and Cypher for speed, but learn RDF/OWL too.** Most GraphRAG tooling targets Neo4j-style property graphs. The hard problems (identity, semantics, validation, interoperability) are solved in the W3C stack. Being fluent in both is rare and valuable.
2. **Make evaluation your signature skill.** Compare every project against strong non-graph baselines and report cost. The literature itself shows graphs do not always win, and people who can say _when_ they win are scarce.
3. **Constrain LLM extraction with ontologies.** Ontology-guided, SHACL-validated extraction is the most reliable way to get KGs clean enough for GraphRAG and agents.
4. **Build memory on bi-temporal models.** Facts change, and invalidating instead of deleting is the right default for agents and regulated domains.
5. **Hedge infrastructure risk.** Keep queries in openCypher/GQL, isolate DB access behind interfaces, and prefer engines with clear governance.
6. **Choose a research niche by month 9–12.** GraphRAG evaluation, temporal agent memory or LLM ontology learning fit your profile best. Target a workshop or challenge first.
7. **Publish continuously in public.** Reproducible blog posts, a GitHub portfolio and talk submissions to LoG, KGC or NODES compound faster than certificates.

---

## 14. Caveats

- **Self-reported numbers.** Results for Zep, Mem0/Mem0g, LazyGraphRAG and DRIFT come from their authors or vendors. Mem0 evaluates on only 10 LOCOMO conversations, and later work questions whether LOCOMO is statistically sound. Reproduce on your own data.
- **Kùzu.** The archiving (10 Oct 2025, last release 0.11.3) is well documented. The Apple acquisition comes from press reports (AppleInsider, heise, Feb 2026) citing Apple's entry in the EU's list of significant acquisitions; the filing itself was not checked.
- **Fast-moving software.** Microsoft GraphRAG has moved well past 1.0: the GitHub release v3.3.0 came out on 8 Oct 2026, after v3.2.0 on 23 Sep 2026. MCP tool names and certification formats also change (the GDS exam went from 40 to 50 questions). Check official docs.
- **LoG 2025 location.** Organizer-recruitment materials mentioned UCLA, while the registration portal referenced Arizona State University. Verify current logistics on logconference.org.
- **Time estimates** assume 15–20 hours a week. Full-time study roughly halves them. Regulated domains (biomedical, finance) need extra domain learning.
- **Book listings.** Author order varies across listings for _Semantic Web for the Working Ontologist_. Hogan et al.'s _Knowledge Graphs_ moved from Morgan & Claypool to Springer along with the Synthesis Lectures series.