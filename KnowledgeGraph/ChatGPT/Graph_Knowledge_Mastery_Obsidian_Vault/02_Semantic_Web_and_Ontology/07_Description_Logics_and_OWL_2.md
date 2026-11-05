---
title: "Description Logics and OWL 2"
type: chapter
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - owl
  - description-logic
  - reasoning
  - ontology
---
# Description Logics and OWL 2

> [!goal]
> Use OWL as a formal language, not as a richer JSON schema. Understand the inferences and computational consequences of each modeling choice.

## 1. Description-logic anatomy

A description-logic knowledge base is often discussed as:

- **TBox** — terminology/concept axioms;
- **RBox** — role/property axioms;
- **ABox** — assertions about individuals.

The terminology is useful even when an OWL file physically mixes these statements.

A basic DL such as ALC includes:

- atomic concepts \(A\);
- top/bottom \(\top,\bot\);
- conjunction \(C\sqcap D\);
- disjunction \(C\sqcup D\);
- negation \(\neg C\);
- existential restriction \(\exists r.C\);
- universal restriction \(\forall r.C\).

OWL 2 DL corresponds to a highly expressive DL commonly associated with SROIQ(D), adding role hierarchies, inverses, nominals, cardinalities and datatypes under global restrictions.

## 2. OWL entities

OWL uses:

- classes;
- object properties between individuals;
- data properties from individuals to literal values;
- annotation properties without direct DL semantic force;
- named individuals;
- datatypes.

The same IRI can be used in certain syntactic categories through **punning**, but the interpretations are separated. Do not assume that class-level and individual-level facts transfer automatically.

## 3. Class axioms

### Subclass

```text
ElectricDealer SubClassOf Dealer
```

Every ElectricDealer is a Dealer.

### Equivalent classes

```text
HighRiskDealer EquivalentTo
    Dealer and (hasFinding some CriticalFinding)
```

This is a definition in both directions.

### Disjointness

```text
Dealer DisjointWith Vehicle
```

If one individual is inferred as both, the ontology becomes inconsistent. Disjointness is powerful for detecting category mistakes but dangerous when classes can legitimately overlap.

### Disjoint union

A parent can be declared exactly partitioned by child classes. Use only when coverage and mutual exclusivity are universal.

## 4. Property restrictions

### Existential

`hasRegion some Region` requires at least one such relation in every model, though the target may be unnamed.

### Universal

`hasRegion only Region` constrains any existing targets but does not assert that one exists.

### Cardinality

- `min 1` — at least one;
- `max 1` — at most one;
- `exactly 1` — both.

Cardinality under OWA and no UNA can surprise you. Two named managers do not necessarily violate `max 1` unless they are known to be different; a reasoner may infer they denote the same individual.

### Has-value and nominals

`hasStatus value Approved` and enumerations `{Alice, Bob}` can express specific values/individuals. Large enumerations are usually a maintenance smell.

## 5. Property axioms

OWL supports:

- subproperties;
- inverse properties;
- equivalent/disjoint properties;
- transitive, symmetric, asymmetric, reflexive and irreflexive characteristics;
- functional/inverse-functional properties;
- property chains;
- domain and range.

Example chain:

```text
hasParent o hasSibling -> hasAuntOrUncle
```

Property chains derive relations but interact with OWL’s global restrictions. Properties used in cardinality and certain characteristics must remain “simple.” Use a reasoner and profile checker rather than relying on intuition.

## 6. Keys and identity

`HasKey` says that individuals of a class sharing specified values/relations are the same under OWL semantics. Real identifiers can be dirty, recycled or scoped, so application-level entity resolution and SHACL uniqueness checks are often safer than global logical identity.

Functional properties do not mean the stored dataset contains only one value; they create equality implications or inconsistency when targets are known different.

## 7. OWL profiles

### OWL 2 EL

Designed for very large class/property hierarchies and polynomial-time core reasoning. It supports existential restrictions and property chains but limits constructs such as universal restrictions and arbitrary negation. Biomedical ontologies often fit EL-like needs. ELK is a specialized reasoner.

### OWL 2 QL

Designed for ontology-based data access over large instance stores. Queries can be rewritten toward relational databases. It is based on DL-Lite ideas and limits expressive features to retain low data complexity.

### OWL 2 RL

Designed for scalable rule-based implementation. It balances useful OWL expressivity with forward-chaining rules.

### OWL 2 DL and Full

OWL 2 DL offers strong expressivity with decidable reasoning under structural restrictions. OWL 2 Full allows unrestricted RDF-style combinations but gives up the same decidability guarantees.

> [!tip] Profile choice
> Start with the least expressive profile that answers the competency questions. Expressivity is a cost budget, not a status symbol.

## 8. Core reasoning tasks

- **Consistency** — does the complete ontology have a model?
- **Class satisfiability** — can a class have any instances?
- **Subsumption** — is every instance of C necessarily an instance of D?
- **Classification** — compute inferred class hierarchy.
- **Instance checking** — is individual a necessarily in class C?
- **Realization** — find most specific inferred classes of an individual.
- **Explanation/justification** — identify axioms sufficient for an entailment or inconsistency.

## 9. Modeling examples

### Defined versus primitive class

Primitive:

```text
LeadershipDealer SubClassOf Dealer
```

Defined:

```text
LeadershipDealer EquivalentTo
  Dealer and (hasScope value NationalScope)
```

Use a defined class only if the condition truly determines membership.

### Roles over time

Avoid asserting `Alice a Manager` as a timeless essence if management is contextual. Model a `ManagementAssignment` or role with organization and interval. Ontology patterns can then classify the assignment or role bearer without erasing time.

### Measurements

Do not define `UnderperformingDealer` solely from an externally changing threshold in OWL unless the threshold semantics and datatype reasoning are supported and stable. Compute observations/rules, assert the resulting status with provenance, or validate through a rule/analytics layer.

## 10. Common OWL mistakes

1. **Universal-only definition** — `Pizza and hasTopping only Cheese` includes pizzas with no toppings. Combine with `some` if existence is intended.
2. **Domain/range as constraints** — they infer types.
3. **Closure assumption** — `hasPart only Wheel` does not mean all known parts have been listed.
4. **Overusing exact cardinality** — the world may be incomplete.
5. **Overusing disjointness** — real categories may overlap or be context-dependent.
6. **Class–individual confusion** — model levels explicitly.
7. **Strong identity mappings** — `sameAs` causes full substitution.
8. **Reasoner-blind authoring** — ontology appears fine until classification reveals unsatisfiable classes.
9. **Encoding workflow/policy as universal truth**.
10. **Mixing versions without import control**.

## 11. Ontology imports and modularity

`owl:imports` includes another ontology’s axioms. Imports are semantic dependencies, not merely hyperlinks. Pin versions, cache artifacts, define trust/licensing and test the combined ontology. A modular ontology typically separates:

- upper/core module;
- domain concepts;
- application constraints;
- mappings to external vocabularies;
- instance data;
- deprecated compatibility layer.

## 12. OWL syntaxes

OWL can be serialized in RDF syntaxes, Functional Syntax, Manchester Syntax and OWL/XML. Manchester Syntax is readable for class expressions; Turtle integrates with RDF data; Functional Syntax mirrors the specification. Compare semantics, not appearance.

Example in Manchester style:

```text
Class: ex:HighRiskDealer
  EquivalentTo:
    ex:Dealer and
    ex:hasFinding some ex:CriticalFinding
```

## 13. Reasoner-driven development

Use this loop:

1. Add one modeling change.
2. Classify ontology.
3. Inspect unexpected inferred parents.
4. Check unsatisfiable classes.
5. Run competency-question tests.
6. Generate explanation for surprising entailment.
7. Commit with a decision note.

Large changes make justifications difficult to interpret.

## 14. Performance reasoning

Reasoning complexity depends on language fragment and ontology structure, not just triple count. Large ABoxes, complex property chains, nominals and qualified cardinalities can be expensive. Profile-specific or rule-based reasoners may scale better than a complete OWL 2 DL reasoner.

Separate workloads:

- offline ontology classification;
- incremental TBox updates;
- high-volume instance inference;
- online query answering;
- explanation generation.

One engine need not handle all of them.

## 15. Exercises

1. Model a dealer/person/role hierarchy and deliberately create an unsatisfiable class; obtain a justification.
2. Show why two manager IRIs do not violate a max-one restriction without `DifferentIndividuals`.
3. Rewrite an overly expressive ontology into EL, QL or RL and document lost semantics.
4. Create definitions for five classes; test whether examples and counterexamples classify correctly.
5. Model a legal amendment with time and source without treating an amended provision as identical to the old version.
6. Compare OWL inference with equivalent SHACL constraints and explain the difference.

## Primary sources

- OWL 2 Overview: https://www.w3.org/TR/owl2-overview/
- OWL 2 Primer: https://www.w3.org/TR/owl2-primer/
- OWL 2 Structural Specification: https://www.w3.org/TR/owl2-syntax/
- OWL 2 Direct Semantics: https://www.w3.org/TR/owl2-direct-semantics/
- OWL 2 Profiles: https://www.w3.org/TR/owl2-profiles/
- OWL 2 Quick Reference: https://www.w3.org/TR/owl2-quick-reference/
- HermiT reasoner: https://www.hermit-reasoner.com/
- ELK reasoner: https://github.com/liveontologies/elk-reasoner

## Next

Apply these foundations in [[08_Ontology_Engineering_Methodology]].
