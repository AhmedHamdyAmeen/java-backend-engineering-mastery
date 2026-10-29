# MID-038 · Redis — Lecture scripts

**Video:** 76 min · **Analogy used throughout:** a very fast shared whiteboard in the office: everyone can read and write it, but it is not the official record. Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-038-L01 · Redis in one picture (8 min)
**Goal:** understand what Redis is and how it executes commands.

**Key points**
- Redis is an in-memory data structure server, accessed by key over the network.
- Commands run on a single main thread, one at a time, so each command is atomic.
- Typical uses: cache, counters, rate limiting, sessions, leaderboards, simple queues.
- It is fast because data is in memory, not because it is simple: bad commands can still block everyone.
- Verify version and licensing/fork options (Redis, Valkey) before recording.

**Show:** `redis-cli` session: `SET greeting hello`, `GET greeting`, `EXPIRE greeting 60`, `TTL greeting`.

**Check:** Why is `INCR` safe without a lock? *(Commands run one at a time, so it is atomic.)*

---

## MID-038-L02 · Data structures and their uses (14 min)
**Goal:** pick the right structure for each problem.

**Key points**
- String: a value or counter; `SET`, `GET`, `INCR`, `SET key v EX 60`. Use for cached JSON and counters.
- Hash: field-value map under one key; `HSET`, `HGET`. Use for objects you update field by field.
- Set: unique members; `SADD`, `SISMEMBER`. Use for tags, "who liked this".
- Sorted set: members with a score, ordered; `ZADD`, `ZRANGE`, `ZINCRBY`. Use for leaderboards and time-ordered indexes.
- Expiration applies to the whole key, not to a hash field or set member.

**Show**
| Problem | Structure |
| --- | --- |
| Cached product JSON | String with TTL |
| Cart (field per product) | Hash |
| Users who viewed a product | Set |
| Top-selling products | Sorted set |

**Check:** Which structure gives "top 10 by score" cheaply? *(Sorted set: `ZREVRANGE`/`ZRANGE ... REV`.)*

---

## MID-038-L03 · Key design (8 min)
**Goal:** name keys so they can be found, expired, and invalidated safely.

**Key points**
- Use namespaces with colons: `shop:product:42:v1`.
- Include a version in the key to change formats without clashes.
- Keep keys short but readable; large key sets cost memory.
- Never use `KEYS *` in production; it scans everything and blocks. Use `SCAN` with a match pattern.
- Group related keys (or use a version/tag key) so invalidation does not need scanning.

**Show:** `shop:product:{id}`, `shop:category:{id}:products`, `shop:catalog:version` = 7 (key includes the version, bump to invalidate a family).

**Check:** Why avoid `KEYS *`? *(It is O(n) and blocks the single thread.)*

---

## MID-038-L04 · Redis from Spring (12 min)
**Goal:** use Redis through Spring Data Redis and cache annotations.

**Key points**
- `spring-boot-starter-data-redis` configures a connection factory; `StringRedisTemplate` handles strings.
- `RedisTemplate` needs serializers; prefer JSON over Java serialization.
- Enable caching with `@EnableCaching`, define a `RedisCacheManager` with per-cache TTL.
- `@Cacheable` fills the cache, `@CacheEvict` removes entries, `@CachePut` updates.
- Annotations work through proxies: a self-call inside the same class bypasses the cache.

**Show**
```java
@Cacheable(cacheNames = "products", key = "#id")
public ProductDto findProduct(long id) { return repo.load(id); }

RedisCacheConfiguration cfg = RedisCacheConfiguration.defaultCacheConfig()
    .entryTtl(Duration.ofMinutes(10)).disableCachingNullValues();
```

**Check:** Why might `@Cacheable` not work on a method called from the same class? *(The proxy is bypassed.)*

---

## MID-038-L05 · Persistence, memory, and eviction (10 min)
**Goal:** know what survives a restart and what happens when memory is full.

**Key points**
- RDB: periodic snapshots; fast restart, may lose the last minutes.
- AOF: log of writes, with `fsync` policies (every second, always); less loss, bigger files.
- No persistence is valid for a pure cache. Replication does not replace backups, and failover can lose recent writes.
- Set `maxmemory` and an eviction policy (`allkeys-lru`, `allkeys-lfu`, `volatile-*`, or `noeviction`).
- `noeviction` makes writes fail when full; a cache usually wants an `allkeys-*` policy.

**Show:** config lines `maxmemory 512mb`, `maxmemory-policy allkeys-lfu`, `appendonly yes`, `appendfsync everysec`.

**Check:** If Redis is the only copy of an order and the node dies, what is lost? *(Anything not yet persisted or replicated: possibly the order. Never use it as the only copy.)*

---

## MID-038-L06 · Demo: a leaderboard with sorted sets (12 min)
**Goal:** build a "top products this week" board. Prepares the data-structure selection scenarios.

**Steps**
1. Create key `shop:top:week:2026-W44` and record sales with `ZINCRBY key 1 productId`.
2. Read the top 10 with `ZRANGE key 0 9 REV WITHSCORES`.
3. Wrap it in a Spring `StringRedisTemplate.opsForZSet()` service.
4. Set `EXPIRE` of two weeks so old boards disappear.
5. **Planned mistake:** store the board as a JSON string and rewrite it on each sale; two concurrent sales overwrite each other. Fix: `ZINCRBY`, which is atomic.
6. Show rank lookup with `ZREVRANK`.

**Check:** Why is `ZINCRBY` better than read-modify-write? *(It is atomic; no lost updates.)*

---

## MID-038-L07 · Demo: caching product details with `@Cacheable` (12 min)
**Goal:** cache product details in Redis with a TTL and metrics. Prepares MID-038-LAB1.

**Steps**
1. Add the Redis starter and a `RedisCacheManager` with a 10-minute TTL for `products`.
2. Annotate `findProduct` with `@Cacheable` and the update method with `@CacheEvict`.
3. Enable cache statistics and read hits/misses in Micrometer (verify the metric names for your Spring Boot version).
4. Run a load test; compare latency with and without the cache.
5. **Planned mistake:** cache a `Product` entity that is not `Serializable` and uses Java serialization; it fails or breaks on a class change. Fix: cache a small DTO with JSON serialization.
6. Show the keys with `SCAN 0 MATCH products::*`.

**Check:** Which operation removes a stale product when its price changes? *(`@CacheEvict`, or event-based invalidation in MID-039.)*
