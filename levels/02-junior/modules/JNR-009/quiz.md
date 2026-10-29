# JNR-009 · IoC and DI — Quiz

Outcomes: O1 IoC and DI · O2 constructor injection · O3 ambiguity · O4 bean lifecycle.

**Q01 (O1)** Inversion of control means: A. Objects are created and connected by someone else B. Code runs backwards C. Classes cannot call each other D. Only static methods are used
**Q02 (O1)** Dependency injection is best described as: A. Copying dependencies into the pom B. Passing a class its collaborators from outside C. Creating them with `new` inside D. Using static fields
**Q03 (O1)** Why program against an interface like `PaymentProvider`? A. It is required by Java B. You can swap implementations and use fakes in tests C. It runs faster D. Interfaces have no methods
**Q04 (O2)** The preferred injection style in Spring is: A. Field injection B. Setter injection only C. Constructor injection D. Static lookup
**Q05 (O2)** A key benefit of constructor injection is: A. Fields can be `final` and the object is complete B. It avoids interfaces C. It needs no beans D. It is slower
**Q06 (O2)** Why is field injection a weakness? A. It hides dependencies and makes plain `new` in tests leave fields null B. It does not work at all C. It needs a database D. It forbids interfaces
**Q07 (O3)** Two beans implement `PaymentProvider` and nothing selects one. What happens? A. Spring picks randomly B. Startup fails with a no-unique-bean error C. The first alphabetically is used silently D. The app starts but throws on first call
**Q08 (O3)** Which annotation marks the default among several beans? A. `@Default` B. `@Qualifier` C. `@Lazy` D. `@Primary`
**Q09 (O4)** Correct bean order: A. Instantiate, inject, initialize, destroy B. Initialize, instantiate, inject, destroy C. Inject, instantiate, destroy, initialize D. Destroy, instantiate, inject, initialize
**Q10 (O4)** Services A and B each need the other via constructors. The best fix: A. Add `@Lazy` everywhere B. Switch to field injection C. Make everything static D. Extract the shared logic into a third class

## Answers
Q01 A · Q02 B · Q03 B · Q04 C · Q05 A · Q06 A · Q07 B · Q08 D · Q09 A · Q10 D

## Practical part
Seven exercises `JNR-009-EX01` to `EX07` plus the lab. The assessment: explain a DI wiring diagram and fix an ambiguous-bean failure. Pass: quiz at least 8/10, diagram explained, failure fixed, lab acceptance met.
