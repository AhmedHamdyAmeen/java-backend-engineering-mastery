# SRA-002 · Long-term system evolution — Quiz

Outcomes: O1 fitness functions · O2 technical roadmaps · O3 managing obsolescence · O4 revising roadmaps.

**Q01 (O1)** Architecture decay is most often caused by: A. Many reasonable local shortcuts adding up B. One bad architect C. Too many tests D. Using Java
**Q02 (O1)** A useful fitness function names: A. Only a tool B. A team slogan C. The quality, measure, threshold, and owner D. Only a dashboard
**Q03 (O1)** To enforce a strict rule on a codebase with existing violations: A. Fail all builds immediately B. Ignore the rule C. Delete old code D. Baseline existing violations and fail only on new ones
**Q04 (O1)** Which quality is best checked from production telemetry or a scheduled job? A. Import structure B. Cost per order C. Banned API use D. Package names
**Q05 (O2)** A transition state should be: A. Stable and valuable on its own B. Incomplete by design C. Identical to the target D. Hidden from stakeholders
**Q06 (O2)** A roadmap checkpoint is: A. A holiday B. A code freeze C. A dated point where evidence decides to continue, adjust, or stop D. A status meeting without decisions
**Q07 (O2)** A roadmap differs from a feature list because it: A. Is shorter B. Links work to outcomes, target state, and assumptions C. Avoids dates D. Has more items
**Q08 (O3)** The main reason to plan upgrades before end of support: A. Vendors require it B. It is cheaper to forget C. Late upgrades become emergencies with no time to test D. Tests run faster
**Q09 (O3)** An obsolescence inventory should cover: A. Only languages B. Every runtime, framework, datastore, and managed service C. Only databases D. Only third-party code
**Q10 (O4)** A vendor announces end of support in 18 months. The best first step is to: A. Append a task to the backlog B. Wait for the deadline C. Identify roadmap items and assumptions affected, then generate options D. Cancel the roadmap

## Answers
Q01 A · Q02 C · Q03 D · Q04 B · Q05 A · Q06 C · Q07 B · Q08 C · Q09 B · Q10 C

## Practical part
Six case exercises `SRA-002-EX01` to `EX06` plus the lab, reviewed as a roadmap and fitness-function set. Pass: at least five of six exercises correct, quiz at least 8/10, and five fitness functions running in CI with an obsolescence calendar covering every runtime, framework, and datastore.
