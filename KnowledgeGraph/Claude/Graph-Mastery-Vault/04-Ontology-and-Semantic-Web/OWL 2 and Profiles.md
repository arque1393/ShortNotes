---
tags: [ontology, owl, semantic-web]
phase: 2
status: not-started
---
# OWL 2 and its Profiles

> [!summary]
> OWL 2 is the W3C ontology language with formal (DL) semantics. Use it to **infer** new knowledge. Pick a **profile** (EL/QL/RL) for tractability.

## Main constructs
- **Classes:** `owl:Class`, `rdfs:subClassOf`, `owl:equivalentClass`, `owl:disjointWith`, `owl:unionOf`, `owl:intersectionOf`, `owl:complementOf`
- **Restrictions:** `owl:someValuesFrom` (∃), `owl:allValuesFrom` (∀), `owl:hasValue`, cardinalities (`owl:minQualifiedCardinality` …)
- **Properties:** object vs datatype; `owl:TransitiveProperty`, `owl:SymmetricProperty`, `owl:FunctionalProperty`, `owl:inverseOf`, `owl:propertyChainAxiom` (e.g., hasParent ∘ hasBrother ⊑ hasUncle)
- **Individuals:** `owl:sameAs`, `owl:differentFrom`, `owl:NamedIndividual`

## Example (Manchester syntax, as in Protégé)
```
Class: VegetarianPizza
    EquivalentTo: Pizza and (hasTopping only VegetarianTopping)

ObjectProperty: hasUncle
    SubPropertyChain: hasParent o hasBrother
```
Same in Turtle:
```turtle
:VegetarianPizza owl:equivalentClass [
    a owl:Class ;
    owl:intersectionOf ( :Pizza
        [ a owl:Restriction ; owl:onProperty :hasTopping ; owl:allValuesFrom :VegetarianTopping ] ) ] .
```

## Profiles
| Profile | Designed for | Reasoning | Engines |
|---|---|---|---|
| **OWL 2 EL** | Huge class hierarchies (biomedicine) | Polynomial classification | ELK, Snorocket |
| **OWL 2 QL** | Ontology-based data access over relational DBs | Query rewriting to SQL (AC⁰ data complexity) | Ontop |
| **OWL 2 RL** | Rule-based materialisation over triple stores | Polynomial, rules | RDFox, GraphDB, Jena rules |
| OWL 2 DL | Full expressivity | N2EXPTIME | HermiT, Pellet, Konclude |

## Classic pitfalls
> [!warning]
> - **Domain/range infer, not check.** Adding `ex:worksFor rdfs:domain ex:Employee` makes every subject an Employee.
> - **OWA:** missing cardinality facts never cause errors.
> - **No UNA:** `maxCardinality 1` + two values ⇒ the two values are inferred to be the *same* individual.
> - `owl:sameAs` abuse in linked data merges things that are only similar.
> - "only" (∀) is trivially satisfied when there are no values — usually pair with "some".

## My notes


## Self-test #flashcards/ontology
Which OWL profile is designed for query rewriting over relational databases?::OWL 2 QL (e.g., Ontop).
Which OWL profile maps to rule-based materialisation?::OWL 2 RL.
What happens in OWL if a functional property has two different values?::The two values are inferred to be the same individual (no UNA), unless declared different → then inconsistency.
What is a property chain axiom?::A rule that a composition of properties implies another, e.g. hasParent ∘ hasBrother ⊑ hasUncle.
Why pair "only" restrictions with "some"?::∀ is vacuously true when no values exist; ∃ ensures at least one.
