# ARC-043 · Solution documentation — Lecture scripts

**Video:** 54 min · **Running case:** *Larkspur Retail* — a mid-size retailer with 120 stores and a dated on-premises web shop; you are the solution architect for a new platform integrated with the existing ERP and CRM.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-043-L01 · The architecture pack (10 min)
**Goal:** assemble documentation as a pack structured by audience, not one big document.

**Key points**
- Four main readers: executives (decision and value), reviewers (compliance and risk), delivery (build detail), operations (run detail).
- A pack has an index, a one-page summary, and sections per audience that link to each other.
- Each document has a purpose, owner, status, version, and date.
- Reuse sources instead of copying them: link to the ADR rather than retyping it.
- Smaller and current beats complete and stale.

**Show:** a pack contents page for Larkspur: executive summary, options and decision, HLD, LLD for order fulfilment, interface contracts, deployment diagram, ADR log, risk register, operations handover; each with reader and owner.

**Check:** Why not write one document for everyone? *(Different readers need different depth; one document serves none of them well.)*

---

## ARC-043-L02 · Decision and assumption logs (10 min)
**Goal:** keep a decision log and an assumptions log that explain why the solution is the way it is.

**Key points**
- A decision log lists each significant decision: context, options, choice, consequences, owner, date, status (ADRs fit here).
- An assumption log lists things believed true but not verified, with an owner and a date by which to confirm.
- Link them: an assumption underlying a decision is a reason to revisit it if proved wrong.
- Write decisions when made, not afterwards from memory.
- Mark superseded decisions rather than deleting them.

**Show:** two sample entries: decision "Use managed payment page so card data never touches Larkspur systems" and assumption "Payment provider supports 3-D Secure flow for click-and-collect; owner: payment lead; confirm by end of month 2".

**Check:** What is different about an assumption entry? *(It records something unverified, with an owner and a date to confirm or reject it.)*

---

## ARC-043-L03 · Risk registers (10 min)
**Goal:** run a risk register that drives action rather than collecting worries.

**Key points**
- Each risk: description (cause, event, effect), likelihood, impact, owner, mitigation, trigger, review date, status.
- Phrase risks as "because X, Y may happen, resulting in Z", not as vague topics like "integration".
- Every risk has a named owner and a date; otherwise it is a note.
- Distinguish a risk (might happen) from an issue (has happened) and from an assumption.
- Review regularly; close or escalate; show top risks in the pack summary.

**Show:** a Larkspur risk row: "Because the ERP vendor releases monthly, a changed stock API may break order promises (likelihood medium, impact high); owner: integration lead; mitigation: contract tests in CI and a change notice agreement; review: monthly".

**Check:** What makes a risk register entry actionable? *(A named owner, mitigation, and review date.)*

---

## ARC-043-L04 · Keeping documentation alive (10 min)
**Goal:** keep documentation current through delivery and hand it over cleanly.

**Key points**
- Assign owners per document and set update triggers: a design change, a new ADR, a release.
- Keep documents next to the work: in the repository or wiki the team already uses, with reviews that include docs.
- Review the pack at each phase boundary; retire what is no longer true.
- Handover to operations and future architects: a short reading order, a "how to find things" page, and open risks and decisions.
- Test it: can someone new answer common questions from the pack alone?

**Show:** a documentation health check: owner present, last reviewed within agreed period, links working, matches deployed reality; scored for each pack document.

**Check:** How do you test the pack at handover? *(Ask someone new to answer typical questions using only the pack.)*

---

## ARC-043-L05 · Demo: assembling Larkspur's architecture pack (14 min)
**Goal:** assemble the Larkspur pack from existing design work, structured by audience. This prepares ARC-043-LAB1.

**Steps**
1. List existing artifacts (options analysis, HLD, LLD, ADRs, roadmap, migration plan, cost model) and map each to a reader.
2. Draft the index and the one-page summary: the decision, scope, key risks, and the ask.
3. **Planned mistake:** merge everything into one long document "for completeness". Fix: split by audience, link instead of copying, and give each part an owner and review date.
4. Build the decision log from ADRs and add an assumption log with owners and confirm-by dates.
5. Create the risk register with five to eight actionable entries and mark top three in the summary.
6. Test: have a colleague answer ten questions (why this platform, how are stock updates handled, who owns the payment integration) using only the pack; fix gaps.

**Check:** What was the planned mistake? *(Combining all content into one document instead of structuring by audience.)*
