# SRA-012 · Engineering standards — Lecture scripts

**Video:** 80 min · **Running case:** *Commerce 2030* — the group formed by Shop and FulfillCo has 25 engineering teams and plans a third-party seller marketplace, a five-country expansion, and doubled order volume each year for three years; the strategy must now be adopted by 25 teams, funded, and executed, with role-players acting as managers, product, finance, security, and executives.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRA-012-L01 · The cost and value of standards (10 min)
**Goal:** show that every standard buys something and costs something, so each must earn its place.

**Key points**
- Value: teams stop re-deciding, work moves between teams, operations and security get predictable behavior.
- Cost: slower local choices, compliance effort, and a standard that fits nobody well.
- A standard nobody follows costs credibility and gives no value.
- Ask of each proposal: what recurring pain does this remove, and for how many teams?

**Show:** a two-column ledger for "all services expose a health endpoint": value (one on-call runbook, one load balancer check) against cost (one hour per service).

**Check:** When is a standard not worth having? *(When its cost to teams exceeds the pain it removes, or nobody follows it.)*

---

## SRA-012-L02 · What to standardize (12 min)
**Goal:** pick the few places where sameness pays and leave the rest to teams.

**Key points**
- Standardize at boundaries: interfaces, events, identity, security, observability, deployment.
- Leave to teams what is inside a boundary: internal design, many libraries, test style.
- Languages and frameworks are a poor first target; the pain is rarely there.
- Standardize where inconsistency hurts people who are not the owning team.

**Show:** a sorting table for Commerce 2030: API error format (standardize), event envelope (standardize), trace and log fields (standardize), internal package layout (leave), choice of mapper library (leave).

**Check:** Why standardize boundaries before languages? *(Boundary inconsistency hurts other teams and operations; language choice mostly affects the owning team.)*

---

## SRA-012-L03 · Principles, defaults, exceptions (10 min)
**Goal:** write standards that are firm where needed and flexible elsewhere.

**Key points**
- Principle: the intent and reason ("every request is traceable end to end").
- Default: the recommended way that satisfies the principle with no extra work.
- Exception: a documented, time-limited deviation with an owner and a reason.
- A standard with no exception path is broken by the first hard case, quietly.

**Show:** template: Principle / Why / Default (with the paved-road link) / How to check / Exception process (who approves, how long it lasts, review date).

**Check:** What does an exception record contain? *(Reason, owner, scope, expiry or review date, and the risk accepted.)*

---

## SRA-012-L04 · Adoption through paved roads (10 min)
**Goal:** make the standard the easiest path so teams choose it.

**Key points**
- A paved road is a supported template, library, or pipeline that already follows the standard.
- Mandates create hidden workarounds; paved roads create voluntary adoption.
- Automate checks (build, CI, platform policy) rather than relying on reviews.
- Measure adoption in numbers and track the reasons teams do not adopt.

**Show:** service template that produces the standard log and trace fields by default, plus a dashboard showing percent of services conforming per team.

**Check:** Why prefer a paved road over a mandate? *(Teams adopt what is easiest and the standard works for them; mandates push deviations underground.)*

---

## SRA-012-L05 · Retiring standards (8 min)
**Goal:** remove standards that no longer pay for themselves.

**Key points**
- Review each standard at least yearly: still needed, still followed, still cheap?
- Signs of decay: many exceptions, tooling now makes it automatic, original problem is gone.
- Retire visibly: announce, set a date, remove the checks and the documentation.
- A shrinking standards set builds trust in the rest.

**Show:** a yearly review table: standard, exceptions count, adoption percent, pain addressed, decision (keep / simplify / retire).

**Check:** What is a signal that a standard should be retired? *(Many exceptions, or the problem it addressed no longer exists.)*

---

## SRA-012-L06 · Demo: writing an observability standard teams accept (15 min)
**Goal:** write and launch a Commerce 2030 observability standard that teams adopt voluntarily; prepares SRA-012-LAB1.

**Steps**
1. Gather the pain: incident reviews where nobody could follow a request across services.
2. Draft with three team leads: principle (traceable end to end), defaults (trace context propagation, structured log fields, a small set of service metrics), and the check.
3. Build the paved road: the service template and a shared library emitting the defaults.
4. **Planned mistake:** publish a 20-page document requiring all teams to migrate by quarter end. Fix: shrink to one page, make the template the path, and start with two teams that feel the pain most.
5. Publish adoption by team on a dashboard and review the numbers monthly.

---

## SRA-012-L07 · Demo: handling a team that wants an exception (15 min)
**Goal:** run a worked leadership session in which a team asks to skip the event standard; prepares SRA-012-LAB1.

**Steps**
1. Hear the team out: the settlement team wants a binary format and no standard envelope for throughput reasons.
2. Check the claim with data: measure the real overhead of the standard envelope on their path.
3. Look for the narrow exception: keep the envelope's identity and trace fields, allow a different payload encoding.
4. **Planned mistake:** refuse on principle in a review meeting. Fix: offer a time-limited exception with an owner, record it, and revisit after three months.
5. Record the exception in the register and ask whether the default should be improved for everyone.

**Show:** an exception record: team, standard, deviation, reason, risk accepted, mitigation, owner, expiry.
