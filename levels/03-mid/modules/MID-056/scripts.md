# MID-056 · Cloud fundamentals — Lecture scripts

**Video:** 72 min · **Analogy used throughout:** renting a city district: you get land, roads, and utilities on demand, but you lock your own doors and pay for every hour. Running project: Shop. Labs are written for the chosen provider (AWS or Azure); verify service names before recording.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-056-L01 · Cloud building blocks (10 min)
**Goal:** map cloud services to the parts of Shop.

**Key points**
- Compute (VMs, containers, Kubernetes), storage (object, block), databases (managed), networking (VPC, load balancers), identity (IAM).
- Managed services trade control for less operations work: patching, backups, failover.
- The shared-responsibility model: the provider secures the cloud; you secure what you put in it (configuration, identity, data).
- Choose managed first unless you have a clear reason.

**Show:** diagram: users → load balancer → Kubernetes → managed PostgreSQL and object storage, inside a VPC.

**Check:** Who configures database access rules in a managed database? *(You; the provider runs the platform.)*

---

## MID-056-L02 · Regions and availability zones (8 min)
**Goal:** choose where to run and how to survive failures.

**Key points**
- A region is a geographic area; an availability zone (AZ) is an isolated data center group within it.
- Spread across at least two AZs for high availability; use several regions for disaster recovery or latency.
- Region choice: latency to users, data-residency law, service availability, price.
- Cross-AZ and cross-region traffic can cost money and add latency.

**Show:** pods spread across three AZs, database with a standby in a second AZ.

**Check:** What protects against the loss of one data center? *(Running across multiple AZs.)*

---

## MID-056-L03 · Identity and access management (12 min)
**Goal:** give every service the minimum permissions it needs.

**Key points**
- Principals (users, roles, workloads) get policies that allow actions on resources.
- Least privilege: start from nothing and add only what is needed; avoid wildcards.
- Workloads use roles (workload identity) rather than long-lived access keys.
- Humans use SSO and MFA; avoid the root account.
- Review permissions regularly and use audit logs.

**Show:** a policy allowing `orders` read and write on one bucket prefix only, nothing else.

**Check:** Why prefer roles to access keys? *(Roles issue short-lived credentials that are not stored in code.)*

---

## MID-056-L04 · Networking: VPCs and subnets (12 min)
**Goal:** design a network where only the entry points are public.

**Key points**
- A VPC (VNet) is your private network; subnets divide it by tier and AZ.
- Public subnets host load balancers; private subnets host applications and databases.
- Internet access for private subnets goes outward only through a NAT gateway.
- Security groups (firewalls) allow traffic by rule: the database accepts connections only from the app's group.
- Use private endpoints to reach managed services without the public internet.

**Show:** table: subnet, tier, route to internet, who may connect.

**Check:** Where should the database live? *(In a private subnet with no public endpoint.)*

---

## MID-056-L05 · Managed databases, load balancers, object storage (12 min)
**Goal:** use the three most common managed services correctly.

**Key points**
- Managed PostgreSQL: backups, patching, failover, read replicas; you tune queries and size.
- Load balancer: terminates TLS, spreads traffic across AZs, performs health checks.
- Object storage: cheap durable storage for images and exports; private by default; use signed URLs for access.
- Encrypt at rest and in transit; enable backups and test restores.

**Show:** config summary: PostgreSQL multi-AZ, private; ALB/Application Gateway with HTTPS; bucket private with lifecycle rules.

**Check:** How do you share a private object temporarily? *(A time-limited signed URL.)*

---

## MID-056-L06 · Reading a cloud bill (6 min)
**Goal:** estimate and control cost.

**Key points**
- Costs come from compute hours, storage, data transfer, managed service tiers, and idle resources.
- Estimate with the provider's pricing calculator before building; tag resources by team and environment.
- Set budgets and alerts; tear down dev environments when idle.
- Data transfer out and NAT gateways are common surprises.

**Show:** a sample bill sorted by service with the three largest lines highlighted.

**Check:** Name one common cost surprise. *(Data transfer or NAT gateway charges, or forgotten idle resources.)*

---

## MID-056-L07 · Demo: a private database reachable only from the app (12 min)
**Goal:** build the network and prove the database is private. Prepares MID-056-LAB1.

**Steps**
1. Create a VPC with public and private subnets across two AZs.
2. Launch a managed PostgreSQL instance in the private subnets with public access disabled.
3. **Planned mistake:** allow `0.0.0.0/0` on the database security group to "test quickly". Fix: allow only the application's security group on port 5432.
4. Create a least-privilege role for `orders` and connect from the app; show that a connection from the internet times out.
5. Write the monthly cost estimate from the calculator and tag all resources; remember to tear down.

**Check:** What proves the database is private? *(It has no public endpoint and accepts connections only from the app's security group.)*
