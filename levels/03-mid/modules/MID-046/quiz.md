# MID-046 · Performance testing — Quiz

Outcomes: O1 test kinds · O2 k6 scenarios and workloads · O3 percentiles and coordinated omission · O4 finding the bottleneck.

**Q01 (O1)** Which test finds slow leaks? A. Spike B. Load C. Soak D. Smoke
**Q02 (O1)** A spike test simulates: A. Steady use for hours B. A sudden jump in traffic C. A single user D. A database restore
**Q03 (O2)** In k6, thresholds are used to: A. Add think time B. Generate data C. Create users D. Fail the run when a limit is broken
**Q04 (O2)** Think time (`sleep`) is added because: A. Real users pause between actions B. The server needs rest C. It reduces errors D. k6 requires it
**Q05 (O2)** For public web traffic the better model is: A. Closed with few users B. A single thread C. Open (arrival-rate) D. Random sleep only
**Q06 (O3)** Average latency is a poor summary because: A. It is hard to compute B. It hides the slow tail C. It is always lower than the median D. Tools cannot show it
**Q07 (O3)** Coordinated omission means: A. A closed-loop tool stops sending during a stall and under-records slow requests B. Skipping failed tests C. Omitting graphs D. Tests run in parallel
**Q08 (O3)** Percentiles from several machines should be: A. Averaged B. Added C. Combined from histograms D. Ignored
**Q09 (O4)** After finding a bottleneck you should: A. Change five settings at once B. Change one thing and retest C. Stop testing D. Restart the load generator only
**Q10 (O4)** The load generator should run: A. On the same machine as the system under test B. Inside the database C. On the developer laptop only D. On a separate machine

## Answers
Q01 C · Q02 B · Q03 D · Q04 A · Q05 C · Q06 B · Q07 A · Q08 C · Q09 B · Q10 D

## Practical part
Seven exercises `MID-046-EX01` to `EX07` plus the load, spike, and soak lab. Pass: at least five exercises and a report with percentiles, graphs, and evidence of the first bottleneck.
