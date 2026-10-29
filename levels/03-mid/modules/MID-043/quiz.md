# MID-043 · Search systems — Quiz

Outcomes: O1 inverted index and relevance · O2 queries and facets · O3 keeping the index in sync · O4 PostgreSQL vs engine.

**Q01 (O1)** An inverted index maps: A. Documents to words B. Words to the documents containing them C. Users to roles D. Keys to ports
**Q02 (O1)** An analyzer typically does: A. Compress files B. Encrypt text C. Tokenize and normalize text D. Create shards
**Q03 (O1)** Stemming helps match: A. "running" with "run" B. Prices with numbers C. IDs with names D. Dates with times
**Q04 (O2)** Filters in a `bool` query are: A. Scored and slow B. Not scored and cacheable C. Only for text D. Not allowed
**Q05 (O2)** Facets show: A. Typos B. Counts per category alongside results C. Shard sizes D. Event order
**Q06 (O2)** Typo tolerance in a `match` query uses: A. `filter` B. `fuzziness` C. `size` D. `alias`
**Q07 (O3)** Best way to sync products to the index: A. Write both stores in the request B. Nightly manual copy C. Consume `ProductUpdated` events and upsert D. Make search the primary database
**Q08 (O3)** To reindex from scratch with little downtime: A. Delete the index and wait B. Build a new index and switch an alias C. Restart the service D. Disable search
**Q09 (O4)** An advantage of PostgreSQL full-text: A. Better facets than any engine B. No extra system and consistent with the data C. Built-in fuzzy search at scale D. Higher relevance tuning
**Q10 (O4)** A reason to adopt a dedicated engine: A. Fewer systems to run B. Immediate consistency C. Rich analyzers, facets, and scale D. It is the source of truth

## Answers
Q01 B · Q02 C · Q03 A · Q04 B · Q05 B · Q06 B · Q07 C · Q08 B · Q09 B · Q10 C

## Practical part
Lab `MID-043-LAB1` plus a tool-choice scenario (`MID-043-EX05`). Pass: quiz at least 8/10, lab with documented reindex and no dual writes, and justified tool choices.
