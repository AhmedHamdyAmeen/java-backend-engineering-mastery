# MID-028 · Apache Kafka — Quiz (partitioning and ordering)

Outcomes: O1 log model · O2 keys and ordering · O3 groups and offsets · O4 Spring and error handling · O5 producer durability.

**Q01 (O1)** In Kafka, a consumed record is: A. Deleted immediately B. Moved to a queue C. Kept until retention expires D. Copied to a database
**Q02 (O1)** Ordering is guaranteed: A. Across the whole topic B. Within a partition C. Across all topics D. Never
**Q03 (O2)** To keep all events of an order in order, key by: A. A random UUID per event B. The timestamp C. A null key D. The order ID
**Q04 (O2)** A null key means: A. Records are spread without per-entity ordering B. Records go to partition 0 only C. The send fails D. All consumers get it twice
**Q05 (O3)** Two groups subscribe to one topic. Each group gets: A. Half the records B. Only new records C. Every record D. Nothing until they merge
**Q06 (O3)** Within one group, a partition is read by: A. Every member B. At most one member C. Exactly three members D. A random member each time
**Q07 (O3)** Committing offsets before processing risks: A. Duplicates only B. Slower reads C. Disk growth D. Message loss on a crash
**Q08 (O4)** After retries are exhausted, a failed record is typically sent to: A. The same partition again B. A dead-letter topic C. The producer D. The offsets topic
**Q09 (O5)** `acks=all` makes the leader wait for: A. The consumer B. No replicas C. All in-sync replicas D. The next record
**Q10 (O5)** The idempotent producer helps prevent: A. Consumer lag B. Duplicates caused by producer retries C. Rebalances D. Large messages

## Answers
Q01 C · Q02 B · Q03 D · Q04 A · Q05 C · Q06 B · Q07 D · Q08 B · Q09 C · Q10 B

## Practical part
Six exercises `MID-028-EX01` to `EX06` plus the lab. Pass: at least five exercises correct, per-order ordering demonstrated, no loss on consumer restart, and a poison record found in the DLT.
