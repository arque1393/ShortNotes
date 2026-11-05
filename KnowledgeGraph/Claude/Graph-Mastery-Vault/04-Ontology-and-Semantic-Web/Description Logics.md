---
tags: [ontology, logic, dl]
phase: 2
status: not-started
---
# Description Logics (DL)

> [!summary]
> DLs are decidable fragments of first-order logic about **concepts** (classes), **roles** (properties) and **individuals**. OWL 2 DL ≈ the DL **SROIQ(D)**.

## ALC — the base language
| Syntax | Meaning | FOL |
|---|---|---|
| $C \sqcap D$ | intersection | $C(x)\land D(x)$ |
| $C \sqcup D$ | union | $C(x)\lor D(x)$ |
| $\neg C$ | complement | $\neg C(x)$ |
| $\exists r.C$ | some r-successor is C | $\exists y\,(r(x,y)\land C(y))$ |
| $\forall r.C$ | all r-successors are C | $\forall y\,(r(x,y)\to C(y))$ |

**Knowledge base** $\mathcal{K} = (\mathcal{T}, \mathcal{A})$:
- **TBox** (schema): $\mathit{Parent} \equiv \mathit{Person} \sqcap \exists \mathit{hasChild}.\mathit{Person}$
- **ABox** (facts): $\mathit{Person}(\mathit{alice})$, $\mathit{hasChild}(\mathit{alice},\mathit{bob})$

## Naming the extensions
- **S** = ALC + transitive roles · **H** role hierarchy · **O** nominals · **I** inverse roles · **N/Q** (qualified) number restrictions · **R** complex role inclusions (property chains) · **(D)** datatypes
- OWL 1 DL ≈ SHOIN(D); **OWL 2 DL ≈ SROIQ(D)**; OWL 2 EL ≈ $\mathcal{EL}^{++}$ (only $\sqcap$, $\exists$, ⊤)

## Reasoning services
1. **Concept satisfiability** — can C have instances?
2. **Subsumption** $\mathcal{T}\models C\sqsubseteq D$ → **classification** (compute full hierarchy)
3. **KB consistency**
4. **Instance checking / query answering**

All reduce to (un)satisfiability → **tableau algorithms** (build a model; clash = unsatisfiable). EL uses polynomial *consequence-based* saturation (ELK).

## Complexity (for intuition)
- $\mathcal{EL}$: polynomial (why SNOMED CT with ~350k concepts classifies in seconds)
- ALC with general TBox: EXPTIME-complete
- SROIQ: N2EXPTIME-complete (but fine in practice for many ontologies)

## Worked example
TBox: $\mathit{Parent}\equiv \mathit{Person}\sqcap\exists \mathit{hasChild}.\top$; ABox: $\mathit{Person}(a)$, $\mathit{hasChild}(a,b)$ ⇒ reasoner infers $\mathit{Parent}(a)$.

## Exercises
- [ ] Translate 5 English sentences about your domain into DL axioms.
- [ ] Run HermiT in Protégé; find one *unsatisfiable class* you created on purpose and read the explanation.

## My notes


## Self-test #flashcards/ontology
OWL 2 DL corresponds to which DL?::SROIQ(D)
What is the difference between TBox and ABox?::TBox holds terminological/schema axioms; ABox holds assertions about individuals.
Which DL family gives polynomial reasoning used for SNOMED CT?::EL (EL++), the basis of OWL 2 EL.
What is classification in DL reasoning?::Computing the complete subsumption hierarchy of all named classes.
Which algorithm family do OWL 2 DL reasoners like HermiT use?::Tableau (HermiT uses hypertableau).
Meaning of ∀r.C?::All r-successors (if any) are instances of C.
