# ARC-013 · Networking — Exercises and lab

## Lab
### ARC-013-LAB1 · Larkspur network design
**Outcomes:** 1–4 · **Time:** ~4 h (one provider; verify service names before recording)
1. Gather existing ranges: data center, stores, head office.
2. Produce the address plan for prod, non-prod, hub, and DR, with growth headroom.
3. Design the VPC/VNet topology: hub-and-spoke, subnets per tier per zone, routing, NAT.
4. Design hybrid connectivity to the data center hosting the ERP.
5. Add private endpoints for each data store and document the DNS approach.
6. Write the connectivity failure modes with detection and behavior.
**Acceptance:** no overlapping ranges; no data store reachable from the internet; connectivity failure mode documented.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-013-EX01 | 1 | The data center uses 10.0.0.0/16 and stores use 10.50.x.x/24 each. Allocate prod, non-prod, and hub blocks that avoid overlap and leave growth. |
| ARC-013-EX02 | 1 | How many addresses does a /24 give and what do you subtract for reservations? Explain why subnet sizing for containers needs care. |
| ARC-013-EX03 | 2 | Sketch a three-zone VPC layout with public, application, and data subnets and state which route each subnet has. |
| ARC-013-EX04 | 2 | Cost review: NAT data transfer is high. Name two design changes that reduce it. |
| ARC-013-EX05 | 3 | Choose between VPN and a dedicated connection for the ERP link and state when you would revisit. |
| ARC-013-EX06 | 4 | A private endpoint was created but the application still connects over the public address. Diagnose and fix. |

## Solutions
- **EX01** Example: prod region 10.100.0.0/16, non-prod 10.101.0.0/16, hub 10.102.0.0/20, DR reserved 10.110.0.0/16; none overlap 10.0.0.0/16 or 10.50.0.0/16. Record in the plan.
- **EX02** 256 addresses, minus a few reserved per subnet by the provider (verify before recording). Containers can consume one address per pod/task, so use larger subnets.
- **EX03** Public: route to internet gateway; application: default route to NAT in same zone; data: local only, no default route.
- **EX04** Use private endpoints for storage and other cloud services; cache or pull artifacts internally; reduce chatty outbound calls.
- **EX05** Start with dual VPN (low volume, fast to deliver); revisit when nightly volume, latency need, or availability target exceeds what VPN gives; keep VPN as a backup afterwards.
- **EX06** DNS still resolves the public address; enable private DNS for the endpoint or add a private zone; then disable public access on the service to prove the path.

**Workplace evidence:** a network design you produced or reviewed for a hybrid environment.

---
Outcome coverage: all outcomes covered by exercises and the lab.
