# SRB-014 · Engineering metrics — Lecture scripts

**Video:** 82 min · **Running case:** *The FulfillCo integration* — the engineer leads the four-team program planned in SRB-P1 through delivery; role-players act as team leads, product, finance, and security.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRB-014-L01 · Why measure delivery (8 min)
**Goal:** explain what delivery metrics are for and what they are not for.

**Key points**
- Metrics make problems visible and let you check whether a change helped.
- They are for the team and program to improve, not to rank people.
- A single number never tells the story; use a few metrics together with context.
- Start with a question ("why do changes take so long to reach production?"), then choose the measure.

**Show** A question-to-metric table: *Are we shipping steadily? deployment frequency. Is change risky? change failure rate.*

**Check:** What should come before choosing a metric? *(The question you want to answer.)*

---

## SRB-014-L02 · DORA metrics (14 min)
**Goal:** define the four DORA metrics and read what each reveals.

**Key points**
- Deployment frequency: how often you release to production.
- Lead time for changes: from commit to running in production.
- Change failure rate: share of releases causing a failure that needs a fix or rollback.
- Time to restore service (older name: mean time to recovery): how long to recover from a failure. Verify current DORA naming and any added metrics before recording.
- Throughput and stability together: speed and safety move together in strong teams.
- Define each precisely for your pipeline (what counts as a deployment or a failure) and keep definitions stable.

**Show** A table: metric | how to compute from pipeline and incident data | what a bad trend suggests. Example: *lead time rising: slow reviews, long queues for environments, or large batches.*

**Check:** What does a rising change failure rate with steady frequency suggest? *(Quality gates or testing are weakening.)*

---

## SRB-014-L03 · Reliability indicators (10 min)
**Goal:** pair delivery metrics with reliability measures.

**Key points**
- SLO attainment: the share of time or requests meeting the service level objective.
- Error budget burn: how fast the allowed unreliability is used.
- Incident rate and severity, and the time to detect and to resolve.
- Reading both: fast delivery with falling SLO attainment is borrowing from reliability.

**Show** A combined view for one service: weekly deployments, lead time, SLO attainment, error budget remaining, incidents, with notes on correlated changes.

**Check:** Why pair delivery metrics with SLO data? *(Speed without reliability is not an improvement.)*

---

## SRB-014-L04 · Metrics that backfire (10 min)
**Goal:** recognize and avoid Goodhart effects.

**Key points**
- Goodhart's law: when a measure becomes a target, it stops being a good measure.
- Common backfires: counting lines or commits, ranking teams by deployment frequency, rewarding closed tickets.
- Symptoms of gaming: tiny meaningless deploys, reclassifying failures, splitting work to lower cycle time.
- Reduce risk: measure at team or program level, use several metrics, discuss trends not targets, and review definitions.

**Show** Table: metric | how it gets gamed | counter-measure. Example: *deployment frequency | empty releases | pair with change size and failure rate.*

**Check:** Why avoid comparing teams by one metric? *(Teams have different contexts, and the metric then invites gaming.)*

---

## SRB-014-L05 · From metric to improvement experiment (10 min)
**Goal:** turn a metric trend into a hypothesis and a small experiment.

**Key points**
- Describe the trend with data, not adjectives.
- Form a hypothesis about cause, then choose a cheap experiment that tests it.
- Define the measure, the baseline, the time window, and what result would count as success.
- Run it, record the result (including failure), and decide to keep, change, or drop.

**Show** Experiment card: trend | hypothesis | change | measure and baseline | duration | result | decision.

**Check:** What makes an improvement experiment valid? *(A baseline, a defined measure, and a decision rule set before the run.)*

---

## SRB-014-L06 · Demo: diagnosing a slow lead time from pipeline data (15 min)
**Goal:** break lead time into stages to find where changes wait; prepares SRB-014-LAB1.

**Steps**
1. Export pipeline and review data for one FulfillCo team for the last quarter.
2. Split lead time into stages: coding, waiting for review, review, build and test, wait for release.
3. Find the largest stage; check whether it is the same for all four teams.
4. **Planned mistake:** use the mean and miss that a few very old changes distort it. Fix: look at the median and the 85th percentile, and inspect the outliers.
5. Form a hypothesis (for example review queue is idle on Mondays) and design an experiment.
6. State what you will measure and when you will check.

**Check:** Why look at percentiles for lead time? *(A few outliers distort the mean and hide the typical case.)*

---

## SRB-014-L07 · Demo: spotting a metric that is being gamed (15 min)
**Goal:** detect and discuss a gamed metric without blaming a team; prepares SRB-014-LAB1.

**Steps**
1. Notice that deployment frequency jumped for one team while features delivered stayed flat.
2. Check companions: change size, lead time, failure rate, incident data.
3. Read the deploys: many trivial or empty releases found.
4. **Planned mistake:** confront the team with accusations. Fix: ask what the metric pressure felt like and what made frequent releases attractive.
5. Remove incentives that created it and adjust the definition (count meaningful changes), or add a companion metric.
6. Record what changed and recheck next month.

**Check:** How do companion metrics help? *(A gamed number diverges from the others, exposing the problem.)*
