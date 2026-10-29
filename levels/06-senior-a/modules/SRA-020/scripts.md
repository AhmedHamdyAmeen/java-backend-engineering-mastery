# SRA-020 · Succession and delegation — Lecture scripts

**Video:** 78 min · **Running case:** *Commerce 2030* — the group formed by Shop and FulfillCo has 25 engineering teams and plans a third-party seller marketplace, a five-country expansion, and doubled order volume each year for three years; the strategy must now be adopted by 25 teams, funded, and executed, with role-players acting as managers, product, finance, security, and executives.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRA-020-L01 · Key-person risk (10 min)
**Goal:** find where the organization depends on one person, including you.

**Key points**
- Key-person risk: if one person is away, work, decisions, or knowledge stop.
- Signs: everything routes through you, only you can approve or fix something, no one else knows the history.
- It harms the organization (single point of failure) and you (no time, no growth, no rest).
- Being indispensable is a risk, not a status.

**Show:** a risk map: area, person, what stops if absent, how long until trouble, current backup.

**Check:** Why is being indispensable a problem? *(It is a single point of failure for the organization and a limit on your own growth.)*

---

## SRA-020-L02 · Delegating ownership (12 min)
**Goal:** hand over ownership of an outcome, not only tasks.

**Key points**
- A task is "do this"; ownership is "make this area succeed and decide how".
- Hand over the goal, the context, the constraints, and the authority to decide.
- Expect different choices than yours; accept them within the agreed boundaries.
- Check in on outcomes and offer help on request; do not take it back at the first problem.

**Show:** a delegation note: area, outcome expected, constraints, decisions the owner makes alone, decisions needing consultation, check-in rhythm.

**Check:** What separates delegated ownership from delegated tasks? *(The authority to decide and responsibility for the outcome.)*

---

## SRA-020-L03 · Decision rights (8 min)
**Goal:** state who decides what so people do not wait for you.

**Key points**
- For each type of decision, name who decides, who must be consulted, and who is informed.
- Write the boundaries: cost limits, risk levels, and what must be escalated.
- Unclear rights send decisions back to the senior person by default.
- Review the document when the area or the team changes.

**Show:** a decision-rights table for the event platform: schema changes (owner team decides, consumers consulted), new topics (owner decides), retention changes (owner decides, security consulted), cross-domain breaking changes (architecture group decides).

**Check:** What does a decision-rights document prevent? *(Decisions queuing up for a single senior person.)*

---

## SRA-020-L04 · Growing successors (10 min)
**Goal:** prepare people to take over your responsibilities.

**Key points**
- Name at least one successor path for each critical area; ask the person.
- Give increasing scope: shadow, co-lead, lead with you reviewing, then lead alone.
- Let successors take the visible moments (reviews, presentations, incidents).
- Measure success by what continues when you are away.

**Show:** a succession ladder for "architecture review practice": observe, review with you, lead reviews, train others.

**Check:** How do you know succession is working? *(The area runs well when you are not there.)*

---

## SRA-020-L05 · Knowledge that survives you (8 min)
**Goal:** record knowledge so it does not leave with a person.

**Key points**
- Record the why (decisions, trade-offs), not only the what.
- Keep it where people look: next to the code, in decision records, and in runbooks.
- Use short formats: decision records, one-page area guides, recorded design walk-throughs.
- Test the documentation: ask someone else to use it without you.

**Show:** a survival checklist: decision records, area guide, runbooks tested by someone else, a list of key contacts, access and ownership transferable without you.

**Check:** How do you test your documentation? *(Have someone else use it to do the job without your help.)*

---

## SRA-020-L06 · Demo: mapping your own key-person risks (15 min)
**Goal:** map where Commerce 2030 depends on you; prepares SRA-020-LAB1.

**Steps**
1. List areas where you are the approver, the expert, or the escalation path.
2. For each, note what would stop if you were absent for a month.
3. Check the evidence: review requests, messages, and incident calls that go to you.
4. **Planned mistake:** list only tasks. Fix: list decisions and knowledge; those are the real dependencies.
5. Rank the risks, choose the top three, and name possible successors.

---

## SRA-020-L07 · Demo: a handover of decision rights for the event platform (15 min)
**Goal:** run a worked handover of the event platform to a team; prepares SRA-020-LAB1.

**Steps**
1. Choose the owner team and agree the outcomes expected: reliability, onboarding of new producers, contract stability.
2. Write the decision-rights table with the team and consult the affected consumers.
3. Hand over documentation and run a walk-through with the team lead.
4. **Planned mistake:** hand over tasks but keep approving every schema change. Fix: move schema decisions to the team and keep only a defined escalation path.
5. Set check-ins for two months, then step away and review results after a quarter.

**Show:** the final decision-rights document, signed by the owner team lead.
