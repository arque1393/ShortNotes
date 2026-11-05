---
tags: [llm-kg, neuro-symbolic, reasoning]
phase: 4
status: not-started
---
# Neuro-Symbolic AI

> [!summary]
> Combine neural learning (robust, perceptual, fuzzy) with symbolic reasoning (exact, compositional, explainable). KGs + ontologies are the natural symbolic substrate for LLM systems.

## Integration patterns
| Pattern | Example |
|---|---|
| Symbolic knowledge → neural model | KG embeddings with ontology constraints; logic as loss (Logic Tensor Networks, semantic loss) |
| Neural → symbolic output | LLM generates SPARQL/Cypher/rules → executed exactly |
| Differentiable reasoning | Neural LP, DRUM (learn rules), NBFNet, DeepProbLog, Scallop |
| Neural proposes, symbolic verifies | LLM answer/triples checked by reasoner or SHACL; reject & retry |
| Symbolic plans, neural executes | Ontology-defined workflows guiding agents |
| Constrained decoding | Restrict LLM outputs to valid ontology terms / grammar |

## Why it matters now
Hallucination control, auditability in regulated domains, data efficiency, compositional generalisation.

## Reading
- Hitzler & Sarker (eds.), *Neuro-Symbolic Artificial Intelligence: The State of the Art*
- Garcez & Lamb, "Neurosymbolic AI: The 3rd Wave" (2020)

## My notes


## Self-test #flashcards/neuro-symbolic
What is the "neural proposes, symbolic verifies" pattern?::An LLM generates answers/facts which are checked by a reasoner, constraint validator or query execution before acceptance.
Name two differentiable rule-learning methods.::Neural LP and DRUM.
What is constrained decoding in KG contexts?::Restricting LLM generation to valid ontology terms or query grammar.
