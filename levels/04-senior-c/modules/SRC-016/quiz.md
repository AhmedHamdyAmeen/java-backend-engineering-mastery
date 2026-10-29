# SRC-016 · Performance engineering — Quiz

Outcomes: O1 benchmark design · O2 bottleneck removal · O3 CI regression detection · O4 reporting.

**Q01 (O1)** JMH is used to: A. Deploy services B. Measure small Java code paths reliably C. Run database backups D. Format logs
**Q02 (O1)** A benchmark whose result is unused may be: A. Faster B. More accurate C. Optimized away as dead code D. Required by JMH
**Q03 (O1)** Why prefer a constant arrival rate in load tests? A. It is simpler B. It uses less memory C. Closed loops slow down with the system, hiding latency D. It avoids warm-up
**Q04 (O1)** A system benchmark needs: A. Production-like data and workload mix B. Only one request C. No warm-up D. A single average
**Q05 (O2)** The first fix should target: A. The easiest change B. The oldest code C. The most disliked class D. The largest measured share of time
**Q06 (O2)** If a step is 5% of time, eliminating it gains at most: A. 50% B. 5% C. 25% D. 100%
**Q07 (O3)** Regression checks in CI should compare against: A. A baseline with a noise-based tolerance B. A fixed number C. Nothing D. The previous single run only
**Q08 (O3)** Benchmarks in CI should run on: A. Any laptop B. Random hardware C. Consistent dedicated hardware D. Spot instances with varied sizes
**Q09 (O2)** When do you stop optimizing? A. At zero latency B. When the target is met with margin C. After one change D. When bored
**Q10 (O4)** An honest performance report includes: A. Only the best run B. Only the average C. Only a chart without setup D. Setup, repeat runs, uncertainty, and limits

## Answers
Q01 B · Q02 C · Q03 C · Q04 A · Q05 D · Q06 B · Q07 A · Q08 C · Q09 B · Q10 D

## Practical part
Performance report review (SRC-016 assessment): critique a given report and present `SRC-016-LAB1` evidence. Pass: at least 8/10 on the quiz, before/after results with variance, and a CI check that fails on a seeded regression.
