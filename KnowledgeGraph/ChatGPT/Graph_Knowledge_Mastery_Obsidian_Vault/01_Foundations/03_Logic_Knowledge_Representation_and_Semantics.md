---
title: "Logic, Knowledge Representation and Semantics"
type: chapter
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - foundations
  - logic
  - knowledge-representation
  - semantics
---
# Logic, Knowledge Representation and Semantics

> [!goal]
> Understand what a representation says, what follows from it, and what remains unknown. This chapter prevents most ontology mistakes.

## 1. Syntax is not semantics

**Syntax** defines legal expressions. **Semantics** defines their meaning through interpretations. Two syntactically different theories may have the same models; one syntactically valid statement may encode an unintended claim.

A vocabulary contains symbols such as `Dealer`, `sells`, and `Vehicle`. An interpretation maps:

- class names to sets of objects;
- relation names to relations over objects;
- individual names to objects;
- datatype terms to values.

A statement is true or false relative to an interpretation. A theory is **satisfiable** if at least one interpretation satisfies every statement.

## 2. Propositional and first-order logic

Propositional logic treats statements as atomic booleans. First-order logic adds variables, predicates, quantifiers and equality.

\[
\forall x\,(Dealer(x)\rightarrow Organization(x))
\]

states that every dealer is an organization.

\[
\forall x\,(Dealer(x)\rightarrow \exists y\,(Region(y)\land inRegion(x,y)))
\]

states that every dealer is in at least one region. Under open-world semantics, failure to record the region does not falsify the claim; the theory permits an unnamed region.

## 3. Necessary and sufficient conditions

- `A SubClassOf B` gives a **necessary** condition: every A is B.
- `A EquivalentTo B and C` gives necessary and sufficient conditions.

Suppose:

\[
HighRiskDealer \equiv Dealer \sqcap \exists hasFinding.CriticalFinding
\]

Any high-risk dealer must be a dealer with a critical finding, and any dealer with such a finding is classified as high-risk. If the second direction is not universally intended, use only subclass axioms or compute a task-specific status outside the ontology.

## 4. Entailment

A theory \(T\) entails \(\varphi\), written \(T\models\varphi\), if every model of \(T\) is also a model of \(\varphi\). An inference engine should be **sound** when everything it derives is entailed, and **complete** for a language/task when it can derive every entailed result.

Different systems support different fragments and entailment regimes. A triplestore returning explicit triples is not equivalent to an OWL DL reasoner.

## 5. Monotonicity

Classical logic and OWL reasoning are monotonic: adding facts cannot invalidate a previous entailment. Operational rules are often non-monotonic:

> “Approve the request if no blocking issue is known.”

Adding a blocking issue reverses the conclusion. Defaults, exceptions, negation-as-failure and changing state usually require rule engines, logic programming, application logic or explicit temporal models rather than pure OWL entailment.

## 6. Open world versus closed world

### Open world

Absence means unknown. This suits a web-scale or multi-source KG where no source is complete.

### Closed world

Absence from a declared complete dataset is treated as false. SQL and operational validation often use this assumption locally.

A mature system uses both deliberately:

- OWL for domain implications under OWA;
- SHACL/database constraints for required fields under a local closed world;
- application rules for workflow state and defaults.

## 7. Unique names and identity

OWL does not infer that two different IRIs denote different entities. You can state `DifferentIndividuals`, or design identifiers and application constraints. Conversely, `owl:sameAs` means full identity: every property of one applies to the other. Use it only for true co-reference, not “similar,” “mapped to,” “same product family” or “approximately equivalent.”

Useful weaker mappings include `skos:exactMatch`, `skos:closeMatch`, custom record-link relations and provenance-qualified mapping assertions.

## 8. Negation types

Do not confuse:

1. **Explicit/classical negation** — the fact is false.
2. **Negation as failure** — the fact cannot be proven from the current database.
3. **Disjointness** — two classes cannot share an instance.
4. **Complement class** — set-theoretic complement under the interpretation.
5. **Constraint violation** — required graph pattern is absent or forbidden pattern exists.

These lead to different conclusions.

## 9. Horn logic and Datalog

A Horn rule has at most one positive conclusion. Datalog uses function-free Horn rules and supports efficient fixed-point evaluation.

```text
eligibleForReview(x) :- Dealer(x), hasCriticalFinding(x, f).
```

Datalog is strong for recursive rules, transitive closure and explainable derivation. Extensions add negation, aggregates, existential heads or probabilistic weights, changing decidability and semantics.

## 10. Description logics

Description logics focus on concepts/classes, roles/relations and individuals with controlled constructors. They aim to retain decidable reasoning. Typical reasoning tasks:

- ontology consistency;
- class satisfiability;
- subsumption/classification;
- instance checking;
- realization of most-specific types;
- query answering under an ontology.

Expressivity has cost. The OWL 2 EL, QL and RL profiles trade language features for predictable reasoning strategies. See [[07_Description_Logics_and_OWL_2]].

## 11. Truth, validation and policy

Separate three layers:

| Layer | Example | Best mechanism |
|---|---|---|
| Domain truth | every BEV is a vehicle | RDFS/OWL axiom |
| Data contract | a vehicle record must contain one VIN | SHACL/database constraint |
| Policy | leadership may view national aggregates | authorization/policy engine |

Encoding policy as ontology truth can create unsafe inference. Encoding universal truth as a database validation rule can block incomplete but valid knowledge.

## 12. Contradiction and inconsistency

In classical logic, an inconsistent theory can entail everything (principle of explosion). Practical reasoners normally report inconsistency rather than return arbitrary facts. Large KGs may instead use paraconsistent, defeasible or source-scoped approaches so local contradictions do not collapse the whole system.

Always ask whether conflicting statements are:

- logically incompatible;
- valid at different times;
- reported by different sources;
- about merged entities that should be separate;
- using different definitions;
- measurements with uncertainty.

## 13. Names versus meaning

A relationship called `HAS_GOOD_PERFORMANCE` has no formal meaning unless defined through axioms, constraints, rules or documentation. LLMs and humans infer meaning from the label; a reasoner does not.

Use natural-language definitions, examples, formal axioms and competency questions together. A formal axiom can be precise but wrong; a textual definition can be clear but not machine-actionable.

## 14. Competency questions as semantic tests

A competency question is a natural-language question the knowledge model must answer, such as:

- Which dealers had an allocation shortfall during a particular program period?
- Which recommendation was based on a superseded policy?
- Which legal section amended a section cited by a judgment at decision time?

Transform each into:

1. required concepts and relations;
2. formal query;
3. positive test data;
4. negative/counterexample data;
5. expected entailments;
6. performance target.

## 15. Mini examples

### Domain/range do not behave like field constraints

In RDFS/OWL, declaring:

```turtle
:hasManager rdfs:domain :Organization ;
            rdfs:range  :Person .
```

means that anything using `hasManager` is inferred to be an `Organization`, and every object is inferred to be a `Person`. It does not reject data whose subject lacks an explicit `Organization` type.

### Universal restriction does not assert existence

`Dealer subClassOf hasRegion only Region` says that any recorded `hasRegion` target is a Region. It does not say every Dealer has a region. Add `some Region` for existence—only when universally true.

## Exercises

1. For ten domain statements, classify each as truth, validation, default, policy or statistical prediction.
2. Construct two interpretations showing why an unstated fact is not false under OWA.
3. Give an example where `owl:sameAs` creates an unwanted property transfer.
4. Convert five business rules to Datalog; identify which use negation or aggregation.
5. Design positive and negative competency-question tests for an automotive incentive ontology.
6. Create a logically consistent graph that nevertheless violates a required-field SHACL shape.

## Primary sources

- OWL 2 overview: https://www.w3.org/TR/owl2-overview/
- OWL 2 direct semantics: https://www.w3.org/TR/owl2-direct-semantics/
- OWL 2 profiles: https://www.w3.org/TR/owl2-profiles/
- RDF 1.2 semantics work: https://www.w3.org/TR/rdf12-semantics/
- *Foundations of Semantic Web Technologies* companion site: https://www.semantic-web-book.org/

## Next

Read [[04_Uncertainty_Causality_and_Probabilistic_Graphs]], then begin the semantic stack with [[05_RDF_RDFS_and_Linked_Data]].
