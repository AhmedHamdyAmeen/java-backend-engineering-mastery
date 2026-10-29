# SRB-014 · Engineering metrics — Exercises and lab

## Lab
### SRB-014-LAB1 · Program dashboard
**Outcomes:** 1–4 · **Time:** ~3 h
1. Define the four DORA metrics for the four FulfillCo teams (what counts as a deployment and a failure) and compute them from pipeline and incident data.
2. Add reliability indicators: SLO attainment, error budget, incident rate.
3. Build the dashboard view with context notes, grouped at team and program level.
4. Choose one trend, write a hypothesis, run one improvement experiment, and record the result.
**Acceptance:** experiment hypothesis, measure, and result recorded.

## Exercises (assessment: metrics narrative review)
| ID | Outcome | Task |
| --- | --- | --- |
| SRB-014-EX01 | 1 | Given a sample pipeline export, compute lead time (median and 85th percentile) and deployment frequency for one team. |
| SRB-014-EX02 | 1 | Define "deployment" and "failure" for the program in one paragraph each, and explain a boundary case. |
| SRB-014-EX03 | 2 | Case: deployment frequency doubled and SLO attainment fell. Write a three-sentence reading and a next step. |
| SRB-014-EX04 | 3 | A director wants a team league table by deployment count. Write the reply with an alternative. |
| SRB-014-EX05 | 3 | List three ways each of lead time and change failure rate could be gamed, with counter-measures. |
| SRB-014-EX06 | 4 | Present a rising lead-time trend as hypothesis, experiment, measure, and decision rule. |
| SRB-014-EX07 | 4 | Write the metrics narrative (half a page) for a monthly program review, including one uncomfortable finding. |

## Solutions
- **EX01** Lead time per change is merge-to-production time; report median and 85th percentile; frequency is deployments per week.
- **EX02** Deployment: a production release of a change, excluding config-only reruns unless counted consistently. Failure: a release needing rollback, hotfix, or causing an incident. State the boundary decision (for example flag flips).
- **EX03** Speed rose at the cost of reliability; likely smaller batches without adequate tests or review. Next step: look at the failing changes, tighten gates, and track the pair together.
- **EX04** Reply that team contexts differ and counts invite gaming; offer trend per team against its own baseline plus reliability indicators.
- **EX05** Lead time: splitting work, starting the clock late. Failure rate: not logging failures, calling them "known issues". Counter: companions, audits of definitions, trend not target.
- **EX06** Hypothesis: reviews wait for hours; change: review rotation and a 4-hour response agreement; measure review wait median; success if it drops by a set amount in four weeks.
- **EX07** Narrative: what moved, probable cause, what we tried, what we ask for; be honest about missing data and about a metric that looks worse.
- Outcome 2 is also covered by the lab dashboard; outcome 3 by Q05-Q07.

**Workplace evidence:** an improvement you drove using delivery or reliability metrics.
