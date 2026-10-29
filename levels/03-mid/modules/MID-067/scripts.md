# MID-067 · Embeddings and vector search — Lecture scripts

**Video:** 65 min · **Analogy used throughout:** a library where books are shelved by meaning, not by title; a question walks to the shelf where similar ideas sit. Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

Version note: embedding models, dimensions, and pgvector releases change. Verify version before recording.

---

## MID-067-L01 · What embeddings are (10 min)
**Goal:** explain that an embedding is a list of numbers that places a text at a point where similar meanings are close.

**Key points**
- An embedding model turns text into a vector: a fixed-length list of numbers (for example 768 or 1536 values; verify per model).
- Texts with similar meaning land near each other: "Where is my parcel?" is close to "Track an order".
- The vector has no readable parts; only distances between vectors carry meaning.
- Vectors from different models live in different spaces: never compare or mix them in one column.
- Embeddings capture meaning, not exact words: product codes and rare names can be missed.

**Show:** three phrases drawn as points on a 2D map: "return policy" and "refund a purchase" close together, "shipping to Riyadh" far away. Then a Spring AI `EmbeddingModel` call returning a `float[]` (verify the API before recording).

**Check:** Why can you not mix vectors from two models in one column? *(Each model has its own space, so distances between them are meaningless.)*

---

## MID-067-L02 · Similarity measures (8 min)
**Goal:** pick the distance measure that matches the embedding model.

**Key points**
- Cosine distance: compares direction, ignores length. The common default for text embeddings.
- Inner product: fast; ranks like cosine when vectors are normalized to length 1.
- Euclidean (L2): straight-line distance; use it when the model was trained for it.
- Rule: use the measure the model documents. A wrong measure still returns results, just worse ones.
- The index must use the same measure as the query.

**Show**
| Measure | pgvector operator | Use when |
| --- | --- | --- |
| Cosine distance | `<=>` | model recommends cosine |
| Inner product (negated) | `<#>` | vectors normalized |
| Euclidean | `<->` | model trained for L2 |

**Check:** What happens if you use a measure the model was not trained for? *(Queries run, but ranking quality drops silently.)*

---

## MID-067-L03 · pgvector: storing and querying vectors (12 min)
**Goal:** store embeddings in PostgreSQL and run a nearest-neighbour query.

**Key points**
- pgvector adds a `vector(n)` column type and distance operators; enable it with `CREATE EXTENSION vector`.
- The dimension `n` must match the model; keep a `model` column so you know what produced each row.
- Query: order by distance, `LIMIT k`. Without an index this is an exact scan, fine for small tables.
- Embeddings stay next to relational data: filter by language or product with a normal `WHERE`.
- Store source text, a content hash, and the article id with the vector so rows can be refreshed.

**Show**
```sql
CREATE EXTENSION IF NOT EXISTS vector;
CREATE TABLE help_chunk (
  id bigserial PRIMARY KEY, article_id bigint NOT NULL, lang text NOT NULL,
  content text NOT NULL, content_hash text NOT NULL,
  model text NOT NULL, embedding vector(768) NOT NULL);

SELECT id, article_id, embedding <=> :q AS distance
FROM help_chunk WHERE lang = 'en'
ORDER BY embedding <=> :q LIMIT 5;
```
Dimension 768 is an example; verify against the model.

**Check:** Why store a `model` column? *(To detect and re-embed rows made with a different model.)*

---

## MID-067-L04 · Approximate indexes: HNSW and IVFFlat (12 min)
**Goal:** choose between HNSW and IVFFlat by recall, build time, and memory.

**Key points**
- Exact search checks every row; approximate (ANN) indexes are faster but may miss true nearest neighbours. The share found is the recall.
- HNSW: graph index; better recall and speed trade-off, slower to build, more memory, can be created on an empty table.
- IVFFlat: groups vectors into lists; faster build, smaller; build it after the data is loaded; recall depends on `lists` and `probes`.
- Tune at query time (`hnsw.ef_search`, `ivfflat.probes`); verify parameter names and defaults for your pgvector version.
- Always measure recall against an exact query on a sample before trusting an index.

**Show**
```sql
CREATE INDEX ON help_chunk USING hnsw (embedding vector_cosine_ops);
SET hnsw.ef_search = 80;
-- recall check: compare top-10 with the index vs. top-10 from an exact scan
```

**Check:** Which index builds faster on a freshly loaded static corpus? *(IVFFlat; HNSW costs more build time and memory but usually gives better recall.)*

---

## MID-067-L05 · Hybrid search: keywords plus vectors (10 min)
**Goal:** combine full-text and vector search and say when each wins.

**Key points**
- Vectors win on meaning and paraphrase ("my package is late").
- Keywords win on exact terms: order numbers, SKUs, error codes, names.
- Hybrid: run both, then merge the rankings. Reciprocal Rank Fusion (RRF) merges by rank, so scores need no common scale.
- PostgreSQL does both: `tsvector` with a GIN index plus pgvector.
- Test with real questions; do not assume hybrid is always better.

**Show:** two ranked lists merged: RRF score = sum of 1 / (k + rank) per list (k = 60 is a common constant). An article ranked 1st in text and 3rd in vector beats one ranked 1st in only one list.

**Check:** Which search finds the order id "ORD-88231"? *(Keyword search; vectors do not match exact codes reliably.)*

---

## MID-067-L06 · Demo: semantic search over Shop's help-center articles (13 min)
**Goal:** build the semantic and hybrid search endpoint that prepares `MID-067-LAB1`.

**Steps**
1. Create the `help_chunk` table and the pgvector extension in a Flyway migration.
2. Embed 20 articles with the embedding model and insert vectors with the model name and content hash.
3. Add `GET /help/search?q=`: embed the query, run the top-5 cosine query.
4. **Planned mistake:** the table was filled with one embedding model and the query embedded with another; results look random. Fix: compare the `model` column and re-embed one side.
5. Add the HNSW index; measure recall against the exact query and record latency and index size.
6. Add `mode=hybrid` with full-text plus RRF and compare on a few questions.
