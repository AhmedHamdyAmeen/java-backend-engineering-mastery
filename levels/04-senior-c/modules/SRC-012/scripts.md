# SRC-012 · SLO engineering — Lecture scripts

**Video:** 86 min · **Running case:** *Order Processing at 10×* — Shop Platform's order subsystem must handle a 10× growth forecast, a 99.95% availability commitment, and a 15-minute recovery objective.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRC-012-L01 · SLOs from user journeys (12 min)
**Goal:** derive SLOs from what users and the business actually need.

**Key points**
- SLI (service level indicator): a measured ratio of good events to valid events. SLO (objective): the target for that ratio over a window.
- Start from a user journey (place an order), not from what the dashboard happens to show.
- Measure at the point closest to the user that you control, such as the load balancer or gateway.
- A business commitment (99.95% availability) becomes a concrete SLI definition: what counts as good, what counts as valid.
- 99.95% over 30 days allows about 21.6 minutes of full outage.

**Show** Journey table: step | SLI | good event | window | target. Example: *submit order | successful responses under 800 ms / all valid requests | 30 days | 99.95%.*

**Check:** What is an SLI? *(A measured ratio of good events to valid events.)*

---

## SRC-012-L02 · Composing SLOs across dependencies (12 min)
**Goal:** avoid promising more nines than the dependencies allow.

**Key points**
- For hard serial dependencies, availabilities multiply: three components at 99.9% give about 99.7%.
- Redundancy, caching, retries with limits, and graceful degradation raise the composite; map each hard dependency and ask what the order flow does without it.
- Ask each dependency owner for an SLO; if there is none, treat it as unknown risk.
- Decide where to degrade (accept the order, charge later) rather than fail.

**Show** Dependency graph for the order journey (gateway, orders, inventory, payment provider, database) with each SLO, which are hard or soft, and the computed ceiling versus the 99.95% target.

**Check:** Two serial hard dependencies at 99.9% each give roughly what availability? *(About 99.8%.)*

---

## SRC-012-L03 · Error-budget policies (12 min)
**Goal:** write a policy that changes behavior when the budget runs out.

**Key points**
- Error budget: allowed unreliability, 100% minus the SLO. It turns reliability into a shared, spendable resource.
- A policy states thresholds and consequences in advance: for example, over 50% spent, extra review of risky changes; exhausted, freeze non-reliability releases until recovered.
- Product and engineering agree it before it is needed; leadership backs it.
- Exceptions are explicit and logged; a budget with no consequences is decoration.

**Show** Policy outline: SLO and window | budget thresholds | actions at each | exception process | owner | review cadence.

**Check:** What makes a budget policy real? *(Pre-agreed consequences that actually change what the team does.)*

---

## SRC-012-L04 · Multi-window burn-rate alerting (12 min)
**Goal:** page quickly on real outages and not on blips.

**Key points**
- Burn rate: how fast the budget is consumed relative to an even spend. Burn rate 1 uses exactly the budget over the window.
- Alert on burn rate, not raw error rate, using a long window for significance and a short window to confirm it is still happening.
- Common pairing from the SRE literature: fast burn (for example 14.4× over 1 h with a 5 min check) pages; slow burn (for example 1× over 3 days) opens a ticket. Verify thresholds against your SLO window before recording.
- Tune for precision (few false pages) and recall (real outages caught) using replay of past data.

**Show** Alert table: severity | long window | short window | burn rate | action. Plus a sketch of a 3-minute blip versus a 40-minute outage and which rules fire.

**Check:** Why add a short window to a burn-rate alert? *(So the alert resets quickly and only fires while the problem is ongoing.)*

---

## SRC-012-L05 · Reviewing and evolving SLOs (8 min)
**Goal:** keep SLOs useful and retire those that are not.

**Key points**
- Review quarterly: was the target met, did it match customer pain, did it drive decisions?
- An SLO nobody acts on, or that is always at 100%, is noise; tighten, loosen, or retire it.
- Incidents that did not breach any SLO reveal a missing SLI.
- Change targets with data and agreement, and record why.

**Show** Review checklist: attainment, budget use, alerts fired and actionable, incidents outside SLOs, decisions changed, proposed change.

**Check:** An SLO is always 100% met and no one looks at it. What do you do? *(Retire it or tighten it so it carries information.)*

---

## SRC-012-L06 · Demo: tuning noisy alerts with burn-rate windows (15 min)
**Goal:** replace noisy threshold alerts with burn-rate alerts; prepares SRC-012-LAB1.

**Steps**
1. Show the current alert (error rate above 1% for 1 minute) and last month's pages: most were blips.
2. Replay recorded error data against the rule and count pages versus real incidents.
3. Define burn-rate rules with long and short windows for the 99.95% SLO.
4. Replay again: blips stay silent, the two real outages page quickly.
5. **Planned mistake:** use only a long window, so the page keeps firing long after recovery. Fix: add the short confirming window.
6. Record precision and recall before and after.

**Check:** Which two numbers measure alert quality? *(Precision and recall.)*

---

## SRC-012-L07 · Demo: negotiating an error-budget policy with product (15 min)
**Goal:** agree a policy with a role-played product lead; prepares SRC-012-LAB1.

**Steps**
1. Open with the business commitment, the budget in minutes, and last quarter's spend.
2. Product pushes back: freezes are unacceptable near a launch.
3. Offer graded actions and a defined exception process instead of an all-or-nothing freeze.
4. **Planned mistake:** argue from reliability purity. Fix: connect to the customer impact and revenue at risk.
5. Agree thresholds, consequences, owners, and a review date; write it down and get sign-off.

**Check:** Why offer an exception process? *(It keeps the policy credible under pressure instead of being ignored.)*
