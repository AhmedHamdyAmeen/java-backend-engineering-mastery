# MID-043 · Search systems — Lecture scripts

**Video:** 62 min · **Analogy used throughout:** the index at the back of a book: look up a word, get the pages, instead of reading every page. Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-043-L01 · How search engines find things (10 min)
**Goal:** explain the inverted index and why full-text search is fast.

**Key points**
- Normal index: document → words. Inverted index: word → list of documents containing it.
- A query looks up each word and combines the lists (AND/OR), so it does not scan every document.
- Engines (Lucene-based: OpenSearch, Elasticsearch) split an index into shards for scale and replicas for availability.
- Search is near-real-time: a document becomes searchable after a refresh (about a second by default; verify).
- A search engine is a derived view of data, not a database of record.

**Show**
| Term | Documents |
| --- | --- |
| red | 1, 3 |
| shoe | 1, 2, 3 |
| leather | 2 |

Query `red shoe` intersects lists to find docs 1 and 3.

**Check:** Why is an inverted index fast? *(It looks up words directly instead of scanning all documents.)*

---

## MID-043-L02 · Analyzers and relevance (10 min)
**Goal:** understand how text is processed and ranked.

**Key points**
- An analyzer = character filters, a tokenizer (split into words), and token filters (lowercase, remove stop words, stemming, synonyms).
- The same analyzer should be applied at index time and query time, unless you deliberately differ (e.g. autocomplete).
- Relevance scoring: BM25 (verify default) rewards rare terms and frequent matches in short fields; field boosts raise importance (title over description).
- Analyzer choice changes results: stemming makes "running" match "run", but can over-match.
- Language matters: use the analyzer for the content language.

**Show:** text "Running Shoes!" → tokens `running`, `shoes` → with stemming `run`, `shoe`.

**Check:** What does stemming do? *(Reduces words to a root so "running" matches "run".)*

---

## MID-043-L03 · Queries, filters, and facets (12 min)
**Goal:** write full-text, filtered, and faceted queries.

**Key points**
- Full-text: `match` query on analyzed text, scored.
- Filters: `term`/`range` inside `bool.filter`; not scored, cacheable, good for category and price.
- Facets (aggregations): counts per category or price range alongside the results.
- Typo tolerance: `fuzziness` in `match` queries (`"AUTO"`).
- Use `keyword` fields for exact values and aggregations; `text` fields for full-text.

**Show**
```json
{ "query": { "bool": {
    "must":   { "match": { "name": { "query": "runing shoes", "fuzziness": "AUTO" } } },
    "filter": [ { "term": { "category": "footwear" } }, { "range": { "price": { "lte": 100 } } } ] } },
  "aggs": { "by_category": { "terms": { "field": "category" } } } }
```

**Check:** Why put category in `filter` rather than `must`? *(Filters are not scored and can be cached.)*

---

## MID-043-L04 · Keeping the index in sync (10 min)
**Goal:** feed the index from the source of truth without dual-write bugs.

**Key points**
- The database is the source of truth; the index is rebuildable.
- Do not write the database and the index in the same request: one can fail and they diverge (dual write).
- Use events: catalog publishes `ProductUpdated` (outbox pattern), an indexer consumes it and upserts the document by product id; deletions as delete events.
- Use the product version as an external version so older events do not overwrite newer ones.
- Document a full reindex: new index, bulk load from the database, switch an alias, delete the old index.

**Show:** flow: catalog DB → outbox → broker → indexer → OpenSearch alias `products` → `products_v2`.

**Check:** Why is dual write dangerous? *(One write can fail, leaving database and index inconsistent.)*

---

## MID-043-L05 · PostgreSQL full-text vs a search engine (8 min)
**Goal:** choose between built-in database search and a dedicated engine.

**Key points**
- PostgreSQL full-text: `tsvector`, `tsquery`, GIN index, ranking; no extra service, same transaction, always consistent.
- Dedicated engine: better relevance tuning, fuzziness, facets at scale, analyzers, horizontal scale, richer features.
- Cost of an engine: another system to run, sync, secure, and back up; eventual consistency.
- Rule: start with PostgreSQL search if needs are modest (see MID-044); move when features or scale demand it.

**Show**
| | PostgreSQL FTS | OpenSearch |
| --- | --- | --- |
| Extra infra | none | cluster |
| Typo tolerance | limited (`pg_trgm`) | built in |
| Facets | manual queries | aggregations |
| Freshness | immediate | near-real-time |

**Check:** When is PostgreSQL full-text enough? *(Modest data and simple search needs, with no typo/facet demands.)*

---

## MID-043-L06 · Demo: product search with typo tolerance and facets (12 min)
**Goal:** index Shop products and query them. Prepares MID-043-LAB1.

**Steps**
1. Start OpenSearch (single node) with Docker; verify image version before recording.
2. Create an index `products_v1` with explicit mappings (`name` text, `category` keyword, `price` scaled/double) and alias `products`.
3. Bulk-load products from the catalog database and run `runing shoes` with fuzziness; show results.
4. Add category and price-range facets from aggregations.
5. **Planned mistake:** rely on dynamic mapping, so `category` is analyzed as text and the facet shows broken words. Fix: explicit mapping with `keyword`, reindex.
6. Apply an indexer consumer for `ProductUpdated` and show an update appearing in search.

**Check:** Why define mappings explicitly? *(Dynamic mapping guesses types and often guesses wrong.)*
