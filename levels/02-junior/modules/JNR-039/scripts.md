# JNR-039 · OAuth 2.0 and OIDC basics — Lecture scripts

**Video:** 74 min · **Analogy used throughout:** a hotel valet key: it opens the car and starts it, but not the trunk or glovebox, and the owner never hands over the master key.
Format: **Goal** · **Key points** · **Show** · **Check**.

Note: verify the Keycloak and Spring Security versions, and current OAuth 2.0 best-practice guidance, before recording.

---

## JNR-039-L01 · The problem OAuth solves (8 min)
**Goal:** explain why we need delegated access.

**Key points**
- Old way: give a third-party app your password so it can read your data. That gives it everything, forever.
- OAuth 2.0 lets an app get limited, revocable access without ever seeing the password.
- The user logs in at a trusted server, which hands the app a token with limited scope.
- OAuth is about authorization (what an app may do), not about proving who the user is.
- It also lets many apps share one login system.

**Show:** two pictures: "give the app my password" versus "app gets a token with scope `orders:read`".

**Check:** Does the third-party app ever see the user's password in OAuth? *(No.)*

---

## JNR-039-L02 · Roles and tokens (8 min)
**Goal:** name the four roles and the tokens.

**Key points**
- Resource owner: the user who owns the data.
- Client: the app that wants access.
- Authorization server: logs the user in and issues tokens (for example Keycloak).
- Resource server: the API that accepts tokens (our Shop API).
- Access token: sent to the API. Refresh token: gets new access tokens. Scopes describe what is allowed.

**Show:** a four-box diagram with arrows: user → client → authorization server → token → resource server.

**Check:** Which role is the Shop API? *(Resource server.)*

---

## JNR-039-L03 · Authorization code + PKCE (12 min)
**Goal:** follow the flow used by web, mobile, and single-page apps.

**Key points**
- The client sends the user's browser to the authorization server to log in and approve.
- The server returns a short-lived authorization code to the client's redirect URL.
- The client swaps the code for tokens at the token endpoint.
- PKCE: the client invents a secret (`code_verifier`), sends its hash (`code_challenge`) first, then proves it with the verifier. A stolen code is then useless.
- Use this flow whenever a user logs in; current guidance recommends PKCE for all clients. The implicit grant and the password grant are not for new systems.

**Show:** a sequence diagram of the steps above with `code_challenge` and `code_verifier` marked.

**Check:** What problem does PKCE solve? *(A stolen authorization code cannot be exchanged without the verifier.)*

---

## JNR-039-L04 · Client credentials (7 min)
**Goal:** use the flow for service-to-service calls.

**Key points**
- No user is involved: a service proves itself with its own client ID and secret.
- It gets an access token for its own permissions.
- Use it for back-end jobs, such as Shop calling an internal service.
- Keep the client secret in a secret store, not in source control.
- If a user is acting, use authorization code instead.

**Show:** one request: `POST /token` with `grant_type=client_credentials` and the client's credentials.

**Check:** When is client credentials the right flow? *(Machine-to-machine, when no user is involved.)*

---

## JNR-039-L05 · OIDC: adding login (8 min)
**Goal:** tell OAuth 2.0 and OpenID Connect apart.

**Key points**
- OIDC (OpenID Connect) is a thin layer on top of OAuth 2.0 that adds login.
- It adds an ID token (a JWT) that tells the client who logged in.
- The ID token is for the client app. Never send it to an API as an access token.
- OIDC also adds a `userinfo` endpoint and standard scopes like `openid` and `profile`.
- OAuth: "what may this app do?" OIDC: "who just logged in?"

**Show:** a table: access token vs ID token: audience, purpose, who reads it.

**Check:** Which token proves who logged in, for the client? *(The ID token.)*

---

## JNR-039-L06 · Spring as a resource server (7 min)
**Goal:** make the Shop API trust an external authorization server.

**Key points**
- Add the OAuth2 resource server starter.
- Set `spring.security.oauth2.resourceserver.jwt.issuer-uri`; Spring discovers the keys from the issuer.
- Spring validates signature, issuer, and expiry; add an audience check as extra validation.
- Map token claims (such as Keycloak realm roles) to Spring authorities with a `JwtAuthenticationConverter`.
- The API never handles passwords.

**Show**
```yaml
spring:
  security:
    oauth2:
      resourceserver:
        jwt:
          issuer-uri: http://localhost:8081/realms/shop
```

**Check:** Where does Spring get the public keys from? *(From the issuer's discovery and JWKS endpoints.)*

---

## JNR-039-L07 · Demo: Keycloak setup and the authorization code + PKCE flow (12 min)
**Goal:** run Keycloak and get tokens with the code flow. Prepares `JNR-039-LAB1`.

**Steps**
1. Start Keycloak locally with Docker; verify image and version before recording.
2. Create a realm `shop`, a client with PKCE enabled, realm roles `customer` and `admin`, and two users.
3. In Postman, use the OAuth 2.0 authorization code with PKCE option and log in.
4. Decode the access token and find `iss`, `aud`, and the roles.
5. **Planned mistake:** a wrong redirect URI in the client setup gives an "invalid redirect" error. Fix: register the exact URI.
6. Compare the access token with the ID token.

---

## JNR-039-L08 · Demo: switching Shop to Keycloak-issued tokens (12 min)
**Goal:** replace self-issued tokens with Keycloak tokens. Prepares `JNR-039-LAB1`.

**Steps**
1. Remove the self-issued login endpoint and key from Shop.
2. Set `issuer-uri` to the Keycloak realm.
3. Add a converter that maps realm roles to `ROLE_` authorities.
4. Call the API with a Keycloak token and see `200` for customer and admin as expected.
5. **Planned mistake:** sending the ID token to the API. Explain why the audience or claims do not fit, and use the access token.
6. Confirm an old self-issued token now returns 401.
