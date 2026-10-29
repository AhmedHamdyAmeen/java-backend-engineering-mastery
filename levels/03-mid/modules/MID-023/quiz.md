# MID-023 · Distributed computing — Quiz (failure scenarios)

Outcomes: O1 fallacies · O2 partial failure · O3 clocks · O4 failure models.

**Q01 (O1)** "The network is reliable" is a fallacy because: A. Packets can be lost, delayed, or duplicated B. Networks never carry data C. Latency is always zero D. Bandwidth is unlimited
**Q02 (O1)** Hard-coding a service IP ignores which fallacy? A. Transport cost is zero B. The network is secure C. Topology does not change D. There is one administrator
**Q03 (O2)** A client call times out. What do you know? A. The operation failed B. The operation succeeded C. The server crashed D. Nothing certain about whether it happened
**Q04 (O2)** Retrying a non-idempotent charge after a timeout risks: A. A double charge B. Lower latency C. A clock jump D. Nothing
**Q05 (O2)** The best defence for safe retries is: A. Longer timeouts only B. Idempotency keys C. Random delays D. Removing logging
**Q06 (O3)** Why can wall-clock timestamps from two nodes not order events? A. Clocks drift and can jump B. Timestamps are text C. Nodes have no clocks D. Time zones differ in Java
**Q07 (O3)** To measure elapsed time within one JVM use: A. `LocalDateTime.now()` B. `System.currentTimeMillis()` C. `new Date()` D. `System.nanoTime()`
**Q08 (O4)** A node stops and never returns: which model? A. Byzantine B. Omission C. Crash D. Timing
**Q09 (O4)** A node sends wrong, conflicting data to different peers: A. Crash B. Byzantine C. Omission D. Clean shutdown
**Q10 (O2)** A failed response (lost reply) after the server did the work is an example of: A. Partial failure B. Total failure C. Clock skew D. Success with no side effects

## Answers
Q01 A · Q02 C · Q03 D · Q04 A · Q05 B · Q06 A · Q07 D · Q08 C · Q09 B · Q10 A

## Practical part
Five exercises `MID-023-EX01` to `EX05` plus the lab. Pass: at least four exercises correct and a lab list that names at least three distinct inconsistencies with their causes.
