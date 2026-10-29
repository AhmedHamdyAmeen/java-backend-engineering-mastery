# MID-063 · Technical documentation — Exercises and lab

## Lab
### MID-063-LAB1 · Shop docs
**Outcomes:** 1–4 · **Time:** ~3 h
1. Produce C4 level 1, 2, and 3 diagrams as code, with titles and legends.
2. Draw sequence diagrams for the order saga: happy path and one compensation path.
3. Write ADRs for the five biggest Shop decisions, each with real alternatives and consequences.
4. Write runbooks for three alerts.
5. Give the docs to a peer unfamiliar with Shop with ten questions.
**Acceptance:** the peer answers the ten questions using the docs alone.

## Exercises (assessment: documentation review; five exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-063-EX01 | 1 | Review a diagram without a legend; list five things a reader cannot know and fix them. |
| MID-063-EX02 | 1 | Write an ADR for "outbox instead of dual writes", with at least two alternatives and consequences. |
| MID-063-EX03 | 2 | Write a one-page RFC outline for adding returns and refunds to Shop, including goals, non-goals, and rollout. |
| MID-063-EX04 | 3 | Draw a C4 container diagram of Shop as code and a Mermaid or PlantUML sequence diagram for payment failure. |
| MID-063-EX05 | 4 | Write a runbook for the alert "consumer lag above threshold for 10 minutes". |

## Solutions
- **EX01** Unknown: meaning of shapes, sync versus async, technology, owner or date, scope. Fix with a legend, labeled arrows, title, and date.
- **EX02** Context: dual writes can lose events. Options: outbox, two-phase commit, best-effort publish. Decision: outbox. Consequences: relay to run, at-least-once delivery so consumers are idempotent.
- **EX03** Problem, goals, non-goals (for example no marketplace refunds), proposal, alternatives, risks, rollout in slices, open questions, reviewers and deadline.
- **EX04** Containers: web, gateway, orders, inventory, payments, Postgres, Kafka with labeled arrows; sequence shows `PaymentFailed` then `ReleaseStock`.
- **EX05** Symptom, impact, check lag dashboard and consumer logs, scale or restart consumer, check poison message and dead-letter topic, verify lag falls, escalation contact.
