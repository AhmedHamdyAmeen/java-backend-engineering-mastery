# JNR-054 · Troubleshooting — Exercises and lab

## Lab
### JNR-054-LAB1 · Break the Shop
**Outcomes:** 1–4 · **Time:** ~3 h
The instructor injects three faults into a deployed Shop (bad config, data-dependent bug, dependency change). Diagnose each with only logs and the codebase.
**Acceptance:** root cause, fix, and regression test for each.

## Exercises (assessment: live troubleshooting session)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-054-EX01 | 1 | From the report "checkout sometimes fails", write the steps and data needed to reproduce it reliably. |
| JNR-054-EX02 | 1 | Reproduce a given bug locally in a failing test before looking for the fix. |
| JNR-054-EX03 | 2 | Given a 30-line stack trace with three "Caused by" sections, name the root cause and the first line in your own code. |
| JNR-054-EX04 | 2 | Using logs, find the first error for request id `abc123` and explain the sequence. |
| JNR-054-EX05 | 3 | Build a comparison table of local versus production for config, data, and versions and mark the likely culprit for a given symptom. |
| JNR-054-EX06 | 4 | Write a bug report with symptom, root cause, fix, and regression test for a bug of your choice. |
| JNR-054-EX07 | 4 | Rewrite a poor help request ("it doesn't work, please help") into a good one. |

## Solutions
- **EX01** List the user, data (for example an order without coupon), sequence of calls, and environment; confirm it fails every time.
- **EX02** The test builds the data from the report, asserts the expected behavior, and fails for the same reason as the report.
- **EX03** The last "Caused by" is the root cause; the first frame with your package (for example `com.shop...`) shows where.
- **EX04** Filter logs by the request id; read the lines in time order up to the first `ERROR`.
- **EX05** For example a missing environment variable in production explains a startup failure; a null column in production data explains a data-dependent failure.
- **EX06** Use the template: Symptom, Steps, Root cause, Fix, Regression test, Prevention.
- **EX07** "Order API returns 500 for orders without a coupon on staging; works locally. Error and logs attached. I checked Java and env vars. Next I will compare data."
- Common mistakes (fixing without reproducing, changing several things at once) are assessed in the live session.
