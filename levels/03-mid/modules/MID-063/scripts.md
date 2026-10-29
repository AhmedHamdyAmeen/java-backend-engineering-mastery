# MID-063 · Technical documentation — Lecture scripts

**Video:** 68 min · **Analogy used throughout:** a city map with a legend: different zoom levels for different travelers, and a note on why each road was built.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-063-L01 · Documentation that gets read (8 min)
**Goal:** write docs people actually use.

**Key points**
- Write for a named reader with a named question: new joiner, on-call engineer, reviewer.
- Keep docs next to the code (docs as code): reviewed in pull requests, versioned in git.
- Prefer a few short, current documents over many stale ones; give each an owner and a date.
- Document why, not what; the code already says what.
- Every diagram needs a title and a legend.

**Show:** a docs folder layout: `docs/adr/`, `docs/rfc/`, `docs/architecture/`, `docs/runbooks/`.

**Check:** What goes wrong with a diagram that has no legend? *(Readers guess what boxes and arrows mean.)*

---

## MID-063-L02 · Architecture decision records (10 min)
**Goal:** capture a decision so it can be understood later.

**Key points**
- An ADR is a short, numbered record of one significant decision.
- Sections: title, status, context, options considered, decision, consequences.
- Write it when deciding, with the real alternatives; written afterwards it becomes justification.
- Status: proposed, accepted, superseded by ADR-nnn. Never delete; supersede.
- Include the trade-off accepted and a review trigger or date.

**Show:** ADR-007 "Use Kafka for order events" with options (outbox + Kafka, RabbitMQ, polling), decision, and consequences.

**Check:** Why list the rejected options? *(So readers see the decision was weighed and can revisit it when conditions change.)*

---

## MID-063-L03 · RFCs and design docs (10 min)
**Goal:** get a change reviewed before building it.

**Key points**
- Use an RFC for changes that are costly to reverse or cross team boundaries.
- Outline: problem, goals and non-goals, proposal, alternatives, risks, rollout, open questions.
- Keep it short; the aim is feedback, not approval theater.
- Set a review deadline and name reviewers, including consumers of the change.
- Accepted RFCs may spawn ADRs; the RFC explores, the ADR records the outcome.

**Show:** an outline for "RFC: move payments to its own service" with non-goals and a rollout plan.

**Check:** What is a non-goal for? *(To state what the proposal deliberately does not try to solve.)*

---

## MID-063-L04 · C4 diagrams (12 min)
**Goal:** draw the system at three zoom levels.

**Key points**
- Level 1, context: your system, its users, and external systems.
- Level 2, container: separately running units (services, databases, brokers) and how they talk.
- Level 3, component: the main building blocks inside one container.
- Level 4 (code) is usually left to the IDE.
- Each element has a name, a type, a short description; each arrow a label such as "Publishes OrderPlaced (Kafka)".
- Diagrams as code: Structurizr DSL, PlantUML C4, or Mermaid; verify version of the C4 support before recording.

**Show:** a Structurizr DSL snippet with `person`, `softwareSystem`, `container`, and a `views` block.

**Check:** Is a Kafka topic a container in C4? *(A broker is; the topic is detail inside it.)*

---

## MID-063-L05 · Sequence diagrams (8 min)
**Goal:** show how a request or saga flows over time.

**Key points**
- Participants across the top, time flowing down, arrows as messages.
- Use them for one scenario: the happy path, then a key failure path.
- Show sync calls and async events differently, and name the event.
- Keep to about 6-8 participants; split the diagram if larger.
- Source as text (Mermaid or PlantUML) so it is diffable.

**Show**
```
sequenceDiagram
  Orders->>Inventory: ReserveStock
  Inventory-->>Orders: StockReserved
  Orders->>Payments: ChargeCard
  Payments--)Orders: PaymentFailed
  Orders->>Inventory: ReleaseStock
```

**Check:** Which scenario should you draw besides the happy path? *(A significant failure, such as payment failing and compensation.)*

---

## MID-063-L06 · Runbooks (8 min)
**Goal:** write a runbook someone can follow at 3 a.m.

**Key points**
- One runbook per known alert or failure; linked from the alert.
- Sections: symptom and alert, impact, quick checks, mitigation steps, escalation, how to verify recovery.
- Give exact commands, dashboard links, and expected output.
- Write in short numbered steps; no assumptions about prior knowledge.
- Update after every incident that used it.

**Show:** runbook "Outbox backlog growing": check lag panel, check relay pod logs, restart relay, confirm backlog drains.

**Check:** What must an alert link to? *(Its runbook.)*

---

## MID-063-L07 · Demo: C4 diagrams of Shop Platform as code (12 min)
**Goal:** model Shop levels 1-3 in one text file. Prepares `MID-063-LAB1`.

**Steps**
1. Create `workspace.dsl` in Structurizr (or Mermaid/PlantUML); define the customer and the payment provider.
2. Add containers: web app, API gateway, orders, inventory, payments, Postgres, Kafka.
3. Add relationships with labels and technologies.
4. **Planned mistake:** unlabeled arrows and no legend; a viewer cannot tell sync from async. Fix: label each arrow and add a legend and title.
5. Add a component view of `orders` and render all views.
6. Commit the file and render in CI so the diagram never drifts.
