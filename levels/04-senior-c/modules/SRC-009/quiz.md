# SRC-009 · Failure-mode analysis — Quiz

Outcomes: O1 dependency mapping and failure domains · O2 FMEA · O3 graceful degradation · O4 failure-injection experiments.

**Q01 (O1)** Which is a hidden dependency? A. The order service B. The orders table C. The load balancer you configured D. DNS or the identity provider
**Q02 (O1)** Blast radius means: A. The size of a server B. How much of the system or how many users a fault affects C. A deploy type D. A monitoring tool
**Q03 (O1)** Which failure is usually hardest to handle? A. A clean crash B. A planned restart C. A slow dependency that exhausts resources D. A rolled-back deploy
**Q04 (O2)** In FMEA, the risk priority is often: A. Likelihood only B. Cost only C. Component count D. Likelihood x impact x detectability rating
**Q05 (O2)** Why include detectability? A. Undetected failures last longer and do more damage B. It lowers the score C. It is optional D. It shortens tables
**Q06 (O2)** FMEA output should be: A. A diagram only B. A ranked list with actions C. A report nobody reads D. A list of blame
**Q07 (O3)** Graceful degradation should: A. Hide errors silently B. Drop data to stay up C. Keep the core journey working and degrade visibly D. Disable checkout
**Q08 (O3)** An unused fallback path: A. Cannot fail B. Is always correct C. Is free D. Tends to rot unless tested
**Q09 (O4)** A failure-injection experiment first needs: A. Production access only B. A hypothesis, limited blast radius, and stop conditions C. A bigger blast radius D. No metrics
**Q10 (O4)** An experiment that finds a weakness is: A. A failure to hide B. A cause for blame C. A success that is recorded and fixed D. Useless

## Answers
Q01 D · Q02 B · Q03 C · Q04 D · Q05 A · Q06 B · Q07 C · Q08 D · Q09 B · Q10 C

## Practical part
Six FMEA exercises `SRC-009-EX01` to `EX06` plus the lab with three experiments run. Pass: quiz at least 8/10, at least five exercises correct, and the lab finds and fixes at least one previously unknown weakness.
