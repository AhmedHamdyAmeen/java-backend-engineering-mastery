# MID-067 · Embeddings and vector search — Exercises and lab

## Lab
### MID-067-LAB1 · Searchable help center
**Outcomes:** 1–4 · **Time:** ~3 h
Embed Shop's help-center and policy documents into pgvector, add an HNSW index, and expose a semantic search endpoint with a hybrid (full-text + vector) mode. Prepare a test set of 30 customer questions with the expected article for each. Record query latency and index size.
**Acceptance:** the right article is in the top 3 for at least 25 of the 30 questions; query latency and index size recorded.

## Exercises (assessment: design exercise)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-067-EX01 | 1 | Explain why "refund my order" and "money back for a purchase" are close as vectors, and name one case where embeddings fail. |
| MID-067-EX02 | 2 | A model documents cosine similarity and returns normalized vectors. Choose the operator and operator class and justify. |
| MID-067-EX03 | 3 | Write the table, an HNSW index, and a top-5 query with a language filter for a 768-dimension model. |
| MID-067-EX04 | 3 | Choose HNSW or IVFFlat for (a) 50 000 chunks updated daily, (b) 20 M chunks rebuilt monthly; compare recall, build time, memory. |
| MID-067-EX05 | 4 | Give three Shop queries and say whether keyword, vector, or hybrid wins for each. |
| MID-067-EX06 | 3 | Design exercise: for a new corpus (10 000 product manuals, 4 languages) choose model, dimensions, index, and refresh strategy and justify each. |

## Solutions
- **EX01** The model maps similar meaning to nearby points. Failure: exact identifiers (SKUs, order numbers) or negation ("not refundable") may be missed.
- **EX02** Cosine distance `<=>` with `vector_cosine_ops`; for normalized vectors inner product gives the same ranking. Use the measure the model documents.
- **EX03** `CREATE TABLE ... embedding vector(768)`; `CREATE INDEX ... USING hnsw (embedding vector_cosine_ops)`; `WHERE lang = 'ar' ORDER BY embedding <=> :q LIMIT 5`. Verify syntax for your pgvector version.
- **EX04** (a) HNSW: handles inserts without rebuild and gives good recall; memory is small at this size. (b) Depends on the memory budget: IVFFlat builds faster and is smaller (build after load, tune `lists` and `probes`); HNSW usually has better recall. Measure recall for both.
- **EX05** "Where is my parcel": vector. "ORD-88231 status": keyword. "Return policy for electronics": hybrid.
- **EX06** Multilingual model if queries cross languages; dimensions as the model provides; HNSW with cosine; store `model` and `content_hash`; refresh only changed documents (hash compare) and re-embed everything only on a model change. Justify each with recall measured on a question set. Verify model choice and prices before deciding.

**Outcomes 1 and 4** are also covered by the quiz and the lab (hybrid mode).
