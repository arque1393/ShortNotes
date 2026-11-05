---
title: "KG Construction from Text and Multimodal Data"
type: chapter
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - information-extraction
  - nlp
  - multimodal
  - knowledge-graph
  - llm
---
# KG Construction from Text and Multimodal Data

> [!goal]
> Convert unstructured evidence into calibrated, provenance-preserving candidate knowledge rather than treating model output as truth.

## 1. The extraction stack

```mermaid
flowchart LR
    S[Documents, audio, images] --> A[Acquisition and parsing]
    A --> C[Chunking and structure recovery]
    C --> M[Mention and event extraction]
    M --> L[Entity linking and normalization]
    L --> R[Relation and attribute extraction]
    R --> F[Coreference and temporal resolution]
    F --> V[Validation and confidence]
    V --> H[Human review / active learning]
    H --> K[Publish to KG]
```

Each stage creates uncertainty. Store intermediate evidence so errors can be localized.

## 2. Document understanding before extraction

Recover:

- document identity and version;
- headings, paragraphs, tables, lists and footnotes;
- reading order;
- page/region coordinates;
- language and encoding;
- OCR confidence;
- references and citations;
- access and license metadata.

Poor parsing can dominate downstream errors. For tables, preserve row/column headers and merged-cell context. For scanned material, route low-confidence regions for review.

## 3. Define the extraction schema

Begin from competency questions and ontology terms. For every target:

- definition and examples;
- exclusion rules;
- required evidence span;
- normalization rule;
- allowed relation arguments;
- temporal and negation handling;
- confidence and review threshold.

Do not ask an LLM to "extract all entities and relationships." It produces an unstable, unbounded schema.

## 4. Mentions are not entities

Text span `Stellantis`, an organization entity, a specific legal entity, and a stock ticker are different layers.

Maintain:

- mention: location in a source;
- candidate entity/type;
- linked canonical entity;
- linking score and alternatives;
- evidence and decision provenance.

Entity linking combines candidate generation and candidate ranking. Signals include aliases, context, type constraints, temporal validity and graph neighborhood.

## 5. Relation and event extraction

### Relation extraction

Predict a typed relation between arguments in a context. It may be sentence-level, document-level or cross-document.

### Event extraction

Identify an event trigger/type, participants, roles, time, location, quantities and modality. Events are usually superior when a relationship has time, multiple participants or evidence.

Example:

```text
ProgramActivation
  program: IncentiveProgram
  appliesTo: VehicleModel
  region: Market
  validFrom: Date
  validTo: Date
  sourceStatement: EvidenceSpan
```

## 6. Difficult linguistic phenomena

- negation: "Dealer A did not join";
- uncertainty: "may qualify";
- modality/obligation: "must submit";
- condition: "eligible if...";
- attribution: "according to the regional manager";
- coreference: "it", "the program", "the latter";
- temporality: "formerly", "from next quarter";
- quantifier scope;
- conflicting sources;
- hypothetical examples.

Model epistemic status. A claim mentioned in text is not automatically an asserted world fact.

## 7. LLM-based extraction

LLMs are useful for schema-constrained extraction, weak supervision, labeling assistance and difficult long-context relations. Robust patterns:

1. provide exact ontology definitions and counterexamples;
2. require structured output with schema validation;
3. require evidence spans/coordinates;
4. separate extraction from entity resolution;
5. validate types, cardinalities and constraints;
6. run deterministic normalization;
7. calibrate confidence empirically;
8. send uncertain/high-impact cases to review.

```json
{
  "claim_type": "ProgramAppliesToModel",
  "subject_mention": "Q4 Retail Bonus",
  "object_mention": "Model X",
  "valid_from": "2026-10-01",
  "evidence": {"document_id": "doc-17", "start": 410, "end": 468},
  "negated": false,
  "model_confidence": 0.83
}
```

Model self-reported confidence is not calibrated probability. Calibrate against labeled validation data using reliability diagrams, Brier score or expected calibration error.

## 8. Weak supervision and active learning

Combine noisy labeling functions:

- dictionaries and regex;
- ontology/type constraints;
- dependency patterns;
- distant supervision from an existing KG;
- LLM labels;
- source metadata.

Active learning selects examples whose annotation is most valuable: uncertainty, disagreement, diversity, rare types or high business impact. Avoid repeatedly sampling only ambiguous noise.

## 9. Multimodal construction

For images/video/audio, distinguish observed media artifacts from interpreted domain entities.

- OCR and layout regions;
- object detection/segmentation;
- visual relation extraction;
- speech recognition and speaker diarization;
- timestamped events;
- cross-modal entity linking;
- geospatial and sensor alignment.

Store region/time coordinates as evidence. A model's interpretation should be a claim with provenance, confidence and version.

## 10. Evaluation

Measure each stage and end-to-end utility:

| Task | Metrics | Important caveat |
|---|---|---|
| NER/mention extraction | precision, recall, F1, exact/partial span | micro scores hide rare classes |
| Entity linking | accuracy, MRR, recall@k, NIL detection | prevent train-test entity leakage |
| Relation extraction | per-class P/R/F1, PR-AUC | evaluate negative sampling |
| Event extraction | trigger and argument F1 | score role and temporal correctness |
| Calibration | ECE, Brier score | test by source/class |
| KG utility | competency answer accuracy, provenance coverage | downstream errors can cancel or compound |

Use document-level splits when near-duplicate documents exist. Create adversarial sets for negation, temporal conditions and alias collisions.

## 11. Publication policy

Use states such as:

- `candidate`;
- `machine-accepted`;
- `human-verified`;
- `contested`;
- `superseded`;
- `retracted`.

Thresholds should depend on consequence. A low-risk search hint and a compliance assertion should not share the same acceptance rule.

## 12. Laboratory

Build a pipeline over 500 domain documents containing prose and tables:

- annotated gold set of at least 100 documents;
- schema-constrained extraction;
- canonical linking;
- event/temporal normalization;
- evidence-level provenance;
- SHACL validation;
- human review queue;
- stage-wise and end-to-end evaluation;
- error taxonomy with the top ten failure modes.

Compare a classical/encoder baseline, an LLM extractor and a hybrid. Report cost and latency as well as accuracy.

## Mastery checklist

- [ ] I distinguish mentions, entities, claims and world facts.
- [ ] Every extracted claim has source-level evidence.
- [ ] I handle negation, attribution, modality and time.
- [ ] Confidence is calibrated on held-out data.
- [ ] I evaluate rare classes and end-to-end KG utility.

## Next reading

- [[17_Entity_Resolution_and_Knowledge_Fusion]]
- [[18_KG_Quality_Governance_and_Evolution]]
- [[29_Knowledge_Graph_and_LLM_Integration]]
- [Knowledge Graphs book, extraction chapters](https://kgbook.org/)
