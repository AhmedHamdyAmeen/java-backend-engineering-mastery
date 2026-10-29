# MID-068 · Retrieval-augmented generation — Quiz

Outcomes: O1 RAG and its limits · O2 chunking and filters · O3 context and citations · O4 freshness · O5 retrieval evaluation.

**Q01 (O1)** RAG mainly helps a model answer from: A. Its training data only B. Random sampling C. Your own current data supplied in the prompt D. A bigger context window
**Q02 (O1)** RAG answers can still be wrong when: A. Retrieval misses the right chunk B. The index has citations C. Chunks have metadata D. The prompt is short
**Q03 (O2)** Chunks that are too large: A. Always improve recall B. Drown the answer and waste tokens C. Remove the need for metadata D. Speed up embedding
**Q04 (O2)** Why store the language as chunk metadata? A. To shorten chunks B. To compress vectors C. To filter out wrong-language chunks D. To avoid embeddings
**Q05 (O3)** When retrieval finds nothing relevant, the assistant should: A. Answer from model memory B. Decline explicitly C. Repeat the question D. Pick a random article
**Q06 (O3)** Citations are useful because: A. They shorten answers B. They remove hallucination C. They replace tests D. Wrong answers can be traced to a source
**Q07 (O4)** The best way to reflect an edited article: A. Rebuild everything nightly B. Restart the service C. Re-embed that article on a change event D. Wait for the TTL
**Q08 (O4)** A re-index handler must be idempotent because: A. Events can be delivered twice B. Vectors are random C. Articles are immutable D. Indexes are read-only
**Q09 (O5)** Recall@4 measures: A. Answer fluency B. Latency C. Token cost D. Whether the right chunk is in the top 4 results
**Q10 (O5)** Low retrieval recall means: A. Prompt tuning alone will fix it B. Fix chunking, filters, or search first C. Use a larger model D. Ignore it if answers sound fluent

## Answers
Q01 C · Q02 A · Q03 B · Q04 C · Q05 B · Q06 D · Q07 C · Q08 A · Q09 D · Q10 B

## Practical part
Diagnosis exercise (`MID-068-EX06`) plus lab `MID-068-LAB1`. Pass: quiz at least 8/10, three bad answers correctly diagnosed and fixed at the right layer, and a lab where every answer cites a source or declines, a changed policy is reflected within one minute, and retrieval recall is measured.
