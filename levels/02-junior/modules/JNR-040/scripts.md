# JNR-040 · Role-based authorization — Lecture scripts

**Video:** 64 min · **Analogy used throughout:** a hotel key card: it opens only your room (ownership) and the gym if your pass includes it (role).
Format: **Goal** · **Key points** · **Show** · **Check**.

Note: verify the Spring Security version and method security annotations before recording.

---

## JNR-040-L01 · Roles, authorities, permissions (8 min)
**Goal:** model who may do what.

**Key points**
- An authority is one permission string, such as `ORDER_READ`.
- A role is a named group of permissions, such as `ADMIN`; in Spring a role is an authority with the `ROLE_` prefix.
- RBAC (role-based access control): assign roles to users, and check roles.
- Keep roles few and meaningful (customer, admin); add finer permissions only when needed.
- A role says what kind of action is allowed, not which records.

**Show:** a table: role / authorities / example endpoints.

**Check:** Does a role decide which orders a customer can see? *(No. That needs an ownership check.)*

---

## JNR-040-L02 · Method security (10 min)
**Goal:** protect service methods with annotations.

**Key points**
- Turn it on with `@EnableMethodSecurity`.
- `@PreAuthorize("hasRole('ADMIN')")` runs before the method.
- SpEL can use method arguments and the current user: `@PreAuthorize("#id == authentication.principal.id")`.
- Put it on the service layer so every caller, not only controllers, is covered.
- URL rules are a first layer; method rules are a second layer (defense in depth).

**Show**
```java
@PreAuthorize("hasRole('ADMIN')")
public void deleteProduct(long id) { ... }
```

**Check:** Which annotation enables `@PreAuthorize`? *(`@EnableMethodSecurity`.)*

---

## JNR-040-L03 · Ownership checks (12 min)
**Goal:** make sure users reach only their own data.

**Key points**
- Take the user's identity from the authenticated principal, never from the request body or a parameter.
- Option 1: load then compare `order.getCustomerId()` with the current user.
- Option 2 (preferred): put ownership in the query: `findByIdAndCustomerId(id, customerId)`.
- When it does not belong to you, return 404, not 403, so you do not reveal that it exists.
- Admins may bypass ownership through an explicit, tested path.

**Show**
```java
Order order = orders.findByIdAndCustomerId(id, currentUser.id())
    .orElseThrow(() -> new OrderNotFoundException(id));
```

**Check:** Why return 404 instead of 403 for another customer's order? *(403 would confirm the order exists.)*

---

## JNR-040-L04 · IDOR: the most common API bug (10 min)
**Goal:** recognize and test for insecure direct object references.

**Key points**
- IDOR: the API takes an ID from the client and returns the object without checking it belongs to the caller.
- Attack: log in as customer A, change `/orders/101` to `/orders/102`.
- Hard-to-guess IDs (UUIDs) help a little but are not a fix.
- Broken access control is the top item on the OWASP Top 10 (verify the current edition before recording).
- Test it: two customers, A requests B's resource, expect 404.

**Show:** a request pair: `GET /orders/101` (own, 200) and `GET /orders/102` (other's, should be 404).

**Check:** Does switching to UUIDs fix IDOR? *(No. You still need an ownership check.)*

---

## JNR-040-L05 · Demo: finding and fixing an IDOR (12 min)
**Goal:** exploit and fix an IDOR in Shop. Prepares `JNR-040-LAB1`.

**Steps**
1. Create two customers, each with an order.
2. Log in as A and request B's order by ID: it returns 200 with B's data.
3. Find the cause: `findById` without an owner condition.
4. **Planned mistake:** fixing only the `GET` and forgetting `DELETE /orders/{id}`. Show the same attack on `DELETE`, and fix every endpoint.
5. Switch to `findByIdAndCustomerId` and return 404.
6. Add a test: A requests B's order and expects 404.

---

## JNR-040-L06 · Demo: method security with ownership checks (12 min)
**Goal:** combine roles and ownership in the service layer. Prepares `JNR-040-LAB1`.

**Steps**
1. Enable method security.
2. Add `@PreAuthorize("hasRole('ADMIN')")` to the "list all orders" service method.
3. Add a service method `getMyOrders(currentUser)` that filters by owner.
4. Remove `customerId` from the create-order request body and take it from the principal.
5. **Planned mistake:** leaving the `customerId` in the body, so customer A creates an order for B. Show the attack, then fix.
6. Add tests for customer A, customer B, and admin.
