# MID-023 · Distributed computing — Exercises and lab

## Lab
### MID-023-LAB1 · Unreliable network
**Outcomes:** 1–4 · **Time:** ~2 h
1. Add Toxiproxy between Shop and its payment provider stub (Docker Compose).
2. Run scenarios: added latency, timeout shorter than latency, dropped response, connection reset.
3. After each, compare Shop's order status with the provider's record.
4. Write the observed inconsistencies and which fallacy or failure model each demonstrates.
**Acceptance:** list of every inconsistency observed.

## Exercises (assessment: failure-scenario quiz; five exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-023-EX01 | 1 | For each of the eight fallacies, write one failure example from Shop. |
| MID-023-EX02 | 2 | Explain, with a timeline, why a timeout on `charge()` does not mean the card was not charged. |
| MID-023-EX03 | 3 | Two services log `OrderPlaced` and `OrderPaid` with local timestamps; paid appears earlier. Explain two causes and a fix. |
| MID-023-EX04 | 4 | Classify: node dies, link drops 5% of packets, node returns corrupted prices. |
| MID-023-EX05 | 1 | Estimate the minimum latency of a request that makes 8 sequential same-datacentre calls of 1 ms each, and say how to reduce it. |

## Solutions
- **EX01** For example: reliable network, lost confirmation; zero latency, N+1 remote calls; secure network, plaintext traffic; topology, stale IP; one administrator, firewall change; zero transport cost, large payload bills; homogeneous, mixed API versions; infinite bandwidth, bulk export slows checkout.
- **EX02** Timeline: request sent, provider charges, reply lost, client times out. Shop cannot distinguish this from a request that never arrived.
- **EX03** Clock skew or NTP correction; fix by ordering with a sequence, a version number, or a single log (e.g. one Kafka partition per order).
- **EX04** Crash; omission; byzantine.
- **EX05** At least 8 ms plus processing; reduce by batching, parallel calls, caching, or merging the calls.
