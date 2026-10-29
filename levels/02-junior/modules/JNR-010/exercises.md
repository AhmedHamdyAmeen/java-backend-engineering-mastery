# JNR-010 · Spring container — Exercises and lab

## Lab
### JNR-010-LAB1 · Third-party beans
**Outcomes:** 1–4 · **Time:** ~2 h
1. Create a `@Configuration` class with `@Bean` methods for a `Clock` and a currency client (a simple third-party-style class).
2. Inject `Clock` into the promotion and order services; replace every `now()` call.
3. Write a test using `Clock.fixed(...)` for a time-dependent rule.
4. Move the main class to a sub-package, observe the missing-bean failure, then fix the layout.
**Acceptance:** no static `now()` calls in services; time-dependent tests are deterministic; the layout failure is explained.

## Exercises (assessment: "why is this bean missing?" debugging exercise)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-010-EX01 | 1 | Print the number of beans and the names starting with `product` from the `ApplicationContext`. |
| JNR-010-EX02 | 2 | For each class choose a stereotype or `@Bean`: `ProductService`, `ProductRepository`, `ProductController`, a third-party `HttpClient`. |
| JNR-010-EX03 | 2 | Write a `@Configuration` class exposing a `Clock` bean and inject it into a service. |
| JNR-010-EX04 | 3 | Add a `private int counter` to a singleton, hit the endpoint twice, and explain the result; then remove the state. |
| JNR-010-EX05 | 3 | Show that two injections of a prototype bean differ and two of a singleton do not (compare references). |
| JNR-010-EX06 | 4 | Given a project whose main class is in `com.shop.app` and a service in `com.shop.service`, explain the startup failure and give two fixes. |

## Solutions
- **EX01** `ctx.getBeanDefinitionCount()` and `Arrays.stream(ctx.getBeanDefinitionNames()).filter(n -> n.startsWith("product"))`.
- **EX02** `@Service`, `@Repository`, `@RestController`, `@Bean` in a `@Configuration`.
- **EX03** `@Bean Clock clock(){ return Clock.systemUTC(); }` and a constructor parameter `Clock clock`.
- **EX04** The counter grows across requests because one instance serves all; keep services stateless.
- **EX05** `a == b` is true for singletons and false for prototypes.
- **EX06** The service package is outside `com.shop.app`, so it is not scanned: `NoSuchBeanDefinitionException`. Fix: move the main class to `com.shop`, or set `scanBasePackages` (the first is preferred).
