---
title: "Experiment - <ID> - <short name>"
type: experiment
status: planned
created: "{{date}}"
project: null
research_question: null
hypothesis: null
code_commit: null
data_snapshot: null
ontology_version: null
seeds: []
tags:
  - experiment
---
# Experiment <ID> - <short name>

## Decision this experiment supports

What will be changed, selected or rejected based on the result?

## Research question

## Falsifiable hypothesis

> If ..., then ..., because ... . The hypothesis is rejected when ... .

## Variables

| Role | Variable | Operational definition |
|---|---|---|
| Independent | | |
| Dependent | | |
| Controlled | | |
| Confounders | | |

## Data contract

- **Source and license:**
- **Snapshot/checksum:**
- **Entity/fact grain:**
- **Construction pipeline version:**
- **Split unit and dates:**
- **Leakage risks:**
- **Exclusion criteria:**

## Semantic contract

- Ontology/schema version:
- Identity policy:
- Time semantics:
- Open/closed-world assumptions:
- Asserted/inferred/predicted separation:

## Baselines and treatments

| ID | Configuration | Why included |
|---|---|---|
| B0 | | simplest valid baseline |
| B1 | | strong conventional baseline |
| T1 | | proposed treatment |

## Metrics and acceptance criteria

| Metric | Direction | Minimum useful change | Slice/CI |
|---|---|---:|---|
| | higher/lower | | |

Include correctness, calibration, latency, cost and safety when relevant.

## Environment

```yaml
python: ""
frameworks: {}
hardware: ""
os: ""
container_image: ""
code_commit: ""
random_seeds: []
```

## Procedure

1.
2.
3.

## Pre-registered analysis

- Primary comparison:
- Statistical test/interval:
- Multiple-comparison treatment:
- Failure slices:
- Stop rule:

## Results

| Run | Seed | Primary metric | Cost/latency | Notes |
|---|---:|---:|---:|---|
| | | | | |

## Plots and artifacts

- Model/checkpoint:
- Query plans:
- Logs:
- Error samples:
- Figure links:

## Failure analysis

| Failure class | Count/rate | Example | Likely cause | Next test |
|---|---:|---|---|---|
| | | | | |

## Interpretation

- What the result supports:
- What it does not support:
- Alternative explanations:
- Generalization boundary:

## Reproducibility checklist

- [ ] Raw data is immutable and checksummed.
- [ ] Code commit and environment are pinned.
- [ ] Seeds and complete configuration are stored.
- [ ] Split generation is versioned.
- [ ] All baselines use comparable tuning budgets.
- [ ] Failed runs and exclusions are documented.
- [ ] Result tables are generated from raw logs.
- [ ] Privacy/license constraints are recorded.

## Decision and next action

**Decision:** adopt / reject / repeat / narrow claim  
**Why:**  
**Next experiment:**  
