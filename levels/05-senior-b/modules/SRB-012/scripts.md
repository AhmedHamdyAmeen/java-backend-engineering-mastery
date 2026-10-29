# SRB-012 · Architecture governance — Lecture scripts

**Video:** 84 min · **Running case:** *The FulfillCo integration* — the engineer leads the four-team program planned in SRB-P1 through delivery; role-players act as team leads, product, finance, and security.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRB-012-L01 · Governance that helps (10 min)
**Goal:** describe governance that speeds good decisions rather than slowing all decisions.

**Key points**
- Governance means how decisions get made, recorded, and revisited; it is not the same as approval gates.
- Good governance gives teams fast answers for small decisions and structured review for large ones.
- Warning signs: reviews that end without decisions, one process for every change, reviewers who are never accountable for outcomes.
- Measure governance by decision time and by whether decisions stick.

**Show** Two timelines for the same decision: ungoverned (three meetings, no owner, reversed later) and governed (RFC, two-week review, decision record, one dissent noted).

**Check:** How can you tell governance is helping? *(Decisions are made on time, recorded, and not reopened by accident.)*

---

## SRB-012-L02 · RFC processes (12 min)
**Goal:** run a request-for-comments process with scope, reviewers, and a deadline.

**Key points**
- An RFC states the problem, options, recommendation, trade-offs, and what feedback is needed.
- Name required reviewers (affected teams, security if relevant) and optional ones; state the decision owner.
- Set a comment deadline and a decision date; after the deadline the owner decides.
- Outcomes are recorded: accepted, accepted with changes, rejected, or withdrawn, with reasons.
- Keep RFCs short; a long document hides the decision.

**Show** RFC template headings: context, goals and non-goals, options, recommendation, risks, rollout, open questions, reviewers, decision deadline. Add a status line: *draft, in review, decided*.

**Check:** What happens at the decision deadline? *(The named owner decides and records the outcome, even if some comments remain.)*

---

## SRB-012-L03 · Running design reviews (12 min)
**Goal:** facilitate a review that improves the design and ends with a decision.

**Key points**
- Send material early; the meeting is for discussion of risks and alternatives.
- The facilitator separates blocking concerns from suggestions and asks the author how each is handled.
- Review the design, not the person; ask questions before offering solutions.
- End by stating the decision, the changes required, and who confirms them.
- Gatekeeping signs: reviewers invent new requirements late, or the author cannot tell what would earn approval.

**Show** A review log table: concern | blocking or suggestion | author response | resolved by.

**Check:** What separates a blocking concern from a suggestion? *(A blocker is a risk that must be fixed or accepted before proceeding; a suggestion is optional.)*

---

## SRB-012-L04 · Exceptions and waivers (10 min)
**Goal:** allow deviations from standards in a controlled way.

**Key points**
- Standards need an exit: sometimes a deviation is correct for a case.
- An exception records what is deviating, why, the risk, the compensating control, an owner, and an expiry date.
- Expiry forces a revisit: renew, fix, or update the standard.
- Review the list of exceptions regularly; patterns suggest the standard itself is wrong.

**Show** Exception record: standard, deviation, reason, risk, mitigation, owner, expiry, follow-up action.

**Check:** Why must an exception have an expiry? *(So temporary deviations do not become permanent unnoticed.)*

---

## SRB-012-L05 · Right-sizing governance (10 min)
**Goal:** match review weight to reversibility and blast radius.

**Key points**
- Two questions: how hard is it to undo, and how many teams or customers does it affect?
- Low reversibility plus wide blast radius gets a full RFC and review; easy to undo and local gets a brief note or none.
- Define tiers with examples so teams self-classify.
- Revisit tiers if incidents show a decision was under-reviewed or reviews are mostly rubber stamps.

**Show** A 2x2 grid: reversibility (easy/hard) by blast radius (one team/many). Cells: no review, peer note, design review, full RFC. Example: choosing a library is easy to reverse; a public event contract is hard to reverse.

**Check:** Which gets the heaviest governance? *(Hard to reverse with a wide blast radius.)*

---

## SRB-012-L06 · Demo: a design review that improves a proposal without blocking it (15 min)
**Goal:** facilitate a review of a FulfillCo proposal, produce improvements, and still reach a decision on time; prepares SRB-012-LAB1.

**Steps**
1. Read the proposal beforehand and classify the change using the tier grid.
2. Open by stating what decision is needed and by when.
3. Collect concerns and label each as blocker or suggestion.
4. **Planned mistake:** let a reviewer raise a brand-new requirement at the end. Fix: classify it as a suggestion or a follow-up item unless it is a real risk, and keep the decision date.
5. Agree required changes with owners; record the decision.
6. Follow up in a week to confirm changes were made.

**Check:** How do you keep a review from becoming a gate? *(Classify concerns, limit blockers to real risks, and decide by the stated date.)*

---

## SRB-012-L07 · Demo: writing an RFC that gets a decision in one review (15 min)
**Goal:** write a compact RFC for a cross-team change and structure it so one review suffices; prepares SRB-012-LAB1.

**Steps**
1. State the decision needed and the deadline in the first lines.
2. Write the problem and constraints in five sentences; list goals and non-goals.
3. Present two or three options with trade-offs and a clear recommendation.
4. **Planned mistake:** bury the recommendation after pages of background. Fix: put the recommendation and the ask at the top, with details below.
5. Name reviewers per concern and pre-answer likely objections (cost, rollback, security).
6. Circulate, then collect comments in a single window.

**Check:** Where should the recommendation appear? *(Near the top, with the decision requested.)*
