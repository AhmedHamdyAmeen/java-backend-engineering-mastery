# SRC-007 · Database scaling — Quiz

Outcomes: O1 replicas and lag · O2 scaling options with evidence · O3 shard keys, hot partitions, resharding · O4 managed distributed SQL.

**Q01 (O1)** Read replicas primarily scale: A. Writes B. Storage only C. Reads D. Schema changes
**Q02 (O1)** Read-your-writes after replication requires: A. Reading from a lagging replica B. Routing recent writers to the primary or waiting for the replica position C. Disabling indexes D. Bigger pages
**Q03 (O1)** The right response to growing replica lag is: A. Ignore it B. Disable monitoring C. Alert and fall back to the primary above a threshold D. Add more replicas only
**Q04 (O2)** Reads are 90% of load and CPU is high with write headroom. The best next step: A. Shard by customer B. Replicas and caching C. Switch databases D. Rewrite the service
**Q05 (O2)** Partitioning within one server mainly helps: A. Write capacity beyond the server B. Cross-region failover C. Pruning and retention management D. Eliminating indexes
**Q06 (O3)** A good shard key: A. Has low cardinality B. Is a timestamp C. Is random and unrelated to queries D. Has high cardinality and appears in the main queries
**Q07 (O3)** A time-based shard key causes: A. All new writes to hit the newest shard B. Perfect balance C. No cross-shard queries D. Faster resharding
**Q08 (O3)** Resharding is easier when you use: A. Many logical shards mapped to physical servers B. One huge shard C. Manual scripts only D. No mapping table
**Q09 (O4)** A fair evaluation of distributed SQL uses: A. Vendor slides B. Your workload in a proof of concept C. Popularity D. Cost only
**Q10 (O3)** Hot-partition risk should be: A. Ignored B. Fixed after launch C. Quantified from real data before choosing D. Left to the database

## Answers
Q01 C · Q02 B · Q03 C · Q04 B · Q05 C · Q06 D · Q07 A · Q08 A · Q09 B · Q10 C

## Practical part
Six shard-key and scaling exercises `SRC-007-EX01` to `EX06` plus the lab ADR. Pass: quiz at least 8/10, at least five exercises correct, and an ADR with quantified hot-partition risk and a migration outline.
