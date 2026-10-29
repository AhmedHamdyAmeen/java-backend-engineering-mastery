# ARC-011 · Cloud service models — Lecture scripts

**Video:** 58 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-011-L01 · IaaS, PaaS, SaaS, managed services (12 min)
**Goal:** tell the service models apart by what the customer still operates.

**Key points**
- IaaS: you rent virtual machines, disks, and networks; you run the OS, runtime, patching, and application.
- PaaS: you deploy code or containers; the provider runs the OS and runtime.
- SaaS: you use a finished application; you configure it and manage its users and data.
- Managed service: one component (a database, a queue) run by the provider; you still design, size, secure, and monitor its use.
- The models are a spectrum; the useful question is "what do my people still have to do at 3 a.m.?"

**Show:** a stack diagram with layers (hardware, network, OS, runtime, application, data, access) and four columns; shade what the customer owns in each column.

**Check:** A managed database service is used. Who patches the engine? *(The provider; you still own schema, access, sizing, and backups strategy.)*

---

## ARC-011-L02 · Shared responsibility by model (12 min)
**Goal:** apply the shared-responsibility model to security and operations for each model.

**Key points**
- The provider secures the cloud itself (facilities, hardware, hypervisor); the customer secures what they put in it.
- The line moves up the stack with each model, but data, identity, and configuration always stay with the customer.
- Most cloud incidents come from customer-side misconfiguration, not provider failure.
- Operations are shared too: backups, monitoring, incident response, and scaling each need a named owner.
- Write the split down; unwritten responsibilities become gaps.

**Show:** a responsibility table with rows (patching, identity, data encryption, backups, monitoring, incident response) and columns (IaaS, PaaS, SaaS) filled with Provider / Customer / Shared.

**Check:** In a SaaS CRM, who is responsible for who can export customer data? *(The customer; access configuration is always theirs.)*

---

## ARC-011-L03 · Control vs operational burden (10 min)
**Goal:** weigh control against the effort of operating.

**Key points**
- More control means more to run: patching, scaling, backup, on-call.
- Higher-level services remove undifferentiated work so the team can spend time on what makes the business different.
- Control is only worth having where you need it: special runtime, unusual network, strict tuning.
- Count people and skills, not just licence price; an unowned VM costs more than its invoice.
- Default to the highest level that meets requirements, and move down only with a stated reason.

**Show:** a two-axis sketch: control on one axis, operating effort on the other, with IaaS, containers, PaaS, SaaS placed along the diagonal.

**Check:** What is the usual mistake when teams choose IaaS by default? *(They take on operations they did not need and cannot staff.)*

---

## ARC-011-L04 · Lock-in, honestly assessed (10 min)
**Goal:** assess lock-in as a cost to compare, not a fear to obey.

**Key points**
- Lock-in comes in kinds: data format, API, skills, contracts, and operating tooling.
- Estimate the exit cost: what would it take, in time and money, to move in a year?
- Avoiding lock-in has its own price: lowest-common-denominator designs, extra abstraction, slower delivery.
- Accept lock-in knowingly where the benefit is high and the exit is affordable; keep data portable.
- Record the exit consideration in the decision.

**Show:** a small table per component: lock-in kind, benefit gained, rough exit effort (days, weeks, months), mitigation.

**Check:** Does avoiding all lock-in make a design better? *(No; it trades delivery speed for an option you may never use.)*

---

## ARC-011-L05 · Demo: choosing service models for each Larkspur component (14 min)
**Goal:** run a worked decision session across the Larkspur components and fill the matrix prepared for `ARC-011-LAB1`.

**Steps**
1. List components: storefront, order service, product search, payments, relational data, media storage, email, identity, monitoring, ERP integration, reporting.
2. For each, ask the three questions: what must be controlled, who will operate it, what is the exit cost.
3. Choose: SaaS for email delivery and the payment gateway; managed database and managed search; PaaS or managed containers for services; object storage for media.
4. **Planned mistake:** put the ERP integration adapter on a self-managed VM "to be safe". Challenge it: nobody on the team owns patching a VM, so a managed container platform is safer.
5. Fill the "who operates what" column and mark gaps: for example, nobody owned database restore testing.
6. Assign owners to every gap and note exit consideration per row.

---
