# ARC-033 · Solution options — Lecture scripts

**Video:** 71 min · **Running case:** *Larkspur Retail* — a mid-size retailer with 120 stores and a dated on-premises web shop; you are the solution architect for a new platform integrated with the existing ERP and CRM.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-033-L01 · Why one option is no option (10 min)
**Goal:** explain why a decision with a single candidate is not a decision, and what a good options analysis protects.

**Key points**
- If only one option is presented, the real decision was made earlier, in private, without the evidence.
- Options let sponsors see what they give up; trade-offs become visible and owned.
- A strawman is an option written to lose; reviewers spot it quickly and stop trusting the analysis.
- Doing nothing (or "extend the old web shop") is always a legitimate baseline option.

**Show:** a one-line comparison: "we will buy Platform X" versus a page showing four options with cost, risk, and time-to-market, so the sponsor can see which trade-off they are choosing.

**Check:** What is a strawman option? *(An alternative written weakly on purpose so the favorite wins.)*

---

## ARC-033-L02 · Generating real alternatives (10 min)
**Goal:** produce options that differ in kind, not in vendor name.

**Key points**
- Differ along the build/buy axis: commerce SaaS, packaged platform run by us, custom build, hybrid (SaaS storefront plus custom order orchestration).
- Add the baseline: keep and modernize the existing web shop.
- Write each option as a short sketch: what it is, what we own, what we rent, rough shape of cost and time.
- Test each option: could a thoughtful stakeholder honestly prefer it? If not, rework it.

**Show:** four option cards for Larkspur: A commerce SaaS, B packaged platform on our cloud, C custom build on our stack, D hybrid. Each card has "we own", "we rent", "first release".

**Check:** Why are "SaaS from vendor 1" and "SaaS from vendor 2" weak as separate options? *(They differ in vendor, not in approach; vendors are compared inside an option later.)*

---

## ARC-033-L03 · Criteria and weights with stakeholders (12 min)
**Goal:** agree evaluation criteria and weights before any option is scored.

**Key points**
- Criteria come from goals and constraints: time-to-market, total cost, fit to Larkspur's processes, integration effort with ERP and CRM, security and compliance, exit risk, team skills.
- Weights are set with stakeholders in a workshop, in writing, before scoring; this is the protection against favorite-first choices.
- Separate must-haves (pass or fail gates) from weighted preferences.
- Keep criteria independent; do not count "cost" three times under different names.

**Show:** a criteria table: gate (data residency, PCI scope), weighted criteria with weights summing to 100, and the stakeholder who endorsed each weight.

**Check:** When must weights be agreed? *(Before scoring, so the result cannot be steered toward a favorite.)*

---

## ARC-033-L04 · Decision matrices and sensitivity (12 min)
**Goal:** score options in a matrix and test whether the answer survives different weights.

**Key points**
- Score each option per criterion on a defined scale (for example 1-5) with a one-line evidence note, then multiply by weight and sum.
- Close totals are a signal, not an answer; the matrix informs the discussion.
- Sensitivity: change each weight up and down (for example by 10 points), or swap two weights, and see whether the winner changes.
- If a small change flips the winner, say so, and look for the real disagreement behind that weight.

**Show:** a matrix with four options and six criteria, plus a second table listing "weight change tested" against "winner".

**Check:** Why run sensitivity analysis? *(To learn whether the recommendation depends on one contested weight.)*

---

## ARC-033-L05 · Demo: four options for Larkspur's commerce platform (14 min)
**Goal:** work through a full options analysis for the Larkspur platform; prepares ARC-033-LAB1.

**Steps**
1. Interview three stakeholders (e-commerce, store operations, finance) and list goals and hard constraints: holiday-season launch target, ERP stays, card data out of scope where possible.
2. Draft four options: commerce SaaS, packaged platform, custom build, hybrid; add the baseline of extending the old web shop for comparison.
3. Run a weighting workshop; record weights and who endorsed them before any scoring.
4. **Planned mistake:** score the options privately and then adjust the weights to "reflect the discussion". Fix: freeze weights first, re-score with evidence notes, and record any later weight change as a logged decision.
5. Complete the matrix with evidence per score, for example vendor documentation, reference calls, or past project estimates.
6. Write the recommendation page: chosen option, rejected options with their honest strengths, and the main risk of the choice.

---

## ARC-033-L06 · Demo: when changing one weight flips the recommendation (13 min)
**Goal:** show how to handle a result that is sensitive to a single weight; prepares ARC-033-LAB1.

**Steps**
1. Start from the Larkspur matrix where the hybrid option wins narrowly over the SaaS option.
2. Raise "speed to market" from 15 to 25 and show the winner flips to SaaS.
3. Trace the flip to its cause: the SaaS option scores high on speed and low on process fit, so the real question is how much customization Larkspur needs.
4. **Planned mistake:** present the original winner and hide the flip. Fix: show the sensitivity table, name the contested weight, and ask the sponsor to rule on it.
5. Take the question back to stakeholders; record their decision on the weight and the owner.
6. Update the recommendation page with the sensitivity result and a trigger for re-evaluation if the weight changes later.
