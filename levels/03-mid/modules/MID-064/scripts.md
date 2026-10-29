# MID-064 · Estimation and delivery — Lecture scripts

**Video:** 56 min · **Analogy used throughout:** planning a road trip: ask where exactly you are going, split it into legs you can drive in a day, give arrival windows, and check the risky mountain pass first.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-064-L01 · Clarifying requirements (10 min)
**Goal:** turn a vague request into testable acceptance criteria.

**Key points**
- Ask who needs it, why, and what changes for them; find the problem behind the solution.
- List unknowns and assumptions; ask about edge cases, limits, and what is out of scope.
- Write acceptance criteria as examples: "Given a delivered order, when the customer requests a return within 30 days, then ...".
- Confirm in writing with the requester.
- Ask early; a question costs minutes, a wrong build costs weeks.

**Show:** the request "add returns" turned into eight questions and three Given/When/Then criteria.

**Check:** Why write criteria as examples? *(They are testable and leave less room for misunderstanding.)*

---

## MID-064-L02 · Slicing work vertically (10 min)
**Goal:** split a feature into independently deliverable slices.

**Key points**
- A vertical slice cuts through all layers (API, logic, database) and delivers a small piece of user value.
- A horizontal slice (all tables first) delivers nothing usable until the end.
- Slice by workflow step, rule, data variation, or happy path before edge cases.
- Each slice can be merged, tested, and released behind a feature flag.
- Aim for slices of one to three days.

**Show:** returns slices: request a return, approve it, refund full amount, partial refund, notify customer.

**Check:** Why is "create all return tables" a bad slice? *(It is horizontal and delivers no user value by itself.)*

---

## MID-064-L03 · Estimating with ranges (10 min)
**Goal:** give honest estimates.

**Key points**
- Estimates are forecasts with uncertainty, not promises.
- Give a range (best case to likely worst case) and your confidence.
- Estimate from similar past work and from slices, not from the whole feature at once.
- Larger or less known work has a wider range; narrow it by learning.
- State assumptions; re-estimate when they change.

**Show:** "3-6 days, 80% confident, assuming the payment provider supports partial refunds".

**Check:** What should accompany an estimate besides the numbers? *(Assumptions and confidence.)*

---

## MID-064-L04 · Risk first: spikes and prototypes (8 min)
**Goal:** reduce the biggest unknowns early.

**Key points**
- List the riskiest assumptions: unknown API, performance, data quality, unclear rule.
- A spike is a time-boxed investigation (for example one day) that ends with an answer, not production code.
- A prototype tests an idea cheaply; throw it away.
- Order work so risky slices come first.
- Write down the result; update the plan and estimates.

**Show:** a risk table: assumption, impact, likelihood, spike to test it.

**Check:** What does a spike produce? *(Knowledge: an answer that reduces uncertainty.)*

---

## MID-064-L05 · Reporting progress honestly (6 min)
**Goal:** communicate progress and slippage early.

**Key points**
- Report slices done, slices remaining, and the current range, not "90% done".
- Raise slippage as soon as you see it, with the cause and options (cut scope, move date, add help).
- Bad news early gives choices; late gives surprises.
- Keep written updates short and regular.
- Do not hide uncertainty with padding.

**Show:** a three-line update: done, next, risk and ask.

**Check:** When should you report slippage? *(As soon as you notice it.)*

---

## MID-064-L06 · Demo: breaking "returns and refunds" into slices (12 min)
**Goal:** plan the Shop returns feature end to end. Prepares `MID-064-LAB1`.

**Steps**
1. Read the one-paragraph request and write down questions (time limit, partial returns, refund method).
2. Write Given/When/Then acceptance criteria from the answers.
3. Slice vertically and order by value and risk; mark the refund provider call as the riskiest.
4. **Planned mistake:** a first slice "database schema and entities". Fix: replace with "customer requests a return, stored and visible in the API".
5. Estimate each slice as a range; schedule a one-day spike for the provider.
6. Write the short plan and share for review.
