# MID-040 · Cache consistency — Quiz

Outcomes: O1 stampedes · O2 invalidation races · O3 hot keys · O4 staleness budgets.

**Q01 (O1)** A cache stampede happens when: A. The cache is empty at start B. Many requests miss the same expired key at once C. Redis restarts only D. TTL is infinite
**Q02 (O1)** Which does NOT reduce stampedes? A. Request coalescing B. TTL jitter C. Early refresh D. Identical TTLs on all keys
**Q03 (O1)** A lock around cache rebuilds should also have: A. A timeout B. No expiry C. A bigger TTL D. A second database
**Q04 (O2)** A stale value stays in the cache after a delete because: A. A late reader refilled it with the old row B. Redis ignores deletes C. The TTL was negative D. The database rolled back
**Q05 (O2)** Which order is safer? A. Delete cache, then update database B. Update database, then delete cache C. Update cache only D. Skip the database
**Q06 (O2)** Versioning fixes races by: A. Rejecting writes of older versions into the cache B. Disabling TTL C. Locking the table D. Adding replicas
**Q07 (O3)** A hot key is: A. A key with a long name B. A key taking a disproportionate share of traffic C. A key without TTL D. An encrypted key
**Q08 (O3)** A good mitigation for a hot key: A. Short-lived local cache in each instance B. A longer key name C. More database indexes D. Removing the TTL
**Q09 (O4)** A staleness budget is: A. The maximum memory for a cache B. The maximum age of data you accept for a cached item C. The cache hit ratio D. The key count
**Q10 (O4)** For data with zero staleness tolerance, such as a payment total: A. Cache with a 1-hour TTL B. Cache in the browser C. Read from the source of truth D. Use write-behind

## Answers
Q01 B · Q02 D · Q03 A · Q04 A · Q05 B · Q06 A · Q07 B · Q08 A · Q09 B · Q10 C

## Practical part
Race-condition analysis (`MID-040-EX02`, `EX03`) plus lab `MID-040-LAB1`. Pass: quiz at least 8/10, correct race diagram and fix, and a lab with bounded database load measured.
