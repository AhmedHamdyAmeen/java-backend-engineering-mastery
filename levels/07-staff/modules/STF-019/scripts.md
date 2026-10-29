# STF-019 · Measuring impact — Lecture scripts

**Video:** 86 min · **Running case:** *Platform 2.0* — the strategy, governance, and platform direction from STF-P1 must now be adopted by about 20 product teams who did not ask for them; role-players act as engineering managers, skeptical tech leads, product, finance, security, and executives.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## STF-019-L01 · Why Staff work is hard to measure (10 min)
**Goal:** understand why impact measurement is difficult and still necessary.

**Key points**
- Staff work is indirect: it changes what many teams do, and many factors affect the result.
- Results arrive late; trends often began before your work.
- Without measures, impact is claimed or disputed on opinion.
- Imperfect measures with honest caveats beat none.

**Show:** a chain: platform change, team behaviour, delivery and reliability metrics, business outcome, with confounders noted at each step.

**Check:** Why measure if attribution is hard? *(To steer the work and show value with honest caveats.)*

---

## STF-019-L02 · Choosing success measures up front (12 min)
**Goal:** define measures before the work starts.

**Key points**
- Cover adoption, reliability, cost, delivery speed, and developer experience.
- Record the baseline now; you cannot measure change without it.
- Each measure has a definition, a data source, an owner, and a target date.
- Few measures, chosen deliberately; avoid vanity metrics (counts of activity).

**Show:** a metric table: metric, definition, baseline (from STF-009), target, data source, owner.

**Check:** Why set the baseline first? *(Change is only visible against a known starting point.)*

---

## STF-019-L03 · Leading and lagging indicators (12 min)
**Goal:** use early signals and late results together.

**Key points**
- Lagging: incidents, lead time, cost; they confirm results but arrive late.
- Leading: adoption rate, support questions, pilot time to first deploy; they predict.
- Use leading indicators to steer and lagging to judge.
- Check that leading indicators really predict the lagging ones.

**Show:** a table pairing indicators: teams on golden path (leading) with lead time to production (lagging).

**Check:** Which is better for steering a quarter? *(Leading indicators; lagging ones come too late.)*

---

## STF-019-L04 · Attribution and honesty (12 min)
**Goal:** claim impact fairly.

**Key points**
- Compare with a control (teams not yet migrated) or the trend before.
- Separate your contribution from other changes (hiring, other programs).
- Report confidence: strong, plausible, or uncertain.
- Do not claim credit for trends that started earlier.

**Show:** a before and after chart with the pre-existing trend line drawn, and a sentence stating how much change is likely ours.

**Check:** How can you check attribution? *(Compare with a control group or the prior trend.)*

---

## STF-019-L05 · Impact dashboards (10 min)
**Goal:** build a simple dashboard leadership trusts.

**Key points**
- One page, few metrics, baseline and target shown.
- Data comes from systems, not from manual claims.
- Show definitions and data freshness on the page.
- Review it regularly; remove metrics nobody uses.

**Show:** a dashboard layout: adoption, lead time, incidents, cost, developer satisfaction; each with trend, target, and last updated.

**Check:** Why show definitions? *(So people trust what the numbers mean.)*

---

## STF-019-L06 · Demo: the Platform 2.0 success metrics, from baseline to target (15 min)
**Goal:** define metrics and targets for the program; prepares STF-019-LAB1.

**Steps**
1. Pull the STF-009 baseline for lead time, incidents, cost, and satisfaction.
2. Choose measures and write definitions and data sources.
3. Set targets with ranges and dates, and check with owners that they are realistic.
4. **Planned mistake:** choosing "number of services on the platform" as the main success measure. Fix: pair it with outcomes such as lead time and incident rate.
5. Mark leading and lagging indicators.
6. Publish the metrics with the sponsor's agreement.

---

## STF-019-L07 · Demo: an impact report that admits what did not work (15 min)
**Goal:** write an honest impact report; prepares STF-019-LAB1.

**Steps**
1. Collect results against the baseline and targets.
2. State what improved and the confidence of attribution.
3. State what did not improve (for example developer satisfaction flat) and the likely reasons.
4. **Planned mistake:** claiming the whole drop in incidents, which had started before the platform. Fix: show the prior trend and claim only the increment.
5. List changes to the program for next quarter.
6. Share the report with teams as well as sponsors.
