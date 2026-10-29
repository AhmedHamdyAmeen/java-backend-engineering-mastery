# MID-067 · Embeddings and vector search — Quiz

Outcomes: O1 embeddings · O2 similarity measures · O3 pgvector and indexes · O4 hybrid search.

**Q01 (O1)** An embedding is: A. A compressed copy of the text B. A fixed-length vector in which similar meanings are close C. A hash used for deduplication D. A keyword list
**Q02 (O1)** Mixing vectors from two models in one column is a mistake because: A. It exceeds disk limits B. PostgreSQL forbids it C. Each model has its own space, so distances are meaningless D. It disables indexes
**Q03 (O1)** Embeddings are weakest for: A. Exact identifiers such as an order number B. Paraphrased questions C. Long paragraphs D. Multiple languages
**Q04 (O2)** Which distance measure should you choose? A. Always Euclidean B. Whatever is fastest C. A random one D. The one the embedding model documents
**Q05 (O2)** For normalized vectors, inner product ranks like: A. Hamming distance B. Edit distance C. Jaccard similarity D. Cosine similarity
**Q06 (O3)** The pgvector column type for 768 dimensions: A. `array(768)` B. `float[768]` C. `vector(768)` D. `embedding`
**Q07 (O3)** Compared with IVFFlat, HNSW usually has: A. Better recall/speed trade-off but slower build and more memory B. Faster build and less memory C. No tuning parameters D. No approximation
**Q08 (O3)** Before trusting an approximate index you should: A. Delete the table B. Drop the extension C. Lower the dimension D. Measure recall against exact search
**Q09 (O4)** Reciprocal Rank Fusion merges results by: A. Averaging raw scores B. Picking the longest text C. Summing 1/(k+rank) across the lists D. Sorting by id
**Q10 (O4)** Which finds "ORD-88231" best? A. Vector search alone B. A bigger embedding C. IVFFlat D. Keyword (full-text) search

## Answers
Q01 B · Q02 C · Q03 A · Q04 D · Q05 D · Q06 C · Q07 A · Q08 D · Q09 C · Q10 D

## Practical part
Design exercise (`MID-067-EX06`) plus lab `MID-067-LAB1`. Pass: quiz at least 8/10, justified model, index, and refresh choices, and a lab with at least 25 of 30 questions answered in the top 3 and latency and index size recorded.
