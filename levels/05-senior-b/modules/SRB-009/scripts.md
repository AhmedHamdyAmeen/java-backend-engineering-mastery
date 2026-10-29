# SRB-009 · Service mesh — Lecture scripts

**Video:** 90 min · **Running case:** The FulfillCo integration (Shop Platform acquires FulfillCo, a 10-year-old Java modular monolith on one PostgreSQL database; four teams integrate in real time and extract capabilities without stopping either business).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRB-009-L01 · What a mesh does (10 min)
**Goal:** list what a service mesh adds to service-to-service traffic.

**Key points**
- A mesh moves networking concerns out of application code into infrastructure.
- Four groups: mutual TLS, traffic management, telemetry, policy.
- It works uniformly across languages, which helps with mixed stacks like FulfillCo plus Shop.
- It is not a fix for unclear ownership or bad APIs.

**Show:** diagram: service A and B with proxies; control plane distributes certificates and routing rules; metrics flow to a telemetry backend.

**Check:** Name the four mesh capability groups. *(mTLS, traffic management, telemetry, policy.)*

---

## SRB-009-L02 · Mesh architectures (10 min)
**Goal:** compare sidecar and sidecar-less meshes.

**Key points**
- Sidecar: a proxy next to every pod; strong isolation, extra resources and startup coupling.
- Sidecar-less (node-level or ambient style): shared proxies per node, less overhead, different trade-offs.
- The control plane is a new critical component.
- Features and maturity change fast: verify current state before recording.

**Show:** a two-column comparison: resource cost, upgrade process, failure blast radius, feature set.

**Check:** What is a cost of sidecars? *(Extra CPU, memory, and operational coupling per pod.)*

---

## SRB-009-L03 · mTLS and workload identity (12 min)
**Goal:** explain how services prove identity to each other.

**Key points**
- Each workload gets a short-lived certificate tied to its identity (not an IP).
- mTLS encrypts and authenticates both sides.
- Rotation is automatic; expiry failures are a classic outage cause.
- Authorization rules use identity: only checkout may call payments.

**Show:** a policy outline: strict mTLS in namespace shop; allow rule from identity checkout to payments on POST /charge; deny by default.

**Check:** Why identity not IP? *(Pods move and IPs are reused.)*

---

## SRB-009-L04 · Traffic management (10 min)
**Goal:** split, retry, and time out traffic centrally.

**Key points**
- Weighted routing sends a small share to a new version for a canary.
- Timeouts, retries, and circuit breaking can be set in the mesh.
- Duplicate retries in mesh and code multiply load.
- Define who owns retry policy.

**Show:** a route rule outline: 95% to v1, 5% to v2; per-route timeout 2s; retries 1 with a budget.

**Check:** What problem arises with duplicate retries? *(Retry amplification under failure.)*

---

## SRB-009-L05 · Policy enforcement (8 min)
**Goal:** apply organization rules in the mesh.

**Key points**
- Authorization, rate limits, and egress control at the proxy.
- Policies are code in a repository with review.
- Test policies in audit mode before enforcement.
- Do not hide business rules in mesh policy.

**Show:** a policy lifecycle: write, audit mode, observe denies, enforce.

**Check:** Why use audit mode first? *(To see what would be denied before blocking.)*

---

## SRB-009-L06 · The cost of a mesh (10 min)
**Goal:** count what a mesh costs before adopting it.

**Key points**
- Costs: latency per hop, CPU and memory, upgrade effort, debugging a new layer, on-call skills.
- Alternatives: libraries, an API gateway, plain TLS with a cert manager.
- Adopt for a named benefit, measured in a trial.
- Reject when the problem is process, not technology.

**Show:** a decision matrix: needs (mTLS everywhere, canary, polyglot telemetry) versus options (mesh, libraries, gateway) with cost estimates.

**Check:** When reject a mesh? *(When the problem is process rather than missing technology.)*

---

## SRB-009-L07 · Demo: canary traffic split and mTLS with a mesh (15 min)
**Goal:** enable mTLS and a canary on two services.

**Steps**
1. Install the mesh in a test cluster (verify version before recording) and inject into two services.
2. Enable permissive then strict mTLS and verify with a test.
3. Create a 90/10 traffic split to a new version and watch metrics.
4. **Planned mistake:** enable strict mTLS before a non-meshed client was onboarded, breaking its calls; fix by moving to permissive first and onboarding clients.
5. Roll the canary to 50% then 100% or roll back.

Prepares SRB-009-LAB1.

---

## SRB-009-L08 · Demo: measuring a mesh's latency and operational overhead (15 min)
**Goal:** collect evidence for the adopt or reject ADR.

**Steps**
1. Baseline latency and resource use without the mesh.
2. Repeat with the mesh enabled under the same load.
3. Record operational effort: install, upgrade, debugging a failure.
4. **Planned mistake:** compare a warm mesh to a cold baseline; fix by warming both and repeating runs.
5. Summarize numbers and list the benefits delivered.

Prepares SRB-009-LAB1.

---
