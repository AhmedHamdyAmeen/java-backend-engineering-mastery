# MID-040 · Cache consistency — Lecture scripts

**Video:** 50 min · **Analogy used throughout:** a crowd at a shop door at opening time, and a price tag that was changed while someone was already walking to the shelf. Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-040-L01 · Stampedes (10 min)
**Goal:** explain a cache stampede and the three standard defences.

**Key points**
- A stampede: a hot key expires and many requests miss at once, all hitting the database for the same row.
- Locking: only one request rebuilds; the others wait or serve the old value.
- Request coalescing (single flight): concurrent loads of one key share one call (Caffeine `LoadingCache` does this per instance).
- Early refresh: refresh before expiry (`refreshAfterWrite`) or add random jitter to TTLs.
- Per-instance coalescing still allows one load per instance; use a distributed lock for stronger protection.

**Show:** timeline: 500 requests at 12:00:00 when `product:7` expires; with a lock, 1 database query instead of 500.

**Check:** Name two ways to avoid a stampede. *(Locking/coalescing, early refresh, TTL jitter.)*

---

## MID-040-L02 · Invalidation races (12 min)
**Goal:** find a race that leaves stale data and fix it.

**Key points**
- Race: reader A misses and reads the old row; writer B updates the row and deletes the key; A then writes the old value to the cache. Stale until TTL.
- Fix 1: delete after write (database first), plus a short TTL.
- Fix 2: versioning: store the row version with the value; only overwrite if the version is newer.
- Fix 3: delayed double delete: delete again after a short pause (reduces but does not eliminate the race).
- "It is rare" is not an argument: at scale rare happens daily.

**Show**
| Step | Reader A | Writer B |
| --- | --- | --- |
| 1 | cache miss, reads price 10 | |
| 2 | | updates to 12, deletes key |
| 3 | writes 10 to cache | |

Fix: A writes only if its version (1) is newer than what is cached; the cache stores version 2 or nothing.

**Check:** Why does a plain delete not prevent this race? *(The late reader refills the cache with the old value after the delete.)*

---

## MID-040-L03 · Hot keys (8 min)
**Goal:** detect and mitigate a key that takes a disproportionate share of traffic.

**Key points**
- A hot key: one product during a flash sale. A Redis node (or one instance) serving it becomes the bottleneck.
- Detect: per-key access counts, `redis-cli --hotkeys` (needs an LFU policy; verify), or metrics from the client.
- Mitigate: local L1 cache with short TTL in each instance, replicate the key under several names (`product:7#1..#4`) and read at random, or serve through CDN.
- Combine with stampede protection: a hot key expiring is the worst case.

**Show:** read path: Caffeine (2 s TTL) → Redis → database, so 20 instances send at most 10 requests per 20 s to Redis for that key.

**Check:** How does a short-lived local cache help with a hot key? *(Most reads never reach Redis.)*

---

## MID-040-L04 · Staleness budgets (8 min)
**Goal:** state how stale each cached item may be.

**Key points**
- Every cached item gets an explicit tolerance agreed with the business: "category list: 1 h", "price: 1 s", "stock shown: 30 s, checked at checkout".
- The TTL and invalidation design follow from the number.
- Record it next to the cache definition, and monitor the real staleness (age of served entries).
- Where tolerance is zero (checkout total, payment), do not cache; read the source of truth.

**Show:** table: item, owner, tolerance, mechanism (TTL, event + TTL, none).

**Check:** Where does the tolerance for a price come from? *(The business decision; engineering then picks a mechanism that meets it.)*

---

## MID-040-L05 · Demo: a stampede after cache expiry, then the fix (12 min)
**Goal:** reproduce a stampede and fix it. Prepares MID-040-LAB1.

**Steps**
1. Cache `product:7` with a 10 s TTL; run a load test of 200 concurrent readers.
2. Count database queries at expiry: a spike to about 200 identical queries.
3. Fix 1: a per-key lock (one loader; the rest wait or serve the stale value) or Caffeine `LoadingCache`; show 1 query.
4. Fix 2: add random jitter of ±20% to TTLs and early refresh.
5. **Planned mistake:** the lock has no timeout and the loader fails; every request waits forever. Fix: lock timeout, and on timeout serve the stale value or fail fast.
6. Show the database query count as a flat line during expiry.

**Check:** Why must the lock have a timeout? *(A failed loader would block all waiters.)*
