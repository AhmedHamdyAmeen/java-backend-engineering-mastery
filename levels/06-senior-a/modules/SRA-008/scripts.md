# SRA-008 · Architecture economics — Lecture scripts

**Video:** 84 min · **Running case:** *Commerce 2030* — the group formed by Shop and FulfillCo has 25 engineering teams and plans a third-party seller marketplace, a five-country expansion, and doubled order volume each year for three years, while its earliest services approach end of life; you are the senior technical leader for the commerce product area.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRA-008-L01 · Architecture decisions are investment decisions (10 min)
**Goal:** treat large architecture choices as investments with costs, returns, and risks.

**Key points**
- Every major decision commits money and engineering time now for benefits later.
- Finance thinks in costs, returns, timing, and risk; translate your argument into those terms.
- Benefits can be revenue, cost avoided, risk reduced, or speed gained; state which.
- Not deciding is also a decision, with its own cost.

**Show:** a one-page template: decision, options, cost by year, benefit by year, risks, assumptions, and the cost of delay.

**Check:** What are four types of benefit an architecture investment can claim? *(Revenue, cost avoided, risk reduced, speed gained.)*

---

## SRA-008-L02 · Build vs buy vs open source (12 min)
**Goal:** compare the three sourcing options on the same basis.

**Key points**
- Build: full control and differentiation, with ongoing maintenance and staffing.
- Buy: speed and shared maintenance, with licence cost, lock-in, and limited customization.
- Open source: no licence fee but you pay for operation, upgrades, and sometimes support.
- Use the subdomain view: build the core, buy or adopt generics.

**Show:** a comparison table with criteria: fit, time to value, control, cost over five years, risk, exit effort, team skills.

**Check:** Does open source mean free? *(No; you still pay for operation, upgrades, security, and staff.)*

---

## SRA-008-L03 · Total cost of ownership (12 min)
**Goal:** compute multi-year cost including the items usually left out.

**Key points**
- Include licences or usage fees, infrastructure, integration, operation, on-call, training, and upgrades.
- Staffing is often the largest cost: engineers needed to run and change it.
- Use a multi-year horizon (five years is common) and account for growth in volume.
- Make assumptions explicit so others can reproduce and challenge the numbers.

**Show:** a five-year TCO spreadsheet outline: rows for each cost type, columns for years, volume assumptions on a separate sheet, and a sensitivity table.

**Check:** Why is comparing a licence fee with zero wrong? *(Building also costs engineers, infrastructure, and maintenance.)*

---

## SRA-008-L04 · Opportunity cost (10 min)
**Goal:** include what the team would not do if it chose an option.

**Key points**
- Engineers building a payments engine cannot build seller tools in the same period.
- Value the alternative use: the benefit forgone from the next best project.
- Staffing decisions have a ramp-up and hiring delay; include them.
- Opportunity cost often decides between two options with similar TCO.

**Show:** a two-column comparison: option A (build) uses 12 engineers for 18 months; the next best use of those engineers is the marketplace seller tools with estimated value.

**Check:** What does opportunity cost measure? *(The value of the best alternative use of the same resources.)*

---

## SRA-008-L05 · Real options thinking (10 min)
**Goal:** value flexibility and the cost of keeping a decision open.

**Key points**
- An option is the right, not the obligation, to do something later.
- Paying a small amount now (an abstraction, a pilot) can avoid a large commitment under uncertainty.
- Estimate the cost of keeping open against the cost of committing wrongly, and the likelihood of change.
- Exit cost matters: a decision that is cheap to reverse needs less analysis.

**Show:** a decision tree: commit now to vendor A at lower unit price, or pay for an abstraction layer and pilot two vendors; probabilities and costs on each branch (state assumptions).

**Check:** When is paying to keep a decision open worth it? *(When uncertainty is high and a wrong commitment is expensive to reverse.)*

---

## SRA-008-L06 · Demo: buy vs build for marketplace seller payouts (15 min)
**Goal:** work through a full sourcing analysis; prepares SRA-008-LAB1.

**Steps**
1. Define the need: pay sellers in five countries, handle fees, holds, tax forms, and reconciliation.
2. List options: build in-house, buy a payout platform, a hybrid with a provider for payments and our own ledger.
3. Build five-year TCO with volume growth, staffing, compliance, and integration cost.
4. Add opportunity cost, exit plan, and risks (provider failure, price changes).
5. **Planned mistake:** compare the vendor's fee with zero for the build option. Fix: add the engineers, on-call, compliance work, and delay to market.
6. Recommend and name the decision triggers that would reopen the choice.

---

## SRA-008-L07 · Demo: a finance review of an architecture business case (15 min)
**Goal:** run a role-played review where finance checks the numbers; prepares SRA-008-LAB1.

**Steps**
1. Present the one-page case: options, costs, benefits, assumptions.
2. Finance asks to reproduce a number: show the model and sources for each input.
3. Handle challenges: discount rate, volume assumption, headcount cost, benefit timing.
4. Run sensitivity on the two most uncertain inputs and show the decision does or does not change.
5. **Planned mistake:** hard-code assumed volumes in cells with no source. Fix: separate an assumptions sheet with owner and source, and re-run.
6. Agree follow-up: which assumptions will be tracked and when to report actuals.
