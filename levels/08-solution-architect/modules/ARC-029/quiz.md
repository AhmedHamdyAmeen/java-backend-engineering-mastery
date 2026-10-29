# ARC-029 · Privacy and compliance — Quiz

Outcomes: O1 data classification · O2 retention, deletion, and data-subject rights · O3 residency and transfers · O4 payment scope reduction · O5 audit trails without sensitive data.

**Q01 (O1)** Classification rules are enforced best by: A. A policy PDF B. Architecture such as masking, access policy, and tagging C. Training only D. Trust
**Q02 (O1)** An order record contains an email and a total. Classification should be: A. One class for the whole record B. Per field, since classes differ C. None needed for orders D. Only for payment fields
**Q03 (O2)** A deletion design most often misses: A. Primary database B. The login page C. Backups and analytics copies D. The firewall
**Q04 (O2)** Erasure is requested but an invoice must be kept for tax. Best action: A. Delete everything B. Refuse the whole request C. Ignore the request D. Keep and restrict the required record, erase the rest, tell the customer
**Q05 (O2)** To serve data-subject requests across many systems you first need: A. A data map showing where a person's data lives B. A new CRM C. More storage D. A larger gateway
**Q06 (O3)** Data stored in-region but supported from another region: A. Has no transfer concern B. May still involve a cross-border transfer C. Is always forbidden D. Is public data
**Q07 (O3)** A way to reduce transfer risk is to: A. Copy more data B. Remove access logs C. Tokenize or pseudonymize before the transfer D. Skip the contract
**Q08 (O4)** A hosted payment page reduces PCI DSS scope because: A. Card data goes to the provider instead of through Larkspur systems B. Cards are no longer accepted C. Audits are removed D. Tokens are card numbers
**Q09 (O4)** After a hosted payment Larkspur may store: A. Full card number B. CVV C. A token, last four digits, and status D. The magnetic stripe data
**Q10 (O5)** A good audit trail records: A. Full request payloads B. Who did what and when, with record IDs, not sensitive content C. Card numbers for evidence D. Nothing

## Answers
Q01 B · Q02 B · Q03 C · Q04 D · Q05 A · Q06 B · Q07 C · Q08 A · Q09 C · Q10 B

## Practical part
Compliance architecture review of the lab artifacts plus exercises `ARC-029-EX01` to `EX06`. Pass: quiz at least 8/10, at least five of six exercises correct, and a lab with no card data stored in Larkspur systems and a deletion path that covers backups and analytics copies.
