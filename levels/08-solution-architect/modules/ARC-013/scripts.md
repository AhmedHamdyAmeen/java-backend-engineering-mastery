# ARC-013 · Networking — Lecture scripts

**Video:** 95 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.
Provider note: VPC (AWS) and VNet (Azure) are used interchangeably; verify provider limits and service names before recording.

---

## ARC-013-L01 · CIDR and address planning (12 min)
**Goal:** plan IP address space so nothing overlaps now or later.

**Key points**
- CIDR notation like 10.20.0.0/16 gives a network prefix; the number after the slash is how many bits are fixed, so a smaller number means a bigger block.
- Private ranges (RFC 1918) are reserved for internal use: 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16.
- Overlapping ranges cannot be peered or routed together; fixing it later means re-addressing.
- Plan one master allocation: per environment, per region, per store, plus the data center, with growth headroom.
- Some services reserve addresses in each subnet; leave margin (verify before recording).

**Show:** an address plan table: block, owner, purpose, size, example 10.10.0.0/16 for prod region A.

**Check:** Which is larger, a /16 or a /24? *(A /16; fewer fixed bits means more addresses.)*

---

## ARC-013-L02 · VPC/VNet layout and subnets (12 min)
**Goal:** lay out a virtual network with public and private subnets across zones.

**Key points**
- A VPC/VNet is your private network in the cloud; subnets divide it, each living in one zone.
- Public subnets host only what must face the internet (load balancers, NAT); everything else sits in private subnets.
- Use at least two or three zones, with a subnet per tier per zone.
- Separate tiers: web, application, data; data subnets have no internet route.
- Size subnets for growth, especially if containers use many addresses.

**Show:** a diagram: one VPC, three zones, columns of public / app / data subnets, load balancer in public, databases in data.

**Check:** Where should a database live? *(A private data subnet with no route to the internet.)*

---

## ARC-013-L03 · Routing and NAT (10 min)
**Goal:** understand how traffic leaves and enters the network.

**Key points**
- Route tables decide where traffic goes by destination range.
- An internet gateway gives public subnets two-way internet access; private subnets use NAT for outbound-only access.
- NAT is a cost and a failure point: one per zone for resilience, and data transfer is billed.
- Prefer private endpoints (ARC-013-L05) over sending traffic to cloud services via NAT.
- Keep routing simple; every exception is documentation to maintain.

**Show:** a route table for a private subnet: local range stays local; default route goes to the NAT in the same zone.

**Check:** Why is outbound traffic from private subnets sent through NAT? *(It lets them reach out without being reachable from the internet.)*

---

## ARC-013-L04 · Hybrid connectivity (12 min)
**Goal:** choose how the cloud connects to on-premises.

**Key points**
- Site-to-site VPN: encrypted tunnels over the internet; fast to set up, variable latency, limited bandwidth.
- Dedicated connection: private circuit from a provider or partner; predictable latency and bandwidth, weeks to order, higher cost.
- Resilience: two tunnels at least; critical links get two independent paths, and a VPN as a backup for a dedicated line.
- Choose by bandwidth, latency, resilience, lead time, and cost.
- Use dynamic routing where available, and plan failover behavior.

**Show:** a decision table: ERP sync volume small and tolerant of delay leads to dual VPN; large nightly data loads lead to dedicated line plus VPN backup.

**Check:** Is one VPN tunnel enough as the only ERP link? *(No; it is a single point of failure.)*

---

## ARC-013-L05 · Private endpoints and private data paths (10 min)
**Goal:** keep data traffic off the public internet.

**Key points**
- A private endpoint gives a cloud service (storage, database) a private address inside your network.
- Combine with disabling public access on the service itself.
- DNS must resolve the service name to the private address; misconfigured DNS is the usual failure.
- Private paths reduce exposure and often reduce NAT and data transfer cost.
- Policy: data stores must have no public endpoint by default.

**Show:** diagram: application subnet to a private endpoint to the managed database, with the database's public access switched off.

**Check:** What commonly breaks after creating a private endpoint? *(DNS resolution to the private address.)*

---

## ARC-013-L06 · Hub-and-spoke topologies (10 min)
**Goal:** structure many networks with a central hub.

**Key points**
- Spokes are workload networks; the hub holds shared services: egress, firewalls, hybrid links, DNS.
- Spokes connect to the hub, not to each other, so traffic is inspected and controlled in one place.
- Connection options: peering (simple, non-transitive) or a transit gateway-style service (scalable, extra cost); verify before recording.
- Central hybrid link means one connection serves all spokes.
- The hub is critical: design it for resilience and keep it small.

**Show:** a star diagram: hub in the middle with the VPN to the data center; prod, non-prod, and shared-services spokes around it.

**Check:** Why avoid spoke-to-spoke links? *(They bypass central inspection and create a tangled mesh.)*

---

## ARC-013-L07 · Demo: planning address space for Larkspur, stores, and the data center (15 min)
**Goal:** produce the address plan for the lab with no overlaps.

**Steps**
1. Collect existing ranges: data center (ask the network team), 120 store networks, head office.
2. Reserve those first; document them as "do not use".
3. Allocate cloud blocks: prod region A, non-prod, shared hub, and a reserved DR region, each with growth room.
4. Carve subnets per tier per zone with a spreadsheet and check overlaps with a script or calculator.
5. **Planned mistake:** choose 10.0.0.0/16 for prod because it is "the default"; discover the data center already uses it. Fix: renumber before any build.
6. Record the plan as the source of truth in the repository.

---

## ARC-013-L08 · Demo: connecting the cloud platform to the on-premises ERP (14 min)
**Goal:** design the hybrid link and document its failure modes for the lab.

**Steps**
1. List ERP traffic: order posting (small, frequent), stock sync (medium), nightly finance export (large).
2. Choose: dual site-to-site VPN tunnels to the hub now; evaluate a dedicated line if nightly volume grows.
3. Place the ERP integration service in a private subnet; the ERP is reached only over the hybrid link.
4. **Planned mistake:** a single VPN tunnel as the only link. Fix: two tunnels on separate devices; add queuing so orders buffer when the link is down.
5. Document failure modes: tunnel down, data center down, ERP slow; each with detection and behavior.
6. Define a test: drop one tunnel in a non-prod environment and watch the failover.

---
