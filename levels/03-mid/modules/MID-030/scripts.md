# MID-030 · Distributed consistency — Lecture scripts

**Video:** 52 min · **Analogy used throughout:** several shop branches sharing one price list on paper: how quickly and in what order each branch sees an update decides what customers experience.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-030-L01 · Consistency models (12 min)
**Goal:** tell the four common consistency models apart with Shop examples.

**Key points**
- **Strong (linearizable):** every read sees the latest completed write, as if there were one copy. Costs latency and availability.
- **Eventual:** if writes stop, all replicas converge. Reads in between may be stale.
- **Causal:** if B happened because of A, nobody sees B without A (a reply never appears before its question).
- **Read-your-writes:** after you write, your own reads see it, even if others lag.
- Pick per operation, not per system.

**Show**
| Shop case | Needed |
| --- | --- |
| Decrement last unit of stock | strong (single writer) |
| Product page view count | eventual |
| "My order" after checkout | read-your-writes |
| Comment and its reply | causal |

**Check:** A customer places an order and the order list does not show it. Which guarantee is missing? *(Read-your-writes.)*

---

## MID-030-L02 · CAP, correctly (10 min)
**Goal:** state CAP precisely and avoid its common misuse.

**Key points**
- CAP describes behavior **during a network partition**: choose consistency (refuse some requests) or availability (answer, possibly stale).
- Partitions are not optional in a distributed system, so "pick any two of three" is misleading.
- When there is no partition, you can have both; CAP says nothing about latency.
- "C" here means linearizability, not the "C" in ACID.
- Labels such as "we are AP" describe one operation or data store under partition, not a whole system.

**Show:** a diagram of two replicas with a broken link; a write to replica 1; a read on replica 2 either errors (CP) or returns the old value (AP).

**Check:** Does CAP say a CP system is slow when the network is healthy? *(No; it only describes the choice during a partition.)*

---

## MID-030-L03 · PACELC (8 min)
**Goal:** add the trade-off CAP leaves out.

**Key points**
- PACELC: if **P**artition, choose **A** or **C**; **E**lse (normal operation), choose **L**atency or **C**onsistency.
- Synchronous replication gives stronger consistency but every write waits for replicas.
- Asynchronous replication is faster but replicas lag.
- This is why a read replica can return stale data on a healthy network.
- Real products are configurable; check settings rather than slogans (verify per product before recording).

**Show**
| Setup | Normal operation | During partition |
| --- | --- | --- |
| Sync replicas, quorum writes | higher latency, consistent | may reject writes |
| Async read replica | low latency, may be stale | serves stale reads |

**Check:** Why can a healthy system still return stale reads? *(Asynchronous replication trades consistency for latency.)*

---

## MID-030-L04 · Designing for eventual consistency (10 min)
**Goal:** make lag a designed behavior, not a surprise.

**Key points**
- Show honest intermediate states: "order pending", "payment processing".
- Return `202 Accepted` with a status URL for work that finishes later.
- Read-your-writes tricks: read from the primary after a write, return the created resource in the response, or pass a version the reader waits for.
- Make updates idempotent and commutative where possible so order does not matter.
- Expect conflicts to be rare but define a rule (last write wins, merge, or ask the user).

**Show**
```
POST /orders          -> 202 Accepted, Location: /orders/42
GET  /orders/42       -> {"status":"PENDING"}  ...later...  {"status":"CONFIRMED"}
```

**Check:** Why return `PENDING` rather than waiting inside the POST? *(Downstream steps are asynchronous; waiting hides lag and ties up resources.)*

---

## MID-030-L05 · Demo: read-your-writes across services (12 min)
**Goal:** reproduce a stale read after checkout and fix it. Prepares MID-030-LAB1.

**Steps**
1. Place an order through `orders`; the `catalog` view of "my recent purchases" is fed by Kafka and lags by a second.
2. Immediately call `GET /my/purchases` and observe the new order missing.
3. **Planned mistake:** add `Thread.sleep(2000)` in the client. It works on a quiet laptop and fails under load. Fix: do not guess lag.
4. Return the created order in the POST response and have the UI merge it into the list until the read model catches up.
5. Alternative: send the order version with the read; the service waits briefly or falls back to the source of truth.
