# MID-038 · Redis — Exercises and lab

## Lab
### MID-038-LAB1 · Catalog cache
**Outcomes:** 1–4 · **Time:** ~3 h
Cache product details (by id) and category listings in Redis with different TTLs, using a `RedisCacheManager`. Add hit/miss metrics. Run a load test before and after and record hit ratio and p95 latency. Set `maxmemory` and an eviction policy for the Redis container.
**Acceptance:** hit ratio and latency improvement measured under load.

## Exercises (assessment: data-structure selection scenarios)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-038-EX01 | 1 | Choose a Redis structure for each: page-view counter, shopping cart, unique visitors per day, top 10 products, session token. |
| MID-038-EX02 | 1 | Using `redis-cli`, build a leaderboard with three products and read the ranking. |
| MID-038-EX03 | 2 | Design key names for product details, category products, and a "catalog version" that supports invalidation. |
| MID-038-EX04 | 3 | Write a `RedisCacheManager` bean with a 10-minute default TTL and a 1-hour TTL for `categories`. |
| MID-038-EX05 | 4 | Redis restarts with no persistence and holds product cache, sessions, and a pending-email queue. What is lost, and what must move elsewhere? |
| MID-038-EX06 | 4 | Pick `maxmemory-policy` for a pure cache and explain why not `noeviction`. |

## Solutions
- **EX01** Counter: string (`INCR`). Cart: hash. Unique visitors: set (or HyperLogLog if approximate is fine). Top 10: sorted set. Session: string with TTL.
- **EX02** `ZADD board 5 p1 9 p2 2 p3`, then `ZRANGE board 0 -1 REV WITHSCORES` gives p2, p1, p3.
- **EX03** `shop:product:{id}:v1`, `shop:category:{id}:products:v{catalogVersion}`, `shop:catalog:version`. Bumping the version makes old category keys unreachable; they expire by TTL.
- **EX04**
```java
RedisCacheConfiguration base = RedisCacheConfiguration.defaultCacheConfig().entryTtl(Duration.ofMinutes(10));
RedisCacheManager.builder(factory).cacheDefaults(base)
    .withCacheConfiguration("categories", base.entryTtl(Duration.ofHours(1))).build();
```
- **EX05** Cache and sessions are lost (users logged out, cache cold, database spike). The email queue is lost permanently: move it to a durable queue or the database. Redis must not be the only copy.
- **EX06** `allkeys-lru` or `allkeys-lfu`: Redis evicts old entries to make room. `noeviction` rejects writes when full, so the cache stops working.

**Outcomes 2-4** are also checked by the lab (key names, TTLs, memory limit).
