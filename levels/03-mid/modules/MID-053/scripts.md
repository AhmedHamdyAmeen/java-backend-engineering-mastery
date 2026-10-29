# MID-053 · Dependency security — Lecture scripts

**Video:** 56 min · **Analogy used throughout:** a restaurant kitchen: the dish is only as safe as the ingredients, so you keep a list of ingredients, check deliveries, and know the supplier. Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-053-L01 · Your code is mostly other people's code (8 min)
**Goal:** see why dependencies are the largest part of the attack surface.

**Key points**
- A Spring Boot service has hundreds of transitive dependencies; most of the running code is not yours.
- A vulnerability is tracked as a CVE with a severity score (CVSS); a library flaw becomes your flaw.
- Examples of impact: remote code execution through a logging or serialization library.
- Defense is a routine, not a one-time scan: inventory, scan, triage, update.

**Show:** `mvn dependency:tree` of `orders`, counting direct versus transitive entries.

**Check:** Who is responsible for a flaw in a transitive library? *(You, because it runs in your service.)*

---

## MID-053-L02 · SCA and triage (10 min)
**Goal:** run software composition analysis (SCA) and decide what to fix first.

**Key points**
- SCA tools (OWASP Dependency-Check, Dependabot, Snyk, Trivy) match your dependencies against vulnerability databases.
- Triage by severity, exploitability (is there a known exploit), reachability (does your code call the vulnerable function), and exposure (internet-facing or not).
- Outcomes per finding: fix (upgrade), mitigate, or accept with a documented reason and an expiry date.
- Automate update pull requests so upgrades stay small.

**Show:** triage table: CVE, library, severity, reachable?, internet-facing?, decision, owner, due date.

**Check:** Name two factors besides severity for triage. *(Exploitability, reachability, or exposure.)*

---

## MID-053-L03 · SBOMs (8 min)
**Goal:** produce a software bill of materials for every build.

**Key points**
- An SBOM lists every component and version in an artifact.
- CycloneDX and SPDX are the common formats; for Maven, the CycloneDX plugin generates one per build.
- When a new CVE appears, search the stored SBOMs to find affected services in minutes.
- Generate SBOMs for the container image too, not only for the code.

**Show:** `mvn org.cyclonedx:cyclonedx-maven-plugin:makeAggregateBom` (verify plugin version before recording) and a short excerpt of the JSON component list.

**Check:** What question does an SBOM answer after a new CVE? *(Which of our artifacts contain that library and version?)*

---

## MID-053-L04 · Image scanning (8 min)
**Goal:** scan container images and keep base images current.

**Key points**
- Images carry operating-system packages as well as Java libraries; scan both (Trivy, Grype, or the registry's scanner).
- Pin the base image by version, ideally by digest, and rebuild regularly to get patches.
- Prefer small, maintained bases (distroless or slim); fewer packages means fewer findings.
- Run as a non-root user; keep build tools out of the final image with a multi-stage build.

**Show:** `trivy image --severity HIGH,CRITICAL --exit-code 1 shop/orders:1.4.2` failing the build on findings.

**Check:** Why pin the base image? *(So builds are reproducible and updates are deliberate, not accidental.)*

---

## MID-053-L05 · Supply-chain security (10 min)
**Goal:** understand attacks on how software is built and delivered, and the controls.

**Key points**
- Risks: typosquatting (a look-alike package name), dependency confusion, compromised maintainers, compromised build systems.
- Controls: lock and verify dependencies, use an internal artifact proxy, least-privilege pipelines, protected branches.
- Sign artifacts and images (for example Sigstore cosign) and keep provenance (who built what, from which commit); SLSA is a framework for levels of assurance. Verify tool details before recording.
- Verify signatures at deploy time with an admission policy.

**Show:** pipeline diagram: source → build (provenance) → sign → registry → cluster admission check.

**Check:** What does a signature on an image prove? *(That a trusted identity produced it and it was not changed since.)*

---

## MID-053-L06 · Demo: triaging a critical CVE (12 min)
**Goal:** triage and fix a critical finding in a Shop service. Prepares MID-053-LAB1.

**Steps**
1. A scan flags a critical CVE in a library inside `orders`. Open the SBOM to confirm the component and the services affected.
2. Check reachability and exposure: is the vulnerable class used, is the endpoint public.
3. **Planned mistake:** suppress the finding as "noise" without reading it. Fix: read the advisory; here the code path is reachable, so it is a real risk.
4. Upgrade the library (or its parent BOM), run tests and the contract tests, and rebuild the image.
5. Confirm the scan is clean and record the decision; document any exception with an expiry date.

**Check:** When may you accept a finding? *(When it is not reachable or mitigated, recorded with a reason, an owner, and an expiry date.)*
