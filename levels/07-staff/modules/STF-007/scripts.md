# STF-007 · Technology portfolio — Lecture scripts

**Video:** 88 min · **Running case:** *Platform 2.0* — the Commerce group (Shop + FulfillCo) now has about 20 product teams; delivery has slowed, every team runs its own pipelines, the same incidents repeat, and onboarding takes weeks; you are a Staff engineer with no team of your own and a mandate to make the whole organization faster and safer.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## STF-007-L01 · Technology choices as a portfolio (12 min)
**Goal:** treat languages, frameworks, and datastores as a portfolio with costs, not a set of personal choices.

**Key points**
- Every technology adds operating cost, hiring needs, security surface, and training.
- A portfolio balances a stable core with a few experiments.
- Count what exists first: you cannot manage what you have not inventoried.
- Decisions are about the organization's cost, not one team's preference.

**Show:** an inventory table: technology, teams using it, owner, version, support status, with two obvious duplicates highlighted.

**Check:** Why inventory before deciding? *(Hidden duplicates and unsupported versions only show up when everything is listed.)*

---

## STF-007-L02 · A technology radar that people use (12 min)
**Goal:** build a radar with clear criteria and owners.

**Key points**
- Four rings: adopt, trial, assess, hold.
- Each ring has criteria, for example adopt needs production evidence and an owner team.
- Each entry has a short rationale and a contact.
- Update on a schedule and invite proposals; a radar nobody can change is ignored.

**Show:** a radar entry template: name, ring, criteria met, owner, rationale, last reviewed; two filled examples.

**Check:** What does "hold" mean on a radar? *(Do not start new work with it; existing use is managed toward retirement.)*

---

## STF-007-L03 · Standardize, consolidate, or diversify (12 min)
**Goal:** decide when to converge and when to allow variety.

**Key points**
- Standardize where variety costs a lot and gives little: CI, logging, base images.
- Allow diversity where problems differ: specialized datastores, analytics tools.
- Consolidate duplicates when the savings exceed migration cost.
- Use a simple test: cost of variety versus benefit of fit.

**Show:** a table of five areas (CI, language, message broker, datastore, observability) with the recommendation and reason.

**Check:** When allow diversity? *(When problems genuinely differ and the fit gain exceeds the cost of supporting another option.)*

---

## STF-007-L04 · Introducing new technology safely (10 min)
**Goal:** let teams try new things without spreading unsupported choices.

**Key points**
- Run bounded trials: one team, a clear goal, a time limit, success criteria.
- Check operations, security, hiring, and exit options before wider use.
- Decide at the end: adopt, extend the trial, or stop.
- Verify version and support status before recording any choice.

**Show:** a one-page trial charter with goal, scope, duration, success measures, and exit plan.

**Check:** Why set an exit plan in a trial? *(So a failed trial does not leave unsupported technology in production.)*

---

## STF-007-L05 · Retiring technology (12 min)
**Goal:** remove technology without abandoning the teams that use it.

**Key points**
- Announce with a reason, a deadline, and a replacement.
- Offer migration support: tooling, guides, and engineering time.
- Track progress per team and handle exceptions openly.
- Switch off at the deadline and confirm it is really gone.

**Show:** a retirement plan outline: inventory of users, target, support offer, milestones, communication schedule.

**Check:** Why offer migration help? *(Teams have their own roadmaps; without help deadlines slip or are ignored.)*

---

## STF-007-L06 · Demo: building the first Platform 2.0 technology radar (15 min)
**Goal:** create a first radar from an inventory; prepares STF-007-LAB1.

**Steps**
1. Extract languages, frameworks, datastores, and CI tools from repositories and build files for all 20 teams.
2. Define ring criteria with three tech leads.
3. Place each item and name an owner for each adopt entry.
4. **Planned mistake:** placing items according to the architect's taste. Fix: apply the written criteria and adoption data; disputed items go to assess with a review date.
5. Publish the radar with a way to propose changes and a quarterly review.

---

## STF-007-L07 · Demo: retiring a second message broker across eight teams (15 min)
**Goal:** plan a retirement with support and deadlines; prepares STF-007-LAB1.

**Steps**
1. Inventory the eight teams, their topics, volumes, and critical flows.
2. Decide the target broker and confirm it meets each team's needs.
3. Build the support offer: client library, migration guide, a migration squad for the hardest teams.
4. **Planned mistake:** announcing a hard shutdown date by email. Fix: agree per-team dates with leads, start with willing teams, and publish a progress board.
5. Plan the dual-run period, verification, and the confirmed shutdown checklist.
