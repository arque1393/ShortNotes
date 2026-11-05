---
title: "Uncertainty, Causality and Probabilistic Graphs"
type: chapter
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - foundations
  - probability
  - causal-graphs
  - uncertainty
---
# Uncertainty, Causality and Probabilistic Graphs

> [!goal]
> Represent uncertainty without confusing confidence, probability, missingness, inconsistency and causality.

## 1. Sources of uncertainty

A KG pipeline can be uncertain because of:

- noisy measurement;
- ambiguous language;
- entity-linking alternatives;
- incomplete sources;
- conflicting reports;
- temporal change;
- probabilistic domain mechanisms;
- model prediction uncertainty;
- annotation disagreement.

A single numeric “confidence” often mixes these. Track the type and provenance of uncertainty.

## 2. Confidence is not probability

An extractor score of 0.92 may be a classifier calibration estimate, a heuristic similarity or an LLM self-rating. It is not automatically the probability that a real-world assertion is true. Check calibration with reliability diagrams, Brier score or expected calibration error on labeled data.

Represent at least:

- method/model version;
- score definition and scale;
- threshold used;
- source evidence;
- timestamp;
- human-review state.

## 3. Probabilistic graphical models

### Bayesian networks

A Bayesian network is a directed acyclic graph encoding a factorization:

\[
P(X_1,\ldots,X_n)=\prod_i P(X_i\mid Pa(X_i))
\]

The arrows encode conditional dependence assumptions, and under causal interpretation require stronger assumptions than statistical prediction.

### Markov random fields

An undirected graph defines factorization over cliques:

\[
P(X)=\frac{1}{Z}\prod_c \psi_c(X_c)
\]

where \(Z\) is the partition function. They are useful for collective inference and relational dependencies.

### Factor graphs

Factor graphs make variables and factors explicit as a bipartite graph. They are useful for message passing and combining heterogeneous constraints.

## 4. Causal DAGs are not ordinary KGs

A KG edge `Drug TREATS Disease` is a semantic relation; it does not by itself encode a causal estimand. A causal graph represents assumptions about data-generating mechanisms and confounding. To estimate the effect of intervention \(do(X=x)\), observational association is insufficient without identification assumptions.

Do not run centrality or a GNN on a causal DAG and call the result a causal effect. Do not infer causality from a frequent path in a KG.

## 5. Structural causal models

An SCM defines variables through structural equations:

\[
X_i := f_i(Pa_i, U_i)
\]

where \(U_i\) are exogenous disturbances. It supports observational, interventional and counterfactual questions.

A useful integration pattern is:

- ontology/KG defines variables, units, populations, evidence and interventions;
- causal model defines structural assumptions and estimands;
- data layer supplies observations;
- provenance records which study supports an edge/parameter.

## 6. Probabilistic knowledge graphs

Approaches include:

- attaching confidence to statements;
- probabilistic soft logic with weighted first-order rules;
- Markov logic networks;
- probabilistic databases;
- Bayesian relational models;
- embedding scores converted cautiously into ranking/confidence;
- ensembles of extraction and fusion models.

No single standard probabilistic semantics is universally adopted across KGs. Document how scores combine, whether facts are independent, and what a query result means.

## 7. Possibility, belief and evidence alternatives

When probabilities are unavailable or unjustified, alternatives include:

- fuzzy membership for graded concepts;
- possibility theory;
- Dempster–Shafer belief functions;
- provenance-weighted evidence aggregation;
- interval probabilities;
- qualitative labels such as asserted, inferred, disputed and retracted.

Fuzzy truth (“to what degree is this entity HighRisk?”) differs from uncertainty (“how sure are we that it is HighRisk?”).

## 8. Contradiction under time and source

Two claims can coexist without inconsistency:

- `Dealer101 hasManager Alice` valid in 2025;
- `Dealer101 hasManager Bob` valid from 2026.

Or they may be competing sources. Model claims as first-class assertions/events when source and validity matter. Avoid flattening them into one timeless edge.

## 9. Missing-data mechanisms

Graph missingness is not uniform:

- **MCAR**: missing independent of observed/unobserved data;
- **MAR**: missing depends on observed variables;
- **MNAR**: missing depends on unobserved value or selection mechanism.

KG completion benchmarks often treat sampled missing edges as negatives or hidden positives, but real missingness is biased. A model may learn source coverage rather than world structure.

## 10. Calibration and decision thresholds

For an entity-resolution or link-prediction system, a good ranking metric does not select a safe threshold. Define costs:

\[
Risk(t)=C_{FP}P(\hat y=1,y=0)+C_{FN}P(\hat y=0,y=1)
\]

Then evaluate calibration, precision/recall at operational volume, reviewer capacity and subgroup behavior. In a KG, a false merge can propagate many downstream errors and may cost far more than a missed merge.

## 11. Uncertain rules and soft constraints

A hard rule says a violation is impossible or invalid. A soft rule contributes evidence:

> Dealers in the same legal entity and address are likely identical.

Soft rules can be learned or weighted. Keep them separate from ontological identity axioms.

## 12. Temporal uncertainty

Dates may be exact, interval-valued, approximate or only ordered. Represent precision explicitly rather than inventing a day. A historical legal fact may be valid during an interval but recorded later. Bi-temporal models distinguish:

- valid time: when it was true in the domain;
- transaction time: when the system knew/stored it.

## 13. Decision guide

| Problem | Appropriate starting point |
|---|---|
| Extraction score | calibrated classifier probability + provenance |
| Conflicting sources | claim nodes, source reliability and temporal scope |
| Soft relational patterns | probabilistic soft logic or learned relational model |
| Cause/effect | causal DAG/SCM with explicit identification assumptions |
| Graded category | fuzzy set/continuous score, not probability by default |
| Link ranking | KGE/GNN score with leakage-safe evaluation |
| Required record | SHACL/database constraint, not probability |

## Labs

1. Calibrate an entity-match model and compare raw similarity to calibrated probability.
2. Represent two conflicting facts as claim nodes with source, confidence and validity intervals.
3. Build a small Bayesian network and show conditional independence by d-separation.
4. Draw a causal DAG for dealer coaching outcomes; list confounders and explain why a KG path is not an effect estimate.
5. Compare hard identity rules with soft evidence using a synthetic duplicate dataset.

## Reading

- Judea Pearl, *Causality* and *The Book of Why* for causal foundations.
- Daphne Koller and Nir Friedman, *Probabilistic Graphical Models*.
- Probabilistic Soft Logic project: https://psl.linqs.org/
- W3C PROV-O for representing derivation and responsibility: https://www.w3.org/TR/prov-o/

## Next

Begin the semantic data stack with [[05_RDF_RDFS_and_Linked_Data]].
