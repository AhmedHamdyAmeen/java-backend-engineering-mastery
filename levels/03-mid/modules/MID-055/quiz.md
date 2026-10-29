# MID-055 · CI/CD advanced — Quiz

Outcomes: O1 build once, promote · O2 quality gates · O3 deployment strategies and rollback · O4 feature flags.

**Q01 (O1)** "Build once, promote everywhere" means: A. Build per environment B. Build on laptops C. Use `latest` D. Deploy the same immutable artifact to every environment
**Q02 (O1)** Environments should differ by: A. The jar contents B. Configuration and secrets C. The Java version D. The source branch
**Q03 (O2)** A good quality gate is: A. Fast, reliable, and owned B. Slow but thorough C. Manual only D. Optional
**Q04 (O2)** Why avoid chasing 100% coverage? A. It is impossible to measure B. Coverage is illegal C. It encourages low-value tests; use a regression threshold instead D. Tests slow the server
**Q05 (O3)** In blue-green deployment you roll back by: A. Rebuilding B. Switching traffic back to the old version C. Restarting the database D. Deleting the pipeline
**Q06 (O3)** A canary release: A. Sends a small share of traffic to the new version first B. Skips tests C. Deploys at night only D. Needs no monitoring
**Q07 (O3)** Safe rollback requires the database schema to be: A. Dropped B. Encrypted C. Compatible with both old and new versions D. Empty
**Q08 (O3)** A readiness probe that always returns 200: A. Speeds up rollout B. Lets a broken version receive traffic C. Improves safety D. Is required
**Q09 (O4)** Feature flags separate: A. Code from tests B. Build from deploy C. Developers from ops D. Deployment from release
**Q10 (O4)** Release flags should be: A. Kept forever B. Hidden from the team C. Removed after rollout D. Duplicated per service

## Answers
Q01 D · Q02 B · Q03 A · Q04 C · Q05 B · Q06 A · Q07 C · Q08 B · Q09 D · Q10 C

## Practical part
Pipeline review (`MID-055-EX01`) plus lab `MID-055-LAB1`. Pass: quiz at least 8/10, a pipeline promoting one artifact through two environments with gates, and a broken release rolled back automatically.
