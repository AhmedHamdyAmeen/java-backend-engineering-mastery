# ARC-010 · Legacy modernization — Exercises and lab

## Lab
### ARC-010-LAB1 · Portfolio disposition
**Outcomes:** 1–4 · **Time:** ~4 h
1. Build an evidence sheet for the Larkspur applications: web shop, store POS integration, order management in ERP, CRM, reporting.
2. Score value, condition, risk, and cost to change; plot the quadrant.
3. Assign a disposition (rehost, replatform, refactor, replace, retire, retain) to each.
4. Sequence the dispositions with coexistence and dependency notes.
5. Write a short business case for the largest change.
**Acceptance:** each decision justified by value, condition, and risk.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-010-EX01 | 1 | Assign dispositions to six Larkspur applications and justify each in one sentence. |
| ARC-010-EX02 | 1 | A team proposes to rehost the web shop to the cloud to "go modern". Assess the proposal. |
| ARC-010-EX03 | 2 | Score three applications on value, condition, risk, and cost to change using a supplied evidence sheet and plot them. |
| ARC-010-EX04 | 3 | Design a strangler sequence for moving web traffic from the old shop to the new platform in three slices. |
| ARC-010-EX05 | 3 | Define system-of-record rules during coexistence for products, customers, and orders. |
| ARC-010-EX06 | 4 | Write a one-page business case for replacing the web shop with "do nothing" as the baseline. |

## Solutions
- **EX01** Web shop: replace; ERP order management: retain and wrap; CRM: retain or replatform; reporting: replatform to a managed analytics service; store POS integration: refactor behind the new interface; old label tool: retire.
- **EX02** Rehosting moves the problem; the shop's issues are agility and mobile support, which hosting does not fix. Prefer replace; rehost only as a short bridge if infrastructure is the urgent risk.
- **EX03** Show scores with evidence references; high value/low condition first for action; low value/low condition for retirement.
- **EX04** Slice 1: browse and checkout for web; slice 2: mobile and accounts; slice 3: store pickup and returns; route by feature flag or gateway; retire the old shop when traffic reaches zero.
- **EX05** Products owned by merchandising source, orders owned by the new platform until posted to the ERP, finance records owned by the ERP, customers by CRM with sync; one owner per entity at any time.
- **EX06** Baseline "do nothing" shows rising run cost and lost sales; option replace shows migration cost, dual running, benefits with ranges, payback; list assumptions and sensitivity.

**Workplace evidence:** a modernization decision you led or shaped and its result.
