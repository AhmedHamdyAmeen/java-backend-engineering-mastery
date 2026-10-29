# MID-041 · NoSQL fundamentals — Quiz

Outcomes: O1 the four models · O2 query-driven modeling · O3 consistency and scaling.

**Q01 (O1)** Best fit for "customers who bought X also bought": A. Graph B. Key-value C. Wide-column D. Document
**Q02 (O1)** A document store is best when: A. Data is read and written as nested objects B. You need many-hop traversals C. You only need counters D. You need joins everywhere
**Q03 (O1)** A key-value store lookup is by: A. Any field B. Full-text C. The key D. SQL join
**Q04 (O1)** Wide-column stores are designed around: A. Joins B. Known queries and a partition key C. Free-form queries D. Graph traversals
**Q05 (O2)** Query-driven modeling means: A. Shape data from the queries you must serve B. Normalize first, ask later C. Skip design D. Use one table
**Q06 (O2)** A trade-off of query-driven modeling: A. Slower writes always B. Flexibility for new queries is lower C. No indexes D. No scaling
**Q07 (O2)** "Schemaless" really means: A. No structure exists B. The database does not enforce it; the application must C. You cannot change data D. Unlimited joins
**Q08 (O3)** CAP says during a network partition you choose between: A. Speed and cost B. Consistency and availability C. Reads and writes D. SQL and NoSQL
**Q09 (O3)** PACELC adds that, without a partition, you still trade: A. Latency and consistency B. Cost and security C. Memory and disk D. Nothing
**Q10 (O3)** Why do many wide-column stores scale writes well? A. They avoid joins and spread data by partition key B. They use one big node C. They never replicate D. They require locks on every row

## Answers
Q01 A · Q02 A · Q03 C · Q04 B · Q05 A · Q06 B · Q07 B · Q08 B · Q09 A · Q10 A

## Practical part
Lab `MID-041-LAB1` (comparison table of reviews in three models). Pass: quiz at least 8/10 and a lab table with at least five queries.
