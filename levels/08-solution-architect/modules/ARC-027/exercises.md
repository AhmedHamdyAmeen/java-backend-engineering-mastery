# ARC-027 · Identity and access — Exercises and lab

## Lab
### ARC-027-LAB1 · Larkspur access model
**Outcomes:** 1–4 · **Time:** ~3 h
1. List the user groups: staff, store managers, customer-service agents, partners, customers.
2. Define roles and attributes; state where each is evaluated.
3. Design identity federation for workforce, partners, and customers.
4. Design privileged-access controls for operators.
5. Write the joiner, mover, and leaver steps and the access review schedule.
6. Demonstrate least privilege for five representative users.
**Acceptance:** least privilege demonstrated for five representative users.

## Exercises (case-based; five exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-027-EX01 | 1 | The access matrix has 380 roles because of store, region, and department combinations. Redesign it. |
| ARC-027-EX02 | 2 | Partner staff must call the Order API on behalf of their company. Draw the federation and token flow. |
| ARC-027-EX03 | 3 | Five engineers share one production admin login. Write the replacement design. |
| ARC-027-EX04 | 4 | A store manager moves to another store and a contractor ends a contract. Write what each process must do. |
| ARC-027-EX05 | 1, 4 | Write the rule and the review process for "customer-service agents see only cases in their queue, and can issue refunds up to a limit". |

## Solutions
- **EX01** Few roles (StoreManager, RegionalManager) with attributes storeId and region evaluated by a policy; remove duplicates.
- **EX02** Partner's identity provider issues a login, Larkspur token service maps to a Partner role with partnerId claim, gateway enforces quota, API checks the partnerId attribute.
- **EX03** Individual privileged accounts, just-in-time approval with expiry, session recording, secrets vault; break-glass account sealed and reviewed.
- **EX04** Mover: remove old store scope and add new one on the effective date; leaver: disable all accounts on the last day, revoke tokens, and review owned resources; contractor accounts expire automatically.
- **EX05** Role CustomerServiceAgent with attributes queueId and refundLimit; policy checks both; quarterly (verify with company policy) owner review plus alert on large refunds.

Outcome 3 on logs is also covered by the lab step 4.

**Workplace evidence:** an access model or federation design you delivered.
