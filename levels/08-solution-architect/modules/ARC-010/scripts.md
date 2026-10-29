# ARC-010 · Legacy modernization — Lecture scripts

**Video:** 83 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-010-L01 · Why modernize, and why not (8 min)
**Goal:** tie modernization to business reasons and know when to leave a system alone.

**Key points**
- Good reasons: blocks business change, security or support risk, high run cost, skills shortage.
- Weak reasons: "it is old", fashion, résumé-driven choices.
- Modernization has cost and risk; a stable system with low change need may be best left alone.
- Always state the outcome: faster change, lower risk, lower cost.

**Show:** two proposals for the Larkspur ERP: "replace because it is old" versus "keep, wrap with APIs, because finance depends on it and change demand is low". Compare outcomes.

**Check:** Is age alone a reason to modernize? *(No; a business or risk reason is needed.)*

---

## ARC-010-L02 · Rehost, replatform, refactor, replace, retire (14 min)
**Goal:** know the disposition options and when each fits.

**Key points**
- Rehost: move as is to new infrastructure; quick, little benefit beyond hosting.
- Replatform: small changes to use managed services; moderate effort and benefit.
- Refactor or re-architect: change the code and structure to gain agility or scale; high effort.
- Replace: swap for a packaged product or SaaS; retire: switch off; retain: keep as is for now.
- Names vary by source; use one set consistently.

**Show:** a Larkspur table: application, option, reason. Web shop: replace; reporting: replatform; ERP: retain; an old store-labelling tool: retire.

**Check:** When is rehosting a poor choice? *(When the reason for moving is a design problem that hosting will not fix.)*

---

## ARC-010-L03 · Assessing an application portfolio (12 min)
**Goal:** assess applications on comparable criteria.

**Key points**
- Business value: how critical, how many users, link to capabilities.
- Technical condition: age, supportability, security, test coverage, documentation.
- Risk: vendor end-of-support, key-person dependence, compliance.
- Cost to change and to run; integration entanglement.
- Plot value versus condition to suggest dispositions.

**Show:** a scoring sheet with columns value, condition, risk, cost to change, dependencies, and a quadrant chart: high value/low condition (invest or replace), low value/low condition (retire).

**Check:** What does a high-value, poor-condition application call for? *(Investment: refactor or replace, with a plan.)*

---

## ARC-010-L04 · Sequencing and coexistence (10 min)
**Goal:** order the work to deliver value early and limit risk.

**Key points**
- Avoid big-bang cutovers; move slices at a time.
- Strangler pattern: route some functions to the new system while the old one continues, shrinking the old over time.
- Coexistence needs data synchronization, routing, and clear system-of-record rules per entity.
- Sequence by value, risk, dependency, and learning; start with a thin, valuable slice.

**Show:** a Larkspur timeline: slice one: browsing and checkout on new platform for web; slice two: mobile; slice three: store pickup; old shop routes remaining traffic until retired.

**Check:** What does the strangler approach avoid? *(A risky big-bang cutover.)*

---

## ARC-010-L05 · The modernization business case (10 min)
**Goal:** make a case a CFO can evaluate.

**Key points**
- Benefits: revenue enabled, cost avoided, risk reduced; each with an estimate and confidence.
- Costs: build or buy, migration, dual running, training, retirement, and ongoing run.
- Compare with doing nothing, including the cost of delay and risk.
- State assumptions and sensitivities; verify numbers with finance.

**Show:** a one-page table: option, cost over five years, benefits, payback, risk, with "do nothing" as the baseline row.

**Check:** Why include "do nothing" as an option? *(It is the baseline that shows the real cost and risk of leaving things.)*

---

## ARC-010-L06 · Demo: assessing Larkspur's application portfolio (15 min)
**Goal:** assess and disposition the portfolio. Prepares `ARC-010-LAB1`.

**Steps**
1. List applications: web shop, store POS integration, order management in ERP, CRM, reporting.
2. Gather evidence per application: support status, incidents, change backlog, users, cost.
3. Score value, condition, risk, and cost to change; plot on the quadrant.
4. Assign dispositions and order them by dependency and value.
5. **Planned mistake:** scoring is done from opinions in one meeting; the ERP is marked "replace" because everyone dislikes it. Fix: use the evidence sheet and reassess; ERP moves to retain-and-wrap.
6. Review with role-played owners and record disagreement.

**Check:** Why use evidence over opinion? *(Opinion biases toward what people dislike; evidence supports defensible decisions.)*

---

## ARC-010-L07 · Demo: replace the web shop, retain the ERP — the case (14 min)
**Goal:** build the case for one concrete pair of decisions.

**Steps**
1. State the outcomes: faster promotion changes, mobile support, stable finance.
2. Describe three options for the web shop: keep, refactor, replace with SaaS or suite; "retain" for the ERP with an API wrapper.
3. Estimate costs and benefits for five years with ranges; include dual running and migration.
4. Show the coexistence plan: strangler routing, product and order data sync, ERP stays finance master.
5. **Planned mistake:** the benefit line counts all future online growth as caused by the new shop. Fix: attribute only the growth tied to specific capabilities and show a conservative range.
6. Present risks, triggers to revisit, and the recommendation.

**Check:** Why retain the ERP in this case? *(Low change demand, finance dependence, and high replacement risk relative to benefit.)*
