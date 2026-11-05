---
tags: [ontology]
phase: 2
status: not-started
---
# Foundational & Domain Ontologies

> [!summary]
> **Foundational (upper) ontologies** provide domain-independent categories (object, process, quality, role). **Domain ontologies** model a field. Aligning to an upper ontology improves interoperability and modelling discipline.

## Foundational
| Ontology | Core split | Notes |
|---|---|---|
| **BFO** (ISO/IEC 21838-2) | Continuant vs Occurrent | Realist; basis of OBO Foundry (biomedicine) |
| **DOLCE** (ISO/IEC 21838-3) | Endurant, Perdurant, Quality, Abstract | Cognitive/linguistic orientation |
| **UFO / gUFO** | Kinds, sub-kinds, roles, phases, relators | gUFO = lightweight OWL implementation; OntoUML |
| schema.org | Pragmatic web vocabulary | Not foundational, but ubiquitous |

## Key distinctions (learn these!)
- **Rigid vs anti-rigid types:** *Person* is a kind (rigid); *Student* is a role (anti-rigid) → never make Student a superclass of Person.
- **Endurants vs perdurants:** things that persist (a car) vs things that happen (a trip).
- **Relators:** reified relationships (an *Employment* mediating Person and Company).

## Domain ontologies worth studying
- **Finance:** FIBO
- **Clinical:** SNOMED CT (OWL EL), ICD
- **Biology:** Gene Ontology, OBO Foundry ontologies, UMLS (metathesaurus)
- **Provenance / time / space:** PROV-O, OWL-Time, GeoSPARQL
- **Web/commerce:** schema.org, GoodRelations
- **Scholarly:** ORKG, FaBiO/SPAR

## My notes


## Self-test #flashcards/ontology
BFO's top-level split?::Continuant vs Occurrent.
Why shouldn't Student be a superclass of Person?::Student is an anti-rigid role; Person is a rigid kind — roles specialise kinds, not the reverse.
What is gUFO?::A lightweight OWL implementation of the Unified Foundational Ontology (UFO).
Which ontology is the basis of the OBO Foundry?::BFO (Basic Formal Ontology).
