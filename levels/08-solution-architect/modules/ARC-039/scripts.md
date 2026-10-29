# ARC-039 · Financial analysis — Lecture scripts

**Video:** 69 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-039-L01 · Finance for architects (10 min)
**Goal:** learn the finance vocabulary needed to argue a technical decision.

**Key points**
- Capital expenditure (capex): one-off investment that is often capitalized and depreciated; operating expenditure (opex): ongoing cost in the period.
- Cloud and SaaS shift cost toward opex; custom build is often capex plus run cost. Treatment rules belong to finance: confirm with them.
- Finance cares about budget cycles, payback, and risk, not architecture beauty.
- Always include what the business gets, not only what it spends.

**Show:** a glossary card: capex, opex, depreciation, NPV, payback, ROI, TCO, with one Larkspur example each (verify definitions with the finance partner).

**Check:** Why care about capex versus opex? *(They hit budgets and reporting differently, which can decide which option is fundable.)*

---

## ARC-039-L02 · Total cost of ownership (12 min)
**Goal:** build a multi-year TCO model.

**Key points**
- Cost lines: build (people, vendors), licences and subscriptions, infrastructure, support, operations people, training, integration, migration, decommissioning.
- Model over several years (five for Larkspur); include growth in usage and price increases.
- Compare options on the same scope and the same period.
- State every assumption and its source; give ranges for uncertain ones.

**Show:** a TCO sheet: rows of cost lines, columns Year 0 to Year 5, totals, assumptions tab with owner and confidence.

**Check:** Why compare a SaaS option against "zero" for the current system? *(Because the current system also costs money; compare all-in costs.)*

---

## ARC-039-L03 · ROI, payback, and benefits (10 min)
**Goal:** estimate ROI and payback with explicit assumptions.

**Key points**
- Benefits: revenue growth, cost reduction, risk reduction, avoided cost; each has an owner in the business.
- ROI: net benefit divided by cost; payback: when cumulative benefit exceeds cumulative cost (discounting and NPV are used by finance; verify their method).
- Benefits nobody owns will not be delivered or tracked.
- Test sensitivity: what if adoption is half, delivery 6 months late, or cost 20 percent higher.

**Show:** a benefits table: benefit, owner, measure, baseline, target, year, confidence; plus a cumulative cash chart with payback year.

**Check:** What is wrong with a benefit that has no owner? *(Nobody is accountable for delivering or measuring it.)*

---

## ARC-039-L04 · Licensing and operating costs (10 min)
**Goal:** understand how licence models and run costs change the numbers.

**Key points**
- Licence models: per user, per store, per transaction, per volume tier, or platform fee; each scales differently.
- Hidden costs: environments, premium support, integration connectors, data egress, overage fees, price uplift clauses.
- Run costs: monitoring, patching, on-call, upgrades, skills.
- Check how cost behaves at 2x volume; some models explode.

**Show:** a small chart comparing per-transaction and per-store licences at 1x, 2x, 4x Larkspur volume (use assumed numbers and label them as such).

**Check:** Why model growth? *(Licence and usage costs scale with volume; a cheap start can become expensive later.)*

---

## ARC-039-L05 · Demo: a five-year TCO for Larkspur's options (14 min)
**Goal:** worked TCO build for the top two options; prepares ARC-039-LAB1.

**Steps**
1. Fix scope and period: web, app, order, stock, payments integration, five years.
2. Fill cost lines for Option A (commerce SaaS) and Option B (custom build): licences, build, integration, support, operations people, infrastructure.
3. Put assumptions on their own tab: volume growth, salary rates, vendor uplift; use clearly labeled placeholders.
4. **Planned mistake:** compare the SaaS licence with zero for the build option's run cost. Fix: include run team, infrastructure, upgrades, and security effort for the custom build.
5. Run sensitivity: 2x volume, 6-month delay; show how the ranking changes.

---

## ARC-039-L06 · Demo: a finance review of the business case (13 min)
**Goal:** run a role-played review with a finance partner; prepares ARC-039-LAB1.

**Steps**
1. Present the case in one page: investment, benefits, payback, key assumptions.
2. The finance partner asks to reproduce each number; show the sheet and sources.
3. Handle challenges: benefit owners, discount rate, capex or opex treatment, risk contingency.
4. **Planned mistake:** a benefit of "improved customer experience" with no number or owner. Fix: translate into conversion rate or fewer calls with a baseline and owner, or label it a non-financial benefit.
5. Agree follow-ups and record the review outcome.
