# SRC-006 · API and data contracts — Quiz

Outcomes: O1 compatibility policies · O2 consumer impact · O3 schema governance · O4 breaking-change migration.

**Q01 (O1)** Which change is generally backward compatible? A. Removing a field B. Changing a field's type C. Adding an optional field D. Changing a field's units
**Q02 (O1)** Changing a field's meaning but not its type is: A. Safe B. Breaking, although the schema validates C. Forward compatible only D. Irrelevant
**Q03 (O1)** A deprecation policy should define: A. Notice period and sunset date B. Nothing C. Team colors D. Only the version number
**Q04 (O2)** Consumer-driven contract tests show: A. Server CPU B. Network cost C. Which consumer expectations would break D. Developer count
**Q05 (O2)** Unknown consumers are: A. Ignorable B. A risk to reduce by discovery or monitoring C. Proof of safety D. Not possible
**Q06 (O2)** To measure impact of a field change you can use: A. Usage logs and registry subjects B. Coin flips C. Release dates D. Logo size
**Q07 (O3)** Governance that scales relies on: A. Weekly review meetings B. A single approver C. Manual sign-off for every change D. Automated CI checks with review by exception
**Q08 (O3)** Every schema should have: A. An owning team B. No owner C. A secret D. Many owners
**Q09 (O4)** Expand and contract means: A. Remove then add B. Add the new beside the old, migrate, then remove the old C. Freeze all changes D. Duplicate teams
**Q10 (O4)** Before removing an old event you should confirm: A. The release is on Friday B. The code is smaller C. Its consumer usage has reached zero D. The topic name is short

## Answers
Q01 C · Q02 B · Q03 A · Q04 C · Q05 B · Q06 A · Q07 D · Q08 A · Q09 B · Q10 C

## Practical part
Six policy exercises `SRC-006-EX01` to `EX06` plus the lab. Pass: quiz at least 8/10, at least five exercises correct, and a policy and migration plan that names every consumer, the sequence, and the rollback.
