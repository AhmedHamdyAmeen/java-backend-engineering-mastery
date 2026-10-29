# ARC-008 · Technology assessment — Exercises and lab

## Lab
### ARC-008-LAB1 · Commerce engine decision
**Outcomes:** 1–4 · **Time:** ~3.5 h
1. Define the commerce capability needs and criteria; agree weights with role-played stakeholders.
2. Describe three options for Larkspur: build on the in-house stack, packaged commerce suite, SaaS commerce platform.
3. Estimate for each: cost over five years, time to market, integration effort with the ERP and CRM, exit cost.
4. Score the options with evidence and run sensitivity on at least two weights.
5. Write a PoC plan targeting the riskiest integration and nonfunctional assumptions.
6. Present the recommendation.
**Acceptance:** exit cost and integration effort estimated for each option.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-008-EX01 | 1 | Classify eight Larkspur capabilities as differentiating or commodity and give a sourcing choice for each. |
| ARC-008-EX02 | 1 | Compare build, buy, and SaaS for customer service ticketing across five criteria. |
| ARC-008-EX03 | 2 | Write ten vendor questions on architecture fit and exit for a commerce platform. |
| ARC-008-EX04 | 3 | Design a PoC to test an ERP integration and peak load; define the success measures and duration. |
| ARC-008-EX05 | 4 | Given a score table, run sensitivity by changing two weights and report whether the winner changes. |
| ARC-008-EX06 | 4 | Draft a one-page recommendation for the CIO with options, weights, risks, and conditions. |

## Solutions
- **EX01** Commodity: payments, tax, email, HR, ticketing; differentiating: click-and-collect, store-aware availability promise. Commodity → SaaS or packaged; differentiating → build or tailor on a platform.
- **EX02** SaaS usually wins on time and run effort; build only when workflow is unique; consider integration with CRM and data location.
- **EX03** Examples: API coverage, rate limits, event or webhook support, data export formats and frequency, tenant isolation, upgrade handling of customizations, SLAs, certification and audit reports, exit assistance.
- **EX04** Test order sync at expected peak using copied or synthetic data with success criteria such as 99% under 30 s and no lost orders; two weeks, timeboxed.
- **EX05** Show a table before and after; if the winner holds under plausible weight changes, say the decision is robust; if not, say which assumption matters.
- **EX06** Include recommendation, why, alternatives, weights, costs with confidence level, risks, what would change the decision, next steps.

**Workplace evidence:** a build/buy/SaaS recommendation you made and its outcome.
