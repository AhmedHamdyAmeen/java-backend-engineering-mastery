# SRB-003 · Distributed data — Quiz

Outcomes: O1 replication · O2 consensus · O3 quorums · O4 evaluating claims.

**Q01 (O1)** Multi-leader replication mainly adds the problem of: A. Conflict resolution B. No failover C. Single writer bottleneck D. No replication lag
**Q02 (O1)** Asynchronous leader replication risks: A. Slower reads B. Needing quorums C. Losing recent writes on failover D. Higher disk usage
**Q03 (O1)** Leaderless stores keep replicas close using: A. A single primary B. Quorums and repair C. Manual copies D. Cron jobs only
**Q04 (O2)** Raft commits an entry when: A. The leader writes it B. All nodes have it C. One follower acks D. A majority of nodes have it
**Q05 (O2)** A 3-node Raft cluster tolerates: A. Two node failures B. None C. One node failure D. Three node failures
**Q06 (O3)** R + W > N means: A. Read and write sets overlap B. Writes are always fast C. No failures can occur D. Linearizability is guaranteed
**Q07 (O3)** Sloppy quorums can cause: A. Faster consensus B. Smaller clusters C. No hinted handoff D. Stale reads despite R + W > N
**Q08 (O4)** Which model is strongest? A. Eventual B. Linearizable C. Causal D. Monotonic reads
**Q09 (O4)** A Jepsen result applies to: A. All future versions B. Any database C. The tested version and configuration D. Only vendors
**Q10 (O4)** Absence of a Jepsen report means: A. The product is safe B. The product is unsafe C. The product is old D. Safety is unproven, test yourself

## Answers
Q01 A · Q02 C · Q03 B · Q04 D · Q05 C · Q06 A · Q07 D · Q08 B · Q09 C · Q10 D

## Practical part
Scenario quiz plus a short written evaluation of the lab's two datastores. Pass: 70% on the quiz and every claim in the evaluation backed by evidence.
