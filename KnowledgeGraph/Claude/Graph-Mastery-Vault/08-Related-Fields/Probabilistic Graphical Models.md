---
tags: [related, pgm]
phase: 5
status: not-started
---
# Probabilistic Graphical Models

> [!summary]
> Graphs encode conditional independences in a joint distribution. **Belief propagation** — passing messages between nodes — is the ancestor of GNN message passing.

## Families
- **Bayesian networks** (directed): $p(x) = \prod_i p(x_i \mid \mathrm{pa}(x_i))$
- **Markov random fields** (undirected): $p(x) = \frac{1}{Z}\prod_{c}\psi_c(x_c)$
- **Factor graphs**, **CRFs** (used in classic NER)

## Inference
- Exact: variable elimination, junction tree
- **Belief propagation (sum-product):** $m_{i\to j}(x_j) = \sum_{x_i}\psi_{ij}(x_i,x_j)\,\psi_i(x_i)\prod_{k\in N(i)\setminus j} m_{k\to i}(x_i)$ — exact on trees, "loopy BP" approximate
- Approximate: MCMC, variational inference

## Connections
- GNNs ≈ learned, neural belief propagation (e.g., Dai et al. 2016 structure2vec)
- Probabilistic KGs, Markov Logic Networks (weighted first-order rules)

## Reading
Koller & Friedman, *Probabilistic Graphical Models* (MIT Press 2009).

## My notes


## Self-test #flashcards/related
Factorisation of a Bayesian network?::p(x) = Π_i p(x_i | parents(x_i))
On which graphs is belief propagation exact?::Trees (acyclic factor graphs).
Relationship between BP and GNNs?::Both pass messages between neighbours; GNNs can be seen as learned, neural generalisations of BP.
