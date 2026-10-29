# MID-056 · Cloud fundamentals — Quiz

Outcomes: O1 regions and shared responsibility · O2 VPC design · O3 IAM least privilege · O4 managed services and cost.

**Q01 (O1)** In the shared-responsibility model, you are responsible for: A. The data center power B. The hypervisor C. Your configuration, identity, and data D. The provider's network cables
**Q02 (O1)** An availability zone is: A. A billing plan B. An isolated data-center group within a region C. A country D. A DNS record
**Q03 (O1)** To survive the loss of one data center, run in: A. One AZ B. One large VM C. One subnet D. At least two AZs
**Q04 (O2)** Which belongs in a public subnet? A. The load balancer B. The database C. Secrets D. Backups
**Q05 (O2)** A database security group should allow: A. All traffic B. Only the application's group on the database port C. Only SSH from anywhere D. Nothing, ever
**Q06 (O2)** A NAT gateway lets private subnets: A. Accept inbound internet traffic B. Host websites C. Reach the internet outward only D. Skip firewalls
**Q07 (O3)** Least privilege means: A. Granting only the permissions the service needs B. Using the root account C. Wildcard policies D. One shared admin key
**Q08 (O3)** Workloads should authenticate with: A. Long-lived keys in code B. Roles that issue short-lived credentials C. The root password D. Shared files
**Q09 (O4)** Sharing a private object temporarily is best done with: A. Making the bucket public B. Emailing the key C. A time-limited signed URL D. A screenshot
**Q10 (O4)** Which is a typical cost surprise? A. Cheap logs B. Free data transfer C. Zero idle cost D. Data transfer or NAT charges and forgotten idle resources

## Answers
Q01 C · Q02 B · Q03 D · Q04 A · Q05 B · Q06 C · Q07 A · Q08 B · Q09 C · Q10 D

## Practical part
Architecture diagram review (`MID-056-EX06`) plus lab `MID-056-LAB1`. Pass: quiz at least 8/10, a private database with no public endpoint, a least-privilege role, and a written cost estimate.
