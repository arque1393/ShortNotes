---
title: "Relational, Heterogeneous and Temporal GNNs"
type: chapter
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - heterogeneous-graph
  - relational-gnn
  - temporal-gnn
  - hgt
  - rgcn
---
# Relational, Heterogeneous and Temporal GNNs

> [!goal]
> Model multiple entity/relation types and evolving interactions without erasing semantics or leaking future information.

## 1. Homogeneous simplification has a price

A heterogeneous graph has node types $\mathcal{T}_V$ and edge/relation types $\mathcal{T}_E$. A knowledge graph is commonly multi-relational. Collapsing everything into one adjacency matrix can mix incompatible meanings.

A typed schema/meta-graph states allowed triples:

```text
Dealer -[LOCATED_IN]-> Region
Dealer -[PARTICIPATES_IN]-> Program
Program -[APPLIES_TO]-> VehicleModel
Coach -[CREATED]-> Recommendation
Recommendation -[SUPPORTED_BY]-> Evidence
```

## 2. R-GCN

Relational GCN uses relation-specific transformations:

$$h_i^{(l+1)}=\sigma\left(W_0^{(l)}h_i^{(l)}+\sum_{r\in\mathcal R}\sum_{j\in\mathcal N_i^r}\frac{1}{c_{i,r}}W_r^{(l)}h_j^{(l)}\right).$$

Many relations create too many parameters. Basis or block-diagonal decomposition shares structure. R-GCN is a strong baseline for multi-relational node classification and KG completion.

## 3. Metapaths

A metapath is a type-level path, such as:

```text
Dealer -> Program -> Dealer
Dealer -> Region -> Dealer
Paper -> Author -> Paper
```

It defines a semantic notion of connection. Metapath-based features/attention can be interpretable, but hand-selection may encode bias and long metapaths can explode. Compare to relation-aware models that learn combinations.

## 4. Heterogeneous attention and transformers

Architectures such as HAN and HGT use node/edge-type-specific parameters and attention. HGT adds type-aware projections and relative temporal/type information. Benefits include expressive cross-type interaction; costs include parameter growth, sampling complexity and harder interpretation.

## 5. Knowledge-graph GNNs

KG GNNs may update both entity and relation representations, compose relation embeddings along paths, or combine message passing with KGE decoders. Examples of ideas include CompGCN, relation-aware attention and subgraph reasoning for inductive link prediction.

Key choice: full-graph entity embeddings versus enclosing-subgraph reasoning. The latter can generalize to unseen entities but is expensive per candidate.

## 6. Dynamic and temporal graphs

Two broad settings:

- **discrete-time snapshots**: graph $G_t$ per interval;
- **continuous-time event streams**: events $(u,v,t,x)$ arrive asynchronously.

Temporal GNNs combine structural aggregation with recurrence, time encoding or memory. Representative ideas include TGAT's temporal attention and TGN's node memories/messages.

### Time-respecting neighborhoods

At prediction time $t$, only events with timestamp $<t$ may influence representation. Neighbor sampling must enforce this.

## 7. Temporal prediction design

For a future edge or event:

- define prediction horizon;
- define observation window;
- decide whether repeated edges count;
- sample negatives from eligible entities at that time;
- avoid future node features and graph normalization;
- evaluate rolling windows;
- measure performance under new nodes and drift.

Static random splits are usually invalid for evolving graphs.

## 8. Memory and staleness

Continuous-time models maintain node memories. Operational questions:

- where memory is stored and checkpointed;
- event ordering and late arrivals;
- replay after failure;
- update consistency across partitions;
- stale memory at serving;
- deletion/privacy propagation;
- cold-start nodes.

The model architecture and streaming system cannot be designed independently.

## 9. Heterophily and signed relations

Different relation types can imply similarity, opposition, hierarchy or causation. Relation-specific channels, signed aggregation, direction-aware propagation and higher-order neighborhoods help. Never assume all neighbors should be smoothed together.

## 10. Hypergraphs and n-ary events

Options:

- event node plus role-specific edges;
- incidence-graph GNN;
- native hypergraph convolution/attention;
- set transformer over event participants.

Compare to the simple event-node representation. Native complexity is justified only when it preserves useful higher-order interaction.

## 11. Evaluation slices

Report:

- seen versus unseen nodes;
- frequent versus rare relation types;
- low/high degree;
- early versus late time windows;
- event recency;
- source/domain;
- cold start;
- relations with few positives;
- latency for updates and predictions.

Macro averaging prevents frequent relations from hiding poor rare-relation performance.

## 12. Laboratory

Build a typed temporal graph with at least four node and five relation types. Compare:

- homogeneous GCN after collapse;
- R-GCN;
- metapath features + conventional model;
- HGT or another heterogeneous model;
- static versus temporal model.

Use rolling time splits, unseen-node evaluation and relation ablations. Record whether extra type/time complexity creates practical improvement.

## Mastery checklist

- [ ] I preserve relation semantics rather than collapsing blindly.
- [ ] I can derive relation-specific message passing.
- [ ] Temporal neighborhoods are strictly past-only.
- [ ] I evaluate unseen nodes and rare relation types.
- [ ] I can explain the systems implications of temporal memory.

## Sources and next reading

- [R-GCN paper](https://arxiv.org/abs/1703.06103)
- [Heterogeneous Graph Transformer](https://arxiv.org/abs/2003.01332)
- [Temporal Graph Networks](https://arxiv.org/abs/2006.10637)
- [PyG heterogeneous graph learning](https://pytorch-geometric.readthedocs.io/en/latest/notes/heterogeneous.html)
- [[26_Graph_Transformers_and_Graph_Foundation_Models]]
