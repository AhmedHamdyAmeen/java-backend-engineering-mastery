# SRB-017 · Large migrations — Quiz

Outcomes: O1 phased migration · O2 rollout and comparison · O3 backfills · O4 decommissioning.

**Q01 (O1)** Every migration phase should have: A. A deadline only B. An owner only C. An exit measure and a rollback D. A freeze
**Q02 (O1)** Why prefer many small reversible steps? A. They limit risk and allow early detection B. They are faster C. They avoid planning D. They need no testing
**Q03 (O2)** Shadow traffic means: A. Running at night B. Hiding the migration C. Doubling the users D. Sending a copy of requests to the new path without affecting users
**Q04 (O2)** A shadow path must NOT: A. Log results B. Compare outputs C. Cause side effects such as writes or payments D. Use a flag
**Q05 (O2)** Cut-over should wait until: A. The deadline B. The mismatch rate is below the agreed threshold C. The weekend D. Legacy is deleted
**Q06 (O2)** A migration flag should have: A. No owner B. A remove-by date and owner C. The same name as other flags D. Permanent status
**Q07 (O3)** An idempotent backfill means: A. It runs once only B. It runs fast C. Running a batch twice gives the same result D. It needs no verification
**Q08 (O3)** The backfill is stopped at 60% and must resume. What lets it continue safely? A. Starting over B. Checkpoints and idempotent writes C. Deleting target data D. Disabling constraints
**Q09 (O4)** Evidence that legacy is unused: A. Nobody complained B. The team says so C. Observed zero traffic over a full business cycle D. The code is old
**Q10 (O4)** Decommissioning is complete when: A. The server is off B. The flag is on C. The ticket closes D. Code, flags, alerts, access, and cost items are removed

## Answers
Q01 C · Q02 A · Q03 D · Q04 C · Q05 B · Q06 B · Q07 C · Q08 B · Q09 C · Q10 D

## Practical part
Submit the migration execution report (SRB-017 assessment) and complete `SRB-017-LAB1`. Pass: at least 8/10 on the quiz, a measured mismatch rate below threshold before cut-over, and rollback rehearsal evidence.
