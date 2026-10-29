# MID-042 · MongoDB — Quiz

Outcomes: O1 embedding vs referencing · O2 indexes and explain · O3 aggregation · O4 transactions · O5 Spring Data MongoDB.

**Q01 (O1)** Embed data when it is: A. Unbounded B. Read together with the parent and bounded C. Shared by many parents D. Huge
**Q02 (O1)** The classic MongoDB modeling mistake: A. Using `_id` B. Unbounded arrays inside a document C. Using indexes D. Using collections
**Q03 (O2)** `COLLSCAN` in `explain` means: A. A collection scan with no usable index B. A fast index lookup C. A transaction D. A shard
**Q04 (O2)** For `find({productId}).sort({createdAt:-1})` the best index is: A. `{ createdAt: 1 }` B. `{ text: 1 }` C. `{ rating: 1 }` D. `{ productId: 1, createdAt: -1 }`
**Q05 (O2)** In `explain("executionStats")`, a healthy query has `totalDocsExamined` that is: A. Much larger than `nReturned` B. Close to `nReturned` C. Always zero D. Negative
**Q06 (O3)** An aggregation pipeline should start with: A. `$group` B. `$sort` on everything C. `$match` D. `$lookup`
**Q07 (O3)** To compute an average rating per product use: A. `$group` with `$avg` B. `$set` C. `$unset` D. `createIndex`
**Q08 (O4)** A single-document update is: A. Not atomic B. Atomic C. Only atomic in a transaction D. Always slow
**Q09 (O4)** A cost of multi-document transactions: A. Free B. Extra latency and locking C. Lost indexes D. No retries
**Q10 (O5)** In Spring Data MongoDB a class is mapped with: A. `@Entity` B. `@Table` C. `@Document` D. `@Repository` only

## Answers
Q01 B · Q02 B · Q03 A · Q04 D · Q05 B · Q06 C · Q07 A · Q08 B · Q09 B · Q10 C

## Practical part
Document-model review (`MID-042-EX06`) plus lab `MID-042-LAB1`. Pass: quiz at least 8/10, a review that names both problems, and a lab with matching indexes and a database-computed summary.
