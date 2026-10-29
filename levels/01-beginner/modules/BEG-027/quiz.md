# BEG-027 · Packages and organization — Quiz

Outcomes: O1 packages and imports · O2 package-private · O3 feature vs layer.

**Q01 (O1)** The package `com.acme.app` maps to the folder: A. `com.acme.app` as one name B. `com/acme/app` C. `app/acme/com` D. Any folder
**Q02 (O1)** The `package` statement must be: A. In a comment B. After the class C. Optional in all cases D. The first statement in the file (before imports)
**Q03 (O1)** Which package needs no import? A. `java.lang` B. `java.io` C. `java.util` D. `java.sql`
**Q04 (O1)** Two classes with the same simple name from different packages: A. Cannot be used B. Rename the JVM C. Import one, use the full name for the other D. Use `static`
**Q05 (O2)** A class declared with no access modifier is visible: A. Only in its own package B. Everywhere C. Only in its file D. Only in subclasses
**Q06 (O2)** A good reason to use package-private: A. Make everything accessible B. Hide implementation helpers C. Speed D. Reduce file size
**Q07 (O2)** The public surface of a package should be: A. As large as possible B. Random C. Empty always D. As small as needed
**Q08 (O3)** Package by feature puts together: A. All controllers B. All interfaces C. All classes for one feature D. All tests only
**Q09 (O3)** A benefit of feature packages: A. More public classes B. Easier to hide internals and to find a feature's code C. No packages at all D. Slower builds
**Q10 (O1)** Using the default package for a real project is: A. Avoided B. Required C. Recommended D. Faster

## Answers
Q01 B · Q02 D · Q03 A · Q04 C · Q05 A · Q06 B · Q07 D · Q08 C · Q09 B · Q10 A

## Practical part
Refactoring exercise `BEG-027-EX05`, the other exercises, and Bank Accounts v5. Pass: project compiles in feature packages and only intended classes are public.
