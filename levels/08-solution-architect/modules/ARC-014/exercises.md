# ARC-014 · Compute choices — Exercises and lab

## Lab
### ARC-014-LAB1 · Compute decisions
**Outcomes:** 1–3 · **Time:** ~3 h
1. List the Larkspur workloads: storefront API, order processing, product search indexing, nightly stock and ERP batch, image resizing.
2. Describe each workload's shape (steady, spiky, event-driven, batch).
3. Choose compute per workload and describe scaling behavior and operating model.
4. Write each choice as an ADR including team skills and on-call capacity.
5. State when each decision should be revisited.
**Acceptance:** the team's skills and operating capacity are part of each decision.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-014-EX01 | 1 | Compare VM, managed containers, Kubernetes, and functions for the product-image resizer on four criteria. |
| ARC-014-EX02 | 1 | List what the Larkspur team still operates when it uses managed containers versus VMs. |
| ARC-014-EX03 | 2 | Match four workloads (checkout API, Black Friday catalog reads, ERP nightly export, order-confirmation email) to compute and justify. |
| ARC-014-EX04 | 2 | A function processes a continuous stream 24 hours a day and the bill is high. Diagnose and propose a change. |
| ARC-014-EX05 | 3 | Write a one-page recommendation on whether Larkspur should run Kubernetes now. |
| ARC-014-EX06 | 3 | Define three measurable revisit triggers that would justify moving to Kubernetes. |

## Solutions
- **EX01** Functions: event-triggered on upload, scale to zero, low effort, ideal; managed containers: fine but idle cost; VM: most effort; Kubernetes: overkill.
- **EX02** Containers: images, deployments, autoscaling rules, application monitoring. VMs: all that plus OS patching, hardening, scaling groups, and host monitoring.
- **EX03** Checkout API: managed containers, autoscaling. Catalog reads: CDN and cache plus autoscaling containers. ERP export: scheduled batch job. Email: queue-triggered function or worker.
- **EX04** Per-run pricing on steady load exceeds a continuous small instance; move to a container service with steady capacity, keep functions for bursts.
- **EX05** Recommend no for now: few services, small team, no platform capacity; operating cost exceeds benefit; use managed containers and revisit.
- **EX06** For example: more than about 15 services, more than three teams deploying independently, a dedicated platform team of at least two, or a requirement for custom scheduling or portability.

**Workplace evidence:** a compute platform decision you made with operating cost considered.

---
Outcome coverage: all outcomes covered by exercises and the lab.
