# SRB-017 · Large migrations — Exercises and lab

## Lab
### SRB-017-LAB1 · Execute phase one
**Outcomes:** 1–4 · **Time:** ~4.5 h
1. Take the first extraction phase planned in SRB-008 and write the phase plan with entry checks, exit measures, and rollback.
2. Implement flags, shadow comparison, and a throttled idempotent backfill; produce a mismatch report.
3. Rehearse rollback, then cut over once the mismatch rate is below the threshold; write the decommission checklist for the legacy path.
**Acceptance:** mismatch rate measured and below threshold before cut-over.

## Exercises (assessment: migration execution report)
| ID | Outcome | Task |
| --- | --- | --- |
| SRB-017-EX01 | 1 | Write a five-phase migration plan for moving returns data to a new service, with exit measures and rollback per phase. |
| SRB-017-EX02 | 1 | Case: the plan has a single cut-over weekend. Rewrite it as reversible phases. |
| SRB-017-EX03 | 2 | Define the shadow comparison for shipment status: fields, key, classification of mismatches, threshold. |
| SRB-017-EX04 | 2 | Choose a rollout strategy (canary, blue-green, cohort) for a write path and justify it. |
| SRB-017-EX05 | 3 | Design a backfill for 200 million rows with throttle, checkpoint, idempotency, and verification. |
| SRB-017-EX06 | 3 | Case: during a backfill, rows are updated in the source. Explain how to avoid stale copies. |
| SRB-017-EX07 | 4 | Write the decommission plan for the legacy status service, including proof of no use and the flag cleanup. |

## Solutions
- **EX01** Example: prepare schema, dual-write behind a flag, backfill and verify, shift reads by cohort, retire old path; each with a measure (mismatch rate, lag) and rollback (flag off).
- **EX02** Split into shadow, partial serving, full serving, and cleanup; keep old path live until measures hold.
- **EX03** Key: shipment ID; fields: status, timestamp, carrier reference; classify timing (settle window), mapping bugs, missing records; threshold agreed in advance.
- **EX04** For writes, a canary by cohort with idempotency and reconciliation, since blue-green duplicates state; justify with reversibility and blast radius.
- **EX05** Batch by key range, rate limit adjustable, checkpoint table, upsert by stable key, verify counts and checksums per range, run off-peak.
- **EX06** Capture ongoing changes (dual-write or change stream) during and after the backfill, then reconcile; compare at the end.
- **EX07** Prove zero traffic over a full cycle; announce, block, scream-test where acceptable; archive; remove code, flags, alerts, access, and cost; confirm with finance.
- Outcome 4 is also covered by the lab checklist and Q08-Q09.

**Workplace evidence:** a migration you executed through cut-over and decommissioning.
