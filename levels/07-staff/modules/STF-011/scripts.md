# STF-011 · Influence without authority — Lecture scripts

**Video:** 98 min · **Running case:** *Platform 2.0* — the strategy, governance, and platform direction from STF-P1 must now be adopted by about 20 product teams who did not ask for them; role-players act as engineering managers, skeptical tech leads, product, finance, security, and executives.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## STF-011-L01 · Authority you have vs influence you build (12 min)
**Goal:** separate the few things a Staff engineer can order from the many they must earn.

**Key points**
- Authority is granted by the org chart; influence is granted by peers, one decision at a time.
- A Staff engineer usually owns a technical direction, not people, budgets, or other teams' roadmaps.
- Influence comes from being useful, right often enough, and easy to work with.
- Borrowing a VP's name gets compliance once and costs trust afterwards.

**Show:** a two-column table for Platform 2.0: "I can decide" (golden-path design, reference code) versus "I must persuade" (20 teams' roadmaps, migration dates, manager priorities).

**Check:** Why is quoting the VP's support a weak first move? *(It produces reluctant compliance and spends borrowed trust; the real objections stay hidden.)*

---

## STF-011-L02 · Trust and credibility (12 min)
**Goal:** show how trust is built before any change is requested.

**Key points**
- Credibility = competence + reliability + good intent; lose one and the others count for less.
- Deposit first: fix a team's pain, review their design well, share credit.
- Do what you said, by when you said; say "I don't know" quickly.
- Be visible in other teams' problems, not only your own initiative.

**Show:** a trust ledger for three product teams: past help given, promises kept, open favors, and one planned small deposit per team before the Platform 2.0 ask.

**Check:** Which should come first with a team you barely know, an ask or a deposit? *(A deposit: useful help builds the credit the ask draws on.)*

---

## STF-011-L03 · Stakeholder mapping (10 min)
**Goal:** decide whom to talk to, in what order, and about what.

**Key points**
- Plot people on influence (can they block or sponsor?) and interest (how much does it affect them?).
- High influence/high interest: engage closely; high influence/low interest: keep informed and avoid surprises.
- Note each person's real concern: delivery date, risk, autonomy, cost.
- Maps go stale; update after every conversation.

**Show:** a grid of the 20 teams' tech leads, managers, security, and finance with a named concern and a first conversation order for each.

**Check:** Who needs the most careful attention: high influence/low interest, or low influence/high interest? *(High influence/low interest can block you quietly; keep them informed early.)*

---

## STF-011-L04 · Negotiation for engineers (14 min)
**Goal:** reach agreements both sides can actually commit to.

**Key points**
- Separate positions ("not this quarter") from interests ("we cannot miss the payments launch").
- Prepare your alternatives and what you can trade: timing, scope, support, shared work.
- Ask questions first; summarize their interest before proposing.
- End with a written, specific commitment: who, what, by when.

**Show:** a negotiation sheet: their position, their interest, our options (delay, pair engineer, reduced scope), and the agreed commitment.

**Check:** What is the difference between a position and an interest? *(A position is what they demand; an interest is the need behind it.)*

---

## STF-011-L05 · Conflict management (12 min)
**Goal:** handle disagreement between teams, and with leaders, without damaging the relationship.

**Key points**
- Name the conflict type: facts, goals, or values; each needs a different fix.
- Move from people to criteria: what would convince each side?
- Disagree with leaders in private, with data, with an option offered.
- Do not avoid the people who disagree; their objections are the free review.

**Show:** a short script: "I see it differently. Here is the data I used; what would change your mind?" followed by an agreed experiment.

**Check:** A leader decides against your proposal. What do you do? *(Raise concerns once with evidence, then commit and help it succeed, or escalate through the agreed channel.)*

---

## STF-011-L06 · Influence and integrity (8 min)
**Goal:** keep influence honest so it lasts.

**Key points**
- Persuade with evidence and honest costs; never with pressure, hidden deadlines, or flattery.
- Disclose your own interest (for example, ownership of the platform).
- Change your mind in public when shown to be wrong.
- Persuading by volume (more meetings, more messages) is a sign the case is weak.

**Show:** a checklist: "Would I be comfortable if the other person saw how I planned this conversation?"

**Check:** Why disclose that you own the platform you are promoting? *(It removes suspicion and makes your evidence easier to trust.)*

---

## STF-011-L07 · Demo: winning over a skeptical tech lead (15 min)
**Goal:** run a one-to-one with a tech lead who thinks the golden path will slow their team; prepares STF-011-LAB1.

**Steps**
1. Prepare: read their last two design docs, list their likely concerns, decide what you can offer.
2. Open with their problem, not your solution; ask what slows the team today.
3. Restate their concerns in their words; name the one you agree with.
4. **Planned mistake:** jump to the platform benefits and talk for five minutes; the tech lead goes quiet. Fix: stop, ask "what did I miss?", and listen.
5. Propose a small reversible trial (one service, two weeks, their success criteria).
6. Close with a written commitment or a recorded objection and a follow-up date.

---

## STF-011-L08 · Demo: negotiating platform migration timing with three managers (15 min)
**Goal:** reach a migration calendar three managers can commit to; prepares STF-011-LAB1.

**Steps**
1. List each manager's interest: payments launch, audit deadline, hiring ramp-up.
2. Share the constraints that are fixed (the legacy pipeline retires in Q4) and those that are not.
3. Offer trades: a pair engineer from the platform team for an earlier slot, a later slot for a team with a launch.
4. **Planned mistake:** negotiating each manager separately and promising the same slot twice. Fix: put all three constraints on one shared calendar and resolve conflicts openly.
5. Record agreed dates, owners, and what happens if a date slips.
6. Send the written summary the same day.
