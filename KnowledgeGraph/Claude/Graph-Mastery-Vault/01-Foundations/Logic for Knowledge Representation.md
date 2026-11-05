---
tags: [foundations, logic, kr]
phase: 0
status: not-started
---
# Logic for Knowledge Representation

> [!summary]
> Ontologies are logical theories. To understand what OWL reasoners do (and why they behave "strangely" for database people) you need **models, entailment, decidability and the open-world assumption**.

## Building blocks
- **Propositional logic:** atoms, connectives; SAT is NP-complete.
- **First-order logic (FOL):** constants, predicates, functions, quantifiers $\forall,\exists$.
- **Interpretation / model:** an assignment making all axioms true.
- **Entailment** $\mathcal{K} \models \varphi$: $\varphi$ is true in *every* model of $\mathcal{K}$.
- **Soundness** (only derives entailed facts) and **completeness** (derives all of them).
- **Decidability:** FOL entailment is undecidable → KR uses decidable fragments: **Description Logics** ([[Description Logics]]), **Datalog**, guarded fragments.

## Rules & Datalog
- Horn clauses: `ancestor(X,Z) :- parent(X,Y), ancestor(Y,Z).`
- Datalog = function-free Horn logic; polynomial data complexity; basis of **OWL 2 RL**, RDFox, many KG rule engines (and of rule mining in [[KG Quality and Refinement]]).

## Two assumptions that confuse everyone
| | Closed world (CWA) | Open world (OWA) |
|---|---|---|
| Missing fact | False | Unknown |
| Used by | SQL, Cypher, **SHACL**, Datalog (negation as failure) | **OWL**, RDFS |
| "Every person has an email" + Alice has none | Violation | Infer Alice has *some* unknown email |

- **Unique Name Assumption (UNA):** OWL does *not* assume different IRIs denote different things → cardinality "violations" may cause *merging* instead of errors.

> [!warning] Practical consequence
> Use **OWL for inference**, **SHACL for validation**. See [[SHACL and ShEx]].

## Exercises
- [ ] Write the Datalog program for transitive closure and run it mentally on a 4-node chain.
- [ ] Give an example where OWA and CWA answers differ for the same query.

## Resources
- Brachman & Levesque, *Knowledge Representation and Reasoning*
- Baader et al., *An Introduction to Description Logic*, ch. 1

## My notes


## Self-test #flashcards/foundations
Define entailment K ⊨ φ.::φ holds in every model (interpretation satisfying all axioms) of K.
Why does KR use Description Logics instead of full FOL?::FOL entailment is undecidable; DLs are decidable fragments.
OWL uses which world assumption?::Open-world assumption (missing facts are unknown, not false).
Does OWL make the Unique Name Assumption?::No — different IRIs may denote the same individual unless declared different.
Which W3C language validates RDF under closed-world semantics?::SHACL
