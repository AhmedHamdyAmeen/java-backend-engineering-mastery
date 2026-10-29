# MID-005 · Concurrent collections — Quiz

Outcomes: O1 `ConcurrentHashMap` · O2 blocking queues · O3 copy-on-write.

**Q01 (O1)** Why is `get` then `put` on a synchronized map unsafe? A. The map is slow B. Keys are lost C. Maps cannot hold ints D. The two calls are not atomic together
**Q02 (O1)** Which call atomically counts occurrences? A. `merge(k, 1, Integer::sum)` B. `get` then `put` C. `containsKey` then `put` D. `size()`
**Q03 (O1)** `ConcurrentHashMap` does not allow: A. String keys B. `null` values C. Integer values D. Iteration
**Q04 (O1)** Inside a `compute` function you should: A. Call `map.put` on the same map B. Sleep for a second C. Keep work short and not modify the map D. Open a database transaction
**Q05 (O2)** `BlockingQueue.put` on a full queue: A. Throws at once B. Drops the item C. Grows the queue D. Blocks until space is free
**Q06 (O2)** Which gives backpressure? A. Bounded `ArrayBlockingQueue` B. Unbounded `LinkedBlockingQueue` C. `ArrayList` D. `HashMap`
**Q07 (O2)** A common way to stop consumers cleanly is: A. `System.exit` B. A poison pill per consumer C. Deleting the queue D. Ignoring them
**Q08 (O2)** An unbounded queue under a fast producer risks: A. Deadlock only B. Faster consumers C. Out of memory D. Lost visibility
**Q09 (O3)** Copy-on-write best fits: A. A large list written constantly B. A small, read-mostly list C. A queue D. A cache with eviction
**Q10 (O3)** A `CopyOnWriteArrayList` iterator: A. Reflects later writes B. Locks the list C. Allows `remove` D. Iterates a snapshot

## Answers
Q01 D · Q02 A · Q03 B · Q04 C · Q05 D · Q06 A · Q07 B · Q08 C · Q09 B · Q10 D

## Practical part
Four exercises `MID-005-EX01` to `EX04` plus the lab. Pass: at least three exercises correct and the lab showing backpressure with no lost events.
