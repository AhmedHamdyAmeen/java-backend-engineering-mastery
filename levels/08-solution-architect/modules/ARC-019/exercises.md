# ARC-019 · High availability and DR — Exercises and lab

## Lab
### ARC-019-LAB1 · Larkspur HA/DR design
**Outcomes:** 1–4 · **Time:** ~4 h
1. List Larkspur capabilities (checkout, catalog, store tills, fulfillment, reporting, back office) and their business impact per hour.
2. Set RPO and RTO per capability with the sponsor's assumptions.
3. Choose the multi-AZ design and the DR pattern per capability and cost each option.
4. Document fallbacks for the ERP, payment provider, and identity, including stores selling offline.
5. Write a DR test plan with scenarios, success criteria, and evidence.
**Acceptance:** targets met at a cost the sponsor accepts, or trade-off escalated.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-019-EX01 | 1 | Convert these impacts into RTO and RPO tiers: checkout loses 8,000 per hour, reporting loses little, the loyalty app loses goodwill. |
| ARC-019-EX02 | 1 | The sponsor says "everything must be five nines". Prepare the conversation. |
| ARC-019-EX03 | 2 | Pick a DR pattern for checkout, catalog, and reporting and justify each. |
| ARC-019-EX04 | 2 | Describe what breaks if the design uses three zones but only enough capacity for three zones' load. |
| ARC-019-EX05 | 3 | The payment provider has an outage. Define the degraded behavior and customer communication. |
| ARC-019-EX06 | 4 | Write a DR test plan for the checkout database failover with success criteria. |

## Solutions
- **EX01** Checkout: RTO under one hour, RPO minutes; catalog: RTO a few hours, RPO hours; reporting: RTO a day, RPO a day; loyalty: relaxed but monitored. Confirm with the sponsor.
- **EX02** Show cost per extra nine, ask what an hour of outage costs, propose tiered targets, make the sponsor choose with prices.
- **EX03** Checkout: warm standby; catalog: pilot light or restore with CDN cache; reporting: backup-restore.
- **EX04** Losing one zone leaves two thirds of capacity for full load, so users see slowness or errors; size with N+1 zones.
- **EX05** Offer alternate payment methods if contracted, queue orders for later capture where legal and safe, show clear messages, and track the provider's recovery.
- **EX06** Scenario: primary zone failure and region failure; steps; measure time to recover and data loss; success: within target RTO and RPO; record results, findings, owners, next test date.

**Workplace evidence:** an HA/DR design you produced and tested.

---
Outcome coverage: all outcomes covered by exercises and the lab.
