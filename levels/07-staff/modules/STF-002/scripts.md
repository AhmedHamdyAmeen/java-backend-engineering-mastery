# STF-002 · Technical strategy — Lecture scripts

**Video:** 100 min · **Running case:** *Platform 2.0* — the Commerce group (Shop + FulfillCo) now has about 20 product teams; delivery has slowed, every team runs its own pipelines, the same incidents repeat, and onboarding takes weeks; you are a Staff engineer with no team of your own and a mandate to make the whole organization faster and safer.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## STF-002-L01 · Strategy at organization scale (12 min)
**Goal:** define technical strategy as a short, evidence-based argument about where engineering effort goes.

**Key points**
- A strategy has three parts: a diagnosis of the situation, guiding policies, and coherent actions.
- It is not a list of projects or a wish list of technologies.
- Its value is in the choices it rules out as well as those it makes.
- Good strategy is short enough that every team lead can explain it.

**Show:** a one-page skeleton with headings Diagnosis, Guiding policies, Actions, Trade-offs, filled with one line each for Platform 2.0.

**Check:** What separates a strategy from a roadmap? *(A strategy explains why and what is excluded; a roadmap only lists what and when.)*

---

## STF-002-L02 · From business priorities to engineering bets (14 min)
**Goal:** link business goals to a few engineering investments explicitly.

**Key points**
- Business priorities usually reduce to growth, margin, risk, and speed.
- Each engineering bet names the priority it serves and the measure that would move.
- Few bets: two or three that the organization can actually fund.
- Ask the business what it would trade away; priorities that cost nothing are not priorities.

**Show:** a traceability table: priority (grow in five countries), bet (self-service service creation), measure (days from idea to production), owner.

**Check:** Why limit the number of bets? *(Capacity is finite; many bets means none is funded properly.)*

---

## STF-002-L03 · Gathering evidence across 20 teams (12 min)
**Goal:** collect data that shows where the organization really hurts.

**Key points**
- Four evidence streams: delivery metrics, incident history, cost, and engineer experience.
- Mix numbers (lead time, change failure rate) with interviews and survey comments.
- Check data quality; inconsistent definitions across teams are common.
- Share raw findings with teams before conclusions, so they trust the diagnosis.

**Show:** a data-source checklist: CI and deploy logs, incident tracker, cloud billing by team, developer survey, onboarding times.

**Check:** Why validate data definitions across teams? *(Teams measure "deploy" or "incident" differently, so naive comparisons mislead.)*

---

## STF-002-L04 · Writing the diagnosis (12 min)
**Goal:** write the diagnosis so that it names the few root problems and stays testable.

**Key points**
- Name the challenge in plain words: what is going wrong and why.
- Group symptoms under two or three causes; link each to evidence.
- Avoid blame; describe structures and incentives.
- State what would change your mind, so the diagnosis can be updated.

**Show:** a sample diagnosis paragraph: "Delivery slowed because each of 20 teams maintains its own pipeline (evidence: 14 variants); incidents repeat because lessons stay inside teams."

**Check:** What makes a diagnosis testable? *(Each claim links to evidence and states what would disprove it.)*

---

## STF-002-L05 · What we will stop doing (10 min)
**Goal:** make trade-offs explicit by naming what is dropped to fund the strategy.

**Key points**
- Capacity comes from stopping something; otherwise the strategy is wishful.
- Candidates: duplicate tools, low-value projects, optional reviews, unused services.
- Name owners affected and give them a transition path.
- Leaders must say the stop out loud; hidden stops cause surprise and resistance.

**Show:** a two-column slide: "We will fund" and "We will stop", with the capacity freed in engineer-months.

**Check:** What happens to a strategy that stops nothing? *(It adds load without capacity and quietly fails.)*

---

## STF-002-L06 · Endorsement and refresh cycles (10 min)
**Goal:** get leaders to adopt the strategy and keep it alive.

**Key points**
- Pre-wire: talk to each leader one to one before the group meeting.
- Ask for specific decisions: a sponsor, a budget line, a named stop.
- Publish where teams can find it; summarize in a page and a short talk.
- Review every six to twelve months against the evidence and retire what no longer holds.

**Show:** a calendar: pre-wires in weeks 1-2, endorsement meeting in week 3, quarterly check-ins, annual refresh.

**Check:** Why pre-wire before the endorsement meeting? *(Surprises in public cause objections; private conversations surface and resolve them.)*

---

## STF-002-L07 · Demo: diagnosing Platform 2.0 from delivery and incident data (15 min)
**Goal:** work from raw data to a three-cause diagnosis; prepares STF-002-LAB1.

**Steps**
1. Pull a year of deploy logs and the incident tracker for all 20 teams.
2. Compute lead time and change failure rate per team; chart the spread.
3. Tag the incidents by cause category; note repeats across teams.
4. **Planned mistake:** conclude "team X is the slow one" from the median alone. Fix: look at the shared causes (pipeline variants, duplicated tooling), not at ranking teams.
5. Write the diagnosis in three sentences, each tied to a chart.

---

## STF-002-L08 · Demo: turning three business goals into two engineering bets (15 min)
**Goal:** convert goals into a small set of bets and a stop list; prepares STF-002-LAB1.

**Steps**
1. Take the CPO's goals: expand to new countries, lower cloud margin cost, reduce outages.
2. Map each goal to candidate engineering investments and the measure each moves.
3. Merge overlapping candidates into two bets: a paved path for new services and a shared reliability program.
4. **Planned mistake:** adding a third pet bet (a new language) to please a vocal team. Fix: test it against evidence; it does not trace to a goal, so it goes to the radar, not the strategy.
5. Name what stops to fund the bets and take the draft to the CTO and CPO for decisions.
