# MID-053 · Dependency security — Quiz

Outcomes: O1 SCA and triage · O2 SBOM · O3 image scanning · O4 supply-chain risks and controls.

**Q01 (O1)** A CVE is: A. A build tool B. A test type C. A Java version D. A public identifier for a known vulnerability
**Q02 (O1)** Reachability asks: A. Whether your code can reach the vulnerable function B. Whether the server is online C. How many users exist D. If the library is popular
**Q03 (O1)** A finding may be accepted when: A. It is boring B. It is old C. It is unreachable or mitigated, with a reason, owner, and expiry D. The build is late
**Q04 (O2)** The main use of an SBOM after a new CVE is: A. Finding which artifacts contain the library B. Speeding up tests C. Compressing images D. Signing commits
**Q05 (O2)** CycloneDX is: A. A database B. An SBOM format C. A cloud provider D. A test framework
**Q06 (O3)** Pinning the base image gives: A. Faster code B. Smaller heap C. Reproducible builds with deliberate updates D. Free licenses
**Q07 (O3)** Image scans should cover: A. Only your jar B. Only Dockerfiles C. Only comments D. OS packages and Java libraries
**Q08 (O4)** Typosquatting means: A. Slow typing B. A look-alike package name carrying malware C. Wrong indentation D. Duplicate tests
**Q09 (O4)** Signing an image lets the cluster: A. Run it faster B. Skip scanning C. Verify who built it and that it is unchanged D. Use less memory
**Q10 (O4)** Which practice supports build provenance? A. Recording who built what from which commit B. Building on laptops C. Sharing the pipeline admin password D. Skipping tests

## Answers
Q01 D · Q02 A · Q03 C · Q04 A · Q05 B · Q06 C · Q07 D · Q08 B · Q09 C · Q10 A

## Practical part
Triage exercise (`MID-053-EX01`) plus lab `MID-053-LAB1`. Pass: quiz at least 8/10, a correct triage with reasons, and a planted vulnerable dependency failing the build.
