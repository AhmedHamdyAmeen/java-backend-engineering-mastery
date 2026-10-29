# MID-053 · Dependency security — Exercises and lab

## Lab
### MID-053-LAB1 · Secure builds
**Outcomes:** 1–4 · **Time:** ~2 h
Add SCA, a CycloneDX SBOM, and an image scan to every Shop pipeline. Add a severity gate (fail on critical/high unless an exception exists) and an exceptions file with reason, owner, and expiry. Pin base images. Plant one vulnerable dependency to prove the gate.
**Acceptance:** a planted vulnerable dependency fails the build; SBOMs are stored as build artifacts.

## Exercises (assessment: triage exercise)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-053-EX01 | 1 | Triage five given findings: decide fix, mitigate, or accept for each, with reasons. |
| MID-053-EX02 | 1 | Explain why a critical CVE in a test-scope library may rank below a medium one in a public endpoint's code path. |
| MID-053-EX03 | 2 | Generate a CycloneDX SBOM for `orders` and find which version of Jackson it contains. |
| MID-053-EX04 | 3 | Scan the `orders` image, list the top findings, and reduce them by changing the base image. |
| MID-053-EX05 | 4 | Describe typosquatting and name two controls against it. |
| MID-053-EX06 | 4 | Draw a pipeline that signs the image and a cluster policy that rejects unsigned images. |

## Solutions
- **EX01** Fix when reachable and exposed; mitigate (config, WAF, disable feature) when no fix exists; accept only when unreachable, with an expiry date and owner.
- **EX02** Test-scope code is not shipped, while the medium finding is reachable by an attacker; exploitability and exposure matter beyond severity.
- **EX03** Plugin goal `makeAggregateBom`; search the JSON `components` for `jackson-databind` and read its `version`.
- **EX04** Example: `trivy image`, then switch to a slim or distroless maintained base, rebuild, and re-scan; findings drop because fewer OS packages are present.
- **EX05** A package with a name close to a popular one that contains malware. Controls: lock files and checksum verification, an internal proxy with an allowlist, review new dependencies.
- **EX06** Build → push → cosign sign (keyless or key-based) → admission policy verifies the signature before a pod starts (verify tool names before use).

**Outcome 2** is also covered by the lab criterion "SBOMs stored as build artifacts" and quiz Q04.
