# MID-037 · Caching fundamentals — Lecture scripts

**Video:** 44 min · **Analogy used throughout:** a notepad on the desk beside the filing cabinet: quick to read, but it can be out of date. Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-037-L01 · Why and where to cache (10 min)
**Goal:** know the layers where a cache can sit and what each one saves.

**Key points**
- A cache keeps a copy of an expensive result close to the caller. It trades freshness for speed and load.
- Layers: browser/client (no request at all), CDN (no trip to origin), gateway (no call to the service), application (no database call), database (buffer pool, query cache).
- The closer to the user, the more you save, and the harder invalidation becomes.
- Cache only data that is read often, changes rarely, and is costly to produce.

**Show:** a request path diagram: browser → CDN → gateway → Shop catalog service → Redis/Caffeine → PostgreSQL, each hop labelled with what a hit there avoids.

**Check:** Which layer saves the most work when it hits? *(The one closest to the user, e.g. the browser: no request is made.)*

---

## MID-037-L02 · Local vs distributed caches (8 min)
**Goal:** choose between an in-process cache and a shared one.

**Key points**
- Local (Caffeine): lives in the JVM heap, nanosecond access, no network. Each instance has its own copy.
- Distributed (Redis): one shared copy, network hop (about a millisecond), survives app restarts.
- Local caches drift between instances; invalidating all of them needs a broadcast.
- Common combo: small local cache (L1) in front of Redis (L2) for the hottest keys.

**Show**
| | Local | Distributed |
| --- | --- | --- |
| Latency | ns | ~1 ms |
| Consistency across instances | weak | strong-ish |
| Memory | app heap | separate service |

**Check:** Why can two Shop instances return different prices from local caches? *(Each holds its own copy, expired or refreshed at different times.)*

---

## MID-037-L03 · Hit ratio and what it hides (8 min)
**Goal:** read hit ratio correctly.

**Key points**
- Hit ratio = hits / (hits + misses). Aim depends on cost of a miss, not a magic number.
- A high ratio can hide a few very expensive misses or a flood of tiny cheap hits.
- Look at it per cache and per key group, plus miss latency and load on the database.
- A cold start has a 0% ratio; measure after warm-up.
- A hit ratio says nothing about stale data served.

**Show:** two caches both at 90%: one saves 1 ms per hit, the other saves 800 ms; the second is worth far more.

**Check:** Does a 99% hit ratio prove the cache is correct? *(No; it can be serving stale data.)*

---

## MID-037-L04 · Eviction and TTL (8 min)
**Goal:** explain how a full cache decides what to drop and how entries expire.

**Key points**
- Eviction applies when memory or size is full: LRU drops the least recently used, LFU the least frequently used.
- LFU protects popular items from one-time scans; LRU adapts faster to changing demand.
- TTL (time to live) removes an entry after a fixed time regardless of use; it bounds staleness.
- Add random jitter to TTLs so entries do not all expire together (see MID-040).

**Show:** a 3-slot cache with accesses A B C A D: LRU evicts B; LFU evicts B or C (count 1), keeps A (count 2).

**Check:** What does TTL guarantee that eviction does not? *(An upper bound on how old an entry can be.)*

---

## MID-037-L05 · Demo: a local Caffeine cache with metrics (10 min)
**Goal:** add a Caffeine cache to a Shop endpoint and read its stats. Prepares MID-037-LAB1.

**Steps**
1. Add the Caffeine dependency and build a `Cache<Long, ProductDto>` with `maximumSize(1000)`, `expireAfterWrite(5, MINUTES)`, and `recordStats()`.
2. Wrap `findProduct(id)`: `cache.get(id, this::loadFromDb)`.
3. Expose `cache.stats()` through Micrometer (hit count, miss count, load time).
4. Generate load with a small script; show the hit ratio rising after warm-up.
5. **Planned mistake:** cache the per-customer discounted price by product id only; a second customer sees the first customer's price. Fix: cache the shared base price and apply the discount afterwards, or include the customer tier in the key.
6. Verify Caffeine version and Micrometer binding names before recording.

**Check:** Why is `recordStats()` needed? *(Without it the cache reports no hit or miss counts.)*
