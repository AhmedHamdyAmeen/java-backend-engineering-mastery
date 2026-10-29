# SRC-005 · Performance modeling — Quiz

Outcomes: O1 latency budgets · O2 Little's Law · O3 queueing near saturation · O4 finding the bottleneck.

**Q01 (O1)** Sequential calls in a budget: A. Take the maximum B. Add up C. Are free D. Cancel out
**Q02 (O1)** Parallel calls contribute to latency as: A. Their sum B. Zero C. Their average D. The slowest one
**Q03 (O1)** A budget should be based on: A. Averages B. The best run C. p99 D. Guesswork
**Q04 (O2)** Little's Law is: A. L = lambda x W B. L = lambda / W C. L = W / lambda D. L = lambda + W
**Q05 (O2)** 400 requests/s at 0.25 s each means about how many in flight? A. 1,600 B. 100 C. 10 D. 400
**Q06 (O3)** Near saturation, waiting time: A. Stays flat B. Falls C. Grows steeply D. Is zero
**Q07 (O3)** A protection against queue-driven latency: A. Unbounded queues B. Bounded queues and load shedding C. Longer timeouts only D. Ignoring it
**Q08 (O3)** With 10 parallel calls each slow 1% of the time, requests hitting a slow call are about: A. 0.1% B. 1% C. 10% D. 50%
**Q09 (O4)** The bottleneck candidate on paper is the resource with: A. Lowest utilization B. Highest utilization C. Most code D. Most logs
**Q10 (O4)** After a model predicts a bottleneck, you should: A. Trust it B. Skip testing C. Delete the model D. Confirm with a load test and compare

## Answers
Q01 B · Q02 D · Q03 C · Q04 A · Q05 B · Q06 C · Q07 B · Q08 C · Q09 B · Q10 D

## Practical part
Six modeling problems `SRC-005-EX01` to `EX06` plus the lab. Pass: quiz at least 8/10, at least five problems correct, and a model within 20% of the load-test measurement or an explained discrepancy.
