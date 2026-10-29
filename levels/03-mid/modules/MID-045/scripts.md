# MID-045 · Advanced testing — Lecture scripts

**Video:** 64 min · **Analogy used throughout:** a written agreement between a supplier and a customer: each side tests against the paper, not against the other's whole factory. Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-045-L01 · Testing distributed systems (10 min)
**Goal:** explain why end-to-end tests across many services do not scale.

**Key points**
- End-to-end tests need every service, database, and broker running: slow to start, slow to run.
- They are brittle: one unrelated outage or data change fails the test, and the failure is hard to locate.
- Environments drift, so results are not repeatable; teams stop trusting them.
- Keep a few end-to-end smoke tests; push most checks lower: unit, integration with Testcontainers, and contract tests.

**Show:** a test pyramid for Shop with contract tests between integration and end-to-end.

**Check:** Name two reasons end-to-end tests are brittle. *(Many moving parts and shared environments; any unrelated failure breaks them.)*

---

## MID-045-L02 · Consumer-driven contracts (12 min)
**Goal:** write a contract from the consumer's needs.

**Key points**
- The consumer states what it uses from the provider: request and the response fields it reads.
- The contract is a file (Pact JSON, or a Spring Cloud Contract definition) generated from consumer tests.
- The provider verifies it against the real provider code, with no consumer running.
- Match only what the consumer needs (types, required fields), not the whole payload.
- Both sides review the contract; writing it from the provider alone defeats the point.

**Show:** `orders` (consumer) expects `GET /stock/{sku}` returns `{sku: string, available: integer}`; the Pact file records exactly that.

**Check:** Who writes the contract's expectations? *(The consumer, from what it actually uses.)*

---

## MID-045-L03 · Contracts for messages (10 min)
**Goal:** apply contracts to Kafka events.

**Key points**
- A message is also an API: the producer must not break consumers' parsing.
- The consumer defines the message shape it reads (`OrderPlaced` with `orderId`, `lines`); the producer verifies it can generate it.
- Pact message pacts and Spring Cloud Contract messaging both support this; verify the version and the supported broker setups before recording.
- Combine with a schema registry for compatibility rules (see the messaging modules).

**Show:** a contract for `OrderPlaced`: required `orderId` (string), `totalCents` (integer); provider test builds the real event and checks it.

**Check:** Why test a message contract? *(Consumers parse fields; renaming one breaks them silently.)*

---

## MID-045-L04 · Contracts in CI (8 min)
**Goal:** make contract verification block bad releases.

**Key points**
- Consumer pipeline publishes contracts (to a Pact Broker or a repo/artifact store).
- Provider pipeline fetches all contracts for its consumers and verifies them; failure fails the build.
- A "can I deploy?" style check asks whether the version is compatible with what is in each environment.
- Breaking change flow: add the new field, migrate consumers, then remove the old one.

**Show:** two pipelines with arrows: consumer publishes, provider verifies, gate before deploy.

**Check:** What happens when the provider renames a field a consumer uses? *(The provider build fails on contract verification.)*

---

## MID-045-L05 · Property-based testing (12 min)
**Goal:** test domain rules over many generated inputs with jqwik.

**Key points**
- Example tests check chosen inputs; property tests state a rule that must hold for any valid input.
- jqwik generates many random inputs and shrinks failures to a minimal case.
- Good properties for Shop: total equals the sum of its lines; adding then removing an item restores the order; total is never negative.
- Define generators (`@Provide`) that produce valid domain objects only.
- Keep the seed from failures to reproduce them.

**Show:**
```java
@Property
void totalIsSumOfLines(@ForAll("orders") Order o) {
    assertThat(o.total()).isEqualTo(o.lines().stream().mapToLong(Line::cents).sum());
}
```

**Check:** What does shrinking do? *(Reduces a failing input to the smallest one that still fails.)*

---

## MID-045-L06 · Demo: a breaking API change caught by a contract (12 min)
**Goal:** see a contract stop a breaking change. Prepares `MID-045-LAB1`.

**Steps**
1. Show the consumer test in `orders` generating the contract against `inventory`.
2. Publish the contract and run provider verification: green.
3. **Planned mistake:** in `inventory`, rename `available` to `quantity` for "clarity".
4. Run the provider build: verification fails and names the missing field and the consumer.
5. Fix: keep `available`, add `quantity`, and plan the migration in two steps.
6. Run the property tests on the Order aggregate as a final check.
