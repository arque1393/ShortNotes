---
tags: [kg-construction, quality]
phase: 2
status: not-started
---
# KG Quality & Refinement

> [!summary]
> No KG is complete or correct. **Refinement** = completion (add missing facts) + error detection (remove wrong ones), using rules, embeddings, external sources or LLMs.

## Quality dimensions
Accuracy (syntactic/semantic) · completeness · consistency · conciseness (no duplicates) · timeliness · trustworthiness · accessibility · licensing.

## Refinement methods
| Goal | Methods |
|---|---|
| Completion: types | Statistical type inference (SDType), classifiers |
| Completion: links | [[KG Embeddings]], GNNs, rules, LLM proposals + verification |
| Error detection | Outlier detection, constraint violations (SHACL), embedding plausibility, rules |
| Rule mining | **AMIE**, AnyBURL — Horn rules like `livesIn(x,y) ⇐ marriedTo(x,z) ∧ livesIn(z,y)` |

## AMIE metrics
- **Support:** # correct predictions of the rule
- **Standard confidence:** support / # predictions (CWA)
- **PCA confidence:** partial completeness assumption — only count as negative if the KG knows *some* object for that subject–relation → fairer under OWA

## Evaluation protocol
Sample-based manual evaluation with confidence intervals (e.g., Wilson interval on precision); stratify by relation type.

## My notes


## Self-test #flashcards/kg-construction
Two goals of KG refinement?::Completion (adding missing knowledge) and error detection (removing incorrect knowledge).
What is the PCA in AMIE?::Partial Completeness Assumption: a missing fact counts as false only if the KG has some object for that subject and relation.
Name two rule miners for KGs.::AMIE and AnyBURL.
