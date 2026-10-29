# SRA-009 · Security and compliance — Lecture scripts

**Video:** 84 min · **Running case:** *Commerce 2030* — the group formed by Shop and FulfillCo has 25 engineering teams and plans a third-party seller marketplace, a five-country expansion, and doubled order volume each year for three years, while its earliest services approach end of life; you are the senior technical leader for the commerce product area.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRA-009-L01 · Compliance as an architecture driver (10 min)
**Goal:** treat regulation as a design input from the start.

**Key points**
- Marketplace, payouts, and new countries bring privacy, payment, tax, and consumer rules.
- Late compliance fixes are expensive: data copies and flows are hard to find afterward.
- Compliance is a result of controls built into the system plus evidence that they work.
- Work with compliance partners; they define obligations, you design how to meet them.

**Show:** a table: obligation (verify with compliance), affected data and systems, architecture response, evidence produced.

**Check:** Who defines the obligation and who designs the response? *(Compliance and legal define it; engineering designs how to meet it and produce evidence.)*

---

## SRA-009-L02 · Privacy by design (12 min)
**Goal:** apply privacy principles as concrete design choices.

**Key points**
- Data minimization: collect and keep only what a purpose needs.
- Purpose limitation: use data only for the declared purpose; tag data with purpose.
- Retention: delete or anonymize on schedule, including derived stores and backups.
- Consent: record, check, and honor withdrawal across systems.

**Show:** a data inventory row for seller data: fields, purpose, legal basis (confirm with legal), retention, systems holding copies, deletion path.

**Check:** What does purpose limitation require in design? *(Data is used only for the declared purpose, with the purpose recorded and enforced.)*

---

## SRA-009-L03 · Auditability (10 min)
**Goal:** make changes and access traceable and tamper-resistant.

**Key points**
- Audit log: who did what, to which data, when, from where, and the outcome.
- Make logs append-only and protected from the people being audited.
- Trace changes through deployment and configuration, not only data access.
- Balance: logs themselves must not leak personal data; retain them as long as required.

**Show:** an audit event schema with actor, action, subject, time, source, result, and request id, written to append-only storage with restricted read access.

**Check:** Why protect audit logs from the people being audited? *(Otherwise records could be altered or deleted, defeating their purpose.)*

---

## SRA-009-L04 · From regulation to requirements (12 min)
**Goal:** translate regulatory text into testable architecture requirements with compliance partners.

**Key points**
- Take each obligation (for example data subject rights, payment card data protection, local data laws) and restate it as a system requirement.
- Use workshops with compliance: they explain intent and evidence they need.
- Each requirement gets an owner, a control, and a test or evidence source.
- Record uncertain interpretations as open items; do not guess.

**Show:** a trace table: regulation clause (verify exact text), requirement, design control, test, evidence location, owner.

**Check:** What should you do with an unclear regulatory interpretation? *(Record it as an open item and resolve it with compliance rather than guess.)*

---

## SRA-009-L05 · Reducing compliance scope (10 min)
**Goal:** shrink the systems that fall under heavy rules.

**Key points**
- Tokenization: replace sensitive values with tokens so most systems never see the real data.
- Segmentation: isolate in-scope systems with strict boundaries and access.
- Use certified providers for the most regulated pieces, such as card capture.
- Fewer in-scope systems means less audit effort and less risk.

**Show:** a before/after diagram: card numbers flowing through twelve services, versus a hosted payment field that returns a token so only one small service is in scope.

**Check:** How does tokenization reduce compliance scope? *(Most systems handle tokens, not sensitive data, so they leave scope.)*

---

## SRA-009-L06 · Demo: shrinking PCI scope with tokenization (15 min)
**Goal:** redesign payments so fewer systems handle card data; prepares SRA-009-LAB1.

**Steps**
1. Trace where card data flows today and list all in-scope services (verify scope rules with the compliance officer).
2. Propose a hosted capture or payment provider that returns tokens to the browser and back end.
3. Redesign flows so orders, refunds, and payouts use tokens; confirm the remaining in-scope boundary.
4. Plan migration and verification: remove old stores and logs that held card data.
5. **Planned mistake:** declare scope reduced while old logs and an analytics export still contain card numbers. Fix: scan stores and pipelines, purge, and add a detection check.
6. Review with the compliance officer and record evidence.

---

## SRA-009-L07 · Demo: designing data deletion across 30 services (15 min)
**Goal:** design right-to-erasure that reaches every store; prepares SRA-009-LAB1.

**Steps**
1. Build the data inventory: which of the thirty services hold personal data, in primary, derived, cache, search, analytics, and backup stores.
2. Choose the pattern: a deletion request event, each owner deletes or anonymizes and confirms, with a coordinator tracking completion.
3. Handle exceptions: legal retention of invoices, fraud records, and backups (expire by schedule); confirm rules with legal.
4. Define evidence: completion report and audit events, with deadlines.
5. **Planned mistake:** delete only from primary databases. Fix: add derived stores, search indexes, analytics, and backup expiry, and test with a synthetic user.
6. Add a fitness function that fails new services lacking a deletion handler.
