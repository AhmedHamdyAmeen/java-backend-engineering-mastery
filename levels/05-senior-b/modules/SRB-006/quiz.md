# SRB-006 · Large-scale messaging — Quiz

Outcomes: O1 partitions · O2 lag · O3 rebalancing · O4 backpressure · O5 capacity and governance.

**Q01 (O1)** Max active consumers in a group per topic equals: A. Number of partitions B. Number of topics C. Number of keys D. Number of brokers
**Q02 (O1)** Same key means: A. Random partition B. Different brokers C. Same partition and ordered D. No ordering
**Q03 (O1)** Sizing partitions only for today risks: A. Over-ordering B. Hitting limits with no easy change C. Lower storage D. No lag
**Q04 (O2)** Best lag metric for users: A. Disk usage B. CPU C. Topic count D. Time lag
**Q05 (O2)** A lag alert should include: A. Only a number B. Only a dashboard C. An action plan D. No owner
**Q06 (O3)** Cooperative rebalancing: A. Moves only needed partitions B. Stops all consumers C. Removes partitions D. Deletes offsets
**Q07 (O3)** Static membership helps: A. Faster producers B. Schema changes C. Compaction D. Restarts without rebalances
**Q08 (O4)** Backpressure is: A. Extra memory B. A signal to slow upstream C. A retry loop D. A topic type
**Q09 (O4)** Unbounded queues: A. Prevent overload B. Reduce latency C. Hide overload D. Replace partitions
**Q10 (O5)** Storage grows with rate, retention and: A. Consumer count B. Key length only C. Number of teams D. Replication factor

## Answers
Q01 A · Q02 C · Q03 B · Q04 D · Q05 C · Q06 A · Q07 D · Q08 B · Q09 C · Q10 D

## Practical part
Design review of the lab's feed design with load test results. Pass: 70% on the quiz and catch-up time within target.
