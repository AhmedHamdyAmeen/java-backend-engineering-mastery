# MID-066 · Technical collaboration — Lecture scripts

**Video:** 56 min · **Analogy used throughout:** a climbing team: you check each other's ropes, call out dangers kindly, teach newcomers the route, and agree who leads when views differ.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-066-L01 · Reviewing beyond style (10 min)
**Goal:** review for correctness, design, and operability.

**Key points**
- Let tools handle formatting and style; spend human attention on behavior.
- Correctness: edge cases, error handling, concurrency, transactions, security.
- Design: boundaries, naming, coupling, whether the change fits the architecture.
- Operability: logs, metrics, timeouts, migrations, rollback, config.
- Read the tests first: do they prove the behavior, or only the happy path?
- Comments should teach: say what, why, and a suggestion or question.

**Show:** a weak comment ("change this") versus a teaching one ("This retries without a limit; a failing provider would flood it. Consider a max of 3 with backoff, see MID-023").

**Check:** Why read the tests in a review? *(They show what behavior is actually verified.)*

---

## MID-066-L02 · Feedback that lands (8 min)
**Goal:** give and receive feedback constructively.

**Key points**
- Be specific and about the work, not the person.
- Separate must-fix from suggestions and nits; label them.
- Ask questions when unsure: "What happens if the list is empty?"
- Praise good work specifically; it teaches too.
- Receiving: assume good intent, ask for clarification, thank, then decide; you may disagree with reasons.

**Show:** labels such as `blocking:`, `suggestion:`, `nit:`, `question:`.

**Check:** What does labeling a comment `nit:` tell the author? *(It is minor and optional.)*

---

## MID-066-L03 · Design reviews (8 min)
**Goal:** review and present designs well.

**Key points**
- Review the problem and constraints before the solution.
- Ask about alternatives, failure modes, rollout, and operations.
- Authors: share early, state non-goals, say what feedback you want.
- Reviewers: critique the design, not the designer; offer options.
- Record the outcome in an ADR (MID-063).

**Show:** a list of reviewer questions: "What if this call times out? How do we roll back? What does it cost at 10x load?"

**Check:** What should the author say at the start of a design review? *(The problem, constraints, and what feedback is wanted.)*

---

## MID-066-L04 · Mentoring juniors (10 min)
**Goal:** help a junior grow without taking over.

**Key points**
- Give well-scoped tasks with a clear outcome and a little stretch.
- Pair: let them drive, ask questions before giving answers.
- Explain the why behind advice; point to docs and resources.
- Let them struggle briefly, then help; set a time limit for being stuck.
- Review their work kindly and thoroughly; check understanding, not just output.
- Collect feedback on how you mentor.

**Show:** a task brief: goal, context links, acceptance, a hint, and "ask me if stuck for 30 minutes".

**Check:** When pairing, who should type? *(Usually the mentee.)*

---

## MID-066-L05 · Disagreement and decisions (8 min)
**Goal:** resolve disagreements and move forward.

**Key points**
- Start from shared goals; state each position and its evidence.
- Test with data or a small experiment when possible.
- Time-box the debate; agree who decides.
- Disagree and commit: once decided, support it fully; record the dissent in the ADR.
- Escalate only when the decision is blocked or the risk is high, with a neutral summary of both views.

**Show:** a neutral escalation note: context, options A and B, trade-offs, what we need decided by when.

**Check:** What does "disagree and commit" mean? *(Voice concerns, then support the decision once made.)*

---

## MID-066-L06 · Demo: reviewing a real pull request out loud (12 min)
**Goal:** review a Shop pull request while thinking aloud. Prepares `MID-066-LAB1`.

**Steps**
1. Read the description and linked issue; restate the intent.
2. Read the tests first and note missing cases.
3. Read the code for correctness, design, and operability; write labeled comments.
4. **Planned mistake:** rewriting the author's method in a comment. Fix: describe the problem and suggest a direction; let the author write it.
5. Add one specific praise and a summary with the decision (approve, request changes).
6. Compare the review against the usefulness rubric.
