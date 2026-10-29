# MID-039 · Caching patterns — Lecture scripts

**Video:** 50 min · **Analogy used throughout:** a library's reserve shelf: who fetches the book, who updates the shelf, and what happens when the main stack changes. Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-039-L01 · Cache-aside (10 min)
**Goal:** implement the most common pattern and know how it fails.

**Key points**
- The application owns the logic: read the cache; on a miss read the database, then fill the cache.
- On write: update the database first, then delete (not update) the cache entry.
- Failure: if the cache is down, reads fall through to the database (slower, still correct). If the delete fails, stale data stays until TTL.
- Simple and robust; the cost is repeated code and a miss penalty on first read.

**Show**
```java
ProductDto get(long id) {
    var hit = cache.get(key(id));
    if (hit != null) return hit;
    var p = repo.load(id);
    cache.put(key(id), p, ttl);
    return p;
}
void update(Product p) { repo.save(p); cache.delete(key(p.id())); }
```

**Check:** On a write, which first: database or cache delete? *(Database, then delete the cache entry.)*

---

## MID-039-L02 · Read-through and write-through (10 min)
**Goal:** know the patterns where the cache layer loads and writes data itself.

**Key points**
- Read-through: the caller asks the cache; the cache loads from the database on a miss (Caffeine `LoadingCache`, Spring `@Cacheable` behave like this).
- Write-through: a write goes to the cache and the database synchronously, in one operation.
- Benefit: one code path and a cache that is always up to date after writes.
- Failure: write-through is as slow as the slower store and needs a plan if one write fails; the two stores can diverge without a transaction.

**Show:** diagram: app → cache layer → database for both read and write; compare to cache-aside where the app talks to both.

**Check:** Who loads data on a miss in read-through? *(The cache layer, not the caller.)*

---

## MID-039-L03 · Write-behind (8 min)
**Goal:** understand why write-behind is risky and when it is acceptable.

**Key points**
- Write-behind: write to the cache, return immediately, persist to the database later in batches.
- Gains: very fast writes, batching, absorbs spikes.
- Risk: if the cache or node dies before the flush, the writes are lost; ordering and failures become hard.
- Acceptable only for data you can lose or rebuild: view counters, last-seen timestamps, analytics. Never for orders or payments.

**Show:** timeline: write at 10:00:00 acknowledged, flush at 10:00:05, crash at 10:00:03: write lost.

**Check:** Why not use write-behind for orders? *(An acknowledged order could be lost before it reaches the database.)*

---

## MID-039-L04 · Invalidation strategies (10 min)
**Goal:** choose how entries stop being stale.

**Key points**
- TTL only: simple, but data is wrong for up to the TTL; unacceptable for prices.
- Explicit invalidation on write: delete the key in the same service that writes.
- Event-driven: the owner publishes `ProductUpdated`; every cache subscriber evicts or refreshes. Works across services.
- Best practice: events plus a TTL as a safety net for lost events.
- Deleting is safer than updating the cache: the next read loads the freshest data.

**Show**
| Strategy | Staleness | Cost |
| --- | --- | --- |
| TTL only | up to TTL | none |
| Delete on write | tiny | coupling |
| Event + TTL | seconds | broker |

**Check:** Why keep a TTL when you have events? *(Events can be lost; the TTL bounds the damage.)*

---

## MID-039-L05 · Demo: event-driven invalidation from `ProductUpdated` (12 min)
**Goal:** evict cached products when the catalog service publishes `ProductUpdated`. Prepares MID-039-LAB1.

**Steps**
1. The catalog service saves the product and publishes `ProductUpdated{productId, version}` after the transaction commits (use the outbox pattern from the messaging phase).
2. The cache service consumes the event and calls `cache.evict("products", productId)`.
3. Update a price and show the new price returned within one second.
4. **Planned mistake:** the handler evicts the cache before the database commit; a concurrent read re-caches the old row. Fix: publish after commit and evict after the commit.
5. Make the consumer idempotent (evicting twice is harmless) and add a 10-minute TTL as a safety net.

**Check:** Why publish only after commit? *(Otherwise readers can reload the old data and re-fill the cache.)*
