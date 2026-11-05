---
tags: [kg-construction, entity-resolution]
phase: 2
status: not-started
---
# Entity Resolution (ER)

> [!summary]
> Decide which records refer to the **same real-world entity** (record linkage, deduplication). Bad ER = duplicated or wrongly merged nodes = broken analytics and GraphRAG.

## Pipeline
1. **Normalisation** (case, whitespace, phone/address standardisation, transliteration)
2. **Blocking** — avoid $O(n^2)$: same postcode, sorted neighbourhood, LSH/MinHash, embedding ANN
3. **Pairwise matching** — rules, **Fellegi–Sunter** probabilistic model (m/u probabilities), ML classifiers, embeddings, LLM adjudication for hard cases
4. **Clustering** — connected components (dangerous: transitive chaining), correlation clustering, center clustering
5. **Canonicalisation** — merge attributes into a golden record; keep lineage

## Fellegi–Sunter in one line
Match weight for field agreement $= \log_2\frac{m}{u}$, where $m=P(\text{agree}\mid\text{match})$, $u=P(\text{agree}\mid\text{non-match})$. Sum weights, threshold into match / possible / non-match.

## Metrics
Pairwise precision/recall/F1, **B-cubed**, cluster-level purity; always measure blocking **pair completeness** (recall of blocking step).

## Tools
**Splink** (Fellegi–Sunter at scale, DuckDB/Spark), Dedupe, Zingg, Senzing, recordlinkage (Python); graph-based ER with GDS node similarity / WCC.

> [!warning]
> Connected-components clustering can chain A≈B, B≈C, … into a giant false cluster. Inspect largest clusters!

## My notes


## Self-test #flashcards/kg-construction
Why is blocking needed in ER?::To avoid comparing all O(n²) pairs by generating only plausible candidate pairs.
Fellegi–Sunter match weight for a field?::log2(m/u), where m = P(agree | match) and u = P(agree | non-match).
Danger of connected-components clustering in ER?::Transitive chaining merges distinct entities into giant clusters.
What does pair completeness measure?::The recall of the blocking step (fraction of true matches kept as candidates).
