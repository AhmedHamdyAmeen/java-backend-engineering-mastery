# ARC-037 · Migration strategy — Exercises and lab

## Lab
### ARC-037-LAB1 · Larkspur migration plan
**Outcomes:** 1–4 · **Time:** ~4 h
1. Compare cutover approaches for the web shop and the 120 stores; choose and justify.
2. Design coexistence: master per data set per phase, routing, synchronization, end date.
3. Write the data migration plan: mapping, cleansing, trial loads, validation, final load, delta.
4. Write go/no-go criteria and a runbook with a rollback and decision owner for every step.
5. Defend the plan to a role-played program director.
**Acceptance:** every cutover step has a rollback and a decision owner.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-037-EX01 | 1 | Compare big bang, phased by capability, phased by store, and parallel run for Larkspur given a November peak; recommend one. |
| ARC-037-EX02 | 1 | The sponsor wants everything live in one weekend to save cost. Write the architect's response with risk trade-offs. |
| ARC-037-EX03 | 2 | During the phased move, both the old shop and the new platform can edit customer addresses. Decide the master per phase and conflict rules. |
| ARC-037-EX04 | 3 | Draft the data migration plan for 2.4 million customers and 9 million orders, including validation checks. |
| ARC-037-EX05 | 4 | Write go/no-go criteria for the first store wave with owners. |
| ARC-037-EX06 | 4 | A rollback plan says "restore the old system from backup". Review it and fix it for data written after cutover. |

## Solutions
- **EX01** Phased by store for the stores, phased by capability for web (catalog, then checkout), avoiding November; big bang rejected for risk; parallel run only for financial postings where reconciliation is cheap.
- **EX02** Cost saved by big bang is small against the revenue-at-risk and rollback difficulty; propose compressed phases with a pilot and a clear rollback; the sponsor decides with the risk visible.
- **EX03** One master per phase (for example the old shop until the account capability moves, then the platform); sync with timestamps; conflicts resolved by master wins; no dual editing, or block edits for migrating accounts.
- **EX04** Mapping sheet; cleansing of duplicates; trial loads timed; checks: record counts, order totals per month against finance, orphan checks, random sample review; dress rehearsal; delta load; sign-off by data owner.
- **EX05** Test results passed, migration validation within thresholds, staff trained, support staffed, monitoring live, rollback rehearsed; each with owner and evidence; decision by the program director.
- **EX06** Restore alone loses new orders. Add: capture new-system orders in an export during the window, replay into the old system or finance, define the last safe rollback point and who decides, and rehearse.

**Workplace evidence:** a migration or cutover you planned and executed.
