# SRB-009 · Service mesh — Exercises and lab

## Lab
### SRB-009-LAB1 · Mesh decision
**Outcomes:** 1, 2, 3 · **Time:** ~3 h
1. Define the problems the mesh should solve for Shop and FulfillCo services.
2. Trial a mesh on a subset of services with mTLS and a canary.
3. Measure latency overhead, resource use, and operational effort.
4. Write the adopt or reject ADR with alternatives.
**Acceptance:** decision supported by measurements.

## Exercises
| ID | Outcome | Task |
| --- | --- | --- |
| SRB-009-EX01 | 1 | List what FulfillCo would gain from a mesh and what it can get without one. |
| SRB-009-EX02 | 1 | Compare sidecar and sidecar-less for 200 small services. |
| SRB-009-EX03 | 2 | Write the policy for mTLS and who may call payments. |
| SRB-009-EX04 | 2 | Design a canary split 95/5 with rollback conditions. |
| SRB-009-EX05 | 3 | A team wants a mesh to fix unclear service ownership. Respond. |
| SRB-009-EX06 | 3 | Spot the problem: mesh retries 3 times and the client retries 3 times. |

## Solutions
- **EX01** mTLS, canary, uniform telemetry versus libraries, gateway, cert manager.
- **EX02** Sidecar costs 200 proxies of resources; sidecar-less reduces overhead but verify maturity and isolation.
- **EX03** Strict mTLS; allow only checkout identity; deny others.
- **EX04** Route weights, success-rate and latency thresholds, automatic rollback.
- **EX05** A mesh cannot fix ownership; address process; revisit when technical need is proven.
- **EX06** Up to 9 attempts; amplification; pick one owner of retries and budget them.

**Workplace evidence:** a platform technology adoption or rejection you led with evidence.
