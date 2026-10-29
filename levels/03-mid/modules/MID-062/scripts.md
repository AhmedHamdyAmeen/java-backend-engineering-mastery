# MID-062 · API evolution — Lecture scripts

**Video:** 58 min · **Analogy used throughout:** a restaurant changing its menu while regulars keep ordering: add dishes freely, never silently change what an existing dish means.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-062-L01 · What counts as a breaking change (10 min)
**Goal:** classify a change as compatible or breaking.

**Key points**
- A breaking change makes a correctly working consumer fail or misbehave without the consumer changing.
- Usually compatible: adding an optional response field, a new endpoint, a new optional request parameter.
- Usually breaking: removing or renaming a field, changing a type or unit, making an optional input required, tightening validation, changing status codes or error shapes.
- Changing meaning (cents to decimal euros) is breaking even when the type stays the same.
- Direction matters: producers break consumers; consumers break producers by requiring more than was promised.

**Show:** a table of ten changes to `GET /orders/{id}` and `OrderPlaced`, each marked compatible or breaking, with the reason.

**Check:** Is renaming `total` to `totalAmount` breaking? *(Yes; existing consumers no longer find `total`.)*

---

## MID-062-L02 · Evolving REST APIs (10 min)
**Goal:** change a REST API without breaking clients.

**Key points**
- Prefer additive change: add the new field next to the old one.
- Expand and contract: add new, migrate consumers, remove old in a later release.
- A new version (`/v2`, media type, header) is for changes that cannot be made additively; do not version every change.
- Keep error shapes stable (for example RFC 9457 problem details).
- Verify compatibility automatically: contract tests (MID-045) and OpenAPI diff tools in CI.

**Show:** `total` stays; add `money: {amount: "12.50", currency: "EUR"}`. Both are returned for one release.

**Check:** What are the three phases of expand and contract? *(Expand: add new; migrate consumers; contract: remove old.)*

---

## MID-062-L03 · Schema registries and compatibility modes (12 min)
**Goal:** enforce event compatibility with a schema registry.

**Key points**
- A schema registry stores versioned schemas (Avro, Protobuf, JSON Schema) per subject, often per topic.
- Producers register the schema; the registry rejects incompatible versions.
- Backward: new schema can read data written with the old one (upgrade consumers first).
- Forward: old schema can read data written with the new one (upgrade producers first).
- Full: both; the safest for long-lived topics. The `_TRANSITIVE` variants check all earlier versions.
- Avro: adding a field needs a default. Protobuf: never reuse field numbers; reserve removed ones.
- Mode names and defaults differ by registry product; verify version before recording.

**Show:** an Avro `OrderPlaced` v2 adding `"currency"` with `"default": "EUR"`, and the registry compatibility check call passing.

**Check:** Which change is safe in Avro under backward mode: add a field with a default, or add one without? *(With a default.)*

---

## MID-062-L04 · Tolerant readers (6 min)
**Goal:** write consumers that survive harmless change.

**Key points**
- Tolerant reader: read only the fields you need; ignore unknown ones.
- Do not fail on new fields, new enum values you can safely default, or reordered fields.
- Be strict about what you depend on: a missing required field is still an error.
- In Jackson, ignore unknown properties for external payloads (`FAIL_ON_UNKNOWN_PROPERTIES` off, or `@JsonIgnoreProperties(ignoreUnknown = true)`).
- Map to your own model; do not leak the provider's DTO through your code.

**Show:** a consumer `PaymentView` record with three fields reading a payload that has fifteen.

**Check:** What should a tolerant reader do with an unknown field? *(Ignore it.)*

---

## MID-062-L05 · Deprecation done properly (8 min)
**Goal:** retire an API or field in four steps.

**Key points**
- Announce: changelog, docs, `Deprecation` and `Sunset` headers (verify the current RFC status before recording), direct message to known consumers.
- Measure: log or metric of who still calls the old field or endpoint, by client id.
- Migrate: help the remaining consumers; give a date and keep to it.
- Remove: only when usage is zero or the deadline passed with owners informed.
- Removal in the same release as the announcement is not deprecation.

**Show:** a Grafana panel "calls per client to `total` field" dropping to zero over six weeks.

**Check:** What must you know before removing an old field? *(Who still uses it, from usage measurement.)*

---

## MID-062-L06 · Demo: changing `OrderPlaced` without breaking consumers (12 min)
**Goal:** replace `total` (cents, long) with `money` (amount, currency) safely. Prepares `MID-062-LAB1`.

**Steps**
1. Show current Avro schema v1 and the registry set to BACKWARD_TRANSITIVE (or FULL).
2. Add `money` with a default and keep `total`; register v2; the check passes.
3. Deploy the producer to emit both fields; consumers on v1 keep working.
4. **Planned mistake:** remove `total` in the same change; the registry rejects it (or a contract test fails). Fix: keep it for a release.
5. Migrate consumers to `money`; watch usage of `total` fall to zero.
6. Register v3 removing `total` after the deprecation window.
