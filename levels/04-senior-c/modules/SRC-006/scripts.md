# SRC-006 · API and data contracts — Lecture scripts

**Video:** 69 min · **Running case:** *Order Processing at 10×* — Shop Platform's order subsystem must handle a 10× growth forecast, a 99.95% availability commitment, and a 15-minute recovery objective.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRC-006-L01 · Contracts as promises between teams (10 min)
**Goal:** treat every API and event as a promise with owners and consumers.

**Key points**
- A contract covers shape, meaning, behavior, and quality (latency, ordering, delivery).
- The producer promises; consumers depend; both sides have obligations.
- Undocumented behavior becomes a contract once someone relies on it.
- Contracts cross team boundaries, so changes are coordination problems.

**Show:** a contract card for `OrderPlaced`: owner, schema, delivery guarantee, ordering key, consumers, deprecation rules.

**Check:** When does undocumented behavior become a contract? *(When a consumer depends on it.)*

---

## SRC-006-L02 · Compatibility policies (12 min)
**Goal:** write rules for what changes are allowed without coordination.

**Key points**
- Backward compatible: new producer, old consumer still works; forward: old producer, new consumer works.
- Safe: add optional fields; risky: remove, rename, change type or meaning.
- Policy: compatibility mode per subject in the schema registry; additive-only by default.
- Meaning changes are breaking even when the schema is unchanged.
- Define deprecation windows and sunset notices.

**Show:** a policy table: change type, allowed without notice, needs notice, requires new version.

**Check:** Is changing a field's meaning but not its type compatible? *(No; it breaks consumers although the schema validates.)*

---

## SRC-006-L03 · Measuring consumer impact (10 min)
**Goal:** know who is affected before changing anything.

**Key points**
- Sources: schema registry subjects, consumer group lists, API gateway usage logs, tracing, code search, ownership maps.
- Contract tests (consumer-driven) show which expectations break.
- Quantify: which consumers, how much traffic, which fields they read.
- Unknown consumers are a risk to be reduced, not ignored.

**Show:** an impact map of `OrderPlaced` fields against five consumers with traffic and owner.

**Check:** How do you find which fields a consumer really uses? *(Contract tests, usage logs, or code search.)*

---

## SRC-006-L04 · Schema governance that scales (12 min)
**Goal:** create guardrails that do not block teams.

**Key points**
- Ownership: every schema has an owning team and a documented contact.
- Automate checks in CI: compatibility, naming, required docs.
- Review by exception: human review for breaking or cross-domain changes.
- Avoid governance by meeting; make the paved path the easy path.

**Show:** a pipeline: PR changes schema, registry checks compatibility, owner and consumers are tagged, merge on pass.

**Check:** What is the opposite of governance by meeting? *(Automated checks in CI with human review by exception.)*

---

## SRC-006-L05 · Coordinating breaking changes (10 min)
**Goal:** plan a multi-team migration with rollback.

**Key points**
- Prefer expand and contract: add the new alongside the old, migrate consumers, then remove the old.
- Sequence: announce, publish both, migrate each consumer, observe usage reach zero, remove.
- Each step has an owner, a date, and a rollback.
- Track progress where everyone can see it.

**Show:** a timeline with phases: dual publish, consumer migrations, verification, removal.

**Check:** What does expand and contract mean? *(Add the new form beside the old, migrate users, then remove the old.)*

---

## SRC-006-L06 · Demo: splitting `OrderPlaced` into two events across five consumers (15 min)
**Goal:** plan the split of one event into two; prepares SRC-006-LAB1.

**Steps**
1. Map the five consumers and what each reads from `OrderPlaced`.
2. Define the new events (for example `OrderAccepted` and `PaymentRequested`) and the compatibility mode.
3. **Planned mistake:** announce and remove the old event in one release. Fix: dual-publish both forms and track the old subject's consumer lag to zero.
4. Sequence the consumer migrations with owners, dates, and contract tests.
5. Define rollback for each step.
6. Verify no consumers remain, then retire the old event.
