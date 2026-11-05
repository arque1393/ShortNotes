---
tags: [llm-kg, agents, mcp]
phase: 4
status: not-started
---
# MCP and Graph Tools for Agents

> [!summary]
> The **Model Context Protocol** standardises how agents connect to tools and data. Graph DBs expose schema, query and memory operations as MCP tools so any MCP-capable agent can use the KG.

## MCP in 30 seconds
- **Host** (agent app) ↔ **client** ↔ **server** (wraps a system)
- Servers expose **tools** (callable functions), **resources** (readable data), **prompts** (templates)
- Transports: stdio (local), HTTP (remote)

## Graph MCP servers
- **Neo4j official** (`neo4j/mcp`): schema introspection, read-cypher, write-cypher, list GDS procedures
- **Neo4j Labs** (`neo4j-contrib/mcp-neo4j`): `mcp-neo4j-cypher`, `mcp-neo4j-memory`, `mcp-neo4j-data-modeling`, Aura manager
- Community servers for other graph/RDF stores; Google MCP Toolbox for Databases

## Tool design pattern for a KG agent
| Tool | Purpose | Guardrail |
|---|---|---|
| `get_schema` | Labels, rel types, properties | Cached, compact |
| `read_query` | Run read-only Cypher/SPARQL | Read-only tx, LIMIT, timeout, token cap on output |
| `search_entities` | Fuzzy/vector entity lookup | Top-k |
| `expand_neighbourhood` | k-hop around entity | Max nodes |
| `write_fact` | Add/update facts | **Human approval**, SHACL validation, provenance |

> [!warning] Security
> Tool outputs can carry **prompt injections** (malicious text stored in node properties). Treat graph content as untrusted data.

## My notes


## Self-test #flashcards/llm-kg
Three things an MCP server can expose?::Tools, resources, prompts.
Why gate write tools for KG agents?::To prevent incorrect/malicious writes — require approval, validation (SHACL) and provenance.
Security risk specific to graph-backed agents?::Prompt injection via text stored in the graph and returned by tools.
