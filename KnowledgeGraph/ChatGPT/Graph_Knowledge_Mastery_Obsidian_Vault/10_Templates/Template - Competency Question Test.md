---
title: "CQ Test - <CQ-ID> - <short name>"
type: competency-question-test
status: draft
created: "{{date}}"
ontology_version: null
data_fixture: null
tags:
  - ontology-test
  - competency-question
---
# CQ Test <CQ-ID> - <short name>

## Natural-language question

## Intended interpretation

Define terms, time window, scope, identity and closure assumptions.

## Expected answer form

- type: boolean / entity / list / path / aggregate / explanation
- grain:
- ordering:
- units:
- empty-result meaning:

## Given fixture

```text
<minimal facts and axioms>
```

## Query

```sparql
# or Cypher/GQL
```

## Expected result

```text
<exact rows/graph/boolean>
```

## Negative and boundary cases

| Case | Change | Expected behavior |
|---|---|---|
| Missing assertion | | unknown / absent under local closure |
| Conflicting source | | |
| Boundary date | | |
| Duplicate input | | |
| Inferred type only | | |

## Provenance expectation

Which source/evidence/inference trace must accompany the answer?

## Test status

- [ ] query executes;
- [ ] expected answer matches;
- [ ] result survives ontology refactor;
- [ ] no unintended answers;
- [ ] performance within budget.
