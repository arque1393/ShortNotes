---
tags: [project]
phase: 5
status: not-started
---
# P10 — Temporal Graph Learning

**Goal:** Compare temporal GNNs with simple baselines; try temporal KG forecasting.

**Data:** TGB datasets (e.g., tgbl-wiki, tgbl-review), ICEWS/GDELT for TKGs.
**Stack:** PyG temporal / TGB loaders, DyGLib.

## Steps
- [ ] Baselines: EdgeBank, static GNN on aggregated graph
- [ ] Models: TGN, DyGFormer (or GraphMixer)
- [ ] Use TGB evaluation protocol (correct negatives)
- [ ] TKG forecasting: RE-GCN or TLogic on ICEWS
- [ ] Analysis: when does memory help? Effect of time encoding?

**Done when:** honest comparison including where baselines win.
Concepts: [[Temporal Graph Learning]] · [[Scalable GNN Training]]
