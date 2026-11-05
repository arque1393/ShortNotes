---
tags: [gds, algorithms]
phase: 1
status: not-started
---
# Path Finding & Similarity

> [!summary]
> Paths answer "how is X connected to Y?" (logistics, explanation paths in KGs). Similarity answers "what is like X?" (recommendation, entity resolution, kNN graphs).

## Path finding
| Algorithm | Use |
|---|---|
| BFS | Unweighted shortest path, k-hop expansion (GraphRAG subgraph retrieval) |
| Dijkstra | Non-negative weights |
| A* | Dijkstra + admissible heuristic (geo routing) |
| Bellman–Ford | Negative weights, detects negative cycles |
| Yen's k-shortest | Alternatives; multiple explanation paths |
| Floyd–Warshall | All-pairs, $O(V^3)$ |
| MST (Prim/Kruskal) | Network design, clustering |
| Random walks | Sampling, node2vec, explanation |

```cypher
// Cypher shortest path (Neo4j 5 syntax also supports SHORTEST k)
MATCH (a:Person {name:'Alice'}), (b:Person {name:'Bob'})
MATCH p = shortestPath((a)-[:KNOWS*..6]-(b))
RETURN p;
```

## Similarity
| Measure | Formula | Use |
|---|---|---|
| Jaccard | $\frac{|N(x)\cap N(y)|}{|N(x)\cup N(y)|}$ | Neighbourhood overlap |
| Overlap | $\frac{|N(x)\cap N(y)|}{\min(|N(x)|,|N(y)|)}$ | Subset detection, taxonomy inference |
| Cosine | on vectors/embeddings | Embedding similarity |
| SimRank | "similar if neighbours similar" | Recursive structural similarity |
| kNN | Build similarity graph from embeddings | Recommendations, ER |

```cypher
CALL gds.nodeSimilarity.stream('purchases')
YIELD node1, node2, similarity
RETURN gds.util.asNode(node1).name, gds.util.asNode(node2).name, similarity
ORDER BY similarity DESC LIMIT 20;
```

## My notes


## Self-test #flashcards/gds
When to use Yen's algorithm?::When you need the k shortest (alternative) paths, not just one.
Why can't Dijkstra handle negative weights?::It finalises nodes greedily; a later negative edge could reduce an already-finalised distance.
Jaccard similarity of node neighbourhoods?::|N(x) ∩ N(y)| / |N(x) ∪ N(y)|
What does A* add to Dijkstra?::An admissible heuristic estimating distance to the goal.
