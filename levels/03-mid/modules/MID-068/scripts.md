# MID-068 · Retrieval-augmented generation — Lecture scripts

**Video:** 80 min · **Analogy used throughout:** an open-book exam: the assistant may only answer from the pages you hand it, must point to the page, and says "not in my book" when the page is missing. Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

Version note: model names, prices, and Spring AI APIs change. Verify before recording.

---

## MID-068-L01 · Why RAG, and its limits (8 min)
**Goal:** explain why RAG grounds answers in your data and where it still fails.

**Key points**
- A model only knows its training data: it does not know Shop's return policy and can invent one.
- RAG (retrieval-augmented generation): find relevant passages in your data, put them in the prompt, ask the model to answer from them.
- Benefits: current data without retraining, answers traceable to sources, access control at retrieval time.
- Failures: retrieval misses, stale chunks, the model ignoring or misreading context, too much irrelevant context.
- RAG reduces hallucination; it does not remove it.

**Show:** flow: question → embed → search index → top chunks → prompt → model → answer with sources.

**Check:** Name two ways a RAG answer can still be wrong. *(Retrieval misses the right chunk; the chunk is stale; the model ignores the context.)*

---

## MID-068-L02 · Chunking strategies (10 min)
**Goal:** split documents into chunks that retrieve well.

**Key points**
- Chunk: the unit you embed and retrieve. Too large drowns the answer and wastes tokens; too small loses context.
- Start with structure: split by headings and paragraphs, then by size (a few hundred tokens is a common start; tune by measurement).
- Overlap a little so a sentence at a boundary is not cut off.
- Metadata per chunk: article id, title, section, language, product, audience, updated time.
- Keep the article id so one article can be re-indexed alone.

**Show:** a returns policy article split into "Eligibility", "Deadlines", "Refund method" chunks, each carrying `{articleId: 42, lang: "en", section: "Deadlines"}`.

**Check:** Why keep the article id on every chunk? *(To cite the source and to replace only that article's chunks on change.)*

---

## MID-068-L03 · Retrieval, filters, and re-ranking (10 min)
**Goal:** retrieve the right chunks using filters and optional re-ranking.

**Key points**
- Filter by metadata before or during the vector search: language, product, customer tier. A wrong-language chunk is a wrong answer.
- Fetch more candidates than needed (for example 20), then keep the best few.
- Re-ranking: a second model scores query-chunk pairs and reorders candidates; better quality, extra latency and cost.
- Set a minimum similarity threshold: weak matches should count as "nothing found".
- Hybrid search (MID-067) helps with exact terms such as order or policy codes.

**Show:** pipeline: filter `lang = 'ar' AND audience = 'customer'` → top 20 by vector/hybrid → optional re-rank → top 4 above threshold.

**Check:** Why a similarity threshold? *(So weak matches lead to "I don't know" instead of a made-up answer.)*

---

## MID-068-L04 · Context assembly and citations (10 min)
**Goal:** build a prompt from chunks with citations and a safe "I don't know".

**Key points**
- Prompt parts: instructions, numbered sources, then the question. Keep instructions separate from retrieved text.
- Tell the model: answer only from the sources, cite source numbers, say it does not know when the sources do not answer.
- If retrieval returns nothing relevant, do not call the model with an empty context: return a fixed decline message.
- Return the citations (article id, title, link) to the client, not just text.
- Retrieved text is untrusted data; instructions inside it must not be followed (see MID-071).

**Show**
```text
Answer using only the sources below. Cite as [1], [2]. If the sources do not
answer the question, reply: "I could not find this in our help center."
[1] (Returns, Deadlines) Items can be returned within 14 days ...
Question: Can I return shoes after three weeks?
```
Deadline values are examples.

**Check:** What should the assistant do when retrieval finds nothing relevant? *(Decline explicitly; do not answer from model memory.)*

---

## MID-068-L05 · Freshness: re-indexing on events (8 min)
**Goal:** keep the index current by re-embedding only what changed.

**Key points**
- Nightly full rebuilds are slow, costly, and leave answers stale for hours.
- Event-driven: `HelpArticleUpdated` (via the outbox, see messaging modules) triggers re-chunking and re-embedding of that article.
- Compare a content hash per chunk and skip unchanged chunks to save embedding calls.
- Replace chunks atomically (delete old, insert new in one transaction); handle `HelpArticleDeleted` too.
- Handlers must be idempotent: the same event twice gives the same index.

**Show:** event `HelpArticleUpdated{articleId:42, version:7}` → consumer → chunk → hash compare → embed 2 changed chunks → transaction replaces rows of article 42.

**Check:** Why make the re-index handler idempotent? *(Events can be delivered more than once.)*

---

## MID-068-L06 · Evaluating retrieval separately from generation (9 min)
**Goal:** measure retrieval quality apart from answer quality.

**Key points**
- Two stages, two questions: did we retrieve the right chunk? Did the model use it correctly?
- Build a question set with the expected article or chunk for each question.
- Retrieval metrics: recall@k (the right chunk is in the top k) and, optionally, rank of the first right chunk.
- Check retrieval first: if recall is low, no prompt change will help.
- Fluent answers prove nothing; judge by sources and the expected content (answer evaluation is covered in MID-070).

**Show:** table: 30 questions, recall@4 = 27/30 = 0.90; the 3 misses listed with their cause (wrong language, chunk too large, missing synonym).

**Check:** Why measure retrieval separately? *(To find whether failures come from search or from generation, and fix the right layer.)*

---

## MID-068-L07 · Demo: the order-support assistant answers with citations (13 min)
**Goal:** build the assistant that prepares `MID-068-LAB1`.

**Steps**
1. Start from the MID-067 index; add a `POST /support/ask` endpoint.
2. Retrieve top 20 with language filter, keep the top 4 above the similarity threshold.
3. Build the prompt with numbered sources and the decline instruction; call the model through Spring AI (verify API and model name before recording).
4. **Planned mistake:** a question about a topic Shop does not cover gets a confident answer from model memory because the prompt had no decline rule and no threshold. Fix: add the rule and return a fixed decline when nothing passes the threshold.
5. Return `{answer, sources:[{articleId,title}]}` and test shipping, returns, payment, and one out-of-scope question.
6. Log the question, retrieved chunk ids, scores, and answer for later diagnosis.

---

## MID-068-L08 · Demo: a stale policy answer fixed by event-driven re-indexing (12 min)
**Goal:** show a stale answer, trace it in the logs, and fix it with a re-index event.

**Steps**
1. Ask "How many days do I have to return an item?" and get the old 14-day answer after the policy changed to 30 days.
2. Read the logs: the cited chunk id and its `updated` time show the stale chunk was retrieved; the model was right to use it.
3. Publish `HelpArticleUpdated` for the article; the consumer re-chunks, hash-compares, and re-embeds only changed chunks.
4. **Planned mistake:** the consumer inserts new chunks but forgets to delete old ones, so both answers are retrieved. Fix: replace the article's chunks in one transaction.
5. Ask again; the answer shows 30 days within one minute; confirm the unchanged articles were not re-embedded.
6. This prepares the freshness criterion of `MID-068-LAB1`.
