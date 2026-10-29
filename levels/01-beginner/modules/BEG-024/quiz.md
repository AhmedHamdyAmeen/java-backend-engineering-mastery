# BEG-024 · Abstract classes and interfaces — Quiz

Outcomes: O1 interfaces · O2 abstract classes · O3 choosing · O4 default methods.

**Q01 (O1)** A class uses an interface with the keyword: A. `extends` B. `uses` C. `implements` D. `abstract`
**Q02 (O1)** A class can implement: A. Many interfaces B. At most two C. Only one interface D. None
**Q03 (O1)** Interface methods are by default: A. `private` B. `protected` C. package-private D. `public`
**Q04 (O2)** You can create an object of an abstract class with `new`: A. Yes, always B. No C. Only if it has no fields D. Only in `main`
**Q05 (O2)** An abstract class can contain: A. Only abstract methods B. Only static methods C. Nothing D. Fields, constructors, and abstract and normal methods
**Q06 (O3)** Two unrelated classes need a shared capability. Use: A. Interface B. Abstract class C. `final` class D. `static` field
**Q07 (O3)** Closely related classes share fields and code. Prefer: A. A `static` method B. Nothing C. Abstract class D. A `null` reference
**Q08 (O4)** A `default` method: A. Has no body B. Has a body inside the interface C. Is private to the class D. Cannot be overridden
**Q09 (O4)** A main reason for default methods is to: A. Slow code B. Hide data C. Remove polymorphism D. Add methods to interfaces without breaking implementers
**Q10 (O3)** "Program to an interface" means: A. Declare variables with the interface type B. Never write classes C. Use only `static` D. Avoid `new`

## Answers
Q01 C · Q02 A · Q03 D · Q04 B · Q05 D · Q06 A · Q07 C · Q08 B · Q09 D · Q10 A

## Practical part
Four exercises plus the design question (`BEG-024-EX01` to `EX05`) and the notification lab. Pass: at least four of five correct and the bank class depends only on `Notifier`.
