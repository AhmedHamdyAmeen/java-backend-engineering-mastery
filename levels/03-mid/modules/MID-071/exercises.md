# MID-071 · AI application threats — Exercises and lab

## Lab
### MID-071-LAB1 · Attack the assistant
**Outcomes:** 1–5 · **Time:** ~3 h
Write automated tests for: direct injection, indirect injection (a planted help article), reading another customer's data through tools, exfiltration through a generated link, and quota exhaustion. Run them, fix what fails, and update the threat model.
**Acceptance:** all attack tests run in CI and pass after the fixes; threat model updated.

## Exercises (assessment: threat-model the assistant)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-071-EX01 | 1 | Map five OWASP LLM categories to concrete threats against the order-support assistant. |
| MID-071-EX02 | 2 | Write a planted help article and a test that proves the assistant does not follow it. |
| MID-071-EX03 | 2 | Explain why the system-prompt defense alone fails and list three stronger layers. |
| MID-071-EX04 | 3 | The assistant renders markdown. Design the control that stops data leaking through image and link URLs. |
| MID-071-EX05 | 4 | Define quotas and loop limits for the assistant, with values and the alert on breach. |
| MID-071-EX06 | 5 | Add three assistant threats to the STRIDE table with mitigations and the test that covers each. |

## Solutions
- **EX01** Example: prompt injection (planted article), sensitive disclosure (other customers' orders), improper output handling (HTML in answers), excessive agency (refund tool), unbounded consumption (long loops).
- **EX02** The article instructs a refund; the test asks about the order and asserts no refund request was created and no foreign link is in the answer.
- **EX03** Models can be talked out of rules. Layers: untrusted-data labeling, tool restriction and approval, output validation, domain allowlist, least-privilege tokens.
- **EX04** Allowlist of image and link domains, strip other URLs, no auto-loading of remote images, escape output.
- **EX05** Example: 4 000 input characters, 6 steps, 30 s, 50 000 tokens per user per day; alert when daily spend exceeds the budget or one user exceeds 5x the median.
- **EX06** Each row: element, STRIDE letter, threat, mitigation, test ID; the tests are those from the lab.

**Outcome 1** is also covered by quiz Q01–Q03; outcome 5 by the lab criterion "threat model updated".
