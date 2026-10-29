# SRA-013 · Decision-making under uncertainty — Lecture scripts

**Video:** 82 min · **Running case:** *Commerce 2030* — the group formed by Shop and FulfillCo has 25 engineering teams and plans a third-party seller marketplace, a five-country expansion, and doubled order volume each year for three years; the strategy must now be adopted by 25 teams, funded, and executed, with role-players acting as managers, product, finance, security, and executives.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRA-013-L01 · Deciding without all the facts (10 min)
**Goal:** accept that important decisions are made before the facts are in, and make that safe.

**Key points**
- Waiting for certainty is itself a decision, usually an expensive one.
- Separate reversible decisions (decide fast) from costly-to-reverse ones (invest in learning first).
- Uncertainty has kinds: facts you could look up, facts you could test, and futures nobody knows.
- The goal is a good decision process, not a guaranteed outcome.

**Show:** a two-by-two grid: reversibility against impact, with "choose a marketplace search tool" and "choose the seller data model" placed in different cells.

**Check:** When should you slow down? *(When the decision is costly to reverse and has high impact.)*

---

## SRA-013-L02 · Surfacing and ranking assumptions (12 min)
**Goal:** list what the decision quietly depends on and find the assumptions that matter most.

**Key points**
- Ask: "what must be true for this plan to work?"
- Rank each assumption on impact if wrong and current uncertainty.
- High impact and high uncertainty come first; the rest can be watched.
- Name an owner and a signal that would show the assumption failing.

**Show:** an assumption map, impact against uncertainty. Example: "sellers will integrate through an API" (high, high), "peak is 3× average" (medium, low).

**Check:** Which assumptions get attention first? *(High impact and high uncertainty.)*

---

## SRA-013-L03 · Experiments that buy information (12 min)
**Goal:** design the cheapest test that reduces the most important uncertainty.

**Key points**
- Write the question as a hypothesis with a measure and a threshold that decides.
- Cheap forms: a spike, a prototype, a fake door, a pilot with three sellers, a load test on a slice.
- Fix time and cost before starting; decide in advance what each outcome will cause you to do.
- Experiments that cannot change the decision are waste.

**Show:** experiment card: assumption, hypothesis, method, cost and time cap, success threshold, decision if it succeeds, decision if it fails.

**Check:** How do you know an experiment is worth running? *(Its result could change the decision, and it is cheaper than being wrong.)*

---

## SRA-013-L04 · Option value and commitment timing (10 min)
**Goal:** decide when to keep options open and when to commit.

**Key points**
- An option is a cheap right to choose later; keeping it costs something.
- Keep options when uncertainty is high and learning is coming soon.
- Commit when delay costs more than the option is worth, or when the facts are in.
- Common techniques: thin interfaces, modular boundaries, buying instead of building first.

**Show:** timeline: marketplace payments launched behind an interface with one provider; the option of a second provider kept for the cost of the interface; commit date set by contract renewal.

**Check:** Why is keeping options not free? *(Maintaining them costs effort and delays benefits; commit when delay costs more.)*

---

## SRA-013-L05 · Decision records with assumptions (8 min)
**Goal:** record a decision so it can be reopened when the world changes.

**Key points**
- Record the decision, the options considered, and the reason for the choice.
- Record the assumptions and the signals that would invalidate them.
- Set a review trigger: a date or a measurable event.
- A record without the "why" cannot be revisited, only argued about.

**Show:** decision record outline: context, decision, options, assumptions with signals, consequences, review trigger, owner.

**Check:** Why record assumptions with the decision? *(So when one fails you know exactly which decisions to revisit.)*

---

## SRA-013-L06 · Demo: an assumption map for the marketplace launch (15 min)
**Goal:** build the assumption map for the Commerce 2030 marketplace and choose experiments; prepares SRA-013-LAB1.

**Steps**
1. Write the marketplace architecture decision under discussion: a separate seller domain with its own data store.
2. List twenty assumptions with product, finance, and security in the room (sellers, volume, payments, compliance).
3. Plot impact against uncertainty and pick the top three.
4. **Planned mistake:** list only technical assumptions. Fix: add business assumptions (seller count, order mix, commission model); they carry the highest impact.
5. Design two experiments with thresholds and a cost cap; record what each result will change.

---

## SRA-013-L07 · Demo: revisiting a decision when its key assumption fails (15 min)
**Goal:** run a worked leadership session in which a recorded assumption fails and the decision is reopened; prepares SRA-013-LAB1.

**Steps**
1. Present the signal: pilot sellers push inventory in bulk files, not through the API as assumed.
2. Open the decision record and list every decision that depended on that assumption.
3. Generate options: keep, adapt (add a batch ingestion path), or reverse; estimate cost and risk of each.
4. **Planned mistake:** defend the original decision because the team already built part of it. Fix: separate sunk cost from remaining cost and decide on the future only.
5. Communicate the change and update the record, including the new assumption and review trigger.

**Show:** revised record with a "supersedes" link to the original.
