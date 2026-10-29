# MID-032 · Distributed coordination — Lecture scripts

**Video:** 48 min · **Analogy used throughout:** a single key to the cash-office: whoever holds it may count the till, but a key that "expired" while its holder dozed must not still open the safe.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-032-L01 · When only one instance may act (8 min)
**Goal:** recognize work that must have a single active runner.

**Key points**
- With replicas, every instance runs the same scheduled jobs and consumers unless you prevent it.
- Examples: nightly reconciliation, sending a daily report, an outbox relay without `SKIP LOCKED`.
- Prefer designs that need no coordination: idempotent work, partitioned work, or `SKIP LOCKED` queues.
- When one runner truly is required, you need a lock or a leader.
- Decide what happens if the runner dies: another must take over.

**Show**
| Job | Needs one runner? | Alternative |
| --- | --- | --- |
| Nightly reconciliation | yes | lock |
| Outbox relay | no | `SKIP LOCKED` |
| Email digest | yes | lock or unique send record |

**Check:** Name a way to avoid needing a lock for a queue of tasks. *(Let workers claim rows with `SKIP LOCKED`.)*

---

## MID-032-L02 · Leases and leader election (10 min)
**Goal:** explain time-limited ownership.

**Key points**
- A **lease** is a lock that expires automatically unless renewed, so a dead holder cannot block forever.
- **Leader election:** instances compete; one wins a lease and acts, others stand by.
- Renew before expiry; if renewal fails, stop acting immediately.
- Clocks and pauses matter: the holder may not notice its lease expired.
- Real consensus (Raft, ZooKeeper, etcd) gives stronger guarantees than a plain database row.

**Show**
```sql
UPDATE lease SET holder = :me, expires_at = now() + interval '30 seconds'
WHERE name = 'nightly' AND (holder = :me OR expires_at < now());
-- 1 row updated = you hold the lease
```

**Check:** Why do leases expire? *(So a crashed holder does not block everyone forever.)*

---

## MID-032-L03 · Distributed locks and their limits (10 min)
**Goal:** know when a lock is safe and when it is only an optimization.

**Key points**
- A lock on a database row or a lock service (ZooKeeper, etcd) is useful for **efficiency**: avoid duplicate work.
- **Unsafe scenario:** instance A takes a lease, pauses (GC, network stall), the lease expires, B takes over, A wakes and still writes.
- A Redis `SET NX PX` lock gives no safety guarantee under pauses and failover; do not use it alone for correctness.
- Keep critical sections short and make the work idempotent.
- ShedLock provides database-backed single-run scheduling and is meant for efficiency, not strict mutual exclusion.

**Show:** a timeline: A acquires, A pauses, lease expires, B acquires and writes, A resumes and writes: both wrote.

**Check:** Why can a paused lock holder still do damage? *(It does not know its lease expired and writes anyway.)*

---

## MID-032-L04 · Fencing tokens (8 min)
**Goal:** make stale holders harmless.

**Key points**
- A **fencing token** is a number that increases every time the lock is granted.
- The holder sends the token with each write; the resource rejects writes with a token lower than one it has seen.
- The check must be at the resource (database, storage), not only in the client.
- In SQL: store `last_token` and add `WHERE last_token <= :token` to the update.
- A version column or a monotonically increasing sequence can provide the token.

**Show**
```sql
UPDATE recon_state SET last_token = :t, result = :r
WHERE id = 1 AND last_token <= :t;   -- 0 rows updated: you are stale, stop
```

**Check:** Where must the token be checked? *(At the resource being written, not just in the client.)*

---

## MID-032-L05 · Demo: a nightly job running once across three replicas (12 min)
**Goal:** run reconciliation exactly once and fence its writes. Prepares MID-032-LAB1.

**Steps**
1. Scale `orders` to three replicas; the `@Scheduled` reconciliation job runs three times.
2. Add ShedLock with a JDBC lock provider (verify library and version before recording) and annotate with `@SchedulerLock(name = "recon", lockAtMostFor = "10m")`.
3. Run again: one replica executes, others skip.
4. **Planned mistake:** set `lockAtMostFor` shorter than the job. A second replica starts while the first still runs. Fix: size it above the worst-case runtime and fence the writes.
5. Add a lock-generation number as a fencing token on the state table.
6. Pause the lock holder with `docker pause`, let the lease expire, let another run, unpause, and show the stale writes are rejected.
