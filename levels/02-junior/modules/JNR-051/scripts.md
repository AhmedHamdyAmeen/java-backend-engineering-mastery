# JNR-051 · CI/CD introduction — Lecture scripts

**Video:** 69 min · **Analogy used throughout:** a factory conveyor belt with quality gates before the goods reach the loading dock.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-051-L01 · CI, CD, and CD (8 min)
**Goal:** tell the three terms apart.

**Key points**
- Continuous Integration (CI): every change is merged often and built and tested automatically.
- Continuous Delivery: every passing change is ready to release; a human presses the button.
- Continuous Deployment: every passing change goes to production automatically.
- The same letters mean two things (delivery and deployment); ask which one a team means.
- The goal is small, frequent, low-risk changes with fast feedback.

**Show:** a pipeline line: commit, build, test, package, (approval), deploy, with the boundary of each term marked.

**Check:** What is the difference between delivery and deployment? *(Delivery waits for a human approval; deployment releases automatically.)*

---

## JNR-051-L02 · GitHub Actions anatomy (12 min)
**Goal:** read and write a workflow file.

**Key points**
- Workflows are YAML files in `.github/workflows/`.
- `on:` sets triggers (push, pull request, tags, manual).
- A workflow has `jobs`; a job runs on a runner (`runs-on: ubuntu-latest`) and has `steps`.
- A step is either `uses:` (a reusable action) or `run:` (a shell command).
- Secrets are stored in repository settings and read as `${{ secrets.NAME }}`; they are masked in logs.
- Pin action versions; verify current versions before recording.

**Show**
```yaml
name: ci
on: [pull_request]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: echo "hello"
```

**Check:** Where do workflow files live? *(`.github/workflows/`.)*

---

## JNR-051-L03 · Build and test pipeline (10 min)
**Goal:** build, test, and cache in a workflow.

**Key points**
- Set up Java with `actions/setup-java` (distribution and version) and enable the Maven or Gradle cache.
- Run `./mvnw verify` so unit and integration tests run; GitHub's Ubuntu runners include Docker, so Testcontainers works.
- Fail the build if tests fail; also check that tests actually ran (report in the logs or upload test reports).
- Upload test reports as artifacts for debugging.
- Keep the pipeline fast; cache dependencies, not build output you cannot trust.

**Show**
```yaml
- uses: actions/setup-java@v4
  with: { distribution: temurin, java-version: '21', cache: maven }
- run: ./mvnw -B verify
```

**Check:** Why upload test reports? *(To read failures without re-running locally.)*

---

## JNR-051-L04 · Artifacts and image publishing (10 min)
**Goal:** publish the JAR and a container image with version tags.

**Key points**
- Artifacts are build outputs (JAR, test reports); `actions/upload-artifact` keeps them with the run.
- Images go to a registry such as GitHub Container Registry (`ghcr.io`).
- Log in with the built-in `GITHUB_TOKEN` (set `permissions: packages: write`) instead of a personal password.
- Tag images with the commit SHA and a version, not only `latest`.
- Build once and promote the same image through environments.

**Show**
```yaml
- uses: docker/login-action@v3
  with: { registry: ghcr.io, username: ${{ github.actor }}, password: ${{ secrets.GITHUB_TOKEN }} }
- uses: docker/build-push-action@v6
  with: { push: true, tags: "ghcr.io/${{ github.repository }}:${{ github.sha }}" }
```

**Check:** Why tag with the commit SHA? *(You can trace and roll back to the exact build.)*

---

## JNR-051-L05 · Branch protection (5 min)
**Goal:** stop broken code reaching `main`.

**Key points**
- Branch protection rules (or rulesets) apply to `main`.
- Require pull requests, at least one review, and passing status checks before merge.
- Block direct pushes and force pushes.
- The required check names must match the job names.
- Rules apply to everyone, including admins if configured.

**Show:** the repository settings page with "Require status checks to pass" ticked and the `build` check selected.

**Check:** What stops a PR with a failing test from merging? *(A required status check.)*

---

## JNR-051-L06 · Demo: building the Shop pipeline in GitHub Actions (12 min)
**Goal:** a PR workflow that builds and tests Shop. Prepares `JNR-051-LAB1`.

**Steps**
1. Create `.github/workflows/ci.yml` triggered by `pull_request`.
2. Add checkout, setup-java with cache, and `./mvnw -B verify`.
3. Push a branch, open a PR, and watch the run.
4. Make a test fail on purpose and see the red check.
5. **Planned mistake:** a build that passes with zero tests run because tests were skipped with `-DskipTests`; remove the flag and confirm the test count in the log.
6. Upload the test report as an artifact.

---

## JNR-051-L07 · Demo: publishing a tagged image on merge (12 min)
**Goal:** publish an image to the registry when `main` changes. Prepares `JNR-051-LAB1`.

**Steps**
1. Add a second workflow (or job) triggered by `push` to `main`.
2. Log in to `ghcr.io` with `GITHUB_TOKEN` and grant `packages: write`.
3. Build and push `shop:<sha>` and `shop:latest` or a version tag.
4. Enable branch protection with the `build` check required.
5. **Planned mistake:** print an environment variable that contains a secret with `echo`; show it masked, then explain why you still never print secrets.
6. Open a PR with a failing test and show it cannot merge.
