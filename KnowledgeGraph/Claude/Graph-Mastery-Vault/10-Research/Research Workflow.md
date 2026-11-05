---
tags: [research, workflow]
phase: 5
status: not-started
---
# Research Workflow

## 1. Reading papers — three passes (Keshav)
1. **5–10 min:** title, abstract, intro, headings, figures, conclusion → category, contribution, relevance
2. **~1 h:** method & experiments; note baselines, datasets, numbers, who evaluated
3. **Deep:** re-derive, find assumptions, imagine reproducing it → research ideas
Use [[Template - Paper Note]] for every paper; link to concept notes.

## 2. Finding a gap
- Read the "Limitations / Future work" sections
- Check what is **self-reported** and on **small benchmarks** (common in GraphRAG/memory)
- Reproduce → the gap between claimed and reproduced behaviour is publishable
- Combine two areas (e.g., temporal KGs × agent memory; SHACL × LLM extraction)

## 3. Reproduction protocol
- [ ] Fix seeds; log configs (Hydra), track runs (W&B/MLflow)
- [ ] Re-run official code before modifying
- [ ] Record compute and cost
- [ ] Keep a running "surprises" log

## 4. Writing
Structure: problem → why existing methods fail → idea → evidence → limitations. Write the intro first; make one figure that explains the idea.

## 5. Publishing path
Workshop / challenge (LLMs4OL, OAEI, OGB-LSC, TGB) → resource paper (ISWC/ESWC resource track, TGDK) → main track.

## 6. Weekly research rhythm
- 3 papers deep-read
- 1 reproduction step
- 1 page written
- 1 public artifact (blog, code, thread)
