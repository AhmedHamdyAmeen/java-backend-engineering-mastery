# ARC-030 · Data governance — Lecture scripts

**Video:** 58 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-030-L01 · Governance that enables use (10 min)
**Goal:** explain governance as a way to make data usable and trusted, not a brake.

**Key points**
- Governance answers: who owns this data, what quality is promised, where did it come from, who may use it.
- Bad governance is a committee that approves requests slowly; good governance is clear owners, published rules, and self-service within them.
- Governance supports the data architecture: without it, two reports show two revenue numbers.
- Start with the data sets that drive decisions, not every table.

**Show:** two Larkspur scenes: the board sees revenue of 41.2M in one report and 40.8M in another; versus a published "net revenue" definition with an owner.

**Check:** What does governance buy the business? *(Trusted, consistent data that people can find and use safely.)*

---

## ARC-030-L02 · Owners and stewards (10 min)
**Goal:** define ownership and stewardship roles for a solution.

**Key points**
- Data owner: accountable business person who decides rules and access (for example the head of finance for revenue).
- Data steward: does the daily work, resolves quality issues, maintains definitions.
- Technical custodian: runs the platform that stores the data; not the owner.
- Each key data set needs one named owner and one steward, tied to its system of record.

**Show:** a table: data set, owner, steward, custodian. Example: product master, head of merchandising, catalog team lead, ERP team.

**Check:** Is the database administrator the data owner? *(No. They are the custodian; the owner is the accountable business role.)*

---

## ARC-030-L03 · Data quality rules (12 min)
**Goal:** specify data quality rules and how they are measured and reported.

**Key points**
- Common dimensions: completeness, validity, uniqueness, consistency, timeliness.
- A rule is specific and testable: "every order has a store or web channel code".
- Each rule has a measure, a threshold, an owner, and a place where results are reported.
- Check rules where data enters, not only in the report; unmeasured rules do not exist.

**Show:** a rule sheet: rule, dimension, measure (percentage of failing rows), threshold, owner, report location, action on breach.

**Check:** What makes a quality rule real? *(It is measured, has a threshold, has an owner, and is reported.)*

---

## ARC-030-L04 · Lineage and access policies (12 min)
**Goal:** capture lineage from source to report and design access policies for consumers.

**Key points**
- Lineage shows each hop: source system, transformation, store, report; it enables impact analysis and root-cause tracing.
- Capture it at the level people need: data set and key transformation, with tooling where available (verify tool support before recording).
- Access policies: by class and role, with masking of personal fields for analytics, approval by the data owner.
- Analytics users should get the least data that serves the question, often pseudonymized.

**Show:** a lineage chain: till sale and web order → platform events → ERP posting → warehouse fact table → daily sales report, with owner at each hop.

**Check:** What question does lineage answer fastest? *(Where did this number come from, and what breaks if I change that source?)*

---

## ARC-030-L05 · Demo: tracing a wrong revenue number back to its source (14 min)
**Goal:** run a worked investigation of a wrong number using lineage and quality rules; prepares ARC-030-LAB1.

**Steps**
1. The board report shows yesterday's revenue 3 percent below the ERP finance view.
2. Walk the lineage backwards: report, warehouse fact, transformation, platform events, ERP postings.
3. Compare counts at each hop and find web orders in a pending state counted differently by the report and the ERP.
4. **Planned mistake:** patch the report formula to match. Fix: agree one definition of net revenue with the data owner, fix at the source transformation, and add a reconciliation rule.
5. Add a quality rule with threshold, owner, and alert, and update lineage documentation.
