# MID-038 · Redis — Quiz

Outcomes: O1 data structures · O2 key design · O3 Redis from Spring · O4 persistence and memory.

**Q01 (O1)** Best structure for a leaderboard: A. String B. Hash C. Set D. Sorted set
**Q02 (O1)** Best structure to hold a cart with one field per product: A. Hash B. Sorted set C. List only D. Pub/sub
**Q03 (O1)** Which command is atomic for counting? A. `GET` then `SET` B. `INCR` C. `KEYS` D. `SCAN`
**Q04 (O2)** Which key is best designed? A. `42` B. `product` C. `shop:product:42:v1` D. `my key!`
**Q05 (O2)** To find keys safely in production use: A. `KEYS *` B. `SCAN` with `MATCH` C. `FLUSHALL` D. `MONITOR`
**Q06 (O3)** `@Cacheable` on a method fails to cache when: A. It is called from the same class (proxy bypassed) B. It returns a DTO C. TTL is set D. Redis is running
**Q07 (O3)** Which removes a cache entry? A. `@Cacheable` B. `@CachePut` C. `@Async` D. `@CacheEvict`
**Q08 (O3)** Per-cache TTL in Spring is configured in: A. `RedisCacheManager` configuration B. `pom.xml` C. A controller D. A browser header
**Q09 (O4)** RDB persistence is: A. A log of every write B. Periodic snapshots, so recent writes can be lost C. Replication D. Encryption
**Q10 (O4)** For a pure cache, memory policy should typically be: A. `noeviction` B. No limit C. `allkeys-lru` or `allkeys-lfu` D. Delete the database

## Answers
Q01 D · Q02 A · Q03 B · Q04 C · Q05 B · Q06 A · Q07 D · Q08 A · Q09 B · Q10 C

## Practical part
Structure-selection scenarios (`MID-038-EX01`, `EX05`) plus lab `MID-038-LAB1`. Pass: quiz at least 8/10, correct structures for all scenarios, and a lab with measured hit ratio and latency.
