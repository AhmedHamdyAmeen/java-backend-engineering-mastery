# ARC-038 · Operational architecture — Lecture scripts

**Video:** 58 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-038-L01 · Designing for operations (10 min)
**Goal:** treat operations as a design input, not an afterthought.

**Key points**
- Operations is where the design is tested every day; ask the operations team early.
- Design questions: who detects a failure, who fixes it, how do they see it, what is the runbook.
- Include operability requirements: observability, deployability, recoverability, supportability.
- Operational acceptance criteria are written at design time and checked before handover.

**Show:** an operability checklist per component: health endpoint, logs, metrics, alerts, runbook, owner, backup and restore, on-call.

**Check:** When should operations be involved? *(From the start of design, not after go-live.)*

---

## ARC-038-L02 · Monitoring a mixed estate (12 min)
**Goal:** design monitoring, alerting, and logging across owned, SaaS, and on-premises components.

**Key points**
- Four views: infrastructure health, application metrics, business metrics (orders per minute), and end-to-end synthetic checks.
- SaaS components: monitor from outside with synthetic checks and provider status feeds; do not assume the vendor will tell you in time.
- Correlation: a trace or order ID passed across systems makes support possible.
- Alert on symptoms that matter to the business, with severity and routing; avoid alert floods.
- Logs: central, searchable, with sensitive data excluded and retention set.

**Show:** a monitoring map: component, owner, signals, alert, destination; SaaS rows use synthetic checks and webhook failure rates.

**Check:** How do you monitor a SaaS you cannot install agents in? *(Synthetic checks, integration error rates, and the vendor's status feed.)*

---

## ARC-038-L03 · Support models and service ownership (12 min)
**Goal:** define support tiers, hours, escalation, and service ownership.

**Key points**
- Tiers: service desk (first line), operations or application support (second), engineering and vendors (third).
- Hours follow business needs: store trading hours and web peaks, not office hours.
- Every service and every integration has one named owner team; shared ownership means no ownership.
- Escalation paths define who is called, in what time, for which severity.

**Show:** an ownership map: service, owner team, support tier path, hours, vendor contact, severity targets.

**Check:** Who owns the order-to-ERP integration? *(It needs one named owner team; it must not fall between platform and ERP teams.)*

---

## ARC-038-L04 · Incident and change processes with vendors (10 min)
**Goal:** align incident and change processes between Larkspur and its vendors.

**Key points**
- Contracts set vendor response and resolution targets; Larkspur's internal severity levels need to map to them.
- Joint incident process: who declares, who communicates, the bridge call, evidence sharing, review.
- Change: vendors' release calendars and maintenance windows must feed Larkspur's change calendar.
- Test vendor escalation before you need it.

**Show:** a table mapping Larkspur severity 1-4 to vendor priority levels and response targets, plus a change-calendar overlay for the payment, CRM, and ERP vendors.

**Check:** Why map severity levels to vendor priorities? *(So a Larkspur severity-1 incident gets the vendor's fastest response, with no argument during the outage.)*

---

## ARC-038-L05 · Demo: Larkspur's operating model on a single page (14 min)
**Goal:** worked session producing a one-page operating model; prepares ARC-038-LAB1.

**Steps**
1. List services and integrations from the architecture: web, app, order, stock, payments, ERP, CRM, carriers, reporting.
2. Assign an owner team, support tier, and hours to each.
3. Define monitoring per service including SaaS synthetic checks, and the on-call route.
4. **Planned mistake:** leave integrations unowned because "both teams touch them". Fix: assign one owner per integration with the other side as a named contact.
5. Add vendor escalation paths and operational acceptance criteria; review with a role-played head of IT operations.
