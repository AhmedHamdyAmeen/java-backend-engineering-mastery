# JNR-051 · CI/CD introduction — Quiz

Outcomes: O1 CI/CD concepts · O2 workflows · O3 artifacts and images · O4 branch protection.

**Q01 (O1)** Continuous deployment means: A. A human approves each release B. Builds only C. Every passing change goes to production automatically D. Nightly manual builds
**Q02 (O1)** Continuous integration mainly: A. Merges and tests changes often B. Deploys weekly C. Replaces code review D. Removes tests
**Q03 (O2)** Workflow files live in: A. `/etc/workflows` B. `.github/workflows/` C. `src/main` D. `.git/hooks`
**Q04 (O2)** A step that uses a reusable action starts with: A. `run:` B. `on:` C. `uses:` D. `needs:`
**Q05 (O2)** Why cache dependencies? A. Hide errors B. Skip tests C. Increase image size D. Speed up builds
**Q06 (O2)** A pipeline that passes with zero tests run is: A. Fine B. Dangerous C. Faster and better D. Required
**Q07 (O3)** A safe tag for traceability is: A. `latest` only B. `final` C. The commit SHA D. `new`
**Q08 (O3)** To push to GHCR from Actions use: A. Your personal password B. `GITHUB_TOKEN` with `packages: write` C. No login D. A shared password in the repo
**Q09 (O4)** To stop failing PRs from merging: A. Ask nicely B. Delete the tests C. Disable CI D. Require the status check on `main`
**Q10 (O4)** Branch protection can also: A. Block direct pushes to `main` B. Compile code C. Start Docker D. Write tests

## Answers
Q01 C · Q02 A · Q03 B · Q04 C · Q05 D · Q06 B · Q07 C · Q08 B · Q09 D · Q10 A

## Practical part
Six exercises `JNR-051-EX01` to `EX06` plus the lab; for the assessment, fix a broken workflow. Pass: quiz 8/10, at least five exercises correct, and a failing-test PR blocked from merging.
