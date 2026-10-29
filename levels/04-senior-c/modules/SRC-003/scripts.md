# SRC-003 · Architecture trade-offs — Lecture scripts

**Video:** 96 min · **Running case:** *Order Processing at 10×* — Shop Platform's order subsystem must handle a 10× growth forecast, a 99.95% availability commitment, and a 15-minute recovery objective.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRC-003-L01 · Every decision is a trade-off (10 min)
**Goal:** accept that every option buys something and costs something.

**Key points**
- If an option has no downside, you have not looked hard enough.
- Compare options on the prioritized attributes from the utility tree, not on taste.
- Cost includes build, run, learn, and change later.
- "It depends" is an incomplete answer; finish it with "on which attribute matters most".

**Show:** a two-option table for order storage (single PostgreSQL vs sharded) with a gain and a cost per attribute.

**Check:** What should you compare options against? *(The prioritized quality attributes and cost.)*

---

## SRC-003-L02 · One-way and two-way doors (10 min)
**Goal:** spend design effort where reversal is expensive.

**Key points**
- Two-way door: easy to reverse (a library, an internal endpoint); decide fast.
- One-way door: costly to reverse (public API, data model, shard key, cloud vendor); decide carefully.
- Reversibility can be bought: feature flags, abstraction at the right place, expand-and-contract migrations.
- Common failure: slow on reversible things, fast on irreversible ones.

**Show:** a list of order-subsystem decisions sorted into doors with a reversal cost estimate.

**Check:** Which decision deserves more analysis, a shard key or a logging library? *(The shard key; it is a one-way door.)*

---

## SRC-003-L03 · Complexity budgets (12 min)
**Goal:** treat complexity as a cost that is spent deliberately.

**Key points**
- Complexity costs cognitive load, operational burden, onboarding time, and incident risk.
- Each new component adds failure modes and on-call work.
- Set a budget: how many moving parts can this team operate well?
- Spend complexity only on the top-priority attributes.

**Show:** a count of components, runbooks, and on-call pages added by each option, next to team size.

**Check:** Why count operational burden in a design comparison? *(Because the team must run it forever; it is part of the cost.)*

---

## SRC-003-L04 · The cost of abstraction (10 min)
**Goal:** judge when an abstraction pays for itself.

**Key points**
- Abstractions hide detail and cost indirection, leaky behavior, and debugging time.
- Abstract after the second or third real use, not for imagined futures.
- "We might switch databases" is a weak reason; ask what the switch would cost without it.
- Good abstractions sit at stable boundaries.

**Show:** a repository interface wrapping JPA "to allow swapping databases" versus a module boundary that enforces ownership; compare benefit and cost.

**Check:** When is an abstraction justified? *(When real, repeated variation or a stable boundary makes its cost worthwhile.)*

---

## SRC-003-L05 · Lightweight architecture evaluation (14 min)
**Goal:** run a half-day ATAM-style review.

**Key points**
- Steps: present drivers (utility tree), present the options, map options to scenarios, find risks and trade-offs, discuss.
- Walk each high-priority scenario through each option; ask "what happens?"
- Include operators and a skeptical reviewer.
- Output: ranked options, risks, sensitivity points, open questions.

**Show:** a grid of scenarios by option with +, 0, - and a note per cell.

**Check:** What do you walk through each option? *(The high-priority scenarios from the utility tree.)*

---

## SRC-003-L06 · Risks, sensitivity points, and trade-off points (10 min)
**Goal:** use the standard vocabulary to record findings.

**Key points**
- Risk: a decision that may cause trouble against a scenario.
- Sensitivity point: a parameter whose value strongly affects an attribute (pool size, replica lag).
- Trade-off point: a decision that improves one attribute and hurts another.
- Record each with the scenario affected and an owner.

**Show:** three findings: risk "single primary at 10× peak"; sensitivity "replication lag"; trade-off "synchronous replica improves durability, adds commit latency".

**Check:** What is a trade-off point? *(A decision that helps one quality attribute and hurts another.)*

---

## SRC-003-L07 · Demo: evaluating three designs for order storage (15 min)
**Goal:** compare vertical scale-up, replicas plus partitioning, and sharding on the utility tree; prepares SRC-003-LAB1.

**Steps**
1. List the top scenarios: 10× write load, 15-minute recovery, p99 latency.
2. Describe each option honestly, including its strengths.
3. Score each against each scenario with a short reason.
4. **Planned mistake:** the favorite option is described in detail while the others are thin. Fix: give each option its best advocate for five minutes.
5. Note risks, sensitivity points, and the complexity cost per option.
6. Pick one provisionally and list what evidence would change the pick.

---

## SRC-003-L08 · Demo: an architecture review that changes its mind (15 min)
**Goal:** show a review where new evidence overturns the first choice.

**Steps**
1. Present the initial choice and its scenarios.
2. A reviewer from operations asks for the recovery procedure; walk it step by step.
3. **Planned mistake:** defend the choice instead of testing the claim. Fix: time the recovery in a rehearsal; it takes 50 minutes against a 15-minute target.
4. Revisit the options with this evidence; a simpler option now meets the target.
5. Update the ADR: status, new decision, the evidence, what was learned.
6. Discuss how to make changing a decision socially safe.
