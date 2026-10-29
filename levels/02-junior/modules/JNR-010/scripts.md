# JNR-010 · Spring container — Lecture scripts

**Video:** 55 min · **Analogy used throughout:** a hotel front desk that knows every staff member, finds them by badge, and hands out the right one when asked.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-010-L01 · The ApplicationContext (8 min)
**Goal:** explain what the container is and holds.

**Key points**
- The `ApplicationContext` is the Spring container: it creates, wires, and keeps beans.
- A bean is just an object the container manages.
- Startup: find bean definitions, create beans in dependency order, then the app is ready.
- You rarely touch the context directly; you ask for dependencies in constructors.

**Show**
```java
ConfigurableApplicationContext ctx = SpringApplication.run(ShopApiApplication.class, args);
ProductService s = ctx.getBean(ProductService.class); // for the demo only
```

**Check:** Should services call `getBean` themselves? *(No. Declare the dependency in the constructor.)*

---

## JNR-010-L02 · Component scanning and stereotypes (10 min)
**Goal:** say how beans are found and which stereotype to use.

**Key points**
- `@SpringBootApplication` includes component scanning of its own package and sub-packages.
- Stereotypes: `@Component` generic, `@Service` business logic, `@Repository` data access, `@Controller`/`@RestController` web.
- They all create beans; the names add meaning and some extra behavior (`@Repository` translates database exceptions).
- A class outside the scanned packages is not found.

**Show:** `com.shop.api.ShopApiApplication` scans `com.shop.api.**`; a class in `com.shop.other` is missed.

**Check:** Where must the main class live? *(In the top package above all your code.)*

---

## JNR-010-L03 · `@Configuration` and `@Bean` (10 min)
**Goal:** register beans you cannot annotate.

**Key points**
- Use `@Bean` methods when the class is third-party or needs set-up code.
- Put them in a class marked `@Configuration`.
- The method name is the bean name; the return type is the bean type.
- Parameters of a `@Bean` method are injected like constructor parameters.

**Show**
```java
@Configuration
class AppConfig {
    @Bean Clock clock() { return Clock.systemUTC(); }
}
```

**Check:** When `@Bean` instead of `@Component`? *(When you cannot edit the class, or it needs custom construction.)*

---

## JNR-010-L04 · Bean scopes (8 min)
**Goal:** pick singleton or prototype.

**Key points**
- Singleton (default): one shared instance per container.
- Prototype: a new instance each time it is requested.
- Web scopes (request, session) exist; use them rarely.
- Almost all Shop beans are singletons.
- A prototype injected into a singleton is created only once, at injection time.

**Show**
```java
@Component @Scope("prototype") class ReportBuilder {}
```

**Check:** What is the default scope? *(Singleton.)*

---

## JNR-010-L05 · Stateless singletons and thread safety (9 min)
**Goal:** explain why singletons must not hold request state.

**Key points**
- One singleton serves many requests at the same time, on many threads.
- A mutable field (a counter, "current user") is shared by all of them: races and wrong data.
- Keep singletons stateless: only `final` dependencies, data in method variables.
- State that must be shared belongs in a database or a thread-safe type, handled later.

**Show**
```java
@Service class BadService { private int lastTotal; /* shared across requests! */ }
```

**Check:** Why is `private int lastTotal` in a service a bug? *(Many requests share and overwrite it.)*

---

## JNR-010-L06 · Demo: injecting a `Clock` to test time-dependent logic (10 min)
**Goal:** make "is the sale active now?" testable; prepares JNR-010-LAB1.

**Steps**
1. Show `PromotionService` calling `LocalDate.now()`; the test passes only on certain days.
2. Add a `Clock` bean in a `@Configuration` class.
3. Inject `Clock` through the constructor and use `LocalDate.now(clock)`.
4. **Planned mistake:** leave one static `Instant.now()` in another service; the test still flakes. Fix: search for `now()` and replace.
5. In the test use `Clock.fixed(...)` and assert both sides of the deadline.
