---
title: "Ontology Engineering Methodology"
type: chapter
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - ontology-engineering
  - competency-questions
  - governance
  - protege
---
# Ontology Engineering Methodology

> [!goal]
> Engineer an ontology as a tested, governed product with explicit scope, stakeholders and use cases—not as a one-time diagram.

## 1. Begin with purpose

An ontology is always built for a purpose and anticipated reuse. Write an Ontology Requirements Specification before creating classes.

Minimum requirements:

- domain and boundaries;
- target users and systems;
- competency questions;
- intended reasoning tasks;
- data sources and ownership;
- required interoperability;
- performance and scale;
- privacy/security constraints;
- release and maintenance model;
- out-of-scope concepts.

A model for search may differ from one for scientific inference or transactional validation.

## 2. Competency questions

Good competency questions are concrete, testable and collectively define scope.

Weak: “What do we know about dealers?”

Strong:

- Which dealers had a sales shortfall for a vehicle line during an active program interval?
- Which coaching recommendation cites evidence collected after the recommendation date?
- Which virtual-business-center users inherit national scope under the current role policy?

For each CQ, record:

- natural-language wording;
- sample expected answer;
- source fields needed;
- query form;
- inference required;
- completeness assumptions;
- access-control context;
- response-time target.

## 3. Gather terminology, but do not copy nouns blindly

Collect terms from experts, documents, schemas, APIs and existing ontologies. Classify candidates as:

- entity/type;
- relation;
- event/process;
- role;
- quality;
- measurement;
- identifier;
- document/information artifact;
- rule/policy;
- synonym or label;
- instance.

A noun can be a class in one model and an individual or role in another. Model based on identity and queries, not grammar alone.

## 4. Reuse before reinventing

Search authoritative ontology catalogs, standards and domain communities. Evaluate reuse by:

- semantic fit;
- governance and maintenance;
- license;
- identifier stability;
- language/profile compatibility;
- documentation and examples;
- adoption;
- import size and dependencies.

Reuse can be:

- direct import;
- local subset/module;
- alignment mapping;
- copied pattern with attribution;
- terminology only.

Full imports can introduce unintended axioms. Treat them as dependencies with version tests.

## 5. Conceptual modeling

Use examples and counterexamples before formal axioms. For every class:

- textual definition;
- parent concept;
- identity criterion when relevant;
- necessary characteristics;
- sufficient characteristics only when justified;
- positive examples;
- near misses/counterexamples;
- source/reference;
- owner/steward.

For every relation:

- domain-independent natural-language definition;
- source and target types;
- direction;
- cardinality expectations;
- time dependence;
- symmetry/transitivity/functionality only if universal;
- inverse relation where useful;
- provenance requirements.

## 6. Choose ontological commitment

A commitment determines what kinds of things the ontology says exist and how categories behave.

Questions:

- Are events first-class entities?
- Are roles distinct from persons/organizations?
- Are measurements observations or direct attributes?
- Are documents and the things they describe distinct?
- Are plans, policies and recommendations information artifacts?
- Are versions distinct entities connected by revision relations?
- Are temporal parts or validity intervals needed?

Too little commitment produces ambiguous data. Too much produces complexity and resistance. Commit only where it improves integration, inference or correctness.

## 7. Top-down, bottom-up and middle-out

- **Top-down** begins with general categories and specializes. It improves coherence but can become abstract.
- **Bottom-up** begins with source fields/instances. It improves data fit but can reproduce accidental schema structures.
- **Middle-out** begins with stable central concepts and expands. It is often most practical.

Use all three iteratively: top-level alignment, core domain concepts, source mapping and CQ tests.

## 8. Naming and identifiers

Good labels improve human use; stable opaque IRIs improve lifecycle management.

Conventions:

- classes as singular nouns (`SalesObservation`);
- object properties as readable verbs (`hasDealer`, `appliesTo`);
- avoid encoding mutable hierarchy in IRIs;
- one preferred English label plus synonyms and language tags;
- textual definitions that state necessary distinctions;
- deprecate terms without reusing IRIs for new meanings.

## 9. Design patterns

Patterns solve recurring modeling problems:

- n-ary relation/event;
- role and participation;
- time-indexed relation;
- measurement/observation;
- provenance-qualified assertion;
- part–whole;
- classification scheme;
- plan and execution;
- versioning/change;
- information artifact versus referent.

A pattern must fit your ontological commitment. Do not combine patterns mechanically.

## 10. Formalization workflow

1. Create classes and hierarchy.
2. Add object/data properties with definitions.
3. Add only high-confidence disjointness.
4. Add necessary restrictions.
5. Add defined classes where automatic classification is required.
6. Add property characteristics/chains cautiously.
7. Run a reasoner.
8. Add individuals for examples and counterexamples.
9. Run CQ queries.
10. Add SHACL shapes for data contracts.

## 11. Testing pyramid

### Syntax tests

- parsable serialization;
- valid IRIs and prefixes;
- profile conformance;
- import resolution.

### Logical tests

- ontology consistent;
- no unintended unsatisfiable classes;
- expected subsumptions and non-subsumptions;
- expected instance classifications;
- explanations for critical entailments.

### Competency tests

- SPARQL/other queries return expected answers over fixtures;
- required inferences are present;
- forbidden answers are absent.

### Data-quality tests

- SHACL shapes pass valid fixtures and fail invalid ones;
- identifiers, datatypes, units and time intervals are checked.

### Regression tests

- ontology changes do not unexpectedly change prior entailments or query answers;
- performance remains within budget.

Tools such as ROBOT, OWLAPI-based tests, SHACL engines, SPARQL test harnesses and CI workflows can automate these layers.

## 12. Modularization

A practical enterprise ontology may use:

```text
core/
  organization.owl
  people-and-roles.owl
  time.owl
domain/
  dealer-network.owl
  sales.owl
  aftersales.owl
application/
  coaching.owl
  dashboard-shapes.ttl
mappings/
  legacy-schema.ttl
examples/
  competency-fixtures.ttl
```

Modules need documented public terms, imports and version policy. Avoid circular dependencies where possible.

## 13. Versioning and change management

Classify changes:

- label/documentation only;
- backward-compatible addition;
- logical-strengthening change;
- deprecation;
- breaking semantic change;
- identifier change;
- external alignment change.

A term’s definition should not be changed so radically that its referents change while retaining the same IRI. Deprecate and create a new term. Publish release notes, migration guidance, machine-readable version IRIs and archived releases.

## 14. Collaboration and governance

Define roles:

- domain owner;
- ontology editor;
- data steward;
- logical reviewer;
- application consumer;
- release manager;
- security/privacy reviewer.

Use issue templates capturing the problem, proposed definition, examples, impacted CQs, migration and evidence. Collaborative tools such as WebProtégé help with comments and change history, but governance still requires decisions and accountability.

## 15. Documentation as product surface

Every released term should have:

- preferred label;
- definition;
- examples;
- parent hierarchy;
- domain/range or usage notes;
- status and version;
- source;
- mappings;
- diagrams or query examples when useful.

Generate HTML documentation and diagrams automatically in CI so documentation stays synchronized.

## 16. Evaluation dimensions

Evaluate ontology quality through multiple lenses:

- **logical** — consistency, satisfiability, redundancy;
- **task** — competency-question coverage;
- **domain** — expert agreement and accuracy;
- **structural** — depth, breadth, tangledness, orphan concepts;
- **reuse/interoperability** — mappings and external adoption;
- **usability** — definitions, naming, learnability;
- **evolution** — issue response, release stability;
- **operational** — query/reasoning performance.

No single metric captures ontology quality.

## 17. A complete mini-project

Build an ontology for dealer coaching evidence.

### Scope

Represent dealer organizations, roles, metric observations, program intervals, coaching findings, recommendations, evidence and source systems.

### CQs

1. Which recommendation was supported by which observations?
2. Was the supporting program active on the observation date?
3. Which user role was authorized to see the evidence?
4. Which recommendation was superseded?
5. Which observation’s unit or grain is incompatible with a comparison?

### Formal model

- event/observation nodes;
- roles with intervals;
- recommendation as information artifact;
- provenance with PROV-O;
- OWL definitions for stable categories;
- SHACL for required fields and allowed units;
- SPARQL tests for CQs.

### Deliverable

Repository with ontology, shapes, example data, tests, generated documentation, changelog and one application query notebook.

## 18. Anti-patterns

- Importing a giant ontology because it “looks comprehensive.”
- Defining terms through circular synonyms.
- Creating subclasses for every source code.
- Using class hierarchy to represent workflow state.
- Treating roles as permanent person types.
- No counterexamples or negative tests.
- No owner for definitions.
- Changing semantics silently.
- Building ontology after the application merely to document existing code.
- Allowing an LLM to generate axioms without logical and domain review.

## Exercises

1. Write 20 CQs for a legal research KG and sort them by required reasoning/query type.
2. Create an Ontology Requirements Specification using [[Template - Ontology Requirements Specification]].
3. Reuse one external ontology term and document why direct import or mapping was chosen.
4. Model the same concept top-down and bottom-up; compare commitments.
5. Introduce a breaking change and write migration notes.
6. Create CI checks for parse, reasoner consistency, SHACL and CQ queries.

## Authoritative resources

- Noy and McGuinness, *Ontology Development 101*: https://protege.stanford.edu/publications/ontology_development/ontology101.pdf
- Protégé support/tutorials: https://protege.stanford.edu/support/
- NeOn methodology: https://oeg.etsiinf.upm.es/index.php/en/methodologies/59-neon-methodology/index.html
- OBO Foundry principles: https://obofoundry.org/principles/fp-000-summary.html
- Protégé short-course topic outline: https://protege.stanford.edu/shortcourse/

## Next

Add validation, vocabulary and provenance in [[09_SHACL_SKOS_Rules_Provenance_and_Identity]].
