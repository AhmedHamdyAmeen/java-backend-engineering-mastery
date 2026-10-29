# MID-030 · Distributed consistency — Quiz

Outcomes: O1 consistency models · O2 CAP and PACELC · O3 choosing and designing.

**Q01 (O1)** Every read sees the latest completed write. This is: A. Eventual consistency B. Causal consistency C. Read-your-writes D. Strong consistency
**Q02 (O1)** A reply must never appear before its question. The needed model is: A. Causal B. Eventual C. Strong only D. None
**Q03 (O1)** After you post a comment you cannot see it, but others can. Missing: A. Causality B. Linearizability for all C. Read-your-writes D. Durability
**Q04 (O2)** CAP's trade-off applies: A. Always B. During a network partition C. Only to SQL databases D. Only to caches
**Q05 (O2)** The "C" in CAP means: A. ACID consistency B. Linearizability C. Constraint checks D. Caching
**Q06 (O2)** PACELC adds, for normal operation, a trade-off between: A. Cost and CPU B. Consistency and disk C. Latency and consistency D. Partitions and clients
**Q07 (O2)** "Our whole system is AP" is: A. Precise B. Misleading; it varies per operation and configuration C. Required by CAP D. Proven by Kafka
**Q08 (O3)** Best model for decrementing the last unit of stock: A. Eventual B. Strong, via a single owner C. None D. Cache first
**Q09 (O3)** Best response for an order finishing asynchronously: A. 200 with final state B. Sleep in the POST C. 202 with a status resource D. Hide the delay
**Q10 (O3)** Which hides eventual consistency badly? A. Showing "pending" B. Returning the created resource C. A status endpoint D. Showing stale data as final

## Answers
Q01 D · Q02 A · Q03 C · Q04 B · Q05 B · Q06 C · Q07 B · Q08 B · Q09 C · Q10 D

## Practical part
Six exercises `MID-030-EX01` to `EX06` plus the consistency-budget lab. Pass: at least five exercises, 8 of 10 quiz answers, and a reviewed table applied to the API.
