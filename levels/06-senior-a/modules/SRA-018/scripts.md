# SRA-018 · Organizational bottlenecks — Lecture scripts

**Video:** 82 min · **Running case:** *Commerce 2030* — the group formed by Shop and FulfillCo has 25 engineering teams and plans a third-party seller marketplace, a five-country expansion, and doubled order volume each year for three years; the strategy must now be adopted by 25 teams, funded, and executed, with role-players acting as managers, product, finance, security, and executives.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRA-018-L01 · Conway's Law (10 min)
**Goal:** see that system structure follows team communication structure.

**Key points**
- Conway's Law: organizations design systems that mirror their own communication structure.
- Two teams that must coordinate on every change will produce a tightly coupled seam.
- A single team owning two unrelated areas tends to blur them.
- The architecture you want will not survive an organization that fights it.

**Show:** Commerce 2030 example: ordering and inventory owned by two teams that must agree on every release; the shared database table is the seam.

**Check:** Why does a team boundary shape the architecture? *(Teams design along their communication paths and avoid costly coordination.)*

---

## SRA-018-L02 · Measuring coordination cost (12 min)
**Goal:** measure how much delivery time goes to waiting for other teams.

**Key points**
- Look at cross-team dependencies per change, handoffs, queues, and wait time.
- Sources: ticket history, pull-request reviews across teams, release calendars, incident links.
- Lead time split into working time and waiting time shows the true cost.
- Measure before proposing; data stops the debate from being about opinions.

**Show:** a table per team: changes in the last quarter, share needing another team, median wait for that team, top three teams waited on.

**Check:** What shows coordination cost best? *(Wait time and the share of changes needing another team.)*

---

## SRA-018-L03 · Team topologies and cognitive load (12 min)
**Goal:** use team types and cognitive load to judge whether team boundaries are workable.

**Key points**
- Team Topologies describes four team types: stream-aligned, platform, enabling, and complicated-subsystem.
- Each team has a limit on the amount it can understand and operate: its cognitive load.
- Overloaded teams slow down, avoid ownership, and burn out.
- Check load by the number of domains, services, on-call burden, and technologies the team must master.

**Show:** a cognitive-load card per team: domains owned, services run, on-call incidents per month, technologies; flagged where above what the team can sustain.

**Check:** What is a sign of a team above its cognitive load? *(Slow change, unclear ownership, heavy on-call, and burnout.)*

---

## SRA-018-L04 · The inverse Conway maneuver (10 min)
**Goal:** shape the teams to produce the architecture you want.

**Key points**
- Inverse Conway: design team boundaries to match the target architecture.
- Reorganizing without architectural change moves the problem; changing architecture without team change fails.
- Align teams to business domains from the context map, with clear ownership of data and interfaces.
- Phase the change; move ownership first, then code, then interfaces.

**Show:** target context map (ordering, inventory, seller, payments) next to the proposed team boundaries, with the interfaces each team will own.

**Check:** Why change both teams and architecture? *(One without the other leaves the old coupling in place.)*

---

## SRA-018-L05 · Working with managers on team design (8 min)
**Goal:** influence team design while respecting that people management belongs to managers.

**Key points**
- You bring the data and the target architecture; managers decide structure, hiring, and people.
- Understand their constraints: headcount, careers, morale, budgets, and reporting lines.
- Offer options with costs and transition steps rather than a final answer.
- Share credit and agree who communicates what to teams.

**Show:** a proposal outline: problem with data, options, effect on architecture, effect on people, transition steps, risks, decision needed from managers.

**Check:** What do you bring to the manager conversation? *(Data, the target architecture, and options; they own structure and people decisions.)*

---

## SRA-018-L06 · Demo: finding the team that every change waits on (15 min)
**Goal:** locate the main coordination bottleneck with data; prepares SRA-018-LAB1.

**Steps**
1. Export a quarter of tickets and pull requests for twelve teams.
2. Build the dependency matrix: which team each change needed.
3. Compute wait time per team and rank them.
4. **Planned mistake:** conclude "the platform team is slow" from the biggest queue. Fix: check what they own; the queue reflects too many unrelated responsibilities, so the finding is overload and mixed ownership.
5. Validate with the team's lead and list the first three changes to test.

---

## SRA-018-L07 · Demo: proposing a team split aligned with the context map (15 min)
**Goal:** run a worked session proposing a team split with engineering managers; prepares SRA-018-LAB1.

**Steps**
1. Start from the data: the overloaded team owns pricing, promotions, and seller fees, which belong to different subdomains.
2. Map to the context map: pricing and promotions are consumer-side; seller fees belong to the seller domain.
3. Propose the split with interfaces and data ownership, and estimate the reduction in dependencies.
4. **Planned mistake:** present a reorganization chart without the architectural changes. Fix: pair it with the interface and data-ownership steps that make the boundary real.
5. Discuss manager constraints (headcount, careers, timing) and agree the transition plan and communication.

**Show:** before-and-after dependency counts for the affected teams.
