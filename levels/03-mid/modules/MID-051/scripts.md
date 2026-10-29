# MID-051 · Advanced API security — Lecture scripts

**Video:** 54 min · **Analogy used throughout:** a building where every office door checks your badge, not just the front desk. Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-051-L01 · OAuth flows revisited (10 min)
**Goal:** choose the right OAuth 2.0 flow per scenario.

**Key points**
- User-facing apps (web, mobile, SPA): authorization code flow with PKCE; no implicit flow.
- Machine-to-machine: client credentials flow; there is no user.
- Delegated access ("on behalf of the user" across services): token exchange, or forwarding the user's token where policy allows.
- OIDC adds identity (ID token) on top of OAuth; access tokens are for APIs.
- Check current OAuth security guidance (for example the OAuth 2.1 draft and best-practice documents) before recording.

**Show:** table: scenario | flow | token holds.

**Check:** Which flow for a nightly job with no user? *(Client credentials.)*

---

## MID-051-L02 · Token validation everywhere (10 min)
**Goal:** make every service verify tokens itself.

**Key points**
- The gateway is not enough: an attacker reaching a service directly bypasses it.
- Each service validates: signature (keys from the issuer's JWKS), issuer, audience, expiry, and scopes or roles.
- Audience matters: a token for `inventory` must not be accepted by `payments`.
- Never trust a header such as `X-User-Id` set by the gateway unless the network path guarantees it and the token is still verified.
- Keep tokens short-lived; cache JWKS with rotation support.

**Show:**
```yaml
spring.security.oauth2.resourceserver.jwt:
  issuer-uri: https://auth.shop.example/realms/shop
```
plus an audience validator.

**Check:** Why validate audience? *(A token meant for one service must not work on another.)*

---

## MID-051-L03 · Scopes, claims, and authorization design (12 min)
**Goal:** design fine-grained authorization.

**Key points**
- Scopes describe what a client may do (`orders:read`, `inventory:write`); claims describe who the user is (subject, roles, tenant).
- Authorization has layers: scope (may this client call this API?), role (may this user do this kind of action?), and ownership or attribute checks (is this their order?).
- Keep tokens small; put stable facts in claims, look up changing permissions in the service.
- Least privilege: admin operations need their own scope.
- Test authorization as code (negative tests).

**Show:** matrix: endpoint | scope | role | ownership check.

**Check:** Which check stops customer A reading customer B's order? *(The ownership check.)*

---

## MID-051-L04 · Service-to-service identity (10 min)
**Goal:** identify calling services safely.

**Key points**
- Client credentials: `orders` has its own client id and secret (stored in a secrets manager) and gets a token for `inventory`.
- Token exchange: swap the user's token for a narrower token for the next service, keeping the user as subject.
- Choose: acting as the service (background, system tasks) versus acting for the user (user-specific data).
- One all-powerful service account is a common mistake; give each service only the scopes it needs.
- mTLS can add transport identity; it complements, not replaces, token checks.

**Show:** diagram: user → gateway → `orders` → (exchange) → `inventory`, with token subject and audience at each hop.

**Check:** Why not one shared service account? *(One leak exposes everything and nothing is traceable.)*

---

## MID-051-L05 · Demo: propagating identity from gateway to inventory (12 min)
**Goal:** pass identity safely across three hops. Prepares `MID-051-LAB1`.

**Steps**
1. Show the gateway validating the user token and forwarding it.
2. Configure `orders` as a resource server; call `inventory` with client credentials for stock checks.
3. Configure `inventory` to require its own scope and audience.
4. **Planned mistake:** `inventory` trusts an `X-User-Id` header; call it directly with curl and a forged header: it works. Fix by validating tokens.
5. Call each service directly without a token: all return 401.
6. Show an admin endpoint rejecting a token that lacks the admin scope (403).
