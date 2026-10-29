# ARC-014 · Compute choices — Lecture scripts

**Video:** 66 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-014-L01 · The compute spectrum (10 min)
**Goal:** place compute options on one spectrum from control to convenience.

**Key points**
- Virtual machines: most control, most operating work.
- Managed container platforms: you ship containers, the provider runs the servers or scheduling.
- Kubernetes: powerful orchestration you operate or rent as a managed control plane.
- Serverless functions: you ship code, pay per run, scale to zero; limits on duration and runtime.
- Compare by control, scaling, cost shape, and operating effort, not by fashion.

**Show:** a table with rows VM, managed containers, Kubernetes, functions and columns control, scaling, cost shape, operating effort, team skill needed.

**Check:** Which option scales to zero and charges per execution? *(Serverless functions.)*

---

## ARC-014-L02 · VMs and managed container platforms (10 min)
**Goal:** know when VMs and managed container platforms fit.

**Key points**
- VMs fit lift-and-shift, special OS or licence needs, and software that cannot be containerized.
- You own patching, images, scaling groups, and hardening.
- Managed container platforms run stateless services with autoscaling and rolling deploys without cluster administration.
- Containers give a repeatable package, which suits Java services well.
- Verify provider service names and limits before recording.

**Show:** the same Java order service shown as a VM with an autoscaling group versus a container service with a task definition; list what the team operates in each.

**Check:** Which option has less patching burden for a standard Java service? *(Managed containers; the platform patches the host.)*

---

## ARC-014-L03 · Kubernetes: when it is worth it (12 min)
**Goal:** decide whether an organization should run Kubernetes at all.

**Key points**
- Kubernetes gives portability, a large ecosystem, fine-grained control, and complex workload scheduling.
- It also brings upgrades, networking, security policy, observability, and a steep learning curve, even when managed.
- Worth it when: many services, multiple teams, platform team exists, workloads need its features.
- Not worth it when: a handful of services, a small team, simple needs.
- A managed container service or PaaS is the default; Kubernetes needs a justification.

**Show:** a checklist with yes/no: more than 15 services, dedicated platform team, need for custom operators or multi-cloud portability, existing skills. Three or more "yes" answers supports Kubernetes.

**Check:** A six-person team with four services considers Kubernetes. Default advice? *(Use a managed container platform; revisit if scale and team grow.)*

---

## ARC-014-L04 · Serverless functions (12 min)
**Goal:** use functions where they fit and avoid them where they do not.

**Key points**
- Fit: event-driven work, spiky or rare traffic, glue code, scheduled tasks.
- Strengths: no servers to manage, scale to zero, pay per use.
- Limits: execution time, cold starts, concurrency limits, harder local testing, vendor-specific triggers.
- Poor fit: long-running steady load, where per-run pricing exceeds a continuous instance, and latency-sensitive paths affected by cold starts.
- Watch downstream limits: functions can scale faster than your database.

**Show:** a cost sketch: break-even between function pricing and a small container as requests per second rise (illustrative; verify prices before recording).

**Check:** Which workload suits functions poorly? *(Long-running steady load.)*

---

## ARC-014-L05 · Matching compute to workload shape (8 min)
**Goal:** choose compute by the shape of the workload.

**Key points**
- Steady: reserved containers or VMs; the cheapest per hour.
- Spiky: autoscaling containers or functions with sensible limits.
- Event-driven: functions or queue-triggered workers.
- Batch: short-lived jobs on demand or discounted capacity that can be interrupted.
- Also weigh latency, state, and operating effort.

**Show:** four cards: steady, spiky, event-driven, batch, each with a Larkspur example and a compute match.

**Check:** What suits a nightly job that can be restarted? *(A scheduled batch job on discounted or on-demand capacity.)*

---

## ARC-014-L06 · Demo: compute choices for Larkspur's storefront, order processing, and nightly batch (14 min)
**Goal:** record ADR-style compute decisions with the team's skills in the decision, preparing `ARC-014-LAB1`.

**Steps**
1. Describe the workloads: storefront API (spiky with seasonal peaks), order processing (steady plus queue bursts), nightly stock and ERP batch.
2. State the context: eight engineers, no platform team, limited on-call.
3. Decide: managed containers for storefront and order services with autoscaling; queue-triggered workers for order bursts; scheduled batch jobs for the nightly run.
4. **Planned mistake:** a colleague proposes Kubernetes "because we will grow". Counter: record it as a revisit trigger (services count, team size) rather than a starting point.
5. Write each as an ADR: context, decision, consequences, operating model, revisit trigger.
6. Check each ADR names who is on call and what skills are required.

---
