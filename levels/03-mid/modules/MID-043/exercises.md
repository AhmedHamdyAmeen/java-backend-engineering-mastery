# MID-043 · Search systems — Exercises and lab

## Lab
### MID-043-LAB1 · Shop search
**Outcomes:** 1–4 · **Time:** ~2.5 h
Build a search service: an OpenSearch index fed by `ProductUpdated` events, with typo tolerance and category and price facets. Write a runbook for reindexing from scratch (new index, bulk load, alias switch). Add a short note comparing PostgreSQL full-text with this setup for Shop.
**Acceptance:** reindex from scratch documented; search never becomes the source of truth.

## Exercises (assessment: lab plus tool-choice scenario)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-043-EX01 | 1 | Build the inverted index for three short product names and answer the query "red shoe". |
| MID-043-EX02 | 1 | Explain what changes if the analyzer lowercases and stems, using the text "Running Shoes". |
| MID-043-EX03 | 2 | Write a query: text search for "wireless headphones", category filter, price at most 200, and a category facet. |
| MID-043-EX04 | 3 | Describe an event flow that keeps the index in sync and explain how deletions and out-of-order events are handled. |
| MID-043-EX05 | 4 | Tool choice: a 5 000-product shop wants simple name search; another has 5 million with facets and typo tolerance. Choose for each. |

## Solutions
- **EX01** red → {1,3}; shoe → {1,2,3} (assuming docs 1 and 3 contain "red"); result docs 1 and 3.
- **EX02** Tokens become `run`, `shoe`; queries "run" and "SHOE" match. Danger: unrelated words sharing a stem can match.
- **EX03** `bool` with `must: match name`, `filter: [term category, range price lte 200]`, and `aggs.terms` on `category` (keyword).
- **EX04** Outbox → broker → indexer upserts by product id; `ProductDeleted` deletes the document; use the product version as external version so older events are ignored.
- **EX05** 5 000 products with simple search: PostgreSQL full-text (no extra system). 5 million with facets and fuzziness: dedicated engine.

**Outcome 3** is also covered by the lab (events feed the index; reindex documented).
