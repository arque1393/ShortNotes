---
title: "Papers by Topic"
type: reference
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - papers
  - research
  - reading-list
  - literature
---
# Papers by Topic

> [!goal]
> Read a curated path from seminal foundations to current frontiers. This is a starting graph, not a claim of completeness.

## 1. Knowledge graphs and surveys

1. Hogan et al. (2021), **Knowledge Graphs** - broad survey/book article. [Open site](https://kgbook.org/)
2. Ji et al. (2022), **A Survey on Knowledge Graphs: Representation, Acquisition, and Applications**. [arXiv](https://arxiv.org/abs/2002.00388)
3. Ehrlinger and Woss (2016), **Towards a Definition of Knowledge Graphs**. [Paper](https://ceur-ws.org/Vol-1695/paper4.pdf)
4. Paulheim (2017), **Knowledge Graph Refinement: A Survey of Approaches and Evaluation Methods**. [Paper](https://doi.org/10.3233/SW-160218)

Read to compare definitions, lifecycle and quality assumptions.

## 2. Ontology engineering and design

1. Gruber (1993), **A Translation Approach to Portable Ontology Specifications**. [DOI](https://doi.org/10.1006/knac.1993.1008)
2. Noy and McGuinness (2001), **Ontology Development 101**. [PDF](https://protege.stanford.edu/publications/ontology_development/ontology101.pdf)
3. Gangemi (2005), **Ontology Design Patterns for Semantic Web Content**. [DOI](https://doi.org/10.1007/11574620_16)
4. Presutti and Gangemi (2008), **Content Ontology Design Patterns as Practical Building Blocks**. [PDF](http://ontologydesignpatterns.org/wiki/images/4/49/Wop2008-presutti.pdf)
5. Sure, Staab and Studer, ontology engineering methodology work; compare METHONTOLOGY and NeOn literature.

Read with actual competency questions and reasoner tests.

## 3. RDF, SPARQL, OWL and validation

The specifications in [[48_Current_Standards_Status_2026]] are primary. Supporting research:

1. Horrocks, Patel-Schneider and van Harmelen (2003), **From SHIQ and RDF to OWL**. [DOI](https://doi.org/10.1016/S1570-2464(03)81005-7)
2. Motik, Patel-Schneider and Grau, **OWL 2 Web Ontology Language Direct Semantics** - W3C specification.
3. Knublauch and Kontokostas (2017), **Shapes Constraint Language (SHACL)** - W3C Recommendation.
4. Corman et al. (2018), **Validating SHACL Constraints over a SPARQL Endpoint**. [DOI](https://doi.org/10.1007/978-3-030-00671-6_9)

## 4. Knowledge graph construction and extraction

1. Dong et al. (2014), **Knowledge Vault: A Web-Scale Approach to Probabilistic Knowledge Fusion**. [PDF](https://research.google/pubs/knowledge-vault-a-web-scale-approach-to-probabilistic-knowledge-fusion/)
2. Del Corro and Gemulla (2013), **ClausIE: Clause-Based Open Information Extraction**. [Paper](https://www.mpi-inf.mpg.de/departments/databases-and-information-systems/research/ambiverse-nlu/clausie)
3. Luan et al. (2018), **Multi-Task Identification of Entities, Relations, and Coreference for Scientific Knowledge Graph Construction**. [arXiv](https://arxiv.org/abs/1808.09602)
4. Cabot and Navigli-related recent LLM-to-KG surveys; use primary evaluated papers and schema-constrained extraction work.
5. For agentic construction, compare 2025-2026 systems against classical extraction and deterministic pipelines rather than only other LLM systems.

## 5. Entity resolution and fusion

1. Fellegi and Sunter (1969), **A Theory for Record Linkage**. [JSTOR](https://www.jstor.org/stable/2286061)
2. Christen (2012), **Data Matching** - book and associated papers.
3. Getoor and Machanavajjhala (2012), **Entity Resolution: Theory, Practice and Open Challenges**. [DOI](https://doi.org/10.14778/2367502.2367564)
4. Papadakis et al. (2021), **Blocking and Filtering Techniques for Entity Resolution: A Survey**. [DOI](https://doi.org/10.1145/3459997)
5. Mudgal et al. (2018), **Deep Learning for Entity Matching**. [DOI](https://doi.org/10.1145/3183713.3196926)

## 6. Network science and graph algorithms

1. Page et al. (1999), **The PageRank Citation Ranking**. [PDF](http://ilpubs.stanford.edu:8090/422/)
2. Kleinberg (1999), **Authoritative Sources in a Hyperlinked Environment**. [DOI](https://doi.org/10.1145/324133.324140)
3. Girvan and Newman (2002), **Community Structure in Social and Biological Networks**. [PNAS](https://doi.org/10.1073/pnas.122653799)
4. Blondel et al. (2008), **Fast Unfolding of Communities in Large Networks** (Louvain). [arXiv](https://arxiv.org/abs/0803.0476)
5. Traag, Waltman and van Eck (2019), **From Louvain to Leiden**. [Scientific Reports](https://doi.org/10.1038/s41598-019-41695-z)
6. Rosvall and Bergstrom (2008), **Maps of Random Walks on Complex Networks Reveal Community Structure**. [PNAS](https://doi.org/10.1073/pnas.0706851105)
7. Fortunato and Hric (2016), **Community Detection in Networks: A User Guide**. [Physics Reports](https://doi.org/10.1016/j.physrep.2016.09.002)

## 7. Knowledge graph embeddings

1. Bordes et al. (2013), **Translating Embeddings for Modeling Multi-relational Data** (TransE). [NeurIPS](https://proceedings.neurips.cc/paper/2013/hash/1cecc7a77928ca8133fa24680a88d2f9-Abstract.html)
2. Yang et al. (2015), **Embedding Entities and Relations for Learning and Inference in Knowledge Bases** (DistMult). [ICLR](https://arxiv.org/abs/1412.6575)
3. Trouillon et al. (2016), **Complex Embeddings for Simple Link Prediction** (ComplEx). [ICML](https://proceedings.mlr.press/v48/trouillon16.html)
4. Sun et al. (2019), **RotatE: Knowledge Graph Embedding by Relational Rotation in Complex Space**. [ICLR](https://arxiv.org/abs/1902.10197)
5. Dettmers et al. (2018), **Convolutional 2D Knowledge Graph Embeddings** (ConvE). [AAAI](https://arxiv.org/abs/1707.01476)
6. Ruffinelli et al. (2020), **You CAN Teach an Old Dog New Tricks! On Training KGE Models**. [ICLR](https://arxiv.org/abs/2005.14001)

## 8. GNN foundations

1. Gori et al. (2005) and Scarselli et al. (2009), early Graph Neural Network models.
2. Kipf and Welling (2017), **Semi-Supervised Classification with Graph Convolutional Networks**. [ICLR](https://arxiv.org/abs/1609.02907)
3. Hamilton, Ying and Leskovec (2017), **Inductive Representation Learning on Large Graphs** (GraphSAGE). [NeurIPS](https://arxiv.org/abs/1706.02216)
4. Velickovic et al. (2018), **Graph Attention Networks**. [ICLR](https://arxiv.org/abs/1710.10903)
5. Xu et al. (2019), **How Powerful are Graph Neural Networks?** (GIN/WL). [ICLR](https://arxiv.org/abs/1810.00826)
6. Gilmer et al. (2017), **Neural Message Passing for Quantum Chemistry**. [ICML](https://arxiv.org/abs/1704.01212)
7. Battaglia et al. (2018), **Relational Inductive Biases, Deep Learning, and Graph Networks**. [arXiv](https://arxiv.org/abs/1806.01261)

## 9. GNN limits, heterophily and scale

1. Oono and Suzuki (2020), depth/over-smoothing analysis. [ICLR](https://arxiv.org/abs/1905.10947)
2. Alon and Yahav (2021), **On the Bottleneck of Graph Neural Networks and its Practical Implications** (over-squashing). [ICLR](https://arxiv.org/abs/2006.05205)
3. Zhu et al. (2020), **Beyond Homophily in Graph Neural Networks**. [NeurIPS](https://arxiv.org/abs/2006.11468)
4. Frasca et al. and related heterophily benchmark papers - inspect split/data artifacts carefully.
5. Zeng et al. (2020), **GraphSAINT**. [ICLR](https://arxiv.org/abs/1907.04931)
6. Chiang et al. (2019), **Cluster-GCN**. [KDD](https://arxiv.org/abs/1905.07953)

## 10. Relational, heterogeneous and temporal graphs

1. Schlichtkrull et al. (2018), **Modeling Relational Data with Graph Convolutional Networks** (R-GCN). [ESWC](https://arxiv.org/abs/1703.06103)
2. Wang et al. (2019), **Heterogeneous Graph Attention Network** (HAN). [WWW](https://arxiv.org/abs/1903.07293)
3. Hu et al. (2020), **Heterogeneous Graph Transformer**. [WWW](https://arxiv.org/abs/2003.01332)
4. Rossi et al. (2020), **Temporal Graph Networks**. [arXiv](https://arxiv.org/abs/2006.10637)
5. Xu et al. (2020), **Inductive Representation Learning on Temporal Graphs** (TGAT). [ICLR](https://arxiv.org/abs/2002.07962)

## 11. Graph transformers and foundation models

1. Ying et al. (2021), **Do Transformers Really Perform Bad for Graph Representation?** (Graphormer). [arXiv](https://arxiv.org/abs/2106.05234)
2. Rampasek et al. (2022), **Recipe for a General, Powerful, Scalable Graph Transformer** (GraphGPS). [NeurIPS](https://arxiv.org/abs/2205.12454)
3. Dwivedi et al., graph transformer benchmarking/positional encoding work.
4. Wang et al. (2025), **Graph Foundation Models: A Comprehensive Survey**. [arXiv](https://arxiv.org/abs/2505.15116)
5. Kim et al. (2026), **Flock: A Knowledge Graph Foundation Model via Learning on Random Walks**. [ICLR 2026](https://proceedings.iclr.cc/paper_files/paper/2026/hash/3ddbd473456a57e3cafb1ee51ddf8ff6-Abstract-Conference.html)
6. Bechler-Speicher et al. (2026), **Billion-Scale Graph Foundation Models**. [arXiv](https://arxiv.org/abs/2602.04768)

Treat GFM results as emerging; inspect target overlap, adaptation and transfer definitions.

## 12. Neuro-symbolic and rule learning

1. Garcez and Lamb (2020/2023), neuro-symbolic AI surveys/books.
2. Badreddine et al. (2022), **Logic Tensor Networks**. [AI Journal/arXiv](https://arxiv.org/abs/2012.13635)
3. Manhaeve et al. (2018), **DeepProbLog**. [NeurIPS](https://arxiv.org/abs/1805.10872)
4. Rocktaschel and Riedel (2017), differentiable theorem proving. [NeurIPS](https://arxiv.org/abs/1705.11040)
5. Yang, Yang and Cohen (2017), **Differentiable Learning of Logical Rules for KGs**. [NeurIPS](https://arxiv.org/abs/1702.08367)

## 13. GraphRAG, KGQA and graph-assisted LLMs

1. Edge et al. (2024), **From Local to Global: A Graph RAG Approach to Query-Focused Summarization**. [arXiv](https://arxiv.org/abs/2404.16130)
2. Gutierrez et al. (2024), **HippoRAG**. [arXiv](https://arxiv.org/abs/2405.14831)
3. Gutierrez et al. (2025), **HippoRAG 2 / From RAG to Memory**. [arXiv](https://arxiv.org/abs/2502.14802)
4. Guo et al. (2024), **LightRAG**. [arXiv](https://arxiv.org/abs/2410.05779)
5. Peng et al. (2025/2026), **Graph Retrieval-Augmented Generation: A Survey**. [ACM TOIS](https://doi.org/10.1145/3777378)
6. Xiang et al. (2026), **When to use Graphs in RAG**. [ICLR 2026](https://proceedings.iclr.cc/paper_files/paper/2026/hash/6c9e01d6cefbbf4cdd265032550e767f-Abstract-Conference.html)
7. Luo et al. (2026), **Graph-Assisted Large Language Models**. [ACL Findings](https://aclanthology.org/2026.findings-acl.945/)
8. Shan et al. (2026), **OntGQA: Type-Constrained KGQA**. [ACL](https://aclanthology.org/2026.acl-long.489/)
9. Kumar and Sharma (2025), **OG-RAG**. [Microsoft Research](https://www.microsoft.com/en-us/research/publication/og-rag-ontology-grounded-retrieval-augmented-generation-for-large-language-models/)

## 14. Evaluation and benchmarks

1. Hu et al. (2020), **Open Graph Benchmark**. [NeurIPS](https://arxiv.org/abs/2005.00687)
2. Wang et al. and benchmark papers on realistic link-prediction splits/negatives.
3. LDBC/Graph Data Council benchmark specifications for systems.
4. GraphRAG-Bench (ICLR 2026) for staged GraphRAG evaluation.
5. Revisit papers on dataset leakage in WN18/FB15k and GNN benchmark pitfalls.

## Reading policy

For each cluster:

1. one survey;
2. two seminal methods;
3. one critical/evaluation paper;
4. two recent papers with code;
5. one reproduction;
6. one cross-domain or robustness extension.

Use [[Template - Paper Note]] and [[39_Paper_Reading_Reproduction_and_Writing]].
