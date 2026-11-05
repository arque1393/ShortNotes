---
tags: [meta, tracker]
start_date: YYYY-MM-DD
---
# 📈 Study Tracker

## Progress by phase (requires Dataview)
```dataview
TABLE phase AS "Phase", status AS "Status"
FROM ""
WHERE phase != null AND !contains(file.folder, "Templates")
SORT phase ASC, file.name ASC
```

## Notes still to start
```dataview
LIST
FROM ""
WHERE status = "not-started" AND !contains(file.folder, "Templates")
SORT phase ASC
```

## Phase checklist
- [ ] **Phase 0 – Calibration** (1–2 wks): implement BFS/DFS, Dijkstra, PageRank, spectral clustering from scratch
- [ ] **Phase 1 – Graph data & network science** (8–12 wks): Neo4j Certified Professional + [[P01 Dual-Model Graph]]
- [ ] **Phase 2 – Ontologies & KG construction** (10–14 wks): [[P02 Domain Ontology]] + [[P03 Text to KG Pipeline]]
- [ ] **Phase 3 – Graph ML** (10–14 wks): CS224W Colabs + [[P04 Fraud Graph Analytics]] + [[P05 KG Embedding Study]] + (optional) Neo4j GDS cert
- [ ] **Phase 4 – LLM + KG + Agents** (10–14 wks): [[P06 GraphRAG Bake-off]] + [[P07 Agent with Temporal KG Memory]] + [[P08 Text-to-Cypher Agent]]
- [ ] **Phase 5 – Research** (6–12+ months): choose niche from [[Open Problems]], reproduce 2–3 papers, [[P11 Research Project]], first workshop paper

## Weekly log
| Week | Dates | Notes studied | Project progress | Hours | Reflection |
|---|---|---|---|---|---|
| 1 | | | | | |
| 2 | | | | | |
| 3 | | | | | |
| 4 | | | | | |
