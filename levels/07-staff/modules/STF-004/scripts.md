# STF-004 · Platform strategy — Lecture scripts

**Video:** 100 min · **Running case:** *Platform 2.0* — the Commerce group (Shop + FulfillCo) now has about 20 product teams; delivery has slowed, every team runs its own pipelines, the same incidents repeat, and onboarding takes weeks; you are a Staff engineer with no team of your own and a mandate to make the whole organization faster and safer.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## STF-004-L01 · Why internal platforms succeed or fail (12 min)
**Goal:** explain the patterns behind platforms that teams adopt versus platforms they avoid.

**Key points**
- Successful platforms solve a pain teams already feel and are easier than the alternative.
- Failed platforms are built for the platform team's interests or mandated without a better experience.
- Adoption is the success measure; a platform nobody uses is cost.
- A platform is a product with customers: the product teams.

**Show:** a two-column list of success and failure signs, with the Platform 2.0 start state: 14 pipeline variants, no shared service template.

**Check:** What is the main success measure of a platform? *(Voluntary adoption and the outcomes it improves for its users.)*

---

## STF-004-L02 · Developer journeys and toil mapping (12 min)
**Goal:** find where developers lose time before deciding what to build.

**Key points**
- A developer journey is the sequence from idea to production: create, build, test, deploy, observe, operate.
- Toil is repetitive manual work that adds no lasting value.
- Interview teams and measure time at each step; note the steps that repeat across teams.
- Rank by total hours lost across all teams, not by loudest complaint.

**Show:** a journey map for "new service to production" with steps, median days, and teams affected per step.

**Check:** Why rank pain by total hours across teams? *(A small pain in 20 teams can cost more than a large pain in one.)*

---

## STF-004-L03 · Paved roads and escape hatches (12 min)
**Goal:** design defaults that are the easiest path while allowing real exceptions.

**Key points**
- A paved road bundles the common choices (template, pipeline, observability, security) behind one command.
- It wins by being faster and safer than doing it yourself, not by being mandatory.
- Escape hatches let teams with special needs leave the road, accepting more responsibility.
- Track who leaves and why; that is product feedback.

**Show:** a diagram: golden path in the middle, three marked exits (custom runtime, alternative datastore, special deployment), each with the added responsibilities.

**Check:** Why keep escape hatches? *(Real needs differ; forcing everyone onto one path breaks them or creates workarounds.)*

---

## STF-004-L04 · The platform as a product (12 min)
**Goal:** apply product practices to an internal platform.

**Key points**
- Define users, their jobs, and a roadmap driven by their needs.
- Provide support: documentation, a help channel, response targets.
- Measure adoption, time saved, satisfaction, and reliability of the platform itself.
- Appoint a product manager or equivalent; do not let engineers guess alone.

**Show:** a one-page product brief: users, problem, scope in and out, success measures, support model.

**Check:** Name two measures for a platform product. *(Adoption rate and developer time saved or satisfaction.)*

---

## STF-004-L05 · Build, assemble, or buy platform capabilities (12 min)
**Goal:** choose the cheapest way to get each capability that stays maintainable.

**Key points**
- Build only what is specific to your context; buy or assemble commodity parts.
- Include operating cost, integration effort, and skills in the comparison.
- Prefer open standards to reduce lock-in.
- Revisit as the market changes; verify vendor and product versions before recording a choice.

**Show:** a decision table for four capabilities (CI, service catalog, secrets, deploy) with build, assemble, buy columns and a recommendation.

**Check:** When should you build a capability? *(When it is specific to your context and no good option exists.)*

---

## STF-004-L06 · Funding and staffing a platform team (10 min)
**Goal:** size a platform team and defend the investment.

**Key points**
- Start small with a few engineers and a product owner; grow with adoption.
- Compare cost with hours saved across teams and incidents avoided.
- Agree the funding model: central budget or chargeback, and why.
- Plan for support load, which grows with adoption.

**Show:** a back-of-envelope sheet: team of six costs X; saves 40 min a week for 160 engineers; payback in months.

**Check:** What should a platform business case compare? *(Platform team cost against time saved and incidents avoided across all users.)*

---

## STF-004-L07 · Demo: mapping the "new service to production" journey across five teams (15 min)
**Goal:** map one journey with real data; prepares STF-004-LAB1.

**Steps**
1. Pick five teams that recently launched services and interview them with one script.
2. Record each step, who did it, wait time, and manual effort.
3. Merge into one journey map showing variance between teams.
4. **Planned mistake:** treating one team's long wait as typical. Fix: use all five and highlight steps slow in at least three teams.
5. Mark the top three bottlenecks with total hours across teams.

---

## STF-004-L08 · Demo: choosing the platform's first three capabilities (15 min)
**Goal:** pick the first capabilities by evidence; prepares STF-004-LAB1.

**Steps**
1. List candidate capabilities from the toil map: service template, shared pipeline, secrets, service catalog.
2. Score each by hours lost, teams affected, and effort to deliver.
3. Choose three that deliver value in six months and build on each other.
4. **Planned mistake:** choosing the most technically interesting item (a service mesh). Fix: return to the data; it affects few teams and costs a lot.
5. Draft the roadmap, support model, and success measures for each, and the team size needed.
