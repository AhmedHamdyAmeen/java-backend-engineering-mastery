# MID-037 · Caching fundamentals — Quiz

Outcomes: O1 where caches sit · O2 local vs distributed · O3 hit ratio, eviction, TTL · O4 should we cache.

**Q01 (O1)** Which cache layer avoids sending any request to the server? A. Browser cache B. Application cache C. Database buffer pool D. Gateway cache
**Q02 (O1)** A CDN mainly saves: A. Database CPU only B. Trips to the origin for public content C. Password hashing D. Compile time
**Q03 (O2)** A downside of a local cache with several instances: A. Slow network hops B. Copies can differ between instances C. It needs Redis D. It cannot expire entries
**Q04 (O2)** A benefit of a distributed cache: A. Zero latency B. One shared copy that survives app restarts C. No memory use D. No invalidation needed
**Q05 (O3)** 800 hits and 200 misses give a hit ratio of: A. 20% B. 25% C. 80% D. 100%
**Q06 (O3)** Two caches have a 90% hit ratio. What decides which is more valuable? A. The cost saved per hit B. The cache name C. The key length D. The language
**Q07 (O3)** LRU evicts: A. The most recently used entry B. The least frequently used entry C. The least recently used entry D. A random entry always
**Q08 (O3)** TTL provides: A. An upper bound on staleness B. Guaranteed freshness C. Higher hit ratio always D. Persistence
**Q09 (O4)** Which data is a poor candidate for a global shared cache? A. Category tree B. Per-user cart contents C. Static policy pages D. Product images
**Q10 (O4)** Before adding a cache you should first: A. Measure access and cost data B. Choose Redis C. Set TTL to one day D. Remove the database index

## Answers
Q01 A · Q02 B · Q03 B · Q04 B · Q05 C · Q06 A · Q07 C · Q08 A · Q09 B · Q10 A

## Practical part
Lab `MID-037-LAB1` (three cache candidates backed by access data). Pass: quiz at least 8/10 and a lab where every decision cites measured numbers.
