# MID-050 · Incident handling — Exercises and lab

## Lab
### MID-050-LAB1 · Game day
**Outcomes:** 1–4 · **Time:** ~2.5 h
The instructor breaks Shop Platform during a load test. Act as incident responder: triage, mitigate, keep a timeline, post status updates, then write the postmortem.
**Acceptance:** mitigation within the time box; postmortem reviewed.

## Exercises (assessment: the MID graduation gate's incident simulation uses this format)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-050-EX01 | 1 | Given three descriptions of failures, assign a severity and justify it. |
| MID-050-EX02 | 1 | Write a severity table for Shop with examples and who is paged. |
| MID-050-EX03 | 2 | For five situations (bad deploy, flag, traffic spike, dependency down, full disk), choose the first mitigation. |
| MID-050-EX04 | 3 | Fill in a timeline and write two status updates from a chat log. |
| MID-050-EX05 | 4 | Rewrite a postmortem sentence that blames a person into a blameless statement of contributing factors. |
| MID-050-EX06 | 4 | Write three action items with owners, due dates, and a measurable outcome. |
| MID-050-EX07 | 1–4 | Run a table-top incident from an alert text and produce triage notes, a timeline, and a postmortem outline. |

## Solutions
- **EX01** Judge by impact (users, revenue path), spread, and workaround; checkout down for all is Sev1.
- **EX02** Sev1 / Sev2 / Sev3 rows with response expectation (page now, page in hours, ticket).
- **EX03** Bad deploy: roll back; flag: switch off; spike: scale or rate-limit; dependency: fail over or degrade; full disk: free space and restart, then fix retention.
- **EX04** Timeline lines have time, actor, action; updates state impact, known, doing, next update time.
- **EX05** "Ana deployed a bad config" becomes "The pipeline allowed a config without validation; no canary caught it."
- **EX06** Example: add config validation in CI (owner: platform, 2 weeks, validation fails the build on bad value).
- **EX07** Check mitigation comes before root cause in the notes.
