# ARC-037 · Migration strategy — Quiz

Outcomes: O1 cutover approaches · O2 coexistence · O3 data migration · O4 rollback and go/no-go.

**Q01 (O1)** Which approach limits blast radius by moving a few locations first? A. Big bang B. Parallel forever C. Phased by store or region D. Cold restart
**Q02 (O1)** The main cost of a parallel run is: A. Faster delivery B. Running two systems and reconciling their results C. No testing D. Lower accuracy
**Q03 (O1)** A big bang just before the peak season is: A. Preferred B. Lowest risk C. Free D. Risky because failure hits peak revenue and rollback is hard
**Q04 (O2)** During coexistence each data set should have: A. Two masters B. Exactly one master at each phase C. No master D. A random master
**Q05 (O2)** Coexistence bridges should: A. Stay forever B. Never be used C. Have an end date and decommission plan D. Be hidden
**Q06 (O3)** Several trial loads are run to: A. Expose mapping errors, bad data, and timing before cutover B. Save disk space C. Skip validation D. Train the CEO
**Q07 (O3)** Which is a data migration validation check? A. Counts and finance totals reconciled B. Screen color C. Team size D. Release name
**Q08 (O3)** After the last trial extract the old system keeps changing. You need: A. A freeze for six months B. A delta load strategy C. Nothing D. A new project
**Q09 (O4)** A go/no-go criterion should be: A. Measurable and agreed before the event B. Decided on the night C. A feeling D. Set by the vendor
**Q10 (O4)** A rollback plan must handle: A. Only configuration B. Only servers C. Data created in the new system after cutover D. Press releases

## Answers
Q01 C · Q02 B · Q03 D · Q04 B · Q05 C · Q06 A · Q07 A · Q08 B · Q09 A · Q10 C

## Practical part
Migration plan defense of the lab plan plus exercises `ARC-037-EX01` to `EX06`. Pass: quiz at least 8/10, at least five of six exercises correct, and a lab where every cutover step has a rollback and a decision owner.
