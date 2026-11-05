---
title: "Current Standards Status - 2026"
type: reference
status: ready
edition: "1.0"
updated: 2026-11-05
tags:
  - standards
  - rdf
  - sparql
  - owl
  - shacl
  - gql
---
# Current Standards Status - 2026

> [!warning] Dated reference
> This status matrix is current to **5 November 2026**. Standards and drafts change. Before a production decision, open the linked official status page and check the exact implementation conformance of every participating tool.

## 1. Deployment rule

Use three labels in architecture decisions:

- **Stable baseline**: a published Recommendation or International Standard with broad enough implementation support for your environment.
- **Candidate/advanced draft**: mature enough for implementation experience, but not yet a final Recommendation.
- **Working draft**: active work that may change, be replaced or be removed.

A specification status is not the same as product support. A final standard can be incompletely implemented; a draft feature can be implemented by several products but remain unstable.

## 2. Stable semantic-web baseline

| Area | Stable specification | Formal status/date | Production guidance |
|---|---|---|---|
| RDF data model | [RDF 1.1 Concepts](https://www.w3.org/TR/rdf11-concepts/) | W3C Recommendation, 25 Feb 2014 | Safest cross-vendor RDF baseline unless all systems explicitly support RDF 1.2 features. |
| RDF semantics | [RDF 1.1 Semantics](https://www.w3.org/TR/rdf11-mt/) | W3C Recommendation, 25 Feb 2014 | State the entailment regime; most stores do not apply every regime by default. |
| RDF Schema | [RDF Schema 1.1](https://www.w3.org/TR/rdf-schema/) | W3C Recommendation, 25 Feb 2014 | Use for classes, properties, subclass/subproperty and domain/range entailment. |
| Turtle | [RDF 1.1 Turtle](https://www.w3.org/TR/turtle/) | W3C Recommendation, 25 Feb 2014 | Human-readable source format; test parser edge cases and base IRI behavior. |
| TriG | [RDF 1.1 TriG](https://www.w3.org/TR/trig/) | W3C Recommendation, 25 Feb 2014 | RDF dataset serialization with named graphs. |
| N-Triples/N-Quads | [N-Triples](https://www.w3.org/TR/n-triples/), [N-Quads](https://www.w3.org/TR/n-quads/) | W3C Recommendations, 25 Feb 2014 | Useful for streaming, diffs and canonical processing; verbose. |
| RDF/XML | [RDF 1.1 XML Syntax](https://www.w3.org/TR/rdf-syntax-grammar/) | W3C Recommendation, 25 Feb 2014 | Maintain for interoperability where required; avoid as the teaching format. |
| JSON-LD | [JSON-LD 1.1](https://www.w3.org/TR/json-ld11/) | W3C Recommendation, 16 Jul 2020 | Strong Web/API serialization; contexts are semantic contracts, not cosmetic aliases. |
| Query | [SPARQL 1.1 Query](https://www.w3.org/TR/sparql11-query/) | W3C Recommendation, 21 Mar 2013 | Stable query baseline; verify vendor extensions separately. |
| Update | [SPARQL 1.1 Update](https://www.w3.org/TR/sparql11-update/) | W3C Recommendation, 21 Mar 2013 | Restrict update privileges; define transaction and dataset behavior per product. |
| Protocol/federation | [SPARQL 1.1 Protocol](https://www.w3.org/TR/sparql11-protocol/), [Federated Query](https://www.w3.org/TR/sparql11-federated-query/) | W3C Recommendations, 21 Mar 2013 | Federation is operationally fragile; enforce timeouts, source trust and result limits. |
| Ontology | [OWL 2, Second Edition](https://www.w3.org/TR/owl2-overview/) | W3C Recommendation, 11 Dec 2012 | Select an OWL profile and reasoner based on competency questions and scale. |
| Shapes | [SHACL 1.0](https://www.w3.org/TR/shacl/) | W3C Recommendation, 20 Jul 2017 | Stable validation baseline. Document recursion, entailment and SHACL-SPARQL support. |
| Taxonomies/thesauri | [SKOS](https://www.w3.org/TR/skos-reference/) | W3C Recommendation, 18 Aug 2009 | Use for concept schemes, labels and mappings; do not treat every broader link as a strict subclass axiom. |
| Provenance | [PROV-O](https://www.w3.org/TR/prov-o/) | W3C Recommendation, 30 Apr 2013 | Reuse core entity/activity/agent patterns, then add domain-specific evidence detail. |
| Time | [OWL-Time](https://www.w3.org/TR/owl-time/) | W3C Recommendation, 19 Oct 2017; later candidate work exists | Pin the profile/version you use, especially if relying on post-2017 additions. |

## 3. RDF 1.2 status

### 3.1 What is mature

[RDF 1.2 Concepts and Abstract Data Model](https://www.w3.org/TR/rdf12-concepts/) was published as a **Candidate Recommendation Snapshot on 7 April 2026**. It adds, among other changes:

- RDF triple terms, enabling a triple to be used as a term in another triple's object position;
- directional language-tagged strings;
- mechanisms supporting version transition and updated terminology.

[RDF 1.2 Semantics](https://www.w3.org/TR/rdf12-semantics/) had a Candidate Recommendation Snapshot on 7 April 2026 and a newer Candidate Recommendation Draft dated 24 September 2026.

### 3.2 What remained draft-track on 5 November 2026

The W3C standards index showed current Working Drafts for several RDF 1.2 serializations and related documents, including:

- [RDF 1.2 Turtle](https://www.w3.org/TR/rdf12-turtle/) - Working Draft dated 1 Nov 2026;
- [RDF 1.2 N-Triples](https://www.w3.org/TR/rdf12-n-triples/) - Working Draft dated 23 Oct 2026;
- [RDF 1.2 N-Quads](https://www.w3.org/TR/rdf12-n-quads/) - Working Draft dated 23 Oct 2026;
- [RDF 1.2 TriG](https://www.w3.org/TR/rdf12-trig/) - Working Draft dated 23 Oct 2026;
- [RDF 1.2 Schema](https://www.w3.org/TR/rdf12-schema/) - Working Draft dated 23 Oct 2026;
- [RDF 1.2 XML Syntax](https://www.w3.org/TR/rdf12-xml/) - Working Draft dated 25 Oct 2026.

### 3.3 Adoption rule

Use RDF 1.2 features only when:

1. every parser, store, serializer, validator and downstream consumer in the path is tested;
2. round-trip tests preserve triple terms and directional language tags;
3. fallback/translation behavior is defined for RDF 1.1 consumers;
4. the chosen feature materially simplifies provenance or statement modeling;
5. draft syntax is isolated behind a compatibility boundary.

Do not equate RDF 1.2 triple terms with a complete provenance model. You still need identity, source, time, evidence and trust semantics.

## 4. SPARQL 1.2 status

[SPARQL 1.2 Query Language](https://www.w3.org/TR/sparql12-query/) was a **W3C Working Draft dated 1 November 2026**. Other SPARQL 1.2 documents, including update, protocol, service description, results formats and entailment work, also remained on the draft track.

Production rule:

- write portable core queries to SPARQL 1.1 unless the deployment is intentionally tied to a tested SPARQL 1.2 implementation;
- place draft-specific queries in conformance tests;
- do not infer feature support from a product saying "SPARQL compatible";
- test unbound/error behavior, paths, datasets, RDF 1.2 terms and update semantics.

## 5. SHACL 1.2 status

[SHACL 1.2 Core](https://www.w3.org/TR/shacl12-core/) was a **W3C Working Draft dated 2 November 2026**. The status text explicitly describes it as work in progress rather than an endorsed Recommendation.

Related draft work includes SHACL 1.2 SPARQL extensions, rules, node expressions and UI-oriented material. Exact document names/status can change as the family evolves.

Production rule:

- treat SHACL 1.0 Core as the portable baseline;
- pin the validator and record which advanced features it implements;
- avoid assuming identical recursion, entailment or report behavior across engines;
- run a shared conformance fixture against every validator used in CI or runtime;
- distinguish normative constraints from UI/code-generation annotations.

## 6. OWL 2 status

OWL 2 Second Edition remains the stable W3C Recommendation family. The key documents are:

- [Overview](https://www.w3.org/TR/owl2-overview/)
- [Primer](https://www.w3.org/TR/owl2-primer/)
- [Structural Specification](https://www.w3.org/TR/owl2-syntax/)
- [Direct Semantics](https://www.w3.org/TR/owl2-direct-semantics/)
- [RDF-Based Semantics](https://www.w3.org/TR/owl2-rdf-based-semantics/)
- [Profiles](https://www.w3.org/TR/owl2-profiles/)
- [Conformance](https://www.w3.org/TR/owl2-conformance/)

Implementation guidance:

1. State whether you rely on OWL 2 DL direct semantics, RDF-based semantics or a product-specific ruleset.
2. Declare the intended profile: EL, QL, RL or DL.
3. Keep ontology consistency tests in CI.
4. Benchmark classification and realization on production-size representative data.
5. Never assume a triple store's optional inference switch equals full OWL 2 DL reasoning.

## 7. Property-graph standards

### 7.1 ISO GQL

[ISO/IEC 39075:2024](https://www.iso.org/standard/76120.html), Database languages - GQL, is the international graph query language standard published in 2024. [Technical Corrigendum 1](https://www.iso.org/standard/93701.html), ISO/IEC 39075:2024/Cor 1:2026, was published in July 2026.

GQL gives the property-graph ecosystem a formal standardized language target. However:

- product support can be partial or absent;
- existing Cypher/Gremlin applications do not become portable automatically;
- schema, procedure, transaction, type and extension behavior must be tested;
- a standard language does not standardize every storage engine or graph algorithm API.

### 7.2 SQL/PGQ

Property Graph Queries (SQL/PGQ) are part of the SQL:2023 family. They allow graph pattern matching over property-graph views integrated with SQL data. Use when graph traversal and relational analytics must coexist in a SQL platform, but inspect the exact vendor implementation and ISO part/profile.

### 7.3 Cypher and Gremlin

- **Cypher** is a widely implemented property-graph query language and an important conceptual predecessor/influence for GQL. It is not interchangeable with the full ISO GQL standard. Version-specific syntax such as Cypher 25 must be treated as implementation documentation.
- **Gremlin** is the Apache TinkerPop graph traversal language/API. It has a different computational model from declarative pattern languages; provider support and optimization differ.

Do not label Cypher or Gremlin code as GQL-conformant without a tested conformance claim.

## 8. Common adjacent standards and vocabularies

| Need | Standard/vocabulary | Use carefully |
|---|---|---|
| Data catalog metadata | [DCAT 3](https://www.w3.org/TR/vocab-dcat-3/) | Profiles and local catalog requirements differ. |
| Sensor/observations | [SOSA/SSN](https://www.w3.org/TR/vocab-ssn/) | Distinguish observation, result, procedure, sensor and feature of interest. |
| Geospatial RDF | [GeoSPARQL](https://www.ogc.org/standard/geosparql/) | Check OGC version and store support for functions/indexing. |
| Units/quantities | QUDT or OM | Select one governance model; conversions and dimensions must be tested. |
| Data quality | DQV | Quality observations still need measurable definitions and ownership. |
| Schema.org Web vocabulary | [Schema.org](https://schema.org/) | Broad interoperability vocabulary, not a replacement for a precise domain ontology. |
| Verifiable credentials | [VC Data Model](https://www.w3.org/TR/vc-data-model-2.0/) | Security/privacy model is broader than RDF representation. |

## 9. Conformance matrix template

Create one matrix per project:

| Capability | Standard target | Product A | Product B | Test fixture | Decision |
|---|---|---|---|---|---|
| RDF-star/triple terms | RDF 1.2 candidate | pass/fail | pass/fail | `rdf12-triple-term.ttl` | enable/avoid |
| SPARQL property path | SPARQL 1.1 | pass/fail | pass/fail | `paths.rq` | portable subset |
| SHACL closed shape | SHACL 1.0 | pass/fail | pass/fail | `closed-shape.ttl` | required |
| OWL RL entailment | OWL 2 RL | pass/fail | pass/fail | `owl-rl-fixture.ttl` | materialize/query-time |
| GQL feature | ISO GQL profile | pass/fail | pass/fail | `gql-001.sql` | vendor-specific |

A product marketing page is not a conformance test.

## 10. Upgrade strategy

1. **Inventory** every standards-dependent feature in data, queries and APIs.
2. **Pin** parser/store/validator/reasoner versions.
3. **Build fixtures** for syntax, inference, validation and round trips.
4. **Run dual mode** on a snapshot when moving from RDF 1.1 to RDF 1.2 or between query-language versions.
5. **Diff semantics**, not only text serialization.
6. **Benchmark** latency, storage and result cardinality.
7. **Document fallback** for old clients.
8. **Gate rollout** behind capability flags.
9. **Retain rollback** and canonical source data.
10. **Update this note** with date, source link and architecture decision.

## 11. Status-summary decision table

| Technology | Status on 5 Nov 2026 | Default for this roadmap |
|---|---|---|
| RDF 1.1 | Stable Recommendation | Production interoperability baseline |
| RDF 1.2 Concepts/Semantics | Candidate Recommendation work | Learn and experiment; deploy with explicit support tests |
| RDF 1.2 serializations/schema | Working Drafts in current index | Avoid untested cross-vendor dependence |
| SPARQL 1.1 | Stable Recommendation | Production query/update baseline |
| SPARQL 1.2 | Working Draft | Research and compatibility testing |
| OWL 2 Second Edition | Stable Recommendation | Formal ontology baseline |
| SHACL 1.0 | Stable Recommendation | Validation baseline |
| SHACL 1.2 | Working Draft | Track and prototype; pin implementation |
| SKOS | Stable Recommendation | Taxonomy/thesaurus baseline |
| PROV-O | Stable Recommendation | Provenance vocabulary baseline |
| JSON-LD 1.1 | Stable Recommendation | Web/API RDF serialization baseline |
| ISO GQL 2024 + Cor 1:2026 | Published International Standard | Learn as the property-graph standard; verify product support |
| Cypher/Gremlin | Implementation/ecosystem languages | Use according to chosen platform, not as automatic standards portability |

## 12. Review checklist

- [ ] I checked the official status page on the decision date.
- [ ] I separated specification maturity from vendor support.
- [ ] I named the exact entailment, validation and query semantics.
- [ ] I have conformance fixtures for every nontrivial feature.
- [ ] Draft-only features are isolated and reversible.
- [ ] Data round trips preserve identity, language, datatype and statement metadata.
- [ ] The architecture decision record links to this matrix.

## Related notes

- [[05_RDF_RDFS_and_Linked_Data]]
- [[06_SPARQL_Query_and_Federation]]
- [[07_Description_Logics_and_OWL_2]]
- [[09_SHACL_SKOS_Rules_Provenance_and_Identity]]
- [[12_Property_Graphs_Cypher_GQL_and_Gremlin]]
- [[14_RDF_vs_Property_Graphs_and_Interoperability]]
