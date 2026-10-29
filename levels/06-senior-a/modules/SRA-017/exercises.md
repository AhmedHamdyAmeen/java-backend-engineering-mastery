# SRA-017 · Architectural reviews — Exercises and lab

## Lab
### SRA-017-LAB1 · Review round
**Outcomes:** 1–4 · **Time:** ~2.5 h
1. Review three designs from other learners (or provided designs) against a risk, complexity, and operability checklist.
2. Label each comment as blocking, suggestion, or question; blocking comments state the risk and a path forward.
3. Include at least three questions that guide the author to a problem.
4. Deliver reviews within the agreed turnaround; authors rate usefulness, fairness, and clarity.
5. Record your review outcomes and one change you will make to your practice.
**Acceptance:** each review separates blocking issues from preferences.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRA-017-EX01 | 1 | Review a short design with a queue between two services and list the risks in priority order. |
| SRA-017-EX02 | 1 | Assess a proposal that adds a new database technology for one team: complexity and operability findings. |
| SRA-017-EX03 | 2 | Classify twelve review comments as blocking or preference and rewrite weak blocking comments with risk and path forward. |
| SRA-017-EX04 | 3 | Write five questions that would let a team discover a lost-event risk without you naming it. |
| SRA-017-EX05 | 3 | Rewrite a verdict-style comment ("this design is wrong") into a question and a clear concern. |
| SRA-017-EX06 | 4 | Given review data (turnaround, number of blocking items, outcomes after launch), propose two improvements to the review practice. |

## Solutions
- **EX01** Priority: message loss or duplicates, ordering, poison messages, backlog growth, rollback; then operability.
- **EX02** New technology costs on-call, expertise, backups, upgrades, and tooling; check whether the existing store meets the need; if not, require an owner, runbooks, and a support plan.
- **EX03** Blocking: data loss, missing authentication, no rollback; preference: naming, minor library choice. Rewrite as "[BLOCKING] If X fails, Y data is lost; consider Z or tell me how you prevent it".
- **EX04** What if the write succeeds and the publish fails? What if the process restarts? How would we find a missing event? How do consumers recover? How is this tested?
- **EX05** "What happens when the second service is down for an hour? I am concerned that requests will queue without bound; how do you limit that?"
- **EX06** Example: reduce turnaround with a two-day target and a template; track defects found in production that the review missed; review blocking items quarterly.

Outcome 4 is also covered by the lab record of outcomes.

**Workplace evidence:** reviews you gave that changed designs before they shipped.
