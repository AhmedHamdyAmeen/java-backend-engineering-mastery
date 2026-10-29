# ARC-008 · Technology assessment — Lecture scripts

**Video:** 67 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-008-L01 · Build, buy, or SaaS (12 min)
**Goal:** frame the three sourcing options and the criteria for choosing.

**Key points**
- Build: full control and fit, highest cost and long-term ownership.
- Buy (packaged software you run): faster, configurable, you operate and upgrade it.
- SaaS: fastest start and no infrastructure, but less control, data in the vendor's platform, and subscription cost.
- Criteria: fit, differentiation, total cost over years, risk, time to market, skills, exit cost.

**Show:** a three-column table for the commerce platform with rows for fit, cost shape (capital versus subscription), time to market, control, operational burden, exit.

**Check:** Which option usually gives the fastest start with the least infrastructure to run? *(SaaS.)*

---

## ARC-008-L02 · Differentiating vs commodity capabilities (10 min)
**Goal:** decide where custom effort belongs.

**Key points**
- Differentiating: gives the company advantage customers notice; worth building or heavily tailoring.
- Commodity: everyone needs it and it gives no edge; buy or subscribe.
- Use the capability map: importance and uniqueness together.
- The line moves over time; revisit it.

**Show:** a Larkspur 2x2: payments, tax calculation, and email delivery are commodity; click-and-collect experience and store-aware inventory promise are differentiating.

**Check:** Should Larkspur build its own payment processing? *(No; it is a commodity capability.)*

---

## ARC-008-L03 · Evaluating vendors' architecture fit (12 min)
**Goal:** look beyond features at how a product fits the architecture.

**Key points**
- Functional fit: required journeys supported out of the box or by configuration.
- Architecture fit: API coverage and quality, event support, data ownership and export, security, extensibility, observability.
- Viability: financial health, roadmap, references, support model.
- Exit cost: how hard it is to extract data and replace the product.

**Show:** vendor questionnaire excerpts: Are all functions available through APIs? Can we export all our data in documented formats? What are API rate limits? How are customizations preserved across upgrades?

**Check:** Why ask about data export? *(It determines exit cost and data ownership.)*

---

## ARC-008-L04 · Proofs of concept that reduce risk (10 min)
**Goal:** design a PoC that tests the riskiest assumptions, not the easy ones.

**Key points**
- List the top risks (integration with the ERP, peak performance, security) and pick what to test.
- Define success criteria before starting and a time limit.
- Use realistic data and load, not demo data.
- A PoC answers questions; it is not the first release.

**Show:** a PoC plan: risk, test, success measure, effort. Example: ERP order sync at 500 orders per hour, 99% under 30 s, using test data from a copy of last year's peak.

**Check:** What should a PoC test first? *(The riskiest integration or quality assumption.)*

---

## ARC-008-L05 · Recommendation and sensitivity (8 min)
**Goal:** present a recommendation that survives challenge.

**Key points**
- Weighted criteria: agree weights with stakeholders before scoring.
- Score each option with evidence, not impressions.
- Sensitivity: change weights and see whether the winner changes.
- State risks, assumptions, and what would change the recommendation.

**Show:** a scoring table with three options, weights, scores, totals, and a sensitivity row: "if integration weight rises from 20% to 30%, rank stays; if cost falls below 10%, option B overtakes".

**Check:** What does sensitivity analysis show? *(Whether the result changes when weights or assumptions change.)*

---

## ARC-008-L06 · Demo: commerce platform — build, packaged suite, or SaaS? (15 min)
**Goal:** work through the decision for Larkspur. Prepares `ARC-008-LAB1`.

**Steps**
1. State the need and the criteria; agree weights with role-played IT and e-commerce leaders.
2. Estimate for each option: cost over five years (verify figures with real quotes), time to market, integration effort with the ERP and CRM, exit cost.
3. Score and compute totals; run sensitivity on integration and cost weights.
4. Design a two-week PoC for the top two options: order import to the ERP, stock lookup latency, promotion day load.
5. **Planned mistake:** the first score sheet is a feature checklist with no data ownership or exit scores. Fix: add architecture-fit and exit-cost criteria and re-score.
6. Write the recommendation with its conditions.

**Check:** What was missing in the first scoresheet? *(Architecture fit, data ownership, and exit cost.)*
