---
tags: [graph-ml, temporal]
phase: 3
status: not-started
---
# Temporal & Dynamic Graph Learning

> [!summary]
> Real graphs evolve (transactions, messages, citations, events). Model either **snapshots** (discrete-time) or **timestamped event streams** (continuous-time).

## Two settings
| | Discrete-time (DTDG) | Continuous-time (CTDG) |
|---|---|---|
| Data | Sequence of snapshots $G_1, …, G_T$ | Stream of $(u, v, t, e)$ events |
| Models | EvolveGCN, GCRN, DySAT | JODIE, DyRep, **TGN**, TGAT, CAWN, GraphMixer, DyGFormer |

## TGN in brief
Per-node **memory** updated by a GRU when the node participates in an event; temporal graph attention with **time encoding** $\cos(\omega t + b)$ produces embeddings for prediction.

## Temporal KG reasoning
Quadruples $(s, r, o, t)$ — e.g., ICEWS, GDELT. Interpolation vs **extrapolation/forecasting**. Models: RE-NET, xERTE, TLogic (temporal rules), RE-GCN.

## Evaluation pitfalls
> [!warning]
> - Random negative sampling inflates scores → use historical & inductive negatives.
> - **EdgeBank** (memorise past edges, no learning) is a shockingly strong baseline.
> - Use chronological splits. Use **TGB / TGB 2.0** (Huang et al., NeurIPS 2023/2024) for standard evaluation.

## Connection
Bi-temporal agent memory → [[Agent Memory as Knowledge Graphs]]; research → [[Open Problems]].

## My notes


## Self-test #flashcards/graph-ml
Difference between DTDG and CTDG?::Discrete-time uses snapshots; continuous-time uses timestamped event streams.
What does TGN's memory module do?::Keeps a per-node state updated (e.g., via GRU) each time the node is in an event.
What is EdgeBank?::A non-learning baseline that predicts edges seen in the past; very strong on many temporal benchmarks.
Standard benchmark suite for temporal graph learning?::TGB (Temporal Graph Benchmark) and TGB 2.0.
