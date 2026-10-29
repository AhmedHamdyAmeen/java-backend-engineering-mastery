# JNR-035 · Security fundamentals — Lecture scripts

**Video:** 50 min · **Analogy used throughout:** a building with a front door, staff-only rooms, and a vault.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-035-L01 · Thinking like an attacker (8 min)
**Goal:** see the Shop API the way someone who wants to abuse it sees it.

**Key points**
- Attackers want something: data, money, free service, or to break things.
- They look for the cheapest way in, not the cleverest.
- Every input the API accepts (URL, header, body, token) is a place to try something odd.
- Most real breaches use simple mistakes, such as a missing check, not movie-style hacking.
- Ask of every feature: "What if someone sends something I did not expect?"

**Show:** a list of goals for Shop: read other customers' orders, get a discount, take the site down, steal accounts.

**Check:** Do most attacks need advanced skills? *(No. Most use simple, common mistakes.)*

---

## JNR-035-L02 · Confidentiality, integrity, availability (8 min)
**Goal:** use the CIA triad to describe what we protect.

**Key points**
- Confidentiality: only the right people can read data.
- Integrity: data is not changed by the wrong people or by accident.
- Availability: the system works when people need it.
- One incident can break one or more: a leaked order list (C), a changed price (I), a flooded server (A).
- Controls often trade off against each other (a very strict lockout helps C but can hurt A).

**Show:** a three-row table: property / Shop example / attack example.

**Check:** A customer's order total is edited by someone else. Which property broke? *(Integrity.)*

---

## JNR-035-L03 · Trust boundaries (10 min)
**Goal:** find the lines where data crosses from less trusted to more trusted.

**Key points**
- A trust boundary is a line where the level of trust changes: browser to API, API to database, API to payment provider.
- Everything coming across a boundary from outside must be checked.
- The client is never trusted, even your own mobile app; users can change requests.
- Data leaving your system also crosses a boundary (logs, emails, third parties).
- A data flow diagram shows actors, processes, stores, and the boundary lines.

**Show:** a diagram: Browser | boundary | Shop API | boundary | Database, plus a payment provider outside.

**Check:** Is the mobile app your company wrote trusted? *(No. The device and requests are controlled by the user.)*

---

## JNR-035-L04 · Least privilege and defense in depth (8 min)
**Goal:** apply two core design rules.

**Key points**
- Least privilege: give each user, service, and database account only the access it needs.
- Defense in depth: several layers, so one failure is not a breach.
- Example layers: authentication, authorization check, validation, database permissions, logging.
- Do not rely on a single check, such as a hidden button in the UI.
- Review defaults: new accounts start with the lowest role.

**Show:** the Shop database user has only `SELECT/INSERT/UPDATE/DELETE` on its own schema, not admin rights.

**Check:** Why have both an API check and limited database rights? *(If one fails, the other still limits the damage.)*

---

## JNR-035-L05 · A first threat list (6 min)
**Goal:** write a short, useful list of threats.

**Key points**
- List assets (what is valuable), entry points (where input arrives), and threats (what could go wrong).
- Use a simple prompt such as STRIDE (spoofing, tampering, repudiation, information disclosure, denial of service, elevation of privilege). Name it only; deeper modeling comes later.
- For each threat write one planned control.
- Rank by likelihood and impact; start with the top ten.
- Security is designed in from the start, not a final checklist.

**Show:** a table row: "Customer reads another's order" / entry: `GET /orders/{id}` / control: ownership check.

**Check:** What is one planned control for "guessing order IDs"? *(An ownership check on every lookup.)*

---

## JNR-035-L06 · Demo: drawing Shop's trust boundaries (10 min)
**Goal:** draw the data flow and extract a threat list. Prepares `JNR-035-LAB1`.

**Steps**
1. Sketch actors: anonymous visitor, customer, admin.
2. Add Shop API, database, and the payment provider; draw boundary lines.
3. Label each flow with the data it carries (credentials, orders, card tokens).
4. **Planned mistake:** drawing the browser inside the trusted zone. Fix: move the boundary so the browser is outside.
5. For each boundary crossing, write one threat and one control.
6. Save the diagram and list in the repo as the seed for the security controls document.
