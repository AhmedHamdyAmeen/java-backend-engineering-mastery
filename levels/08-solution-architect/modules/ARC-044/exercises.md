# ARC-044 · Architecture communication — Exercises and lab

## Lab
### ARC-044-LAB1 · Present Larkspur
**Outcomes:** 1–4 · **Time:** ~4 h
1. Build a ten-minute executive presentation with a clear ask, options, roadmap, cost and benefit, risks, and next steps; prepare backup slides.
2. Build a 30-minute technical session for engineering with context, structure, interfaces, failure cases, and fixed-versus-flexible decisions.
3. Present to a role-played executive panel; then to a role-played engineering panel that challenges the design.
4. Label each answer as fact, assumption, or trade-off; log unanswered challenges as follow-ups with owners and dates.
5. Write a short reflection on what you would change.
**Acceptance:** executives can state the decision asked of them; the engineering panel's challenges are answered with evidence or recorded as follow-ups.

## Exercises (case-based; five exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-044-EX01 | 1 | Rewrite the opening of a draft executive presentation ("Our architecture uses an event-driven integration layer…") so that it starts with the ask and the business benefit. |
| ARC-044-EX02 | 1 | List the headline facts an executive needs on one slide for the Larkspur recommendation, including stated assumptions. |
| ARC-044-EX03 | 2 | Plan a 30-minute session for the order-fulfilment team: agenda, which diagrams, and what is fixed versus team-decided. |
| ARC-044-EX04 | 3 | A panel member says "you cannot guarantee stock accuracy across 120 stores". Write a reply separating fact, assumption, and trade-off. |
| ARC-044-EX05 | 4 | Choose the diagrams and narrative for (a) the executive board, (b) the store operations leads, (c) the engineering teams; justify each. |

## Solutions
- **EX01** "We ask you to approve the platform and phase-one budget; in six months online orders will show real store stock, cutting cancelled orders" then the minimum of how.
- **EX02** The decision, recommended option and why, first-value date, five-year cost and benefit with ROI and key assumptions, top three risks, next steps.
- **EX03** Context and constraints (5), component and sequence views (10), contracts and failure cases (10), questions logged (5); fixed: principles, contracts, NFR targets; team-decided: internal structure within them.
- **EX04** Fact: test results on stock sync lag; assumption: order rates and store scan discipline, to be confirmed by a date; trade-off: reservation window and a safety buffer versus availability; follow-up: pilot-store measurement.
- **EX05** Board: context diagram and roadmap one-pager, business story; store leads: a "what changes for you" view with a process flow; engineers: component, sequence, and deployment views and contracts.

All four outcomes are also covered by the lab acceptance and the quiz.

**Workplace evidence:** a solution presentation that secured approval or funding.
