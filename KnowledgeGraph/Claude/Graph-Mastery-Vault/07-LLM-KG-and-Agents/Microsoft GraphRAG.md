---
tags: [llm-kg, graphrag, microsoft]
phase: 4
status: not-started
---
# Microsoft GraphRAG

> [!summary]
> Edge et al. (arXiv 2404.16130): LLM-extract an entity graph from documents → **hierarchical Leiden communities** → LLM-written **community reports** → answer global questions by map-reduce over reports.

## Indexing
1. Chunk documents (text units)
2. LLM extracts **entities, relationships, (optional) claims** with descriptions
3. Merge/summarise duplicate entity descriptions
4. **Hierarchical Leiden** → multi-level communities ([[Community Detection]])
5. LLM writes **community reports** per community and level
6. Embed entities, text units, reports

## Query modes
| Mode | For | How |
|---|---|---|
| **Local search** | Entity-specific questions | Entity linking → neighbours, relationships, text units, related reports |
| **Global search** | "Main themes?" sensemaking | Map: each community report → partial answer with score; Reduce: combine top partials |
| **DRIFT search** (Oct 2024) | Mix | Starts from community-level context, then follows up with local queries |
| **LazyGraphRAG** (Nov 2024) | Low cost | Defers LLM summarisation to query time; noun-phrase graph; indexing cost ≈ vector RAG (0.1% of full GraphRAG, per Microsoft) |

## CLI sketch (check current docs — versions move fast; v3.x in 2026)
```bash
pip install graphrag
graphrag init --root ./ragtest          # creates settings.yaml + prompts
# put .txt files in ./ragtest/input, set API key in .env
graphrag index --root ./ragtest
graphrag query --root ./ragtest --method global --query "What are the main themes?"
graphrag query --root ./ragtest --method local  --query "Who is X connected to?"
```

## Strengths / weaknesses
- ✅ Global sensemaking, corpus-level summaries, explainable structure
- ❌ Expensive indexing, prompt-tuning needed per domain, updates were costly (incremental `update` now exists), evaluation in the paper used LLM-judged comprehensiveness/diversity — be critical ([[Evaluating GraphRAG]]).

## My notes


## Self-test #flashcards/llm-kg
How does Microsoft GraphRAG answer global questions?::Map-reduce over LLM-generated community reports from hierarchical Leiden communities.
What is DRIFT search?::A hybrid mode starting from community-level context, then refining with local follow-up queries.
LazyGraphRAG's key cost idea?::Defer LLM summarisation to query time, making indexing about as cheap as vector RAG.
Main weakness of GraphRAG indexing?::High LLM cost (entity/relation extraction and community reports for the entire corpus).
