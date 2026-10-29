# MID-032 · Distributed coordination — Exercises and lab

## Lab
### MID-032-LAB1 · Single runner
**Outcomes:** 1–3 · **Time:** ~2 h
Make the nightly reconciliation job in `orders` run once across three replicas using a database lock (ShedLock or an equivalent lease table). Add a fencing token: each lock grant increments a number that the job writes with its results, and the update rejects lower tokens.

**Acceptance:** a test that pauses the lock holder past its lease, lets another instance run, then resumes the first does not double-apply any change.

## Exercises (assessment: quiz)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-032-EX01 | 1 | List three Shop jobs and say which truly need a single active worker and which can use another design. |
| MID-032-EX02 | 1 | Explain leader election and what must happen when the leader dies. |
| MID-032-EX03 | 2 | Draw the timeline of an unsafe lease: holder pause, expiry, takeover, double write. |
| MID-032-EX04 | 2 | Write the SQL update that applies a fencing token. |
| MID-032-EX05 | 3 | Configure `lockAtMostFor` and `lockAtLeastFor` for a job that normally takes 3 minutes and at worst 20. |
| MID-032-EX06 | 2 | Review a design that "uses Redis `SET NX` for exactly-once payouts" and recommend changes. |

## Solutions
- **EX01** Reconciliation: one runner (lock + fencing). Outbox relay: `SKIP LOCKED`. Email digest: lock or unique "sent for date" record. Cleanup of old rows: idempotent, can run anywhere.
- **EX02** Instances compete for a lease; the winner acts and renews it; if it dies the lease expires and another wins. The old leader must stop on failed renewal.
- **EX03** A acquires; A stalls; lease expires; B acquires and writes; A resumes and writes: both applied.
- **EX04** `UPDATE state SET last_token = :t, ... WHERE id = :id AND last_token <= :t` and treat 0 rows as stale.
- **EX05** `lockAtMostFor` of about 30 minutes (above worst case, still releases after a crash); `lockAtLeastFor` of 1 to 5 minutes to prevent immediate re-run through clock skew.
- **EX06** Redis locks cannot guarantee exclusion under pauses or failover. Make payouts idempotent (unique payout key), add fencing in the payout table, and use the lock only to reduce duplicate work.

Outcome 3 is mainly assessed by the lab and quiz Q09 and Q10.
