# SRB-015 · Cost optimization — Exercises and lab

## Lab
### SRB-015-LAB1 · Cost per order
**Outcomes:** 1–4 · **Time:** ~3.5 h
1. Take a sample cloud bill for the combined Shop plus FulfillCo platform and group it by driver (compute, storage, transfer, managed services).
2. Attribute costs to services and teams with a tag scheme and a shared-cost rule; compute cost per order.
3. Deliver a savings plan with levers, estimates, risks, and sequencing.
**Acceptance:** savings estimate traceable to bill line items.

## Exercises (assessment: cost analysis review)
| ID | Outcome | Task |
| --- | --- | --- |
| SRB-015-EX01 | 1 | Given a bill, group lines into the four driver categories and name the top three. |
| SRB-015-EX02 | 1 | Case: transfer cost doubled after a service split. Explain the likely cause and how to confirm it. |
| SRB-015-EX03 | 2 | Design a tag scheme and allocation rule for shared Kubernetes cluster costs. |
| SRB-015-EX04 | 2 | Compute cost per order for three months of totals and orders; explain the trend. |
| SRB-015-EX05 | 3 | Choose three levers for a bill dominated by compute and estimate savings with assumptions. |
| SRB-015-EX06 | 4 | Case: the plan proposes removing a standby replica to save cost. Write the risk assessment and a decision. |
| SRB-015-EX07 | 4 | Compare a three-year commitment versus on-demand for a load that may fall by 40%; recommend with reasoning. |

## Solutions
- **EX01** Group by service type; top drivers usually compute, managed database, and transfer; verify with your data.
- **EX02** Cross-zone or cross-region calls between split services; confirm via flow logs or transfer line items by usage type.
- **EX03** Required tags: service, team, environment; allocate cluster cost by resource requests or usage; report the untagged share.
- **EX04** Cost per order = month cost / orders; if totals rise slower than orders, unit cost fell; state caveats such as seasonal volume.
- **EX05** Rightsizing, non-production schedules, and storage lifecycle; compute estimated hours or GB saved times price from bill lines.
- **EX06** Saving versus recovery objective and availability commitment; likely reject or replace with a cheaper redundancy option, recorded with the owner.
- **EX07** Commit only to the stable baseline portion; partial commitment covers the floor and leaves variable load on demand.
- Outcomes 3 and 4 are also covered by the lab savings plan and risks.

**Workplace evidence:** a cost reduction you delivered with numbers.
