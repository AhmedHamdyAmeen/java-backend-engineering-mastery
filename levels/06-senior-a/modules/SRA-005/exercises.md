# SRA-005 · Multi-region trade-offs — Exercises and lab

## Lab
### SRA-005-LAB1 · Five-country plan
**Outcomes:** 1–4 · **Time:** ~2 h
1. List the five target countries, their drivers (latency, residency, resilience, market), and the capabilities affected.
2. Build the capability-by-capability decision table for availability versus consistency.
3. Map jurisdictional requirements onto data flows and mark what stays local; verify assumptions with a role-played legal/compliance advisor.
4. Estimate infrastructure, on-call, tooling, and staffing cost for at least three options over three years.
5. Sequence the expansion with triggers and go/no-go criteria.
**Acceptance:** reviewed with a role-played legal/compliance advisor.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRA-005-EX01 | 1 | Choose consistency and failover patterns for catalog, inventory reservation, and payments across two regions; justify each. |
| SRA-005-EX02 | 1 | Product asks for "active-active everywhere". Write a one-page reply with the questions and a counterproposal. |
| SRA-005-EX03 | 2 | A country requires that customer personal data stay in-country. Redraw a data flow so orders can still be fulfilled globally. |
| SRA-005-EX04 | 2 | List five questions you would bring to the compliance advisor before designing for a new jurisdiction. |
| SRA-005-EX05 | 3 | Cost a second region over three years, including on-call, tooling, data transfer, and staffing; state the five biggest assumptions. |
| SRA-005-EX06 | 4 | Sequence a five-country launch: for each stage give the design, the trigger, and the go/no-go criterion. |

## Solutions
- **EX01** Catalog: replicated reads, eventual consistency. Inventory reservation: single writer per item or region with clear ownership, accepting some latency. Payments: single region with failover and idempotency keys. Justify by cost of staleness.
- **EX02** Ask which capabilities, what staleness is acceptable, what the downtime cost is. Counterproposal: active-active only for read-heavy capabilities; regional ownership or single region with failover elsewhere.
- **EX03** Keep personal data in a regional store; fulfillment uses pseudonymous identifiers or only the fields required; global systems hold references or tokens. Verify transfers with legal.
- **EX04** Examples: which data categories are in scope? Is processing, not only storage, restricted? Which transfer mechanisms are acceptable? Retention and local entity requirements? Regulator reporting duties?
- **EX05** Include infrastructure, replication traffic, tooling and observability per region, on-call load, engineering for region-aware features, and compliance work. Assumptions: traffic share, data volume, headcount cost, rates (verify), replication needs.
- **EX06** Example: stage 1 existing region; stage 2 regional data for residency when legal need confirmed; stage 3 second region for latency once revenue threshold is met; each with criteria and a review.

Outcome 3 and outcome 4 are also covered by the lab cost and sequencing steps and the quiz.

**Workplace evidence:** a regional or residency strategy you contributed to.
