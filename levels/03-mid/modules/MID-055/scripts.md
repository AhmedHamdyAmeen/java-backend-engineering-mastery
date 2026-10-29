# MID-055 · CI/CD advanced — Lecture scripts

**Video:** 60 min · **Analogy used throughout:** a sealed parcel moving through checkpoints: you pack it once, each checkpoint inspects it, and if one fails the parcel goes back. Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-055-L01 · Build once, promote everywhere (10 min)
**Goal:** deploy the same artifact to every environment.

**Key points**
- Build one immutable image per commit, tagged by version or commit SHA, never `latest`.
- Environments differ only by configuration and secrets, injected at deploy time.
- What passed staging is byte-for-byte what reaches production.
- Rebuilding per environment can produce a different artifact and breaks that guarantee.

**Show:** pipeline: build → image `shop/orders:3f2a9c1` → deploy dev → deploy staging → deploy prod, one image digest throughout.

**Check:** Why not rebuild for production? *(The rebuilt artifact may differ from the one that was tested.)*

---

## MID-055-L02 · Environments and approvals (8 min)
**Goal:** model environments and decide where humans approve.

**Key points**
- Typical path: dev (automatic), staging (automatic, production-like), production (gated).
- Keep staging close to production in shape and configuration; data is synthetic or masked.
- Approvals suit regulated or high-risk changes; routine releases should rely on automated gates.
- Protect production deployment credentials with environment-scoped permissions.

**Show:** pipeline config with an `environment: production` job requiring approval from the owning team.

**Check:** What should differ between environments? *(Configuration and secrets, not the artifact.)*

---

## MID-055-L03 · Quality gates (10 min)
**Goal:** block bad changes automatically.

**Key points**
- Gates: unit and integration tests, contract verification (MID-045), coverage thresholds, static analysis, dependency and image scans (MID-053).
- A gate must be fast, reliable, and clearly owned; flaky gates get ignored.
- Coverage thresholds guard against regressions; do not chase 100%.
- Post-deploy gates: smoke tests and SLO checks (MID-049).

**Show:** stage list with fail conditions: tests pass, no critical CVE, contracts verified, coverage not below baseline.

**Check:** Why do flaky gates hurt? *(People learn to ignore or bypass them.)*

---

## MID-055-L04 · Deployment strategies (12 min)
**Goal:** release with low risk and automatic rollback.

**Key points**
- Rolling: replace pods gradually; needs readiness probes and backward-compatible changes.
- Blue-green: run the new version beside the old, switch traffic at once, switch back to roll back.
- Canary: send a small share of traffic first and compare error rate and latency.
- Automated rollback triggers on failed health checks or SLO burn; the database must be compatible with both versions (expand then contract).
- Tools: Kubernetes Deployments, Argo Rollouts, or Flagger; verify versions before recording.

**Show:** a table comparing the three by speed of rollback, resource cost, and risk exposure.

**Check:** What must be true of the database for a safe rollback? *(The schema must work with both old and new code.)*

---

## MID-055-L05 · Feature flags (8 min)
**Goal:** separate deployment from release.

**Key points**
- Deploy code dark behind a flag; turn it on for staff, a percentage, or a segment.
- Flags allow instant disable without redeploying.
- Types: release flags (short-lived), ops flags (kill switches), experiment flags.
- Cost: every flag doubles code paths; remove release flags after rollout and track them with an owner and date.

**Show:** `if (flags.enabled("new-checkout", user)) {...}` and a flag list with owner and removal date.

**Check:** Name one risk of keeping flags forever. *(Dead code paths, untested combinations, and confusion.)*

---

## MID-055-L06 · Demo: an automated rollback on a failed health check (12 min)
**Goal:** watch a broken release revert with no human action. Prepares MID-055-LAB1.

**Steps**
1. Show the pipeline promoting `orders` image `3f2a9c1` from staging to production with a rolling strategy.
2. Deploy a deliberately broken version whose readiness endpoint fails.
3. **Planned mistake:** the readiness probe returns 200 always, so the broken version takes traffic. Fix: make readiness check real dependencies and add a post-deploy smoke test.
4. Watch the rollout halt and roll back automatically (for example `kubectl rollout undo` triggered by the pipeline, or the rollout tool's analysis).
5. Review the timeline: detection time, rollback time, and the user impact on the dashboard.

**Check:** What detected the bad release? *(The failed readiness probe and post-deploy check, not a person.)*
