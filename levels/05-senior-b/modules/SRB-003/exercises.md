# SRB-003 · Distributed data — Exercises and lab

## Lab
### SRB-003-LAB1 · Datastore evaluation
**Outcomes:** 1, 2, 3, 4 · **Time:** ~3.5 h
1. State FulfillCo's stock ledger requirements (no oversell, multi-warehouse, failure tolerance).
2. Pick two candidate datastores and document their replication and consistency models.
3. Gather evidence: documentation, Jepsen findings, or a small partition experiment.
4. Write a comparison and recommendation with caveats.
**Acceptance:** every consistency claim backed by documentation, Jepsen findings, or experiment; recommendation stated.

## Exercises
| ID | Outcome | Task |
| --- | --- | --- |
| SRB-003-EX01 | 1 | A leader fails with asynchronous replication. Describe what is lost and how to limit it. |
| SRB-003-EX02 | 2 | A 5-node cluster splits 3/2. Which side accepts writes and why? |
| SRB-003-EX03 | 3 | N=5. Choose W and R for a stock ledger and justify, then list one failure scenario to test. |
| SRB-003-EX04 | 3 | Show that W=1, R=1 with N=3 can return stale data. |
| SRB-003-EX05 | 4 | Find the version tested in a Jepsen report for a store you know and list the findings relevant to you. |
| SRB-003-EX06 | 4 | A vendor claims 'strong consistency, always available'. Write three questions to test it. |

## Solutions
- **EX01** Writes not yet replicated; reduce with synchronous or semi-synchronous replication at a latency cost.
- **EX02** The 3-node side holds a majority; the 2-node side cannot commit.
- **EX03** W=3, R=3 (overlap); test slow node plus sloppy quorum or concurrent writers.
- **EX04** The write lands on replica A, the read hits replica B which has not received it.
- **EX05** Answers depend on the report; must cite version, configuration, anomaly, and whether it is fixed.
- **EX06** Under which partition? Which configuration? Which published analysis or test supports it? Also: what happens to minority-side clients?

**Workplace evidence:** a datastore decision you informed with consistency analysis.
