# MID-010 · Java module system — Quiz

Outcomes: O1 module descriptors · O2 classpath vs module path · O3 JPMS decision and alternatives.

**Q01 (O1)** Which keyword makes a package available to other modules? A. `requires` B. `opens` C. `exports` D. `uses`
**Q02 (O1)** `requires transitive` means: A. Dependents also read that module B. The module is optional C. The module is deleted D. Only tests use it
**Q03 (O1)** `module-info.java` belongs: A. In `META-INF` B. At the root of the source tree C. In the `lib` folder D. In `application.yml`
**Q04 (O1)** `exports com.x.api to com.y` means: A. Anyone can access B. Nobody can access C. Only `com.y` can access D. Reflection is open
**Q05 (O2)** Strong encapsulation means: A. Private fields are encrypted B. Public classes in non-exported packages are inaccessible to other modules C. All code is final D. The classpath is faster
**Q06 (O2)** The classpath, compared with the module path, is: A. Explicit about dependencies B. Strongly encapsulated C. Flat, and any public class is visible D. Removed from Java 9
**Q07 (O3)** `InaccessibleObjectException` at startup usually calls for: A. `opens` for the package B. A bigger heap C. A new JDK only D. `final` fields
**Q08 (O3)** A frequent reason to avoid JPMS in a Spring Boot service is: A. Spring forbids modules B. Deep reflection and library gaps raise the cost C. Java 9 is missing D. Modules slow the GC
**Q09 (O3)** A cheap tool to enforce package-level boundaries: A. Docker B. `javap` C. ArchUnit D. `jcmd`
**Q10 (O3)** An ArchUnit rule violation will: A. Fail the test, and so the build B. Be silently ignored C. Restart the server D. Delete the class

## Answers
Q01 C · Q02 A · Q03 B · Q04 C · Q05 B · Q06 C · Q07 A · Q08 B · Q09 C · Q10 A

## Practical part
Six exercises `MID-010-EX01` to `EX06` plus the lab. Pass: at least five exercises correct, eight of ten quiz questions right, and the lab where a forbidden dependency fails the build.
