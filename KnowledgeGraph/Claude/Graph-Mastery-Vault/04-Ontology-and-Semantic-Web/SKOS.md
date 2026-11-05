---
tags: [ontology, skos, taxonomy]
phase: 2
status: not-started
---
# SKOS — Simple Knowledge Organization System

> [!summary]
> SKOS represents **taxonomies, thesauri and controlled vocabularies**. Most enterprise "ontologies" are really SKOS concept schemes — and that's fine.

## Core vocabulary
- `skos:ConceptScheme`, `skos:Concept`, `skos:inScheme`, `skos:hasTopConcept`
- Labels: `skos:prefLabel` (one per language), `skos:altLabel` (synonyms), `skos:hiddenLabel` (misspellings)
- Hierarchy: `skos:broader`, `skos:narrower` (and `broaderTransitive`)
- Association: `skos:related`
- Mapping across schemes: `skos:exactMatch`, `skos:closeMatch`, `skos:broadMatch`, `skos:narrowMatch`
- Documentation: `skos:definition`, `skos:scopeNote`, `skos:notation`

```turtle
ex:MachineLearning a skos:Concept ;
    skos:prefLabel "Machine learning"@en ;
    skos:altLabel "ML"@en ;
    skos:broader ex:ArtificialIntelligence ;
    skos:related ex:Statistics ;
    skos:exactMatch <http://www.wikidata.org/entity/Q2539> .
```

## SKOS vs OWL
| | SKOS | OWL |
|---|---|---|
| broader / subClassOf | Loose "is narrower than" (no inheritance semantics) | Strict set inclusion |
| Purpose | Navigation, tagging, search, synonyms | Logical definition & inference |
| Effort | Low | High |

> [!tip] Practical use
> SKOS `altLabel`s are gold for **entity linking** and **GraphRAG keyword expansion**; `exactMatch` links your vocabulary to Wikidata.

## My notes


## Self-test #flashcards/ontology
Is skos:broader the same as rdfs:subClassOf?::No — broader is an informal hierarchical relation without set-inclusion semantics.
SKOS property for synonyms?::skos:altLabel
SKOS property to align concepts across schemes as equivalent?::skos:exactMatch
