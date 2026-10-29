# MID-068 · Retrieval-augmented generation — Exercises and lab

## Lab
### MID-068-LAB1 · Order-support assistant v1
**Outcomes:** 1–5 · **Time:** ~3.5 h
Answer customer questions about shipping, returns, and payment policies from the MID-067 index, citing the source articles. When an article changes, a `HelpArticleUpdated` event re-embeds only that article. Measure retrieval recall on the question set separately from answer quality.
**Acceptance:** every answer cites at least one source or explicitly declines; a changed policy is reflected within one minute; retrieval recall measured on the question set.

## Exercises (assessment: diagnose three bad answers)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-068-EX01 | 1 | Explain in five lines why RAG helps with Shop's changing policies and list three ways it can still fail. |
| MID-068-EX02 | 2 | Chunk a 1 500-word returns article: choose size, overlap, and metadata, and justify. Add the filter for an Arabic-speaking customer. |
| MID-068-EX03 | 3 | Write the prompt for the assistant with numbered sources, citation format, and the decline rule. Say what happens when no chunk passes the threshold. |
| MID-068-EX04 | 4 | Sketch the consumer for `HelpArticleUpdated`: steps, idempotency, deletions, and why not a nightly rebuild. |
| MID-068-EX05 | 5 | Compute recall@4 for 20 questions where the right chunk was in the top 4 for 16; name two fixes for the misses. |
| MID-068-EX06 | 1–5 | Diagnose three bad answers from logs and fix each at the right layer: (a) right article not in retrieved ids; (b) retrieved chunk dated before the policy change; (c) right chunk retrieved but answer contradicts it. |

## Solutions
- **EX01** Model lacks private, current data; RAG injects it and enables citations. Failures: retrieval miss, stale chunk, model ignores context, irrelevant context, wrong filter.
- **EX02** Split by headings, then to a few hundred tokens with small overlap (tune by recall); metadata: article id, section, language, product, updated time. Filter `lang = 'ar'` and customer audience.
- **EX03** "Answer only from the sources; cite [n]; if not answered, say you could not find it." With no chunk above the threshold: skip the model call and return a fixed decline.
- **EX04** Receive event, load article, chunk, compare hashes, embed only changed chunks, delete old and insert new in one transaction. Idempotent by article version or hash. `HelpArticleDeleted` removes chunks. Nightly rebuild is slow, costly, and stale for hours.
- **EX05** 16/20 = 0.80. Fixes: add hybrid search or synonyms; adjust chunk size; add re-ranking; fix metadata filters.
- **EX06** (a) Retrieval miss: fix chunking, hybrid search, filters, or threshold. (b) Stale chunk: re-index on event, check the hash comparison. (c) Ignored context: tighten the prompt, reduce irrelevant context, check the model; evaluate in MID-070.

**Outcomes 3 and 5** are also covered by the quiz and the lab (citations, decline, recall measurement).
