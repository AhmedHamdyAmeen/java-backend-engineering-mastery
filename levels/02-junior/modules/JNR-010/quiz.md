# JNR-010 · Spring container — Quiz

Outcomes: O1 ApplicationContext and scanning · O2 stereotypes and `@Bean` · O3 scope and thread safety · O4 missing-bean diagnosis.

**Q01 (O1)** The `ApplicationContext` is: A. A database B. The container that creates and wires beans C. A web page D. A test library
**Q02 (O1)** Component scanning finds beans in: A. Every package on the disk B. The main class's package and its sub-packages C. Only `src/test` D. Only classes named `*Bean`
**Q03 (O2)** Best annotation for business logic: A. `@Repository` B. `@Controller` C. `@Configuration` D. `@Service`
**Q04 (O2)** To register a third-party class you cannot edit: A. `@Component` on it B. A `@Bean` method in a `@Configuration` class C. Copy its source D. It is impossible
**Q05 (O2)** `@Repository` additionally: A. Translates persistence exceptions B. Opens HTTP ports C. Makes it a prototype D. Deletes data
**Q06 (O3)** The default scope is: A. Prototype B. Request C. Session D. Singleton
**Q07 (O3)** Why must singleton services be stateless? A. Java forbids fields B. One instance is shared by many concurrent requests C. Spring clears fields D. They run on one thread
**Q08 (O3)** A prototype bean is requested: A. Once per container B. Once per JVM C. A new instance each time it is requested D. Never
**Q09 (O4)** A service in `com.shop.service` is missing and the main class is in `com.shop.app`. Likely cause: A. Wrong Java version B. The package is outside the scanned tree C. Missing getter D. Missing database
**Q10 (O4)** The simplest layout fix: A. Move the main class to the top package above all code B. Add `@Lazy` C. Rename the service D. Add a static `main`

## Answers
Q01 B · Q02 B · Q03 D · Q04 B · Q05 A · Q06 D · Q07 B · Q08 C · Q09 B · Q10 A

## Practical part
Six exercises `JNR-010-EX01` to `EX06` plus the lab. The assessment is the "why is this bean missing?" exercise (EX06). Pass: quiz at least 8/10, EX06 diagnosed with a correct fix, lab acceptance met.
