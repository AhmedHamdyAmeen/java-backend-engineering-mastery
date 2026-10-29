# STF-012 · Technical proposals — Lecture scripts

**Video:** 98 min · **Running case:** *Platform 2.0* — the strategy, governance, and platform direction from STF-P1 must now be adopted by about 20 product teams who did not ask for them; role-players act as engineering managers, skeptical tech leads, product, finance, security, and executives.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## STF-012-L01 · Why good ideas fail on paper (10 min)
**Goal:** name the common ways a sound idea is rejected because of how it was written.

**Key points**
- Readers decide in the first page whether the problem matters to them.
- Typical failures: solution first, hidden costs, no alternatives, no clear ask.
- A proposal is a tool for a decision, not a record of your thinking.
- Surprise kills proposals; people who first hear of it in review will resist.

**Show:** a rejected RFC, annotated: where a reader stopped caring (page one, no problem statement), and what was missing (cost, alternatives, decision needed).

**Check:** What is a proposal for? *(To enable a decision by the right people.)*

---

## STF-012-L02 · Problem framing (12 min)
**Goal:** make readers agree the problem is worth solving before they see the solution.

**Key points**
- State who is hurt, how much, and since when, with a number if possible.
- Separate the problem from symptoms and from your preferred solution.
- Say what is out of scope and what happens if nothing is done.
- Test the framing with two skeptical readers before writing more.

**Show:** a problem statement: "Twenty teams maintain 20 different pipelines; new services take 3 weeks to reach production; 4 audit findings last year came from pipeline drift" (numbers from the STF-009 baseline; verify before recording).

**Check:** Why test the framing first? *(If readers disagree on the problem, no solution will be accepted.)*

---

## STF-012-L03 · Evidence and alternatives (12 min)
**Goal:** support the proposal with evidence and honest alternatives.

**Key points**
- Use data, incidents, and prototype results; label opinion as opinion.
- Always include "do nothing" and at least two real alternatives.
- Compare on the same criteria: cost, risk, time, effect on teams.
- State what you do not know and how you will find out.

**Show:** a decision table: do nothing, extend current pipelines, golden path, buy a vendor tool; rows for cost, time, risk, team effort, with the reasoning for the recommendation.

**Check:** Why include "do nothing"? *(It is the baseline every reader silently compares against.)*

---

## STF-012-L04 · Structure of a strong RFC (12 min)
**Goal:** give the document a shape readers can navigate and critique.

**Key points**
- Order: summary, problem, goals and non-goals, proposal, alternatives, costs and risks, rollout, open questions, decision needed.
- The summary alone should let a busy reader decide whether to engage.
- Put costs and risks in plain view, not an appendix.
- End with a specific ask and a review deadline.

**Show:** a one-page RFC template with each heading and a one-line instruction under it.

**Check:** Where should risks go? *(In the main body, visible, with mitigations.)*

---

## STF-012-L05 · Running the review to a decision (12 min)
**Goal:** circulate, respond, and close the review.

**Key points**
- Talk to key reviewers before publishing; no surprises.
- Set a review window and name the decision maker up front.
- Answer every comment: accepted, rejected with reason, or deferred with owner.
- Close the review: record the decision, dissent, and follow-ups, even if the answer is no.

**Show:** a review tracker with columns: comment, author, severity, response, status; and a decision record template.

**Check:** What happens if the review never closes? *(The proposal dies slowly and teams act on rumours; always record a decision.)*

---

## STF-012-L06 · One proposal, three audiences (10 min)
**Goal:** serve engineers, managers, and executives from one source of truth.

**Key points**
- Engineers want design detail and trade-offs; managers want effort, timing, and risk to their roadmap; executives want cost, benefit, and the decision.
- Keep one document; layer it: summary for executives, impact section for managers, detail for engineers.
- Use each audience's words and avoid jargon in the summary.
- Check each layer stands alone.

**Show:** the golden-path RFC with three highlighted entry points: a 5-line summary, a "what changes for your team" section, and the technical design.

**Check:** Why one document instead of three? *(Separate documents drift apart and create conflicting versions.)*

---

## STF-012-L07 · Demo: rewriting a rejected RFC so it gets approved (15 min)
**Goal:** repair a solution-first RFC for the golden path; prepares STF-012-LAB1.

**Steps**
1. Read the rejection comments and sort them: framing, evidence, cost, process.
2. Rewrite the opening as a problem statement with baseline numbers.
3. Add alternatives and a visible cost and risk section.
4. **Planned mistake:** answering critics by defending the old text. Fix: change the document where the criticism is right and explain where it is not.
5. Pre-circulate to two former critics and incorporate their feedback.
6. Republish with a review window and a named decision maker.

---

## STF-012-L08 · Demo: handling 60 comments on a controversial proposal (15 min)
**Goal:** reach a decision despite a heavy comment load; prepares STF-012-LAB1.

**Steps**
1. Cluster the 60 comments into themes (security, autonomy, migration cost, tooling).
2. Mark blocking versus non-blocking; answer blockers in the document.
3. Hold a short synchronous session on the two hardest themes only.
4. **Planned mistake:** replying to all 60 one by one over two weeks, and missing the deadline. Fix: answer by theme, update the text once, and keep the review window.
5. Record decision, owner, dissent, and follow-up items.
6. Announce the outcome to all commenters and thank them.
