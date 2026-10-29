# SRC-017 · Technical debt — Lecture scripts

**Video:** 75 min · **Running case:** *Order Processing at 10×* — Shop Platform's order subsystem must handle a 10× growth forecast, a 99.95% availability commitment, and a 15-minute recovery objective.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRC-017-L01 · What technical debt is and isn't (10 min)
**Goal:** use the debt metaphor precisely and classify debt.

**Key points**
- Technical debt: a design or implementation shortcut, or a gap, that makes future change costlier; the "interest" is the extra cost each time you touch it.
- Quadrants: deliberate or inadvertent, prudent or reckless. Deliberate and prudent ("ship now, fix next sprint, knowing the cost") is a valid choice.
- Not debt: bugs, missing features, or code you simply dislike.
- Debt with no interest (code nobody changes) can be left alone.

**Show** A 2×2 with an example in each cell from the Shop Platform: *deliberate-prudent* a manual reconciliation step before launch; *inadvertent-prudent* a design that was good until volume grew; *deliberate-reckless* skipping tests; *inadvertent-reckless* copy-pasted payment logic unaware of consequences.

**Check:** Why is code nobody changes low-priority debt? *(It pays no interest, since no change work is slowed down.)*

---

## SRC-017-L02 · Measuring the interest (12 min)
**Goal:** express debt in concrete costs.

**Key points**
- Costs are time, risk, and money: slower changes, incident frequency, onboarding time, infrastructure cost.
- Gather evidence: how long a typical change in this area takes, how many incidents trace to it, how often it is touched (from version history).
- Estimate interest per month, such as engineer-days lost, plus the probability and cost of failure.
- Admit uncertainty with ranges rather than false precision.

**Show** Worked estimate: order pricing module touched 18 times last quarter; each change takes about 2 extra days due to missing tests; interest about 36 engineer-days per quarter, plus 2 incidents.

**Check:** What three kinds of cost express interest? *(Time, risk, and money.)*

---

## SRC-017-L03 · A debt register (8 min)
**Goal:** keep a lightweight list that supports decisions.

**Key points**
- Each item: description, area, type (quadrant), interest estimate, cost to fix, risk, owner, evidence links.
- Keep it where the team works (tracker or repository), reviewed regularly, not a graveyard.
- Remove items that no longer matter; merge duplicates.
- A list with no costs cannot be prioritized.

**Show** Register row: *DEBT-12 | pricing has no tests | inadvertent-prudent | interest 36 days/quarter | fix 15 days | risk: high | owner: orders team | evidence: PR history.*

**Check:** What makes a debt register usable? *(Each item has costs and evidence, so items can be compared.)*

---

## SRC-017-L04 · Prioritizing by cost of delay (10 min)
**Goal:** rank debt by what waiting costs.

**Key points**
- Cost of delay: the interest plus the risk you carry for each period you wait.
- Compare against cost to fix: a simple ratio such as interest per period over fix cost orders items.
- Consider timing: debt in an area about to receive heavy feature work has a high payoff now.
- Include risk items (security, reliability) that are not about speed.

**Show** Table: item | monthly interest | fix cost | payback months | risk | rank. Example: payback of 15 days of fix against 12 days per month interest is about 1.25 months.

**Check:** Why does upcoming work in an area raise a debt item's priority? *(Interest will be paid more often there.)*

---

## SRC-017-L05 · Incremental remediation (10 min)
**Goal:** pay down debt alongside feature work instead of in rewrites.

**Key points**
- Boy-scout rule: leave code a little better than you found it, within the change you are making.
- Strangler technique: route new behavior to a new implementation and retire the old piece by piece.
- Make the change safe first: add characterization tests before refactoring.
- Allocate a steady share of capacity, or attach debt work to features that touch the area.
- "Rewrite everything" is rarely a remediation plan: it delays value and repeats risk.

**Show** A strangler plan for pricing: add tests, extract an interface, route the new discount rules to a new module behind a flag, shrink the old module until removable.

**Check:** Why add tests before refactoring? *(To confirm behavior stays the same.)*

---

## SRC-017-L06 · Making the case (10 min)
**Goal:** persuade leadership with business language.

**Key points**
- Translate to outcomes: faster delivery, fewer incidents, lower cost, reduced risk, with numbers and ranges.
- Offer options: do nothing (state the cost), partial, full; and a small first step with a checkpoint.
- Know the audience: product cares about delivery dates and customer impact, finance about cost.
- Report results afterward, so later requests are trusted.

**Show** One-page pitch: problem, evidence, cost of delay, proposed work and cost, options, expected outcome and how it will be measured.

**Check:** What does a good pitch show for "do nothing"? *(The ongoing cost and risk of delay.)*

---

## SRC-017-L07 · Demo: turning a vague complaint into a funded debt item (15 min)
**Goal:** convert "the order code is a mess" into a prioritized, approved item; prepares SRC-017-LAB1.

**Steps**
1. Start with the complaint and ask where it hurts: which changes, how long, which incidents.
2. Pull evidence: change history, cycle times, incident links for the pricing module.
3. Estimate interest and fix cost with ranges; classify the debt.
4. **Planned mistake:** propose a rewrite of the entire order module. Fix: scope a strangler plan with a first slice and checkpoint.
5. Write the one-page pitch with options and expected outcome.
6. Role-play the product conversation and capture the decision.

**Check:** What replaced the rewrite proposal? *(A small first slice with a checkpoint, using the strangler approach.)*
