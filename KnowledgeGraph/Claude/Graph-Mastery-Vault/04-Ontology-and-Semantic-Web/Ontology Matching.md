---
tags: [ontology, alignment]
phase: 2
status: not-started
---
# Ontology Matching (Alignment)

> [!summary]
> Find correspondences (≡, ⊑, ⊒) between entities of two ontologies/KGs. Essential for integrating sources; benchmarked yearly by **OAEI**.

## Matcher types
- **Lexical:** label/synonym similarity, normalisation (LogMap, AML start here)
- **Structural:** neighbours, hierarchy propagation
- **Logical repair:** remove mappings that cause incoherence (LogMap's strength)
- **Embedding/LM-based:** BERTMap (fine-tuned BERT on synonyms), OWL2Vec*
- **LLM-based:** candidate retrieval + LLM verification (2023+)
- **Instance-based:** shared instances imply class correspondence

## Pipeline
candidate generation (blocking) → scoring → selection (1:1 constraints, thresholds) → logical repair → human validation

## Evaluation
Precision, recall, F1 against reference alignments; OAEI tracks (anatomy, biomedical/Bio-ML, conference, knowledge graph track).

## Connection
Same structure as [[Entity Resolution]], but at schema level.

## My notes


## Self-test #flashcards/ontology
What is OAEI?::Ontology Alignment Evaluation Initiative — annual matching benchmark campaign (with ISWC's OM workshop).
What does logical repair do in ontology matching?::Removes mappings that make the merged ontology incoherent/inconsistent.
Name an LM-based ontology matcher.::BERTMap
