---
tags: [llm-kg, text-to-query]
phase: 4
status: not-started
---
# Text-to-Cypher & Text-to-SPARQL

> [!summary]
> Translate natural-language questions into graph queries. Gives **exact, aggregate, verifiable** answers that vector RAG can't (counts, filters, paths).

## Robust pipeline
1. **Schema extraction** — labels, relationship types, properties, sample values (compact form!)
2. **Schema linking** — which labels/properties does the question mention? Use embeddings + value indexes
3. **Few-shot retrieval** — fetch similar (question, query) pairs from an exemplar store
4. **Generation** — LLM writes the query (temperature 0)
5. **Validation** — syntax check (`EXPLAIN` in Neo4j), schema check (labels exist? direction correct?)
6. **Execution** with safety limits
7. **Self-correction** — on error/empty result, feed error back (max 2–3 retries)
8. **Answer synthesis** from results + show the query

## Safety
> [!warning]
> - Read-only DB user/transaction; block `CREATE/MERGE/DELETE/SET/CALL apoc.*` unless explicitly allowed
> - Always add `LIMIT`, set timeouts
> - Prompt-injection through data values is possible

## Metrics & data
Execution accuracy (results match gold), exact/structural match, validity rate, latency. Datasets: Neo4j Text2Cypher dataset, LC-QuAD 2.0, QALD-9/10, Spider-style adaptations.

## Ontology-constrained variant (research-y)
Use ontology/SHACL to constrain allowed patterns (domain/range) and reject impossible queries before execution.

## My notes


## Self-test #flashcards/llm-kg
Most important accuracy metric for text-to-query?::Execution accuracy — whether executed results match the gold answer.
How can you syntax-check Cypher without running it?::Prefix the query with EXPLAIN.
Name three safety measures for LLM-generated queries.::Read-only access, enforced LIMIT/timeouts, blocking write/admin procedures.
What is schema linking?::Identifying which schema elements (labels, relations, properties, values) a question refers to.
