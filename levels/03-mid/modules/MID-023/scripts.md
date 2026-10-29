# MID-023 · Distributed computing — Lecture scripts

**Video:** 62 min · **Analogy used throughout:** sending letters by post between offices: letters get delayed, lost, or duplicated, and each office has its own clock.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-023-L01 · The eight fallacies (12 min)
**Goal:** name the false assumptions and a failure each causes.

**Key points**
- The network is reliable: a dropped packet loses an order confirmation.
- Latency is zero: a loop of 100 remote calls takes seconds.
- Bandwidth is infinite: huge JSON payloads saturate the link.
- The network is secure: plain HTTP between services leaks data.
- Topology does not change: hard-coded IPs break after a redeploy.
- There is one administrator: teams change firewalls and certificates independently.
- Transport cost is zero: serialization, bandwidth, and egress cost money.
- The network is homogeneous: different versions, protocols, and clients coexist.

**Show:** a table of the eight fallacies with one Shop failure each.

**Check:** What breaks if you hard-code a service IP? *(The call fails when the topology changes.)*

---

## MID-023-L02 · Latency numbers every engineer should know (8 min)
**Goal:** estimate costs by order of magnitude.

**Key points**
- Memory access is nanoseconds; SSD reads are microseconds; a same-datacentre round trip is about half a millisecond.
- A cross-continent round trip is on the order of 100 ms or more.
- Each remote call costs roughly thousands of times a local call.
- Chaining calls adds up: five sequential 20 ms calls cost at least 100 ms.
- Numbers shift with hardware; use them for ratios, not precision (verify figures before recording).

**Show:** a log-scale bar chart: memory, SSD, same-zone network, cross-region network.

**Check:** Five sequential 20 ms calls take at least how long? *(100 ms.)*

---

## MID-023-L03 · Partial failure (12 min)
**Goal:** explain why a timeout is not a failure.

**Key points**
- In one process, a call succeeds or fails. Across a network, parts fail while others work.
- A timeout means "no answer in time". The request may have been lost, executed, or the reply lost.
- Retrying a payment after a timeout risks charging twice.
- The sender cannot tell which case happened without asking again or checking state.
- Defences: idempotency keys, status queries, and reconciliation (MID-029).

**Show**
```
Shop --charge $50--> Payments   (Payments charges the card)
Shop <--response lost--         Shop sees a timeout
```

**Check:** After a timeout, did the operation happen? *(Unknown: it may or may not have.)*

---

## MID-023-L04 · Clocks and ordering (12 min)
**Goal:** see why wall-clock time cannot order events across nodes.

**Key points**
- Each machine has its own clock; they drift and are corrected by NTP, sometimes jumping backward.
- Two events with timestamps from different machines cannot be reliably ordered.
- Within one machine use a monotonic clock for durations (`System.nanoTime()`), not wall time.
- Logical ordering uses counters: Lamport clocks and vector clocks (conceptual).
- Practical choices: order by a single log (Kafka partition) or a database sequence.

**Show:** two nodes, one at 10:00:05 and one at 10:00:03, where the later event has the smaller timestamp.

**Check:** Which clock measures elapsed time safely? *(A monotonic clock, `System.nanoTime()`.)*

---

## MID-023-L05 · Failure models (6 min)
**Goal:** name the three models at a conceptual level.

**Key points**
- Crash: a node stops and stays stopped (the simplest model).
- Omission: a node or link drops some messages or fails to send or respond.
- Byzantine: a node behaves arbitrarily or maliciously, sending wrong data.
- Most business systems assume crash and omission failures, and rely on security controls against byzantine behaviour.
- Byzantine tolerance matters for blockchains and some safety-critical systems.

**Show:** a three-row table: model, example, typical defence.

**Check:** Which model covers dropped messages? *(Omission.)*

---

## MID-023-L06 · Demo: injecting latency and packet loss with Toxiproxy (12 min)
**Goal:** reproduce failures on purpose. Prepares `MID-023-LAB1`.

**Steps**
1. Run Toxiproxy with Docker Compose; create a proxy in front of the payment provider stub.
2. Point Shop's payment URL at the proxy and place an order normally.
3. Add a `latency` toxic of 3 s with a 2 s client timeout; watch the order status.
4. Add a toxic that drops the response (for example `limit_data` or `reset_peer` on the downstream); check whether Payments recorded the charge.
5. **Planned mistake:** retry blindly on timeout and show a double charge in the stub's records. Fix with an idempotency key (preview of MID-029).
6. Write the list of inconsistencies observed.

---
