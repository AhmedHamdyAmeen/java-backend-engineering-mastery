# SRC-010 · Architecture documentation — Lecture scripts

**Video:** 67 min · **Running case:** *Order Processing at 10×* — Shop Platform's order subsystem must handle a 10× growth forecast, a 99.95% availability commitment, and a 15-minute recovery objective.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRC-010-L01 · Documentation for different readers (10 min)
**Goal:** write for a named reader and purpose.

**Key points**
- Engineers need structure and decisions; operators need procedures and signals; leadership needs risks, costs, and outcomes.
- One document for every audience serves none.
- State the audience and the question the document answers at the top.
- Link between documents instead of copying.

**Show:** a matrix of audience, question, document type, and length for the order subsystem.

**Check:** Why avoid one document for every audience? *(Each reader needs different content and detail.)*

---

## SRC-010-L02 · C4 at subsystem scale (10 min)
**Goal:** describe a subsystem with the C4 levels that matter.

**Key points**
- Levels: context, containers, components, code; subsystem docs mostly need context and containers, plus selected components.
- Show responsibilities, technologies, and key flows, not every class.
- Add the quality attributes and constraints that shaped the design.
- Keep diagrams as text (for example Mermaid or PlantUML; verify tool choice) so they diff.

**Show:** a container diagram description: gateway, order service, PostgreSQL, Kafka, inventory, with arrows labeled by protocol.

**Check:** Which C4 levels does a subsystem description mainly need? *(Context and containers, with selected components.)*

---

## SRC-010-L03 · Docs as code (8 min)
**Goal:** keep documents current by treating them like code.

**Key points**
- Store docs in the repository beside the code; change them in the same pull request.
- Review docs; check links and diagram builds in CI.
- Give each document an owner and a review date.
- Delete or archive stale documents.

**Show:** a repository layout with `docs/architecture`, `docs/adr`, `docs/runbooks`, and a CI step checking links.

**Check:** Why change docs in the same PR as code? *(So they stay accurate and are reviewed together.)*

---

## SRC-010-L04 · Runbooks under pressure (12 min)
**Goal:** write steps a tired on-call engineer can follow.

**Key points**
- Structure: symptom, impact, quick checks, decision, actions, verification, escalation, rollback.
- Each step is a specific command or click with an expected result; never "investigate".
- Put the most likely cause first; include links to dashboards.
- Test runbooks by having someone else run them; update after incidents.

**Show:** a runbook skeleton for "order consumer lag rising".

**Check:** What is wrong with the step "investigate the database"? *(It is not specific or testable; give exact checks and expected results.)*

---

## SRC-010-L05 · Design docs that get decisions (12 min)
**Goal:** write a design doc that results in a decision in one review.

**Key points**
- Start with the decision needed, the context, goals and non-goals.
- Present options with trade-offs and a recommendation tied to quality attributes.
- Name risks, open questions, and rollout and rollback plans.
- Keep it short; pre-wire reviewers; record the outcome as an ADR.

**Show:** a design doc outline: summary, decision needed, context, goals, options, recommendation, risks, rollout.

**Check:** What should a design doc state at the top? *(The decision needed and who decides.)*

---

## SRC-010-L06 · Demo: reviewing and rewriting a confusing runbook (15 min)
**Goal:** transform a vague runbook; prepares SRC-010-LAB1.

**Steps**
1. Read the existing runbook as the on-call engineer at 3 a.m.; note every point of confusion.
2. Identify missing symptoms, vague steps, and absent rollback.
3. **Planned mistake:** rewrite it alone and call it done. Fix: have a colleague execute it; they stumble at step 4, so rewrite it with exact commands and expected output.
4. Add escalation and verification.
5. Link it from the alert.
6. Schedule a review after the next incident.
