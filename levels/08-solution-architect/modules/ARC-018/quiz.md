# ARC-018 · Network security — Quiz

Outcomes: O1 layered controls · O2 segmentation · O3 private connectivity · O4 network and identity controls.

**Q01 (O1)** Defense in depth means: A. One strong firewall B. Hiding the network C. Several layers so one failure does not expose everything D. Disabling logs
**Q02 (O1)** A WAF is used to: A. Assign IP addresses B. Inspect HTTP traffic for attacks and abuse C. Store backups D. Provide DNS
**Q03 (O1)** Restricting the origin to accept traffic only from the CDN: A. Slows pages B. Is unnecessary C. Prevents bypassing edge protection D. Removes TLS
**Q04 (O2)** A flat network is risky because: A. It is too fast B. It needs more firewalls C. It cannot use TLS D. One foothold can reach everything
**Q05 (O2)** Segmenting payment components also: A. Reduces compliance scope B. Raises scope C. Removes the need for tokenization D. Removes the need for logging
**Q06 (O2)** A good default for security group rules is: A. Allow all B. Deny by default and allow only required flows C. Allow all outbound and inbound D. Open admin ports to the internet
**Q07 (O3)** For a sensitive partner flow, prefer: A. Plain HTTP B. Open internet with no auth C. Private connectivity where available D. Email attachments
**Q08 (O3)** If only the internet path exists to a partner, use: A. TLS, strong authentication, and allow-lists B. No authentication C. Shared password in a document D. Public file shares
**Q09 (O4)** Network controls do not stop: A. Port scans B. Floods at the edge C. Traffic from blocked ranges D. A valid stolen token used from an allowed network
**Q10 (O4)** The right relationship between network and identity controls is: A. Network replaces identity B. Identity replaces network C. They complement each other D. They are unrelated

## Answers
Q01 C · Q02 B · Q03 C · Q04 D · Q05 A · Q06 B · Q07 C · Q08 A · Q09 D · Q10 C

## Practical part
Security design review of the `ARC-018-LAB1` plan plus exercises `ARC-018-EX01` to `EX06`. Pass: quiz at least 8/10, at least five of six exercises correct, payment components isolated, and every public endpoint protected.
