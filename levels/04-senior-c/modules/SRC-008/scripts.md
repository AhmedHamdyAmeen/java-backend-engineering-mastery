# SRC-008 · Architectural decomposition — Lecture scripts

**Video:** 92 min · **Running case:** *Order Processing at 10×* — Shop Platform's order subsystem must handle a 10× growth forecast, a 99.95% availability commitment, and a 15-minute recovery objective.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRC-008-L01 · Decomposition is a means, not a goal (10 min)
**Goal:** tie every split or merge to a concrete need.

**Key points**
- Legitimate drivers: team autonomy, different scaling needs, fault isolation, different change rates, compliance.
- A split buys independence and costs network, operations, and consistency work.
- State the benefit as a measurable change, e.g. fewer cross-team merge conflicts or isolated failures.
- A modular monolith is a valid destination.

**Show:** a criteria table: driver, evidence needed, expected benefit, cost.

**Check:** What must a proposed split name? *(The driver and the evidence that it will be realized.)*

---

## SRC-008-L02 · Kinds of coupling (12 min)
**Goal:** detect coupling beyond the call graph.

**Key points**
- Code: shared classes and libraries; data: shared tables or schemas; deployment: must release together; temporal: must be up at the same time; change: files that change together.
- Shared databases hide strong coupling.
- Chatty calls between two services signal a wrong boundary.
- Detect each kind with a different tool: dependency graph, schema ownership, release history, Git history, traces.

**Show:** a matrix of the order, inventory, and payment services against the five coupling kinds with evidence per cell.

**Check:** Which coupling does a shared table create? *(Data coupling, often with hidden deployment coupling.)*

---

## SRC-008-L03 · Evidence from change history (10 min)
**Goal:** use Git history to see what really changes together.

**Key points**
- Files that change in the same commit or PR show change coupling.
- Count co-changes across a time window; ignore noise (formatting, dependency bumps).
- Cross-service co-change means the boundary does not match the change pattern.
- History shows what is; it does not show what should be; combine with domain knowledge.

**Show:** a table: pair of modules, co-change count, percent of commits, interpretation.

**Check:** What does frequent co-change across two services suggest? *(The boundary may be in the wrong place or they should be merged.)*

---

## SRC-008-L04 · Team topology and boundaries (10 min)
**Goal:** align boundaries with teams.

**Key points**
- Conway's law: system structure mirrors communication structure.
- A service owned by several teams or a team owning ten services both signal strain.
- Cognitive load limits how much one team can own.
- Boundaries and team responsibilities should be designed together.

**Show:** a map of services, owning teams, and cognitive-load notes.

**Check:** What does Conway's law imply for architecture? *(Boundaries should match team communication; design them together.)*

---

## SRC-008-L05 · When to merge services back (10 min)
**Goal:** recognize and recommend consolidation.

**Key points**
- Signals: lockstep releases, chatty calls, shared database, one team on-call for both, low independent change.
- Merging reduces network cost, operations, and consistency complexity.
- Merge decisions need the same evidence as split decisions.
- Treat a merge as learning, not failure.

**Show:** a scorecard for two chatty services: calls per request, joint deploys, shared data, team overlap.

**Check:** Name two signals that services should merge. *(Lockstep releases and chatty calls, or shared database.)*

---

## SRC-008-L06 · Migration criteria and exit conditions (10 min)
**Goal:** plan a decomposition path that can stop or reverse.

**Key points**
- Incremental approaches: strangler pattern, branch by abstraction, extract the data last or first with care.
- Define exit criteria: what success looks like and what failure triggers rollback.
- Keep the old path until the new one is proven.
- Measure benefit at each stage and be ready to stop.

**Show:** a staged plan with criteria per stage: module boundary enforced, data separated, service deployed, old path removed.

**Check:** Why define exit conditions? *(So the migration can stop or revert when evidence says it is not working.)*

---

## SRC-008-L07 · Demo: mining Git history for change coupling (15 min)
**Goal:** extract co-change data from history; prepares SRC-008-LAB1.

**Steps**
1. Choose a time window and list commits touching more than one module or service.
2. Compute pair counts with a small script over `git log --name-only` (verify exact options before recording).
3. **Planned mistake:** include a dependency-bump commit touching every service. Fix: filter bulk commits by size or message.
4. Rank pairs and look at the top ones.
5. Cross-check with team ownership and domain meaning.
6. Write the finding with its limits.

---

## SRC-008-L08 · Demo: making the case to merge two chatty services (15 min)
**Goal:** argue for consolidation with evidence.

**Steps**
1. Gather data: calls per request, latency contribution, deploy history, incidents.
2. Show that 80% of changes touch both services.
3. **Planned mistake:** frame it as "the split was wrong". Fix: frame it as new evidence and name what was learned.
4. Present the merge plan: steps, risk, rollback, expected gains.
5. Address team ownership of the merged service.
6. Define the success measure and review date.
