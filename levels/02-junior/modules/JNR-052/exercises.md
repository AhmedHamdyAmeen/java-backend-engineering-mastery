# JNR-052 · Deployment basics — Exercises and lab

## Lab
### JNR-052-LAB1 · Shop goes live
**Outcomes:** 1–4 · **Time:** ~3 h
Deploy from the pipeline to a public URL with a managed database, configured through environment variables, with probes and graceful shutdown; perform and document a rollback.
**Acceptance:** deployed instance reachable; rollback under 5 minutes.

## Exercises (assessment: deployment walkthrough)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-052-EX01 | 1 | Compare VM, PaaS, and managed containers for Shop on cost, control, and effort; recommend one. |
| JNR-052-EX02 | 1 | Write the numbered steps from "merge to main" to "live URL". |
| JNR-052-EX03 | 2 | Convert a `application-prod.yml` with a database password into environment-variable configuration. |
| JNR-052-EX04 | 3 | Enable liveness and readiness probes and show both endpoints' responses. |
| JNR-052-EX05 | 3 | Explain why liveness should not call the database, using a database-outage scenario. |
| JNR-052-EX06 | 4 | Enable graceful shutdown and prove an in-flight request finishes during a stop. |
| JNR-052-EX07 | 4 | Write a five-step rollback runbook with expected timing. |

## Solutions
- **EX01** For example: VM is cheapest but needs patching and setup; PaaS is fastest to start; recommend a PaaS for a first deployment. Verify current prices.
- **EX02** Merge, CI passes, image pushed with SHA tag, deploy job updates the service, health check passes, URL serves traffic.
- **EX03** Remove the password; set `SPRING_DATASOURCE_PASSWORD` in the platform secret store; keep only non-secret defaults in the file.
- **EX04** `management.endpoint.health.probes.enabled=true`; `/actuator/health/liveness` and `/actuator/health/readiness` return `{"status":"UP"}` (verify for your Boot version).
- **EX05** If the database goes down, liveness failing restarts every instance, causing restart loops and extra load; readiness failing only removes traffic until it recovers.
- **EX06** `server.shutdown=graceful` and a shutdown timeout; start a slow request, send SIGTERM, and see the response complete before exit.
- **EX07** Identify the bad release; find the previous tag; redeploy it; verify health; record the time; communicate the result.
- Common mistakes (credentials in the image) are checked in the walkthrough assessment.
