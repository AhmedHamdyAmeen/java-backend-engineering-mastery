# ARC-036 · Solution roadmaps — Lecture scripts

**Video:** 56 min · **Running case:** *Larkspur Retail* — a mid-size retailer with 120 stores and a dated on-premises web shop; you are the solution architect for a new platform integrated with the existing ERP and CRM.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-036-L01 · Roadmaps that deliver value early (10 min)
**Goal:** explain why a roadmap should deliver measurable value in each phase.

**Key points**
- A roadmap that pays off only at the end carries all the risk until the end and is the first thing cut under budget pressure.
- Each phase should stand alone: if funding stopped after it, the business would still hold something useful.
- Value is stated in business terms: orders handled, hours saved, stock accuracy, not "services deployed".
- Early phases also reduce risk: they test the riskiest assumptions first.

**Show:** two timelines for Larkspur: one with all value at month 18, one with value at months 4, 9, and 18; mark where a funding cut hurts least.

**Check:** What should each roadmap phase be able to do? *(Deliver measurable business value on its own.)*

---

## ARC-036-L02 · Phasing a solution (12 min)
**Goal:** break a solution into phases using value, risk, and dependency.

**Key points**
- Slice vertically, by capability a user can use (web ordering for one range), not horizontally by layer (database first, UI last).
- Order slices by value and by risk: put the scariest unknown (ERP integration) early with a thin version.
- Keep phases a size the organization can absorb: change fatigue in stores is real.
- Each phase has a scope statement, an out-of-scope list, and an owner.

**Show:** a table of candidate phases for Larkspur: web ordering with ERP stock, click and collect, store returns, loyalty, analytics; columns value, risk, depends on.

**Check:** Why slice vertically? *(A vertical slice gives users a working capability each phase; layers deliver nothing usable until all are done.)*

---

## ARC-036-L03 · Dependency mapping (10 min)
**Goal:** map the dependencies that decide the sequence and may break it.

**Key points**
- Four kinds: technical (API must exist first), organizational (store staff training), vendor (SaaS roadmap or delivery date), contractual (notice periods, licence renewal dates).
- Draw them as arrows between phases and mark the owner of each external dependency.
- Vendor and contract dependencies are the ones left implicit most often; list them.
- Find the critical path and the dependencies with no slack.

**Show:** a dependency diagram: ERP interface upgrade to order posting to click and collect, plus contract date for the old web shop hosting ending in month 14.

**Check:** Name the four dependency types. *(Technical, organizational, vendor, contractual.)*

---

## ARC-036-L04 · Milestones and exit criteria (10 min)
**Goal:** define milestones with measurable exit criteria and keep the roadmap current.

**Key points**
- A milestone is an observable state, not an activity: "10 pilot stores taking orders" rather than "development finished".
- Exit criteria are measurable and agreed in advance: performance target met, error rate under a limit, operations accepted handover.
- Review the roadmap at a regular rhythm and after major changes in scope, funding, or vendors.
- Record each change with its reason; a roadmap that is never updated becomes fiction.

**Show:** a milestone card: name, date, exit criteria (three measurable items), owner, and dependency status.

**Check:** What makes an exit criterion good? *(It is measurable and agreed before the work begins.)*

---

## ARC-036-L05 · Demo: Larkspur's 18-month roadmap, phase by phase (14 min)
**Goal:** build the Larkspur roadmap as a worked design session; prepares ARC-036-LAB1.

**Steps**
1. Collect the business goals from sponsors: grow web sales, reduce stock errors, retire the old web shop hosting before month 14.
2. List candidate capabilities and rate value and risk; choose phase one: web ordering for a pilot product range with live ERP stock.
3. Sequence later phases (click and collect, returns, loyalty, analytics) using dependencies and the hosting contract date.
4. **Planned mistake:** place the ERP interface work in phase three because it is "just plumbing". Fix: pull a thin ERP stock interface into phase one, as phase one needs it and it is the highest risk.
5. Write exit criteria for each milestone and the first release scope with an out-of-scope list.
6. Check the roadmap for value at months 4 and 9 and for implicit vendor dependencies; add the missing ones.
