# SRA-002 · Long-term system evolution — Lecture scripts

**Video:** 84 min · **Running case:** *Commerce 2030* — the group formed by Shop and FulfillCo has 25 engineering teams and plans a third-party seller marketplace, a five-country expansion, and doubled order volume each year for three years, while its earliest services approach end of life; you are the senior technical leader for the commerce product area.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRA-002-L01 · Architecture decays unless guided (10 min)
**Goal:** explain why good architecture erodes without active guidance, and what guidance looks like.

**Key points**
- Decay is the sum of many reasonable local decisions: a shortcut, a copied client, an unowned dependency.
- Reviews catch decay late and do not scale to 25 teams.
- Guidance means writing down what must stay true and checking it automatically.
- Decay also comes from outside: versions age, vendors change, traffic shapes shift.

**Show:** a chart idea for Commerce 2030: count of cross-domain imports per quarter, rising steadily, with the one incident it later caused marked on the line.

**Check:** Why do reviews alone fail to stop architectural decay at 25 teams? *(They are manual and late; they cannot see every change across every team.)*

---

## SRA-002-L02 · Fitness functions (12 min)
**Goal:** define fitness functions that express important qualities as checks.

**Key points**
- A fitness function measures one architectural quality: performance, coupling, security, cost, or operability.
- Good ones are specific, have a threshold, and an owner who acts when it fails.
- Pick qualities tied to business goals, such as checkout latency or cost per order.
- Few, meaningful functions beat dozens nobody reads.

**Show:** a table with five rows: quality, measure, threshold, owner. For example, coupling: "no domain depends on another domain's internal packages", threshold zero violations, owner domain team.

**Check:** What four things should every fitness function name? *(The quality, the measure, the threshold, and the owner.)*

---

## SRA-002-L03 · Automating fitness functions (10 min)
**Goal:** run fitness functions continuously so the signal is cheap and early.

**Key points**
- Run in CI for structure (dependency rules, banned APIs, license and vulnerability checks).
- Run in pipelines or production telemetry for runtime qualities (latency, cost per order).
- Decide per rule whether failure blocks a merge, warns, or only reports a trend.
- Roll out gradually: record current violations as a baseline and forbid new ones.

**Show:** a CI job outline: build, dependency-rule test, vulnerability scan, then a nightly job that queries cost per order and posts a trend to the team channel.

**Check:** How can you adopt a strict rule on a codebase that already violates it? *(Baseline existing violations and fail only on new ones.)*

---

## SRA-002-L04 · Technical roadmaps: target and transition states (12 min)
**Goal:** build a roadmap that connects where we are, where we want to be, and safe steps between.

**Key points**
- Target state: the architecture the business needs in about three years, described by capabilities and qualities, not products.
- Transition states: stable intermediate states, each useful on its own and each reversible.
- Checkpoints: dated points where evidence decides whether to continue, adjust, or stop.
- A roadmap is not a feature list; it links work to outcomes and to assumptions.

**Show:** a three-row timeline for Commerce 2030: now, month 12, month 24, target at month 36, with capabilities, assumptions, and a checkpoint after each step.

**Check:** What makes a transition state valid? *(It is stable and delivers value on its own, even if later steps are delayed.)*

---

## SRA-002-L05 · Managing obsolescence (10 min)
**Goal:** track end-of-life risk so upgrades are planned, not forced.

**Key points**
- Inventory every runtime, framework, datastore, and managed service with its version and end-of-support date.
- Vendor viability counts: funding, licence changes, and community health. Verify dates before use.
- Plan upgrades on a calendar, with effort and ownership, ahead of the deadline.
- Security emergencies are the price of a missed calendar.

**Show:** an obsolescence calendar table: component, current version, end of support (verify before recording), owner, planned upgrade quarter, effort, risk if missed.

**Check:** Why plan upgrades before end of support rather than at it? *(Late upgrades become emergencies with no time to test or negotiate extended support.)*

---

## SRA-002-L06 · Demo: a fitness function that blocks a coupling regression (15 min)
**Goal:** write and roll out a coupling fitness function across teams; prepares SRA-002-LAB1.

**Steps**
1. State the rule from the architecture goal: marketplace code must not read order-domain tables or internal packages.
2. Implement it as a dependency-rule test run in CI and capture the current violations as a baseline.
3. Demonstrate a pull request that adds a new forbidden dependency and fails the build with a clear message.
4. Agree with team leads on ownership, an exception process, and a retirement plan for baseline violations.
5. **Planned mistake:** make the rule block all builds on day one, including existing violations. Fix: baseline them, block only new ones, and report the trend.
6. Define how the team knows the function is working: violations trend and exceptions granted.

---

## SRA-002-L07 · Demo: replanning a roadmap after a vendor end-of-life notice (15 min)
**Goal:** replan when an assumption breaks; prepares SRA-002-LAB1.

**Steps**
1. Scenario: the vendor of the search engine used by commerce announces end of support in 18 months (verify real dates before recording).
2. Identify the roadmap items and assumptions touched: marketplace search, country expansion, two planned upgrades.
3. Generate options: migrate early, extended support, replace with open source, pause nonessential work.
4. Re-sequence into new transition states with checkpoints; communicate the trade-offs to product leadership.
5. **Planned mistake:** just append a "search migration" item to the feature list. Fix: restate the target state, remove or delay dependent items, and set a decision checkpoint.
6. Update the obsolescence calendar and log the assumption that changed.
