# SRB-020 · Stakeholder communication — Lecture scripts

**Video:** 82 min · **Running case:** *The FulfillCo integration* — the engineer leads the four-team program planned in SRB-P1 through delivery; role-players act as team leads, product, finance, and security.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRB-020-L01 · Knowing your audience (10 min)
**Goal:** adapt a message to what each audience needs.

**Key points**
- Different audiences ask different questions: executives want impact, decisions, and risk; product wants scope and dates; engineers want detail.
- Identify the decision or action you want from the reader.
- Use their vocabulary, and define any term they might not know.
- Lead with the point; supply detail after.

**Show** Audience table: audience | main question | what they decide | format. Example: *finance | what does it cost and when does it pay back | budget | one-page summary.*

**Check:** What should you know before writing for a leader? *(What decision or action you need from them.)*

---

## SRB-020-L02 · Business impact framing (12 min)
**Goal:** translate technical work into business effects.

**Key points**
- Four lenses: revenue, risk, cost, and customer experience.
- Convert technical facts into effects: "no replay of events" becomes "a lost order update could mean unshipped paid orders".
- Use numbers with ranges and state assumptions.
- Do not overstate; honest uncertainty builds trust.

**Show** A translation table: technical statement | business impact | evidence. Example: *shipment status delay of 20 minutes | more support contacts and refunds | support ticket count.*

**Check:** Name the four lenses. *(Revenue, risk, cost, customer experience.)*

---

## SRB-020-L03 · Status reports (10 min)
**Goal:** write status reports that are honest and useful.

**Key points**
- Structure: overall status, progress since last report, next period, risks, and asks (decisions or help needed).
- Define status colors by criteria (for example amber when a milestone is at risk of slipping), so green is meaningful.
- State risks while they can still be fixed; do not wait for red.
- Keep it to one page and the same format every time.

**Show** A one-page template with the status criteria and a sample amber entry: *"Warehouse API contract not signed; decision needed from product by Friday; if missed, phase one slips two weeks."*

**Check:** Why define the status colors? *(So the reader can trust that green means green.)*

---

## SRB-020-L04 · Technical proposals for decision-makers (12 min)
**Goal:** write a proposal a non-technical leader can approve.

**Key points**
- Start with the decision requested, the recommendation, and cost and benefit.
- Describe the problem in business terms, then give options with trade-offs.
- Say what happens if nothing is done.
- Put technical detail in an appendix.
- End with next steps, owners, and the date a decision is needed.

**Show** Proposal outline: ask, recommendation, problem, options table (cost, benefit, risk), risks, timeline, decision date, appendix.

**Check:** What goes first in a proposal for executives? *(The decision requested and the recommendation.)*

---

## SRB-020-L05 · Delivering bad news (8 min)
**Goal:** deliver bad news early, clearly, and with options.

**Key points**
- Tell as soon as you are reasonably sure; waiting makes it worse.
- State facts first: what happened, impact, what is known and unknown.
- Offer options with trade-offs and a recommendation.
- Own the part you are responsible for, without blame or excuses.
- Agree the next update time.

**Show** A structure: *headline, impact, cause as known, options (with cost and date), recommendation, next update.*

**Check:** When should you deliver bad news? *(As soon as you are reasonably sure, with options.)*

---

## SRB-020-L06 · Demo: rewriting an engineering update for the executive team (15 min)
**Goal:** rewrite a technical update into a half-page executive update; prepares SRB-020-LAB1.

**Steps**
1. Read the original: details on event schemas and consumer lag with no stated impact.
2. Identify the executive's question and the decision needed.
3. Write the headline and status with the criteria used.
4. **Planned mistake:** keep the technical terms and add a glossary. Fix: translate into effects on orders, cost, and dates; put detail in a link.
5. Add risks and a clear ask with a date.
6. Test: can a colleague outside engineering state the ask after one read?

**Check:** What is the test of a good executive update? *(A non-engineer can state the decision asked of them after reading.)*

---

## SRB-020-L07 · Demo: telling leadership the program is four weeks late (15 min)
**Goal:** deliver a four-week slip to leadership with options; prepares SRB-020-LAB1.

**Steps**
1. Verify the facts: which milestone, the cause, and confidence in the new date.
2. Prepare options: reduce scope, add people (and the limits of that), or accept the date.
3. Write the one-page brief: headline, impact on customers and cost, options, recommendation.
4. **Planned mistake:** open with a long technical history to justify the slip. Fix: lead with the headline and options; offer history afterwards.
5. Hold the conversation, listen, and answer what you do not know with a date to find out.
6. Send a written summary with decisions and the next update date.

**Check:** What should the opening line contain? *(The slip, its size, and that options follow.)*
