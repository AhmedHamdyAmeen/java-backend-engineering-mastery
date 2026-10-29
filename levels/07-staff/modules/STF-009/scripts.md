# STF-009 · Engineering productivity — Lecture scripts

**Video:** 98 min · **Running case:** *Platform 2.0* — the Commerce group (Shop + FulfillCo) now has about 20 product teams; delivery has slowed, every team runs its own pipelines, the same incidents repeat, and onboarding takes weeks; you are a Staff engineer with no team of your own and a mandate to make the whole organization faster and safer.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## STF-009-L01 · What productivity means for engineers (12 min)
**Goal:** define productivity as the ability to deliver value smoothly, not as activity.

**Key points**
- Output counts (lines, tickets, story points) can be gamed and mislead.
- Useful view: delivery speed and stability, developer experience, and low cognitive load.
- Productivity is a property of the system the engineers work in.
- Goal: remove friction, not push people harder.

**Show:** a three-part frame: delivery outcomes, developer experience, cognitive load, with one example metric each.

**Check:** Why are lines of code a poor measure? *(They reward volume, are easy to game, and ignore value.)*

---

## STF-009-L02 · Measuring without surveillance (12 min)
**Goal:** measure at team and system level without ranking individuals.

**Key points**
- Use delivery metrics: lead time, deployment frequency, change failure rate, time to restore.
- Add surveys for experience and cognitive load; ask the same questions regularly.
- Aggregate data; never publish individual leaderboards.
- Say what you will and will not do with the data, and keep to it.

**Show:** a metric sheet of eight indicators, the source, the level (team or org), and a "never used for" note.

**Check:** Why avoid individual rankings? *(They damage trust, invite gaming, and hide system causes.)*

---

## STF-009-L03 · Feedback loops: where time goes (12 min)
**Goal:** find the longest delays in the developer loop.

**Key points**
- Loops: edit-build-test, code review, CI, deploy, incident response, onboarding.
- Measure the wait time, not only work time.
- Look for shared delays that affect many teams.
- Fix the biggest delay first; the next one becomes visible.

**Show:** a timeline chart for a change from commit to production with waits marked: CI queue 20 min, review wait 6 hours, deploy approval 1 day.

**Check:** Why measure wait time? *(Waiting often dominates and is invisible in work measures.)*

---

## STF-009-L04 · Build and test pipelines at scale (12 min)
**Goal:** speed up pipelines where gains compound across teams.

**Key points**
- Tools: caching, parallel test sharding, incremental builds, faster runners, removing flaky tests.
- Shared base images and templates fix many teams at once.
- Track pipeline time and flake rate per template.
- Verify tool versions and features before recording choices.

**Show:** a before and after outline of a pipeline: sequential 40 minutes into parallel stages with cache.

**Check:** Why fix the shared pipeline before one team's? *(A shared fix helps all teams using it.)*

---

## STF-009-L05 · Onboarding as a product (10 min)
**Goal:** cut the time for a new engineer to ship.

**Key points**
- Measure time to first commit and to first production change.
- Provide one-command setup, a starter task, and a named buddy.
- Keep documentation current by assigning owners.
- Ask new hires for feedback in their first month.

**Show:** an onboarding checklist: access in day one, environment in an hour, first pull request in week one, with owners.

**Check:** Name a metric for onboarding. *(Time to first production change.)*

---

## STF-009-L06 · Making the business case (10 min)
**Goal:** justify productivity investment with numbers leaders accept.

**Key points**
- Convert time saved to engineer-hours per month and to delivery outcomes.
- State assumptions and show a range, not a single optimistic number.
- Add quality counter-metrics so speed gains do not hide quality loss.
- Compare cost with payback period.

**Show:** a simple model: 160 engineers x 3 builds a day x 12 minutes saved = hours per month; investment cost; payback.

**Check:** Why include counter-metrics? *(To show speed gains do not cost quality.)*

---

## STF-009-L07 · Demo: cutting a 40-minute CI pipeline to 8 minutes (15 min)
**Goal:** reduce a pipeline step by step with measurements; prepares STF-009-LAB1.

**Steps**
1. Record a baseline: stage durations, queue times, and flake rate over two weeks.
2. Find the longest stages and the dependency cache misses.
3. Apply changes one at a time: dependency cache, parallel test shards, faster runners, quarantine flaky tests.
4. **Planned mistake:** changing everything at once. Fix: change one thing per run so each effect is measurable.
5. Compare with baseline, roll the template to other teams, and record hours saved.

---

## STF-009-L08 · Demo: running a developer-experience survey and acting on it (15 min)
**Goal:** run a survey that leads to action; prepares STF-009-LAB1.

**Steps**
1. Design ten questions on build speed, review, tooling, cognitive load, and onboarding.
2. Run it anonymously, aim for a high response rate, and explain its purpose.
3. Analyze by theme and by team size, not by person.
4. **Planned mistake:** collecting results and doing nothing. Fix: publish top three themes within two weeks with owners and dates.
5. Repeat in six months and compare.
