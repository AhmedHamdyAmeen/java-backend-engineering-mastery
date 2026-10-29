# SRC-008 · Architectural decomposition — Quiz

Outcomes: O1 split or keep criteria · O2 detecting coupling · O3 merging back · O4 migration and exit criteria.

**Q01 (O1)** A legitimate driver for extracting a service is: A. Fashion B. Fewer repositories C. Evidence of different scaling or team autonomy needs D. Every noun gets one
**Q02 (O1)** A modular monolith is: A. Always a failure B. A valid destination C. Only temporary D. Forbidden
**Q03 (O1)** Conway's law says structure mirrors: A. Database size B. Communication structure C. Language choice D. Server count
**Q04 (O2)** A shared database between services is: A. Hidden strong coupling B. Isolation C. No coupling D. Temporal coupling only
**Q05 (O2)** Co-change coupling is best seen from: A. CPU graphs B. Git history C. Invoices D. Logos
**Q06 (O2)** A dependency-bump commit touching every service should be: A. Counted heavily B. Filtered as noise C. The main result D. Merged into one
**Q07 (O3)** A signal to merge services: A. Independent releases B. Separate data C. Lockstep releases and chatty calls D. Clear team ownership
**Q08 (O3)** Presenting a merge is best framed as: A. Blame B. New evidence and learning C. Failure D. Secret
**Q09 (O4)** Why define exit conditions? A. To stop or revert when evidence says it is not working B. To delay C. To add meetings D. For marketing
**Q10 (O4)** An incremental extraction approach: A. Big bang rewrite B. Delete the old path first C. Strangler with the old path kept until proven D. Freeze development

## Answers
Q01 C · Q02 B · Q03 B · Q04 A · Q05 B · Q06 B · Q07 C · Q08 B · Q09 A · Q10 C

## Practical part
Six boundary exercises `SRC-008-EX01` to `EX06` plus the lab. Pass: quiz at least 8/10, at least five exercises correct, and a boundary recommendation backed by change-coupling data and team considerations, defended against assessor challenges.
