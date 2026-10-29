# ARC-040 · Vendor and procurement — Exercises and lab

## Lab
### ARC-040-LAB1 · Commerce platform RFP
**Outcomes:** 1–4 · **Time:** ~3 h
1. Write the technical RFP sections for Larkspur's commerce platform: context, needs, non-functional requirements, integration, exit, support.
2. Build an evaluation scorecard with weights traceable to requirements.
3. Design the evaluation steps: coverage, scripted demos, proof of concept, references.
4. Review a provided sample contract for SLA and exit clauses; list risks and asks.
5. Present to a role-played procurement lead and legal advisor.
**Acceptance:** scorecard traceable to requirements; exit risks identified.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-040-EX01 | 1 | Rewrite a requirement "must use Brand X search" into a need-based requirement with measurable criteria. |
| ARC-040-EX02 | 1 | Write six non-functional requirements for the RFP (availability, store offline support, security, data residency, API limits, exit). |
| ARC-040-EX03 | 2 | Design a two-day technical evaluation for three vendors including a scripted demo of five Larkspur scenarios. |
| ARC-040-EX04 | 2 | A vendor claims "unlimited scale". Define the proof-of-concept test and pass criteria. |
| ARC-040-EX05 | 3 | A sample contract has 99.5 percent availability measured monthly, credits capped at 10 percent, data returned within 90 days in a proprietary format, 12-month minimum term. List the architectural risks and asks. |
| ARC-040-EX06 | 4 | Legal wants to remove the exit-assistance clause to speed negotiations. Write the technical advisor's note to procurement and legal. |

## Solutions
- **EX01** "Provide search across 500 000 products with filters, results in under 500 ms at the 95th percentile at peak, typo tolerance, and synonym management by business users." Vendor names removed.
- **EX02** Examples: availability target and measurement; store tills sell offline up to a stated time; security certifications and testing evidence; data stored and processed in stated regions; API rate limits stated and sufficient for peak; exit support, export formats, and timelines.
- **EX03** Day 1 scripted demos on the same data (search, checkout, returns, partner API, offline), day 2 integration and operations walk-throughs; scoring sheets completed independently by two scorers; references called; weights fixed beforehand.
- **EX04** Load test with Larkspur's peak profile (and a multiple), measure latency and error rates, test scaling time and cost at load, run for a stated duration with observers; pass criteria set in advance.
- **EX05** 99.5 percent allows about 3.6 hours per month of downtime; credits are not a remedy; proprietary export format raises lock-in; long return time; minimum term. Asks: higher target and measurement definition, open formats, shorter return time, termination for repeated failure, exit assistance.
- **EX06** Exit assistance is the safeguard against lock-in and vendor failure; removing it saves time but leaves Larkspur unable to leave without penalty; propose a shorter but explicit version covering data return, transition period, and rates.

**Workplace evidence:** a vendor evaluation you ran or contributed to.
