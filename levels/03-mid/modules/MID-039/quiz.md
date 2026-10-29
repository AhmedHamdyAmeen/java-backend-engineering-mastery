# MID-039 · Caching patterns — Quiz

Outcomes: O1 the four patterns and their failures · O2 invalidation by events · O3 write-behind risk.

**Q01 (O1)** In cache-aside, on a miss the: A. Cache loads the data B. Application loads from the database and fills the cache C. Database pushes to the cache D. CDN loads it
**Q02 (O1)** On a write in cache-aside, the usual order is: A. Delete cache, then write database B. Update cache only C. Write database, then delete the cache entry D. Write both in parallel
**Q03 (O1)** If the cache is down in cache-aside: A. Reads fall back to the database B. Reads return empty C. The database is corrupted D. Writes are lost
**Q04 (O1)** Write-through means: A. Write to cache and database synchronously B. Write to cache only C. Write to the database only D. Write later in batches
**Q05 (O1)** Read-through differs from cache-aside because: A. The cache layer loads on a miss B. There is no cache C. It needs a CDN D. It is always faster
**Q06 (O2)** Best way to keep prices fresh across services: A. Long TTL B. Restart the service C. Publish `ProductUpdated` and evict on receipt D. Cache nothing ever
**Q07 (O2)** Why still use a TTL with events? A. It speeds up writes B. Events can be lost, TTL bounds staleness C. It removes the broker D. It is required by Redis
**Q08 (O2)** Why delete rather than update the entry on change? A. The next read loads the freshest data B. Delete is slower C. Update is illegal D. Deletes are never lost
**Q09 (O3)** Main risk of write-behind: A. High memory B. Acknowledged writes can be lost before the flush C. Slow reads D. No batching
**Q10 (O3)** Where is write-behind acceptable? A. Payments B. Orders C. Inventory reservation D. View counters

## Answers
Q01 B · Q02 C · Q03 A · Q04 A · Q05 A · Q06 C · Q07 B · Q08 A · Q09 B · Q10 D

## Practical part
Pattern-choice scenarios (`MID-039-EX03`, `EX04`) plus lab `MID-039-LAB1`. Pass: quiz at least 8/10, correct patterns in the scenarios, and a lab where a price change is visible within one second.
