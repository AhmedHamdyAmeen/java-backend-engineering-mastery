# SRC-009 · Failure-mode analysis — Lecture scripts

**Video:** 96 min · **Running case:** *Order Processing at 10×* — Shop Platform's order subsystem must handle a 10× growth forecast, a 99.95% availability commitment, and a 15-minute recovery objective.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRC-009-L01 · How real systems fail (12 min)
**Goal:** learn the common failure patterns before analyzing your own system.

**Key points**
- Most outages come from change (deploys, config), capacity, dependencies, and operations errors, not exotic hardware faults.
- Failures cascade: a slow dependency exhausts threads, which makes callers slow, and so on.
- Partial failure and slowness are harder than clean crashes.
- Gray failures: components look healthy but serve wrong or slow results.

**Show:** a timeline of a cascading failure from a slow payment provider to checkout thread exhaustion.

**Check:** What is usually harder to handle: a crash or a slow dependency? *(Slow dependency; it ties up resources and spreads.)*

---

## SRC-009-L02 · Dependency mapping (10 min)
**Goal:** list every dependency, including the hidden ones.

**Key points**
- Visible: services, databases, brokers, third-party APIs.
- Hidden: DNS, identity provider, certificates, configuration service, container registry, shared clusters, time sync, secrets store.
- Map by tracing a request end to end and by reading deployment config.
- For each dependency note: critical or optional, timeout, fallback.

**Show:** a dependency graph for checkout with hidden nodes highlighted: DNS, auth provider, config server.

**Check:** Name two hidden dependencies. *(For example DNS and the identity provider.)*

---

## SRC-009-L03 · Failure domains and blast radius (10 min)
**Goal:** limit how much one fault can break.

**Key points**
- A failure domain is a set of things that fail together: a node, an AZ, a region, a shared cluster, a team's release.
- Blast radius: how many users or features a fault affects.
- Reduce it with isolation: bulkheads, cells, separate pools, staged rollouts.
- Shared components make bigger domains than diagrams suggest.

**Show:** a diagram where two services share a database cluster, enlarging their failure domain.

**Check:** What is blast radius? *(How much of the system or how many users one fault affects.)*

---

## SRC-009-L04 · FMEA for software (14 min)
**Goal:** run a structured failure-mode and effects analysis.

**Key points**
- For each component list failure modes, effects, causes, existing controls.
- Rate likelihood, impact, and detectability (for example 1-5 each); risk priority is their product.
- Detectability matters: failures you cannot see are the most dangerous.
- Output: ranked list and actions (mitigate, detect, accept).

**Show:** a table: component, failure mode, effect, L, I, D, score, action.

**Check:** Why include detection in the rating? *(An undetected failure lasts longer and does more damage.)*

---

## SRC-009-L05 · Graceful degradation (10 min)
**Goal:** keep the core journey working when parts fail.

**Key points**
- Rank features: core (checkout) versus optional (recommendations, reviews).
- Fallbacks: cached data, default values, queueing, disabling features, clear "temporarily unavailable" states.
- Never degrade by silently corrupting or dropping data; degrade visibly.
- Test the degraded modes; unused fallbacks rot.

**Show:** a table: dependency fails, user sees, system does, data safety.

**Check:** What must degradation never do? *(Silently corrupt or lose data.)*

---

## SRC-009-L06 · From analysis to experiments (10 min)
**Goal:** convert findings into safe failure-injection experiments.

**Key points**
- Write a hypothesis: "if X fails, then Y still works within Z".
- Start small and in test or staging; define blast radius, stop conditions, and observation.
- Typical injections: kill a pod, add latency, block a dependency, expire a certificate (use tools verified for your stack).
- Fix findings and rerun.

**Show:** an experiment sheet: hypothesis, injection, metrics, abort condition, result.

**Check:** What does an experiment need before it starts? *(A hypothesis, a limited blast radius, and stop conditions.)*

---

## SRC-009-L07 · Demo: FMEA of the checkout path (15 min)
**Goal:** analyze checkout for failure modes; prepares SRC-009-LAB1.

**Steps**
1. Trace the checkout path and list components and dependencies.
2. List failure modes for each: down, slow, wrong, partial.
3. **Planned mistake:** only analyze services we own. Fix: add the payment provider, DNS, identity, and the shared database cluster.
4. Rate L, I, D and rank.
5. Design degradation for the top three.
6. Turn the top findings into experiments.

---

## SRC-009-L08 · Demo: a hidden dependency found by failure injection (15 min)
**Goal:** show an experiment exposing something the map missed.

**Steps**
1. Hypothesis: if the recommendation service is down, checkout still works.
2. Inject the failure in staging.
3. Observe checkout failing; trace shows a synchronous config lookup that goes through the same service.
4. **Planned mistake:** declare the experiment a failure and stop. Fix: it succeeded, it found a weakness; record it.
5. Fix by caching config locally and adding a timeout with default.
6. Rerun to confirm, update the dependency map.
