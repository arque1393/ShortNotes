---
tags: [ontology, methodology]
phase: 2
status: not-started
---
# Ontology Engineering Methodologies

> [!summary]
> Build ontologies like software: **requirements (competency questions) → reuse → model with patterns → test → document → iterate**.

## Workflow you can actually follow
1. **Scope & purpose** — which application? Who uses it?
2. **Competency questions (CQs)** — 20–50 questions the ontology must answer, e.g., *"Which suppliers of component X are located in a sanctioned country?"* CQs become **SPARQL test queries**.
3. **Reuse** (NeOn scenarios) — search LOV, BioPortal, OBO Foundry, schema.org before inventing terms.
4. **Conceptualise** — glossary of terms; identify classes, properties, individuals.
5. **Apply Ontology Design Patterns (ODPs)** — n-ary relation, participation, part-of, time-indexed situation, agent-role, event.
6. **Align upwards** — to a foundational ontology if interoperability matters ([[Foundational and Domain Ontologies]]).
7. **Formalise** in OWL (Protégé), add SHACL shapes.
8. **Test** — reasoner consistency, unsatisfiable classes, CQ SPARQL queries, OOPS! pitfall scanner, ROBOT `report`.
9. **Document & publish** — WIDOCO, persistent IRIs (w3id.org), versioning, licence.

## Methodologies to know
| Name | Key idea |
|---|---|
| METHONTOLOGY | Lifecycle: specification → conceptualisation → formalisation → implementation → maintenance |
| NeOn | 9 scenarios emphasising reuse and re-engineering of existing resources |
| eXtreme Design (XD) | Agile, CQ-driven, pattern-based |
| MOMo | Modular ontology modelling with ODPs |
| Ontology Development 101 (Noy & McGuinness) | Classic beginner guide |
| LLM-assisted (Ontogenia, OntoChat) | LLMs draft CQs and axioms; humans review |

> [!tip]
> CQs are the single most useful practice: they make an ontology *testable* and keep scope under control.

## My notes


## Self-test #flashcards/ontology
What are competency questions?::Natural-language questions the ontology must answer; they define requirements and become test queries.
What does the NeOn methodology emphasise?::Reuse and re-engineering of existing ontological and non-ontological resources (9 scenarios).
Name three ontology design patterns.::N-ary relation, part-of (partonomy), time-indexed situation (also participation, agent-role).
Tool that generates ontology documentation?::WIDOCO
