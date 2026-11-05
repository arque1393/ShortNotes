---
title: "Entity Resolution and Knowledge Fusion"
type: chapter
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - entity-resolution
  - record-linkage
  - knowledge-fusion
  - identity
  - data-quality
---
# Entity Resolution and Knowledge Fusion

> [!goal]
> Resolve which records refer to the same real-world entity, preserve uncertainty and history, and fuse conflicting claims without destroying evidence.

## 1. Separate four problems

1. **Deduplication**: find duplicate records within one source.
2. **Record linkage**: connect records across sources.
3. **Entity linking**: map a mention to a canonical knowledge base entity.
4. **Knowledge fusion**: select, combine or represent conflicting claims after identity decisions.

Identity errors are high-impact: a false merge contaminates every neighbor; a missed merge fragments evidence.

## 2. Formal view

Given records $r_i$ and $r_j$, estimate whether they refer to the same entity:

$$P(M=1\mid \phi(r_i,r_j)),$$

where $\phi$ contains name, address, identifier, temporal, type and relational features. The output should support:

- match;
- non-match;
- uncertain/review;
- match type, such as same organization versus same branch.

## 3. Pipeline

```mermaid
flowchart LR
    N[Normalize] --> B[Block candidates]
    B --> F[Compute features]
    F --> S[Score/classify]
    S --> C[Cluster]
    C --> V[Validate constraints]
    V --> R[Review uncertain cases]
    R --> X[Create crosswalk and provenance]
```

### Normalization

Standardize case, whitespace, punctuation, transliteration, addresses, phone numbers, dates and organization suffixes. Keep raw values.

### Blocking

All-pairs comparison is $O(n^2)$. Blocking retrieves plausible candidates using exact keys, phonetic keys, token indexes, locality-sensitive hashing, vector retrieval, graph neighborhoods or learned blocking.

Optimize candidate recall first; a missed candidate cannot be recovered by the matcher.

## 4. Features

- exact/partial identifier agreement;
- edit/Jaro-Winkler/token similarity;
- address component agreement;
- geographic distance;
- date compatibility;
- type compatibility;
- shared parent/contacts;
- relational/neighborhood similarity;
- source reliability;
- temporal overlap or contradiction;
- embedding similarity.

A relational feature can be powerful but circular: incorrect graph links can reinforce incorrect matches. Use staged inference and audit feedback loops.

## 5. Matching approaches

### Deterministic rules

Transparent and strong for reliable identifiers. Brittle under missing/noisy values.

### Probabilistic record linkage

Fellegi-Sunter-style models compare agreement frequencies under match and non-match hypotheses. They are interpretable and useful with labeled or estimated distributions.

### Supervised classification

Logistic regression, gradient boosting or neural pair encoders. Require representative labeled pairs and careful class imbalance handling.

### Collective/graph resolution

Jointly infer matches using relationships and cluster consistency. Useful when local attributes are weak, but computationally and operationally more complex.

### LLM-assisted resolution

Useful for explanation, hard semantic comparisons and label generation. Do not rely on unconstrained pairwise prompting at scale. Combine with blocking, structured evidence and deterministic constraints.

## 6. Clustering and transitivity

Pairwise decisions may be inconsistent: A=B, B=C, A!=C. Clustering options include connected components above a threshold, correlation clustering, hierarchical clustering and constrained union-find.

Constraints:

- cannot-link rules;
- maximum one record per source/account type;
- temporal impossibility;
- type/category incompatibility;
- parent-child distinction;
- branch versus legal organization.

Do not blindly take transitive closure of weak pair matches.

## 7. Canonical entity model

Preserve:

- canonical entity ID;
- all source-record IDs;
- match assertions and scores;
- model/rule version;
- reviewer decisions;
- merge/split history;
- preferred attributes with provenance;
- aliases;
- active/valid intervals.

A reversible identity graph is safer than physically deleting source records.

```text
SourceRecord --denotes?--> CanonicalEntity
MatchDecision --aboutPair--> SourceRecord A/B
MatchDecision --generatedBy--> ModelVersion
MatchDecision --reviewedBy--> Human
```

## 8. Knowledge fusion

After identity, sources may disagree about a value. Strategies:

- source priority;
- latest valid observation;
- majority vote;
- weighted trust;
- truth discovery jointly estimating source reliability;
- retain all claims with context;
- domain-specific reconciliation rules.

The "right" strategy depends on the property. Legal name, address, measured sales and expert diagnosis require different policies.

Distinguish:

- assertion time;
- valid time;
- source confidence;
- model confidence;
- source authority;
- current preferred view.

## 9. Evaluation

At pair level:

- precision, recall, F1;
- precision-recall curve;
- cost-weighted false merge/missed merge;
- calibration.

At cluster level:

- B-cubed precision/recall;
- pairwise cluster metrics;
- variation of information;
- cluster purity/completeness.

At system level:

- downstream query/decision quality;
- manual-review volume;
- time to resolution;
- merge reversal rate;
- subgroup/source fairness.

Use entity-disjoint temporal test sets where possible. Random pair splits leak the same entities and aliases across train and test.

## 10. Human-in-the-loop review

A review UI should show:

- side-by-side normalized and raw records;
- matching and conflicting fields;
- neighborhood evidence;
- source provenance;
- model score and rule trace;
- merge consequences;
- accept/reject/defer/split actions.

Prioritize cases by expected value, not uncertainty alone: probability of error x consequence x reach.

## 11. Laboratory

Resolve 100,000 noisy organization/dealer/person records from three sources. Requirements:

- high-recall blocking;
- deterministic baseline;
- probabilistic or supervised matcher;
- constrained clustering;
- reversible crosswalk;
- human-review sample;
- pair and cluster metrics;
- downstream CQ evaluation;
- documented false-merge incident response.

## Mastery checklist

- [ ] I separate blocking, matching, clustering and fusion.
- [ ] I optimize blocking recall and measure it independently.
- [ ] I preserve source records and reversible identity history.
- [ ] I evaluate entity-disjoint and by source/subgroup.
- [ ] I represent conflicts instead of overwriting evidence blindly.

## Sources and next reading

- Peter Christen, *Data Matching*
- [JedAI entity resolution framework](https://github.com/scify/JedAIToolkit)
- [Splink probabilistic record linkage](https://github.com/moj-analytical-services/splink)
- [[18_KG_Quality_Governance_and_Evolution]]
- [[23_Knowledge_Graph_Embeddings_and_Link_Prediction]]
