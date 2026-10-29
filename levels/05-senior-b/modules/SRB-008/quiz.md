# SRB-008 · Architecture migration — Quiz

Outcomes: O1 strangler · O2 branch by abstraction · O3 dual writes · O4 data migration · O5 rollback and exit.

**Q01 (O1)** The strangler pattern routes: A. Requests gradually to the new system B. All traffic at once C. Only internal traffic D. Nothing
**Q02 (O1)** Extract first: A. The hardest part B. Everything C. A bounded, valuable, lower-risk piece D. The database
**Q03 (O1)** Big-bang rewrites fail partly because: A. Teams are too fast B. The legacy keeps changing C. Customers want it D. Tests are too good
**Q04 (O2)** Branch by abstraction uses: A. A long-lived branch B. A database copy C. A cron job D. An interface with two implementations
**Q05 (O3)** Dual writes cause: A. Atomicity B. Faster writes C. Drift between systems D. Less code
**Q06 (O3)** An alternative to dual writes is: A. Outbox with events B. Two retries C. Manual updates D. Ignoring failures
**Q07 (O4)** During cut-over the number of writers is: A. Two B. Three C. None D. One
**Q08 (O4)** Verification of migrated data uses: A. Opinion B. Counts, checksums, sampling C. Logs only D. Nothing
**Q09 (O5)** Each step needs: A. No rollback B. A longer weekend C. A tested rollback D. A new team
**Q10 (O5)** Legacy retirement should be: A. Left to chance B. Never done C. Done first D. Planned with criteria

## Answers
Q01 A · Q02 C · Q03 B · Q04 D · Q05 C · Q06 A · Q07 D · Q08 B · Q09 C · Q10 D

## Practical part
Migration plan defense: present the lab plan and answer challenges. Pass: 70% on the quiz and a plan with no shared-writer phase.
