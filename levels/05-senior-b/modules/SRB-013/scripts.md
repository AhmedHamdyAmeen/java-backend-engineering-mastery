# SRB-013 · Technology evaluation — Lecture scripts

**Video:** 90 min · **Running case:** *The FulfillCo integration* — the engineer leads the four-team program planned in SRB-P1 through delivery; role-players act as team leads, product, finance, and security.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRB-013-L01 · Start with the problem (10 min)
**Goal:** frame an evaluation around the problem before any product is named.

**Key points**
- Write the problem, constraints, and success measures first; options come later.
- Include the do-nothing and build-it-ourselves options as real candidates.
- State what is out of scope so the evaluation stays small.
- Name the decision owner and the date; evaluations without a deadline expand.

**Show** A one-page evaluation charter: problem (FulfillCo returns involve several steps across two systems and compensation on failure), constraints (team skills, compliance, budget), options (workflow engine, hand-built sagas, do nothing), decision owner, date.

**Check:** Why include "build it ourselves" as an option? *(It is a real alternative and sets the baseline the products must beat.)*

---

## SRB-013-L02 · Criteria and weights (10 min)
**Goal:** choose and weight criteria before looking at products.

**Key points**
- Derive criteria from the problem: fit, operability, security, team skill, cost, exit cost.
- Separate must-haves (pass/fail) from weighted preferences.
- Agree weights with stakeholders and write them down before scoring.
- Changing weights after seeing scores must be visible and justified.

**Show** Criteria table: criterion | type (must/weighted) | weight | how it will be measured. Example: *durable state survives restart | must | pass/fail | PoC kill test.*

**Check:** Why fix weights before scoring? *(To prevent tuning criteria to favor a preferred option.)*

---

## SRB-013-L03 · Proofs of concept that answer questions (12 min)
**Goal:** design a time-boxed PoC that tests the riskiest assumptions.

**Key points**
- A PoC answers specific questions; list them first and rank by risk.
- Test the unhappy paths: failures, retries, timeouts, upgrades, observability, not just the demo flow.
- Time-box (for example two days) and define what counts as pass or fail.
- Throw the PoC code away or label it; do not promote it silently.
- Record results with evidence, including what was not tested.

**Show** PoC plan table: question | why risky | test | pass criteria. Example: *what happens to in-flight workflows when a worker dies? | data loss | kill worker mid-run | workflow resumes without duplicates.*

**Check:** Why test failure paths in a PoC? *(Happy paths work in every tool; failures reveal real operational cost.)*

---

## SRB-013-L04 · Evaluation matrices (10 min)
**Goal:** compare options with a transparent weighted matrix.

**Key points**
- Rows are criteria, columns are options; each cell has a score and the evidence behind it.
- Compute weighted totals, then read the notes, not just the totals.
- Run a sensitivity check: does the winner change if the top weight changes?
- Include total cost over a fixed horizon (for example three years): licence or hosting, engineering time, operations, training.

**Show** A small matrix with three options, five criteria, weighted totals, a cost row, and a sensitivity line: *winner unchanged unless operability weight drops below X.*

**Check:** What does a sensitivity check reveal? *(Whether the result depends on a single contested weight.)*

---

## SRB-013-L05 · Exit costs and lock-in (10 min)
**Goal:** estimate how hard it would be to leave a choice.

**Key points**
- Lock-in sources: proprietary APIs and data formats, workflow definitions in a vendor language, skills, contracts.
- Estimate exit cost: what to rewrite, migrate, and retrain; how long; what runs in parallel.
- Reduce it with thin abstractions at the right level, open formats, and data export tests.
- Some lock-in is fine when the benefit is large; decide knowingly and record it.

**Show** Exit plan outline: triggers to leave, data export path, parts to rewrite, estimated effort, how to test the exit (export a sample and re-import).

**Check:** Is lock-in always bad? *(No; accept it when the benefit outweighs the exit cost, and record that choice.)*

---

## SRB-013-L06 · Bias in technology choices (8 min)
**Goal:** recognize the common biases that distort evaluations.

**Key points**
- Novelty bias: new feels better; ask what problem it solves that the current option does not.
- Sunk cost: past investment is not a reason to continue.
- Vendor demos show the best path; ask to see failure, scale, and pricing at your volume.
- Resume-driven choice and familiarity bias also push results; use criteria and a second reviewer.
- Choosing the favorite first and criteria second is the most common bias of all.

**Show** A bias checklist: *Were criteria written before options? Did we test failure paths? Is the do-nothing option scored? Who benefits from each choice?*

**Check:** What is the most reliable guard against a pre-chosen favorite? *(Written criteria and weights agreed before options are scored.)*

---

## SRB-013-L07 · Demo: evaluating two workflow engines in a two-day PoC (15 min)
**Goal:** plan and run a two-day PoC comparing two workflow engines for the FulfillCo returns process; prepares SRB-013-LAB1.

**Steps**
1. Write the questions ranked by risk: durability, retries and compensation, visibility, versioning of running workflows, operational load.
2. Allocate day one to the returns flow with a happy path and a failure path; day two to kill tests, upgrade tests, and observability.
3. Implement the same returns scenario in both engines with the same test data.
4. **Planned mistake:** spend day one on the happy path and run out of time for failures. Fix: reorder so the riskiest tests run first.
5. Record results with evidence per question; note what was not tested.
6. Compare against the hand-built saga baseline from the existing design.

**Check:** What should you test first in a time-boxed PoC? *(The riskiest assumptions.)*

---

## SRB-013-L08 · Demo: scoring options and checking the matrix for bias (15 min)
**Goal:** fill the matrix, compute totals, and audit the result for bias; prepares SRB-013-LAB1.

**Steps**
1. Confirm criteria and weights were written before the PoC.
2. Score each cell with evidence from the PoC; leave a cell unscored if there is no evidence.
3. Add three-year cost and exit cost, then compute weighted totals.
4. **Planned mistake:** a team member quietly raises the weight of a criterion that favors the engine they like. Fix: weights changes require a recorded reason and a re-run of the sensitivity check.
5. Run sensitivity and bias checklist; ask a second reviewer to challenge two scores.
6. Write the recommendation with exit plan and what would change it.

**Check:** What do you do about a cell with no evidence? *(Leave it unscored or mark it as an assumption; do not guess a score.)*
