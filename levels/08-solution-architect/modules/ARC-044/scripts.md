# ARC-044 · Architecture communication — Lecture scripts

**Video:** 70 min · **Running case:** *Larkspur Retail* — a mid-size retailer with 120 stores and a dated on-premises web shop; you are the solution architect for a new platform integrated with the existing ERP and CRM.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-044-L01 · One solution, many audiences (10 min)
**Goal:** explain why the same solution is told differently to each audience while staying consistent.

**Key points**
- Executives decide on value, cost, risk, and timing; engineers need contracts, constraints, and reasons; operations need run impact; stores need what changes for them.
- One set of facts, several framings: never change the facts, only the depth and the story.
- Start from the audience's question and the decision or action you want from them.
- Choose the diagram per audience: context and roadmap for executives, component and sequence views for engineers.
- Keep one source of truth (the architecture pack) so versions of the story do not diverge.

**Show:** a table for Larkspur: audience, their question, what they must decide or do, the artifact used (roadmap one-pager, HLD, LLD, store change sheet).

**Check:** What may change between audiences and what must not? *(Depth and framing may change; the facts may not.)*

---

## ARC-044-L02 · Presenting to executives (12 min)
**Goal:** present a solution in business terms with a clear ask.

**Key points**
- Open with the decision you need, then the reason: value, cost, risk, timing, and what happens if we do nothing.
- Use business language: orders, stock accuracy, store hours saved, rather than service names.
- Show options considered and why this one, in one slide; give the headline cost and benefit with key assumptions stated.
- Name the top three risks with mitigations, and the next steps with owners and dates.
- Keep it short: ten minutes, plus backup material for questions.

**Show:** a ten-minute outline for Larkspur: the ask; the problem; the recommendation; options compared; roadmap with first value date; cost and benefit; top risks; decision and next steps.

**Check:** What should executives be able to state after the talk? *(The decision asked of them and why.)*

---

## ARC-044-L03 · Presenting to engineering teams (10 min)
**Goal:** present the design with the technical depth teams need to build it.

**Key points**
- Start with context and constraints, then structure: components, responsibilities, interfaces, data, and failure behaviour.
- Explain the decisions and the rejected alternatives, so teams can make consistent local choices.
- Show the contract details: events, APIs, error cases, and non-functional targets.
- Invite challenge early; record questions and follow-ups with owners.
- Be clear what is fixed (principles, contracts) and what teams may decide.

**Show:** a session plan: 10 min context, 20 min component and sequence walkthrough for order fulfilment, 15 min contracts and failure cases, 15 min questions logged as follow-ups.

**Check:** Why explain rejected alternatives to engineers? *(So they understand the trade-offs and make consistent choices when facing similar decisions.)*

---

## ARC-044-L04 · Defending a design (10 min)
**Goal:** answer challenges while separating facts, assumptions, and trade-offs.

**Key points**
- Listen to the whole challenge; restate it; then answer.
- Label your answer: "this is measured" (fact), "this is assumed and we will confirm by…" (assumption), "we chose X over Y because…" (trade-off).
- Do not claim certainty you do not have; say what you will check and by when.
- Do not defend by authority; defend by evidence, test results, or decision records.
- If a challenge is valid, concede and record the change; a good challenge improves the design.

**Show:** three sample answers to the same question ("will it handle Black Friday?"): a fact (load test result), an assumption (growth forecast, owner and date), and a trade-off (cost of extra capacity versus risk).

**Check:** What should you do when you do not know the answer? *(Say so, state what you will check, and commit to a date.)*

---

## ARC-044-L05 · Demo: Larkspur's ten-minute executive presentation (14 min)
**Goal:** build and rehearse the executive presentation for the Larkspur platform decision. This prepares ARC-044-LAB1.

**Steps**
1. Write the ask first: approve the platform recommendation and the phase-one budget at the next steering meeting.
2. Draft the storyline: problem (old web shop, stock errors), recommendation, options compared, roadmap, cost and benefit, top three risks, next steps.
3. **Planned mistake:** a slide on the integration architecture with service names and protocols. The imagined CFO asks what it means. Fix: replace it with a one-line business effect ("stock shown online matches the stores") and move the diagram to backup.
4. Convert numbers into business terms and state assumptions behind the headline figures.
5. Rehearse to ten minutes and prepare three backup slides for likely questions (cost, risk, vendor lock-in).
6. Close with the decision requested, owners, and dates, and check an observer can restate the ask.

**Check:** What was the planned mistake? *(Technical architecture detail on an executive slide instead of its business effect.)*

---

## ARC-044-L06 · Demo: a hostile technical design defense, handled (14 min)
**Goal:** handle an aggressive engineering panel with evidence and follow-ups. This prepares ARC-044-LAB1.

**Steps**
1. Prepare: list the five weakest points (ERP coupling, eventual consistency of stock, vendor lock-in, cost, migration risk) and the evidence for each.
2. Open with a concise structure and the key decisions; invite the panel to challenge.
3. **Planned mistake:** answer the claim "your stock sync will oversell" with "it will not happen". Fix: state what is measured (test results), what is assumed (peak order rate), and the trade-off (reservation window versus availability), then agree a follow-up test.
4. Concede a valid point (retry behaviour missing in the contract) and record the design change.
5. Keep calm on personal remarks: restate the technical question and answer that.
6. Close by reading back the challenges, the answers given, and follow-ups with owners and dates.

**Check:** What was the planned mistake? *(Claiming certainty instead of separating fact, assumption, and trade-off.)*
