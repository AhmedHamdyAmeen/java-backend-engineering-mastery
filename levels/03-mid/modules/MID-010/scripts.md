# MID-010 · Java module system — Lecture scripts

**Video:** 43 min · **Analogy used throughout:** an office building with badge access: each department (module) lists which rooms are open to others (exports) and who it needs (requires); everything else is locked.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-010-L01 · Classpath problems JPMS solves (8 min)
**Goal:** explain why the Java Platform Module System (JPMS) exists.

**Key points**
- The classpath is a flat list of JARs; any public class is reachable by anyone.
- Problems: missing dependencies found only at runtime, split packages, version conflicts, no real encapsulation.
- JPMS (Java 9) adds explicit dependencies and strong encapsulation.
- The JDK itself is modularized; internal packages are no longer open by default.
- Adoption in application backends is uneven.

**Show:** a diagram: classpath (one flat bag) vs modules (boxes with arrows).

**Check:** What does `public` mean without JPMS? *(Visible to everything on the classpath.)*

---

## MID-010-L02 · Writing module descriptors (10 min)
**Goal:** write a `module-info.java`.

**Key points**
- Place `module-info.java` at the source root; the module name is usually reverse-domain style.
- `requires` declares a dependency; `requires transitive` passes it on to users.
- `exports` makes a package accessible to other modules; unexported packages stay hidden even if public.
- `exports ... to` limits to named modules.
- A JAR with a descriptor on the module path is a module; unnamed or automatic modules cover legacy JARs.

**Show**
```java
module com.shop.core {
    requires java.sql;
    exports com.shop.core.api;
}
```

**Check:** Can another module use a public class in a non-exported package? *(No.)*

---

## MID-010-L03 · Reflection and `opens` (7 min)
**Goal:** explain why frameworks need `opens`.

**Key points**
- `exports` allows compile-time and runtime access to public types; it does not allow deep reflection on private members.
- `opens` allows reflective access at runtime (including `setAccessible`) to a package.
- `open module` opens everything; `opens ... to` targets specific modules.
- Frameworks such as Spring, Hibernate, and Jackson reflect on your classes and need them opened.
- Symptom: `InaccessibleObjectException` at startup.

**Show**
```java
module com.shop.core {
    exports com.shop.core.api;
    opens com.shop.core.model to com.fasterxml.jackson.databind;
}
```

**Check:** Which keyword fixes an `InaccessibleObjectException` caused by reflection? *(`opens`.)*

---

## MID-010-L04 · JPMS in practice for backend services (8 min)
**Goal:** decide whether a Spring service should use JPMS.

**Key points**
- Spring Boot applications mostly run on the classpath; framework reflection, auto-configuration, and many libraries (some without module descriptors) make JPMS costly.
- Benefit is mainly for libraries and some shared modules with clear APIs.
- Alternatives for boundaries: Maven or Gradle multi-module builds, package structure conventions, and ArchUnit rules.
- Check the JPMS support of your framework versions before committing (verify version).
- Choose by cost and benefit, not fashion.

**Show:** a table: Option / enforcement / cost — JPMS: compile and runtime / high with frameworks; multi-module build: compile / medium; ArchUnit: test time / low.

**Check:** Name one cheaper alternative to JPMS for boundaries. *(ArchUnit tests or build modules.)*

---

## MID-010-L05 · Demo: enforcing boundaries with ArchUnit (10 min)
**Goal:** make a forbidden dependency fail the build; prepares MID-010-LAB1.

**Steps**
1. In Shop API, define feature packages: `orders`, `catalog`, `payments`.
2. Add an ArchUnit test: classes in `orders..` must not depend on `payments.internal..`.
3. Run it; it passes on the clean codebase.
4. **Planned mistake:** import a `payments` internal class from `orders`. The test fails with a readable violation. Fix: call the public API of `payments` instead.
5. Add a layering rule (controllers do not access repositories directly); verify the ArchUnit version for the API.
