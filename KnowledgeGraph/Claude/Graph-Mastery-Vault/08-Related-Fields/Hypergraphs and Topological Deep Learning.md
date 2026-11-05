---
tags: [related, tdl, hypergraphs]
phase: 5
status: not-started
---
# Hypergraphs & Topological Deep Learning

> [!summary]
> Many relationships are **higher-order** (a paper with 5 authors, a reaction with 4 molecules, an n-ary fact). Hypergraphs, simplicial and cell complexes model them; topological deep learning (TDL) generalises message passing to them.

## Structures
- **Hypergraph:** hyperedges join any number of nodes; incidence matrix $H \in \{0,1\}^{|V|\times|E|}$
- **Simplicial complex:** closed under subsets (triangle ⇒ its edges); **Hodge Laplacian** $L_k = B_k^\top B_k + B_{k+1}B_{k+1}^\top$
- **Cell complex**, **combinatorial complex** (most general)
- **Sheaf neural networks:** attach vector spaces & maps to nodes/edges → help with heterophily

## Models
HGNN, HyperGCN, AllSet; simplicial networks (SCN, MPSN); CW networks; sheaf diffusion.

## KG link
n-ary / hyper-relational KGs (Wikidata qualifiers): StarE, HINGE, hyper-relational link prediction.

## Reading & tools
Hajij et al. "Topological Deep Learning" (arXiv 2206.00606); Papamarkou et al. position paper (ICML 2024); TopoX, TopoBench.

## My notes


## Self-test #flashcards/related
What is a hyperedge?::An edge that connects any number of nodes (not just two).
Property of a simplicial complex?::Closed under taking subsets (faces of a simplex are included).
What is a hyper-relational KG?::A KG whose facts carry qualifiers (key–value pairs), like Wikidata statements.
