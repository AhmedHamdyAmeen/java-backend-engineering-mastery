# SRC-015 · Advanced troubleshooting — Quiz

Outcomes: O1 starvation, exhaustion, deadlocks · O2 cascading and metastable failure · O3 hypothesis testing · O4 cross-layer causes.

**Q01 (O3)** Before restarting a misbehaving service you should: A. Capture evidence such as thread dumps B. Delete logs C. Do nothing D. Increase retries
**Q02 (O1)** Low CPU with rising latency most suggests: A. Faster disks B. A cold cache only C. Too many cores D. Threads blocked waiting on something
**Q03 (O1)** Two thread dumps showing the same threads in the same call indicate: A. A stuck call point B. Healthy load C. A GC cycle D. Normal idle
**Q04 (O1)** Connection exhaustion can be caused by: A. Short transactions B. Remote calls inside transactions C. Smaller payloads D. Faster queries
**Q05 (O2)** A metastable failure: A. Ends when the trigger ends B. Only happens in tests C. Persists because the system's own reaction sustains it D. Is caused by hardware only
**Q06 (O2)** Three layers each retrying 3 times can multiply calls by: A. 3 B. 9 C. 27 D. 6
**Q07 (O2)** To break a retry storm you should first: A. Shed load and limit retries B. Restart everything at once C. Add more retries D. Wait silently
**Q08 (O1)** The standard remedy for lock-order deadlocks is: A. Longer transactions B. Random order C. Disabling locks D. A consistent lock order
**Q09 (O4)** Latency spikes with low average CPU in a container may indicate: A. Network cables B. CPU throttling C. A typo D. Too much memory
**Q10 (O3)** Which is the best use of a hypothesis log? A. Record hypotheses, tests, and results so the team stays aligned B. Assigning blame C. Replacing monitoring D. Skipping tests

## Answers
Q01 A · Q02 D · Q03 A · Q04 B · Q05 C · Q06 C · Q07 A · Q08 D · Q09 B · Q10 A

## Practical part
Live troubleshooting simulation (SRC-015 assessment, graduation gate component) plus the three `SRC-015-LAB1` scenarios with logs. Pass: at least 8/10 on the quiz, and each scenario solved with an evidence chain within its time box.
