# SRC-022 · Operating AI in production — Exercises and lab

## Lab
### SRC-022-LAB1 · Run the assistant
**Outcomes:** 1–4 · **Time:** ~4 h
Put the order-support assistant's prompts and model choice under versioned configuration. Add an evaluation gate and a canary. Rehearse a bad-output incident with a kill switch and a human review queue, then write the postmortem.
**Acceptance:** a seeded regression is blocked by the gate; the kill switch disables the feature in under one minute; postmortem written.

## Exercises (assessment: incident simulation on a misbehaving AI feature)
| ID | Outcome | Task |
| --- | --- | --- |
| SRC-022-EX01 | 1 | Design the configuration bundle for the assistant: what is versioned, what is pinned, and what is logged per answer. |
| SRC-022-EX02 | 1 | Case: the team edits the prompt in a production console. Write the review comment and the process replacing it. |
| SRC-022-EX03 | 2 | Specify an evaluation gate: case categories, per-category thresholds, hard safety cases, and promote/abort rules for a canary. |
| SRC-022-EX04 | 3 | Case: answers worsen in November with no deploy. List four hypotheses and the signal that tests each. |
| SRC-022-EX05 | 4 | Write the kill-switch design and a runbook for "assistant gave wrong refund advice to many customers". |
| SRC-022-EX06 | 4 | Review an incident timeline where the fix was a prompt warning not to leak data. Explain why it is insufficient and propose the real control. |

## Solutions
- **EX01** Version: prompt, model id (pinned), parameters, retrieval index and settings, eval set. Log: bundle ID, model version, retrieved source IDs, request ID.
- **EX02** Direct edits skip review, tests and rollback. Replace with config in version control, PR review, eval gate, staged rollout, audit log.
- **EX03** Categories (refunds, shipping, account); overall and per-category thresholds relative to baseline; zero tolerance on leakage and unsafe cases; promote after bake with stable escalation and thumbs-down rates.
- **EX04** Model updated by provider (compare pinned version, rerun eval), knowledge data changed (index diff), seasonal topics (topic clusters), new user behavior (sampled grading). Each tested by scheduled eval or sampling.
- **EX05** Flag checked on each request, falling back to a safe path such as handing off to humans; tested regularly and timed under one minute. Runbook: detect, kill, contain, identify affected customers, communicate, root cause, add eval case, postmortem.
- **EX06** Prompts are advisory and can be bypassed; enforce authorization in the retrieval and tool layer using the caller's identity, and add cross-customer eval cases.
- Outcome 2 is also covered by the lab gate and Q04-Q05.

**Workplace evidence:** a release process or incident you ran for an AI feature.
