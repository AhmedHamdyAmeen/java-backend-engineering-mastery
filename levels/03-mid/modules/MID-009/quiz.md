# MID-009 · Advanced generics and reflection — Quiz (proxy behavior)

Outcomes: O1 erasure · O2 PECS · O3 reflection and annotations · O4 proxies and Spring.

**Q01 (O1)** At runtime `List<String>` is seen as: A. `List<String>` B. `List<Object>` only in Java 21 C. A different class from `List<Integer>` D. A plain `List`
**Q02 (O1)** Which does not compile? A. `new T()` for type parameter `T` B. `new ArrayList<String>()` C. `List<?>` D. `Class<T>` parameter
**Q03 (O1)** Heap pollution typically shows up as: A. A compile error B. A later `ClassCastException` C. A GC pause D. A missing import
**Q04 (O2)** For a source you only read from, use: A. `? super T` B. Raw type C. `? extends T` D. `Object`
**Q05 (O2)** For a destination you add `T` to, use: A. `? extends T` B. `? super T` C. `?` D. Raw type
**Q06 (O3)** An annotation readable by reflection needs: A. `@Retention(RUNTIME)` B. `@Retention(SOURCE)` C. `@Deprecated` D. `final`
**Q07 (O3)** A fair concern about reflection is: A. It cannot read methods B. It is blocked on all classes C. It is slower and loses compile-time checks D. It requires Java 5
**Q08 (O4)** A JDK dynamic proxy requires the target to implement: A. An interface B. `Serializable` C. A superclass D. `Runnable`
**Q09 (O4)** `this.save()` inside a Spring bean with `@Transactional` on `save`: A. Always starts a transaction B. Throws at startup C. Calls the proxy D. Bypasses the proxy, so no transaction is started
**Q10 (O4)** Which gives annotation-driven behavior around calls in Spring? A. Proxies B. Static initializers C. Garbage collection D. The classpath

## Answers
Q01 D · Q02 A · Q03 B · Q04 C · Q05 B · Q06 A · Q07 C · Q08 A · Q09 D · Q10 A

## Practical part
Six exercises `MID-009-EX01` to `EX06` plus the lab. Pass: at least five exercises correct, at least eight of the ten quiz questions right, and the lab showing the self-invocation limitation.
