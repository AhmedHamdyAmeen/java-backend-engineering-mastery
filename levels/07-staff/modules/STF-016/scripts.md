# STF-016 · Decision facilitation — Lecture scripts

**Video:** 94 min · **Running case:** *Platform 2.0* — the strategy, governance, and platform direction from STF-P1 must now be adopted by about 20 product teams who did not ask for them; role-players act as engineering managers, skeptical tech leads, product, finance, security, and executives.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## STF-016-L01 · Why technical decisions get stuck (10 min)
**Goal:** diagnose the reasons a decision drags on.

**Key points**
- No clear owner, no deadline, or no agreed criteria.
- Hidden disagreement: people argue solutions while their values differ.
- Fear of being wrong or blamed; too many people want a veto.
- Cost of waiting is rarely written down, so delay feels free.

**Show:** a checklist of five stuck-decision causes with a question to test each ("Who decides? By when? On what criteria?").

**Check:** Why does delay feel free? *(Its cost is invisible until written down.)*

---

## STF-016-L02 · Structuring a decision (12 min)
**Goal:** frame the decision so a group can reach it.

**Key points**
- State the decision, the options, the criteria, the owner, and the deadline.
- Agree criteria before comparing options.
- Separate who decides, who advises, and who must be informed.
- Keep the scope small: split large decisions into steps.

**Show:** a decision brief: question, options, criteria with weights, owner, advisers, deadline, what happens at the deadline.

**Check:** Why agree criteria before options? *(Otherwise people choose criteria to fit their preferred option.)*

---

## STF-016-L03 · Making trade-offs explicit (12 min)
**Goal:** turn arguments about people into choices about values and evidence.

**Key points**
- Every option gains something and gives up something; write both.
- Find what is factual (can be measured) and what is a value (can only be chosen).
- Test claims with data or a small experiment.
- Name the underlying values: speed vs consistency, autonomy vs safety, cost vs resilience.

**Show:** a trade-off table for observability stacks: options against cost, team effort, migration risk, flexibility, with the value each criterion represents.

**Check:** How do you handle a disagreement about facts? *(Get the data or run a small test.)*

---

## STF-016-L04 · Consensus and its limits (10 min)
**Goal:** know when consensus helps and when it stalls.

**Key points**
- Consensus builds commitment but costs time and can water down the answer.
- Aim for consent: "can everyone live with this?" rather than "does everyone love it?"
- Hearing every voice matters more than counting agreement.
- Set the deadline so consensus-seeking has a limit.

**Show:** a ladder: fist-to-five or consent check, what to do at each result (proceed, adjust, escalate).

**Check:** What is the difference between consensus and consent? *(Consensus means everyone prefers it; consent means nobody has a serious objection.)*

---

## STF-016-L05 · Disagree and commit (10 min)
**Goal:** use "disagree and commit" without losing trust.

**Key points**
- It works when the decision is heard, owned by a named person, and reversible or reviewable.
- Dissent is recorded, not erased.
- Commit means act on the decision, not quietly resist.
- Set a review date for the assumptions that were disputed.

**Show:** a decision record line: "Dissent: team B preferred stack X because of cost; review at six months using agreed metrics."

**Check:** What must happen to dissent? *(Be recorded and, where useful, reviewed later.)*

---

## STF-016-L06 · Decisions that stick (10 min)
**Goal:** record and communicate decisions so they are followed.

**Key points**
- Write the decision, reasons, owner, dissent, and date in one place (an ADR).
- Tell everyone affected, including those absent.
- Define what would reopen the decision.
- Follow up: actions, owners, deadlines.

**Show:** a decision record template: context, decision, options considered, consequences, dissent, revisit trigger.

**Check:** Why define a revisit trigger? *(It stops endless reopening while allowing change when facts change.)*

---

## STF-016-L07 · Demo: facilitating the "one CI system or many" debate (15 min)
**Goal:** run a structured decision session; prepares STF-016-LAB1.

**Steps**
1. Pre-work: collect positions, agree the decision owner and the deadline.
2. Set criteria with the group: cost, speed, security evidence, team autonomy.
3. Score options together and surface which differences are facts and which are values.
4. **Planned mistake:** the facilitator states their preferred answer to speed things up. Fix: return to criteria and ask the owner to decide.
5. Check consent; record dissent.
6. Publish the decision record the same day.

---

## STF-016-L08 · Demo: a decision meeting where the facilitator does not decide (15 min)
**Goal:** show the facilitator's role: process, not answer; prepares STF-016-LAB1.

**Steps**
1. Open by stating who decides and by when.
2. Keep time and make sure each lead speaks; summarize, do not argue.
3. When the group splits, ask what evidence would change each side's mind.
4. **Planned mistake:** slipping into advocacy for the option you like. Fix: say so, step back, and hand the question to the owner.
5. The owner decides; confirm understanding and commitment from each lead.
6. Record owner, decision, dissent, review date.
