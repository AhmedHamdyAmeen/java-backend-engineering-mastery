# SRC-019 · Incident leadership — Exercises and lab

## Lab
### SRC-019-LAB1 · Command a game day
**Outcomes:** 1–4 · **Time:** ~3.5 h
Lead a multi-team simulated incident on the order subsystem with role-players: assign roles, run the response, send cadenced updates, decide on a risky mitigation. Then facilitate its blameless postmortem.
**Acceptance:** assessed on coordination, communication, and action quality.

## Exercises (assessment: incident-command simulation, a graduation gate component)
| ID | Outcome | Task |
| --- | --- | --- |
| SRC-019-EX01 | 1 | Case: five responders join at once and all start debugging. Write your first three messages as IC. |
| SRC-019-EX02 | 2 | Write three consecutive stakeholder updates for a 90-minute checkout outage, including one with no new information. |
| SRC-019-EX03 | 3 | Choose between rolling back, failing over, and shedding load with unclear evidence. Complete a decision table and state your check. |
| SRC-019-EX04 | 4 | Rewrite blaming postmortem lines ("Alex deployed without testing") into blameless contributing factors. |
| SRC-019-EX05 | 4 | Draft five actions from an incident, make each specific, owned, and dated, and rank them. |
| SRC-019-EX06 | 1 | Case: you have been IC for six hours. Plan a handover and explain what to include. |

## Solutions
- **EX01** Declare incident and name IC, assign ops lead, comms lead, scribe; state the goal (restore checkout) and ask for hypotheses with owners and a check-in time.
- **EX02** Each update has status, impact, actions, next update time. The no-news update says so, confirms actions continue, and gives the next time.
- **EX03** Prefer the reversible, bounded option such as rollback or shedding; state the assumption and the signal that shows it worked; ask a second opinion and time-box.
- **EX04** For example: "The deployment process allowed a change without load testing and had no canary analysis; the checklist did not cover pool sizing."
- **EX05** Examples: add canary analysis (owner, date), alert on pool saturation, add a runbook step, practice rollback; rank by prevention and detection value.
- **EX06** Handover: current state, hypotheses and tests, actions in flight, stakeholders and cadence, pending decisions; say it aloud and confirm acceptance.
- Outcome 2 is also covered by the lab and Q04-Q05.

**Workplace evidence:** an incident you led as commander and its postmortem.
