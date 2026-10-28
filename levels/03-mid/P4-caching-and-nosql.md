# MID-P4 — Caching and Nonrelational Data

**Phase goal:** the learner adds caching where it pays off without serving wrong data, and chooses nonrelational stores from workload evidence rather than fashion.

**Running project:** *Shop Platform* gains a Redis cache for the catalog, a search service backed by OpenSearch, and a decision record on whether reviews belong in MongoDB.

**Phase total:** ~9.8 h video · ~24 h practice

---

### MID-037 · Caching fundamentals
`n: 145` · **Video:** 44 min · **Practice:** 1.5 h

**Prerequisites:** MID-023

**Learning outcomes** — the learner can:
1. Explain where caches sit (client, CDN, gateway, application, database) and what each saves.
2. Compare local and distributed caches.
3. Reason about hit ratio, eviction policies (LRU, LFU), and TTL.
4. Decide whether a given endpoint should be cached at all.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-037-L01 | Why and where to cache | 10 |
| MID-037-L02 | Local vs distributed caches | 8 |
| MID-037-L03 | Hit ratio and what it hides | 8 |
| MID-037-L04 | Eviction and TTL | 8 |
| MID-037-L05 | Demo: a local Caffeine cache with metrics | 10 |

**Lab** — `MID-037-LAB1` *Cache candidates:* measure Shop's endpoints and pick the three worth caching, with expected hit ratios. Acceptance: decision backed by access data.

**Common mistakes:** caching before measuring; caching personalized or rapidly changing data globally.

**Assessment:** quiz.

**Career relevance:** every high-traffic service.

---

### MID-038 · Redis
`n: 146` · **Video:** 76 min · **Practice:** 3 h

**Prerequisites:** JNR-050, MID-037

**Learning outcomes** — the learner can:
1. Use Redis strings, hashes, sets, sorted sets, and expirations for appropriate problems.
2. Design key names and namespaces that support invalidation.
3. Use Redis from Spring (Spring Data Redis, `@Cacheable` with a Redis cache manager).
4. Explain Redis persistence options and memory limits, and what is lost on failure.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-038-L01 | Redis in one picture | 8 |
| MID-038-L02 | Data structures and their uses | 14 |
| MID-038-L03 | Key design | 8 |
| MID-038-L04 | Redis from Spring | 12 |
| MID-038-L05 | Persistence, memory, and eviction | 10 |
| MID-038-L06 | Demo: a leaderboard with sorted sets | 12 |
| MID-038-L07 | Demo: caching product details with `@Cacheable` | 12 |

**Lab** — `MID-038-LAB1` *Catalog cache:* cache product details and category listings in Redis with TTLs and metrics. Acceptance: hit ratio and latency improvement measured under load.

**Common mistakes:** `KEYS *` in production; unbounded memory; Redis as the only copy of important data.

**Assessment:** data-structure selection scenarios.

**Career relevance:** caching patterns (MID-039) and rate limiting (MID-034).

---

### MID-039 · Caching patterns
`n: 147` · **Video:** 50 min · **Practice:** 2.5 h

**Prerequisites:** MID-038

**Learning outcomes** — the learner can:
1. Implement cache-aside, read-through, write-through, and write-behind, and state each one's failure behavior.
2. Invalidate on change via events instead of relying on TTL alone.
3. Explain the risk of write-behind and when it is acceptable.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-039-L01 | Cache-aside | 10 |
| MID-039-L02 | Read-through and write-through | 10 |
| MID-039-L03 | Write-behind | 8 |
| MID-039-L04 | Invalidation strategies | 10 |
| MID-039-L05 | Demo: event-driven invalidation from `ProductUpdated` | 12 |

**Lab** — `MID-039-LAB1` *Fresh catalog:* invalidate cached products when the catalog service publishes `ProductUpdated`. Acceptance: price change visible within one second.

**Common mistakes:** updating cache and database in the wrong order; relying on TTL for prices.

**Assessment:** pattern-choice scenarios.

**Career relevance:** cache consistency (MID-040).

---

### MID-040 · Cache consistency
`n: 148` · **Video:** 50 min · **Practice:** 2 h

**Prerequisites:** MID-030, MID-039

**Learning outcomes** — the learner can:
1. Explain and prevent cache stampedes (locking, request coalescing, early refresh).
2. Identify invalidation races that leave stale data and fix them (delete-after-write, versioning).
3. Detect and mitigate hot keys.
4. State an explicit staleness tolerance for each cached item.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-040-L01 | Stampedes | 10 |
| MID-040-L02 | Invalidation races | 12 |
| MID-040-L03 | Hot keys | 8 |
| MID-040-L04 | Staleness budgets | 8 |
| MID-040-L05 | Demo: a stampede after cache expiry, then the fix | 12 |

**Lab** — `MID-040-LAB1` *Flash sale:* simulate a flash sale on one product; prevent the stampede and the hot key from overwhelming the database. Acceptance: database load stays bounded.

**Common mistakes:** identical TTLs on everything; ignoring races because "it's rare".

**Assessment:** race-condition analysis.

**Career relevance:** large-scale performance (SRA-007).

---

### MID-041 · NoSQL fundamentals
`n: 149` · **Video:** 54 min · **Practice:** 1.5 h

**Prerequisites:** BEG-048, MID-030

**Learning outcomes** — the learner can:
1. Describe key-value, document, wide-column, and graph models with a fitting use case for each.
2. Explain query-driven data modeling and its trade-off against flexible querying.
3. Relate each store's consistency and scaling model to the CAP/PACELC discussion.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-041-L01 | Why NoSQL exists | 8 |
| MID-041-L02 | Key-value and document stores | 10 |
| MID-041-L03 | Wide-column stores | 8 |
| MID-041-L04 | Graph databases | 8 |
| MID-041-L05 | Modeling for queries | 8 |
| MID-041-L06 | Demo: the same data in four models | 12 |

**Lab** — `MID-041-LAB1` *Model comparison:* model Shop's reviews in a document, wide-column, and relational form and list the queries each supports well. Acceptance: comparison table.

**Common mistakes:** "schemaless" meaning "no schema design".

**Assessment:** quiz.

**Career relevance:** data selection (MID-044) and database architecture (ARC-016).

---

### MID-042 · MongoDB
`n: 150` · **Video:** 68 min · **Practice:** 2.5 h

**Prerequisites:** MID-041

**Learning outcomes** — the learner can:
1. Model documents with embedding vs referencing decided by access patterns.
2. Create indexes and read query plans in MongoDB.
3. Write aggregation pipelines.
4. Use multi-document transactions where needed and explain their cost.
5. Use MongoDB from Spring Data MongoDB.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-042-L01 | Documents and collections | 8 |
| MID-042-L02 | Embedding vs referencing | 12 |
| MID-042-L03 | Indexes and explain | 10 |
| MID-042-L04 | Aggregation pipelines | 12 |
| MID-042-L05 | Transactions | 6 |
| MID-042-L06 | Spring Data MongoDB | 8 |
| MID-042-L07 | Demo: building the reviews service on MongoDB | 12 |

**Lab** — `MID-042-LAB1` *Reviews service:* product reviews with ratings summary via aggregation. Acceptance: indexes match queries; summary computed in the database.

**Common mistakes:** unbounded arrays inside documents; relational schemas copied into collections.

**Assessment:** document-model review.

**Career relevance:** polyglot persistence decisions.

---

### MID-043 · Search systems
`n: 151` · **Video:** 62 min · **Practice:** 2.5 h

**Prerequisites:** MID-012, MID-041

**Learning outcomes** — the learner can:
1. Explain inverted indexes, analyzers, tokenization, and relevance scoring.
2. Index documents and run full-text, filtered, and faceted queries in OpenSearch/Elasticsearch.
3. Keep a search index in sync with the source of truth via events.
4. Compare PostgreSQL full-text search with a dedicated engine.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-043-L01 | How search engines find things | 10 |
| MID-043-L02 | Analyzers and relevance | 10 |
| MID-043-L03 | Queries, filters, and facets | 12 |
| MID-043-L04 | Keeping the index in sync | 10 |
| MID-043-L05 | PostgreSQL full-text vs a search engine | 8 |
| MID-043-L06 | Demo: product search with typo tolerance and facets | 12 |

**Lab** — `MID-043-LAB1` *Shop search:* a search service fed by catalog events, with typo tolerance and category/price facets. Acceptance: reindex from scratch documented; search never becomes the source of truth.

**Common mistakes:** dual writes to database and index; using search as primary storage.

**Assessment:** lab plus tool-choice scenario.

**Career relevance:** data platform integration (SRB-007).

---

### MID-067 · Embeddings and vector search
`n: new (added in v2.0)` · **Video:** 65 min · **Practice:** 3 h · `version:` embedding models and pgvector releases change — verify before recording

**Prerequisites:** JNR-056, MID-043

**Learning outcomes** — the learner can:
1. Explain what an embedding is and why semantically similar texts end up close together.
2. Choose a similarity measure (cosine, inner product, Euclidean distance) consistent with the embedding model.
3. Store and query embeddings in PostgreSQL with pgvector, and choose between HNSW and IVFFlat indexes by recall, build time, and memory.
4. Combine keyword (full-text) and vector search into hybrid search and explain when each wins.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-067-L01 | What embeddings are | 10 |
| MID-067-L02 | Similarity measures | 8 |
| MID-067-L03 | pgvector: storing and querying vectors | 12 |
| MID-067-L04 | Approximate indexes: HNSW and IVFFlat | 12 |
| MID-067-L05 | Hybrid search: keywords plus vectors | 10 |
| MID-067-L06 | Demo: semantic search over Shop's help-center articles | 13 |

**Lab** — `MID-067-LAB1` *Searchable help center:* embed Shop's help-center and policy documents into pgvector, add an HNSW index, and expose a semantic search endpoint with a hybrid (full-text + vector) mode. Acceptance: a test set of 30 customer questions shows the right article in the top 3 for at least 25; query latency and index size recorded.

**Common mistakes:** mixing embeddings from different models in one column; using a distance measure the model was not trained for; approximate indexes without measuring recall; re-embedding everything on every change.

**Assessment:** design exercise — choose model, dimensions, index, and refresh strategy for a new corpus and justify each choice.

**Career relevance:** the data layer of every RAG feature (MID-068) and of AI solution architectures (ARC-045).

---

### MID-068 · Retrieval-augmented generation
`n: new (added in v2.0)` · **Video:** 80 min · **Practice:** 3.5 h

**Prerequisites:** MID-067

**Learning outcomes** — the learner can:
1. Explain why retrieval-augmented generation (RAG) grounds model answers in your own data and where it still fails.
2. Chunk documents with sensible size, overlap, and metadata, and retrieve with filters (e.g., language, product, customer tier).
3. Assemble a prompt from retrieved chunks with source citations, and make the assistant say "I don't know" when retrieval finds nothing relevant.
4. Keep the index fresh by re-embedding on change events instead of nightly full rebuilds.
5. Measure retrieval quality (recall of the right chunk) separately from answer quality.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-068-L01 | Why RAG, and its limits | 8 |
| MID-068-L02 | Chunking strategies | 10 |
| MID-068-L03 | Retrieval, filters, and re-ranking | 10 |
| MID-068-L04 | Context assembly and citations | 10 |
| MID-068-L05 | Freshness: re-indexing on events | 8 |
| MID-068-L06 | Evaluating retrieval separately from generation | 9 |
| MID-068-L07 | Demo: the order-support assistant answers with citations | 13 |
| MID-068-L08 | Demo: a stale policy answer fixed by event-driven re-indexing | 12 |

**Lab** — `MID-068-LAB1` *Order-support assistant v1:* answer customer questions about shipping, returns, and payment policies from the MID-067 index, citing the source articles; when an article changes, a `HelpArticleUpdated` event re-embeds only that article. Acceptance: every answer cites at least one source or explicitly declines; a changed policy is reflected within one minute; retrieval recall measured on the question set.

**Common mistakes:** chunks so large they drown the answer; no citations, so wrong answers cannot be traced; answering from model memory when retrieval is empty; judging RAG only by how fluent the answers sound.

**Assessment:** diagnose three bad answers (retrieval miss, stale chunk, ignored context) from logs and fix each at the right layer.

**Career relevance:** the most common pattern in enterprise AI features; evaluated in MID-070, secured in MID-071, operated in SRC-022.

---

### MID-044 · Data selection
`n: 152` · **Video:** 40 min · **Practice:** 2 h

**Prerequisites:** MID-038, MID-042, MID-043

**Learning outcomes** — the learner can:
1. Characterize a workload (access patterns, volume, consistency, latency, query flexibility).
2. Select a store from that characterization and justify it in an ADR.
3. Count the operational cost of each additional datastore.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-044-L01 | Characterizing a workload | 10 |
| MID-044-L02 | PostgreSQL first, and when not | 10 |
| MID-044-L03 | The operational cost of another database | 8 |
| MID-044-L04 | Demo: writing the reviews datastore ADR | 12 |

**Lab** — `MID-044-LAB1` *Datastore ADRs:* ADRs for catalog, orders, reviews, search, and sessions. Acceptance: each cites workload evidence; at least one concludes "PostgreSQL is enough".

**Common mistakes:** choosing by popularity; ignoring backup, monitoring, and skills cost.

**Assessment:** ADR review.

**Career relevance:** technology evaluation (SRB-013) and database architecture (ARC-016).
