# JNR-036 · Spring Security — Lecture scripts

**Video:** 84 min · **Analogy used throughout:** a series of security desks a visitor must pass before reaching the office.
Format: **Goal** · **Key points** · **Show** · **Check**.

Note: verify the Spring Security major version and API names before recording; examples use the lambda DSL of current versions.

---

## JNR-036-L01 · Filters and the security filter chain (12 min)
**Goal:** explain where Spring Security sits in a web request.

**Key points**
- A servlet filter is code that runs before (and after) a controller for every request.
- Spring Security adds one big filter, which holds its own ordered list of security filters: the security filter chain.
- Each filter has one job: read credentials, check a session or token, check access, handle errors.
- If a filter rejects the request, the controller never runs.
- Order matters: the first matching rule decides.

**Show:** a diagram: Request → Security filters → `DispatcherServlet` → Controller.

**Check:** If a security filter rejects a request, does the controller run? *(No.)*

---

## JNR-036-L02 · Configuring `SecurityFilterChain` (12 min)
**Goal:** write request rules in a `SecurityFilterChain` bean.

**Key points**
- Define a `@Bean SecurityFilterChain` that takes an `HttpSecurity`.
- Use `authorizeHttpRequests` with `requestMatchers(...)` to say who may call what.
- Rules are checked top to bottom; put specific rules first and `anyRequest()` last.
- End with `anyRequest().authenticated()` or `denyAll()`, not `permitAll()`.
- For a stateless JSON API, you usually turn off sessions and form login; CSRF is covered in a later lecture.

**Show**
```java
@Bean
SecurityFilterChain api(HttpSecurity http) throws Exception {
    http.authorizeHttpRequests(a -> a
        .requestMatchers(HttpMethod.GET, "/api/products/**").permitAll()
        .requestMatchers(HttpMethod.POST, "/api/products/**").hasRole("ADMIN")
        .anyRequest().authenticated())
      .httpBasic(Customizer.withDefaults());
    return http.build();
}
```

**Check:** Where must `anyRequest()` go? *(Last.)*

---

## JNR-036-L03 · Users from the database (10 min)
**Goal:** authenticate against users stored in the Shop database.

**Key points**
- `UserDetailsService` has one method: `loadUserByUsername`. It returns a `UserDetails` (name, password hash, authorities).
- Load the user with a repository; throw `UsernameNotFoundException` if missing.
- Spring Security compares the submitted password with the stored hash using a `PasswordEncoder`.
- Map your role column to authorities; `hasRole("ADMIN")` looks for `ROLE_ADMIN`.
- Never store plain passwords (next module covers hashing).

**Show**
```java
@Service
class DbUserDetailsService implements UserDetailsService {
    public UserDetails loadUserByUsername(String email) {
        var u = users.findByEmail(email).orElseThrow(() -> new UsernameNotFoundException("no user"));
        return User.withUsername(u.getEmail()).password(u.getPasswordHash())
                   .roles(u.getRole()).build();
    }
}
```

**Check:** What does `hasRole("ADMIN")` look for? *(The authority `ROLE_ADMIN`.)*

---

## JNR-036-L04 · 401 vs 403 and error bodies (8 min)
**Goal:** return the right status with a clear Problem Details body.

**Key points**
- 401 Unauthorized: "I do not know who you are" (missing or bad credentials). Despite the name, it is about authentication.
- 403 Forbidden: "I know who you are, but you may not do this."
- Configure `authenticationEntryPoint` for 401 and `accessDeniedHandler` for 403.
- Return `application/problem+json` using `ProblemDetail` so errors match the rest of the API.
- Do not leak detail: no stack traces, no "user does not exist".

**Show:** a `ProblemDetail.forStatusAndDetail(HttpStatus.FORBIDDEN, "Access denied")` written to the response in the handler.

**Check:** Anonymous user calls a protected endpoint. 401 or 403? *(401.)*

---

## JNR-036-L05 · Testing security (10 min)
**Goal:** write tests for secured endpoints.

**Key points**
- Add the Spring Security test dependency.
- `@WithMockUser(roles = "ADMIN")` runs a test as a fake user.
- With MockMvc, `SecurityMockMvcRequestPostProcessors` can set a user or a JWT per request.
- Always test three cases: anonymous, wrong role, right role.
- A test of "anonymous gets 401" would have caught a forgotten `permitAll`.

**Show**
```java
@Test @WithMockUser(roles = "CUSTOMER")
void customerCannotCreateProduct() throws Exception {
    mvc.perform(post("/api/products").contentType(APPLICATION_JSON).content("{}"))
       .andExpect(status().isForbidden());
}
```

**Check:** Which three callers should every endpoint be tested with? *(Anonymous, a user without the role, a user with the role.)*

---

## JNR-036-L06 · Reading Spring Security's debug output (8 min)
**Goal:** find out why a request was rejected.

**Key points**
- Set `logging.level.org.springframework.security=DEBUG` locally only.
- The log shows which filters ran and which rule matched.
- Look for "Securing GET /..." and the authorization decision.
- Never leave debug logging on in production; it can expose request details.
- Check rule order first when behavior surprises you.

**Show:** a short log excerpt with "Securing POST /api/products" followed by "Access Denied".

**Check:** Where should debug security logging be enabled? *(Only in local development.)*

---

## JNR-036-L07 · Demo: securing the Shop API endpoint by endpoint (12 min)
**Goal:** apply the rules to every Shop endpoint. Prepares `JNR-036-LAB1`.

**Steps**
1. Add the Spring Security starter and see every endpoint become locked (401).
2. Write the chain: catalog `GET` public, cart and orders authenticated, catalog writes admin only.
3. Add `DbUserDetailsService` and seed one customer and one admin.
4. **Planned mistake:** put `.anyRequest().permitAll()` while debugging and forget it. Fix: replace with `authenticated()` and add a test that fails if an endpoint is open.
5. Add the 401 and 403 handlers with Problem Details.
6. Call each endpoint with curl as anonymous, customer, and admin.

---

## JNR-036-L08 · Demo: testing the access matrix (12 min)
**Goal:** prove the rules with a test for every endpoint and role. Prepares `JNR-036-LAB1`.

**Steps**
1. Write a table: endpoint × anonymous/customer/admin → expected status.
2. Turn it into a parameterized test with MockMvc.
3. Run it and see all green.
4. **Planned mistake:** put a broad `permitAll` rule before a `hasRole("ADMIN")` rule; the admin-only test fails because the first match wins. Fix: reorder.
5. Commit the matrix test as the safety net for later changes.
