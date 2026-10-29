# MID-032 · Distributed coordination — Quiz

Outcomes: O1 leases and leaders · O2 lock safety and fencing · O3 single-runner jobs.

**Q01 (O1)** Three replicas each run a `@Scheduled` job. By default the job runs: A. Once B. On the leader only C. Never D. Three times
**Q02 (O1)** A lease differs from a plain lock because it: A. Cannot be released B. Expires unless renewed C. Needs no storage D. Is always safe
**Q03 (O1)** Which design avoids needing a lock for a task queue? A. `SKIP LOCKED` claiming B. Sleeping randomly C. One giant transaction D. Disabling retries
**Q04 (O2)** Why is an expired-lease holder dangerous? A. It crashes B. It may not know it lost the lease and keeps writing C. It releases early D. It deletes the lock
**Q05 (O2)** A fencing token is: A. A password B. A random UUID C. A cache key D. An increasing number checked at the resource
**Q06 (O2)** Where must a fencing check live? A. At the resource being written B. Only in the client C. In a log file D. In the load balancer
**Q07 (O2)** A Redis `SET NX PX` lock alone is: A. Enough for correctness B. Proven by Raft C. Fine for efficiency but not for correctness D. Always fenced
**Q08 (O2)** A write with token 7 arrives after token 8 was accepted. The resource should: A. Accept it B. Reject it C. Merge both D. Delete the data
**Q09 (O3)** ShedLock is mainly used to: A. Encrypt data B. Elect a Raft leader C. Replace the database D. Run a scheduled job on one instance at a time
**Q10 (O3)** If `lockAtMostFor` is shorter than the job's runtime: A. Another instance may start while the first runs B. The job runs faster C. Nothing changes D. The lock becomes permanent

## Answers
Q01 D · Q02 B · Q03 A · Q04 B · Q05 D · Q06 A · Q07 C · Q08 B · Q09 D · Q10 A

## Practical part
Six exercises `MID-032-EX01` to `EX06` plus `MID-032-LAB1`. Pass: at least five exercises, 8 of 10 quiz answers, and a paused-instance test with no double-applied change.
