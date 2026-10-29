# MID-008 · Performance profiling — Quiz

Outcomes: O1 JFR and JMC · O2 flame graphs · O3 thread dumps · O4 heap dumps · O5 measurement loop.

**Q01 (O5)** The correct loop is: A. Guess, change many things, ship B. Measure, hypothesize, change one thing, re-measure C. Re-measure only D. Optimize first, measure later
**Q02 (O1)** JFR is notable for: A. Being a paid tool only B. Needing the app stopped C. Low overhead and built into the JVM D. Only working on Windows
**Q03 (O1)** Command to start JFR on a live process: A. `jstat -gc` B. `javap -c` C. `java -version` D. `jcmd <pid> JFR.start`
**Q04 (O1)** First place to look in JMC: A. Automated Analysis B. The `.class` files C. The source repository D. The OS registry
**Q05 (O2)** In a flame graph, frame width shows: A. Time order B. Share of samples C. Memory size D. Thread count
**Q06 (O2)** A wide frame at the top of a stack means: A. Cold code B. The GC ran C. A hot method D. A deadlock
**Q07 (O3)** Many threads BLOCKED on the same monitor indicates: A. Idle CPU B. A full disk C. A GC bug D. Lock contention
**Q08 (O3)** Why take several thread dumps? A. To see what is stuck versus moving B. To slow the app C. To compress logs D. To fill disk
**Q09 (O4)** Retained size of an object is: A. Its header size B. Its shallow size C. Memory freed if it were removed D. Its class file size
**Q10 (O4)** To explain why a leaked object stays alive, use: A. Path to GC roots B. `javap` C. `ping` D. The branch name

## Answers
Q01 B · Q02 C · Q03 D · Q04 A · Q05 B · Q06 C · Q07 D · Q08 A · Q09 C · Q10 A

## Practical part
Six exercises `MID-008-EX01` to `EX06` including an unseen-recording investigation, plus the lab investigation log. Pass: at least five exercises correct and a log showing evidence, one change per iteration, and before/after numbers for both planted problems.
