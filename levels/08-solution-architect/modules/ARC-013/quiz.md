# ARC-013 · Networking — Quiz

Outcomes: O1 CIDR planning · O2 VPC/VNet layout, routing, NAT · O3 hybrid connectivity · O4 private endpoints.

**Q01 (O1)** Which block is larger? A. /24 B. /28 C. /16 D. /30
**Q02 (O1)** Overlapping CIDR ranges between cloud and on-premises mainly cause: A. Cheaper bills B. Faster routing C. Better security D. Inability to peer or route between them
**Q03 (O1)** Best practice for address planning is: A. Use the default range B. Pick ranges per project randomly C. One central plan covering all environments, regions, and on-premises D. Reuse ranges across environments
**Q04 (O2)** Which belongs in a public subnet? A. A database B. A load balancer C. The ERP adapter D. Secrets store
**Q05 (O2)** Outbound-only internet access from private subnets uses: A. NAT B. An internet gateway route in the data subnet C. Public IPs on databases D. A second VPC
**Q06 (O2)** For NAT resilience you should: A. Use one NAT for all regions B. Remove NAT C. Use one NAT per zone D. Put NAT in the data subnet
**Q07 (O3)** A single VPN tunnel as the only ERP link is a: A. Best practice B. Compliance requirement C. Cost saver with no risk D. Single point of failure
**Q08 (O3)** A dedicated connection compared with VPN typically offers: A. Predictable latency and bandwidth B. Shorter setup time C. Lower cost always D. No need for redundancy
**Q09 (O4)** A private endpoint should be combined with: A. Making the service public B. Disabling public access on the service C. Removing DNS D. Using a single zone
**Q10 (O4)** In hub-and-spoke, spokes connect to: A. Each other directly B. The internet only C. The hub D. Nothing

## Answers
Q01 C · Q02 D · Q03 C · Q04 B · Q05 A · Q06 C · Q07 D · Q08 A · Q09 B · Q10 C

## Practical part
Network design review of the `ARC-013-LAB1` address plan, topology, hybrid link, and failure-mode notes plus exercises `ARC-013-EX01` to `EX06`. Pass: quiz at least 8/10, at least five of six exercises correct, no overlapping ranges, and no data store reachable from the internet.
