# SRB-019 · Risk management — Lecture scripts

**Video:** 82 min · **Running case:** *The FulfillCo integration* — the engineer leads the four-team program planned in SRB-P1 through delivery; role-players act as team leads, product, finance, and security.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRB-019-L01 · Risk in technical programs (10 min)
**Goal:** explain what a risk is and why programs need a managed view of it.

**Key points**
- A risk is an uncertain event that could hurt the program; an issue is a risk that has happened.
- Programs fail from unmanaged risks more often than from known problems.
- Risk management is cheap early and expensive late.
- The aim is better decisions under uncertainty, not eliminating all risk.

**Show** A line: *risk (might happen) -> trigger -> issue (has happened) -> response.* Example: *the FulfillCo warehouse API may not be ready by week 6.*

**Check:** What is the difference between a risk and an issue? *(A risk might happen; an issue already has.)*

---

## SRB-019-L02 · Identifying risks (10 min)
**Goal:** find risks across technical, dependency, people, and schedule categories.

**Key points**
- Technical: unproven technology, data quality, performance at scale.
- Dependency: another team's API, vendor contract, shared environment.
- People: key-person dependency, availability, skill gaps.
- Schedule: estimates with no slack, fixed external dates, long lead items.
- Methods: pre-mortem ("it failed, why?"), walk the dependency map, ask each team lead for their top three worries.

**Show** A pre-mortem prompt and a sample of outputs for the FulfillCo program: legacy data quality, one expert on the warehouse system, a security review queue.

**Check:** What does a pre-mortem ask? *(Imagine the program failed; what caused it?)*

---

## SRB-019-L03 · Risk registers that are used (10 min)
**Goal:** keep a register that changes decisions.

**Key points**
- Fields: description, likelihood, impact, score, owner, trigger, response, status, review date.
- Every risk has one named owner and an observable trigger.
- Review on a rhythm (monthly, or weekly for top risks) and close or add risks each time.
- Keep it short: track the top ten that matter.
- A register nobody reads is paperwork; link reviews to plan changes.

**Show** Register table: ID | risk | likelihood | impact | owner | trigger | response | status. Example trigger: *API contract not signed by week 3.*

**Check:** Why does each risk need a trigger? *(So you know when it is turning into an issue and can act.)*

---

## SRB-019-L04 · Buying information early (12 min)
**Goal:** reduce uncertainty early at low cost.

**Key points**
- Spike: time-boxed investigation to answer a technical question.
- Prototype: a thin end-to-end slice that exposes integration problems.
- Staged commitments: commit to the next stage, not the whole program, until risks fall.
- Tackle the riskiest, least understood parts first, not the easiest.
- Record what you learned and update the register.

**Show** A table: risk | question | spike or prototype | time box | decision it enables. Example: *can we sync stock at the required rate? | load spike on sync path | 3 days | choose events or batch.*

**Check:** Why do risky work first? *(Learning early leaves time to change the plan.)*

---

## SRB-019-L05 · Contingency planning (10 min)
**Goal:** prepare responses and decide when to use them.

**Key points**
- Mitigation reduces likelihood or impact now; contingency is the plan if the risk occurs.
- A contingency has a trigger, an owner, actions, and a cost.
- Decide the invocation threshold in advance, so the decision is not made under panic.
- Some contingencies need early investment, such as keeping the old system running.
- Review contingencies when conditions change.

**Show** Contingency card: risk | trigger | action | owner | cost | decision deadline. Example: *if warehouse API slips past week 6, use batch file exchange for phase one.*

**Check:** What is the difference between mitigation and contingency? *(Mitigation acts before the risk occurs; contingency is the plan after it occurs.)*

---

## SRB-019-L06 · Demo: a monthly risk review that changes the plan (15 min)
**Goal:** run a monthly review of the FulfillCo program risks that leads to a plan change; prepares SRB-019-LAB1.

**Steps**
1. Send the register ahead and ask each owner to update status and triggers.
2. Check which triggers have fired and which top risks changed score.
3. Discuss the top three with owners: is the response working?
4. **Planned mistake:** review every risk equally and run out of time. Fix: spend the time on the top risks and skim the rest.
5. Decide plan changes (add a spike, reorder work, start a contingency early) and update dates.
6. Record decisions and new risks, and share a short summary.

**Check:** How do you know a review was worthwhile? *(It changed something: plan, priority, or a response.)*

---

## SRB-019-L07 · Demo: invoking a contingency plan when a dependency slips (15 min)
**Goal:** invoke a contingency when the warehouse API slips; prepares SRB-019-LAB1.

**Steps**
1. Notice the trigger: the contract is unsigned at week 3 and the provider reports a slip.
2. Confirm the facts with the provider and estimate the new date.
3. Compare the threshold in the contingency card with the situation.
4. **Planned mistake:** wait another week hoping for recovery. Fix: follow the agreed threshold and invoke at the decision deadline.
5. Communicate the switch to affected teams and leadership with impact and options.
6. Update the register, timeline, and costs; set a new trigger for returning to the original plan.

**Check:** Why set the invocation threshold in advance? *(So the decision follows the plan rather than hope or pressure.)*
