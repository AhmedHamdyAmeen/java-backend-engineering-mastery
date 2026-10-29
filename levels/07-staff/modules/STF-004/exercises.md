# STF-004 · Platform strategy — Exercises and lab

## Lab
### STF-004-LAB1 · Platform 2.0 platform strategy
**Outcomes:** 1–4 · **Time:** ~3.5 h
1. Interview role-played teams and map the new-service-to-production journey with timings.
2. List toil items with total hours and teams affected.
3. Define platform scope: what is in and what is out, and the paved road with escape hatches.
4. Write the capability roadmap with build, assemble, or buy choices (verify versions before recording).
5. Propose the team size, product ownership, funding, and success measures; defend to role-played leadership.
**Acceptance:** each capability is backed by toil or delay data from at least three teams.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| STF-004-EX01 | 1 | Given toil data for six candidate capabilities, rank them and state which two you leave out of scope, with reasons. |
| STF-004-EX02 | 1 | A platform team wants to build a custom container scheduler. Write a one-page challenge using journey and toil evidence. |
| STF-004-EX03 | 2 | Design a paved road for "new service" with three escape hatches and the extra responsibilities each carries. |
| STF-004-EX04 | 3 | Write a product brief for the shared pipeline: users, scope, support model, and four measures. |
| STF-004-EX05 | 3 | Compare build, assemble, and buy for a service catalog; recommend with criteria and cost drivers. |
| STF-004-EX06 | 4 | Draft a business case for a six-person platform team serving 160 engineers, with assumptions stated. |

## Solutions
- **EX01** Rank by hours x teams / effort; leave out items affecting fewer than three teams or with a good existing option.
- **EX02** Show no journey step needs a custom scheduler; the delays are in pipelines and setup; recommend a managed option.
- **EX03** Road: template, pipeline, observability, security defaults. Hatches: custom runtime, other datastore, special network; each adds on-call, security review, and upgrades owned by the team.
- **EX04** Users: product teams; scope: build, test, deploy; support: channel with response targets; measures: adoption, lead time, satisfaction, platform availability.
- **EX05** Criteria: integration, operating cost, skills, lock-in; likely assemble or buy, build only the glue. Verify current product versions before recording.
- **EX06** Cost of team versus hours saved (for example 40 min a week x 160 engineers) plus incidents avoided; state assumptions and payback; include support load growth.

Outcome coverage: all four covered by exercises and lab.

**Workplace evidence:** a platform capability you shaped and its adoption numbers.
