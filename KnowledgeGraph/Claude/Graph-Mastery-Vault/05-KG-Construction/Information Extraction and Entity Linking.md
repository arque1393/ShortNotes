---
tags: [kg-construction, nlp]
phase: 2
status: not-started
---
# Information Extraction & Entity Linking

> [!summary]
> Classic text→KG = **NER** (find mentions) → **coreference** → **relation extraction** (find facts) → **entity linking** (attach to KG IDs). LLMs now do much of this jointly, but the decomposition is still how you debug and evaluate.

## Subtasks
| Task | Input → Output | Methods | Benchmarks |
|---|---|---|---|
| NER | text → typed spans | CRF → BiLSTM-CRF → transformers; zero-shot **GLiNER** | CoNLL-2003, OntoNotes |
| Coreference | mentions → clusters | span-based neural models | OntoNotes |
| Relation extraction | (text, e1, e2) → relation | supervised, **distant supervision**, document-level, generative (REBEL) | TACRED, DocRED |
| Open IE | text → (arg, rel, arg) strings | OpenIE, LLM prompting | — (used by HippoRAG) |
| Entity linking | mention → KG entity | candidate generation (alias tables) + disambiguation (BLINK, ReFinED) | AIDA-CoNLL |
| Event extraction | triggers + arguments | | ACE |

## Distant supervision
If KG has `(Paris, capitalOf, France)`, label every sentence mentioning both as expressing `capitalOf` → noisy but scalable; mitigated by multi-instance learning.

## Entity linking pipeline
1. Mention detection
2. Candidate generation (alias dictionary from SKOS `altLabel`, Wikidata aliases, fuzzy match)
3. Disambiguation (context embedding similarity + prior popularity + coherence with other entities)
4. NIL detection (entity not in KG → create new)

```python
import spacy
nlp = spacy.load("en_core_web_sm")
doc = nlp("Marie Curie worked at the University of Paris.")
print([(e.text, e.label_) for e in doc.ents])
```

## My notes


## Self-test #flashcards/kg-construction
What is distant supervision?::Automatically labelling sentences with a relation if they mention an entity pair that the KG already links with that relation.
Steps of entity linking?::Mention detection, candidate generation, disambiguation, NIL detection.
What is GLiNER?::A compact zero-shot NER model that extracts arbitrary entity types given as labels.
Open IE outputs what?::Schema-free (argument, relation phrase, argument) string triples.
