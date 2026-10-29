# MID-004 · Thread safety — Quiz

Outcomes: O1 races · O2 visibility and happens-before · O3 choosing tools · O4 immutability and deadlocks.

**Q01 (O1)** `if (stock > 0) stock--;` on shared state is an example of: A. Atomic update B. Immutability C. Visibility only D. Check-then-act race
**Q02 (O1)** `count++` is unsafe because it is: A. Three steps, not atomic B. A method call C. Always cached D. Static
**Q03 (O2)** Which creates a happens-before edge? A. Two plain writes B. A `volatile` write then read C. A comment D. Local variables
**Q04 (O2)** A plain flag read in a loop may: A. Always be seen at once B. Throw an error C. Never be seen as changed D. Become final
**Q05 (O3)** `volatile` alone is enough for: A. A stop flag B. A counter C. Check-then-act D. Two-field invariants
**Q06 (O3)** For a single lock-free counter, prefer: A. `synchronized` on `this` B. `AtomicInteger` or `LongAdder` C. `volatile int` D. A plain `int`
**Q07 (O3)** `ReentrantLock` is chosen over `synchronized` mainly to get: A. Speed always B. Memory savings C. Automatic unlock D. `tryLock` with timeout
**Q08 (O3)** Where does `lock.unlock()` belong? A. After the try block only B. In `finally` C. In a constructor D. Nowhere
**Q09 (O4)** A safe lock object is: A. A `String` literal B. `this` in a public class C. A private final `Object` D. A boxed `Integer`
**Q10 (O4)** Deadlock from opposite lock order is prevented by: A. Adding `volatile` B. Raising priority C. More threads D. A global lock ordering

## Answers
Q01 D · Q02 A · Q03 B · Q04 C · Q05 A · Q06 B · Q07 D · Q08 B · Q09 C · Q10 D

## Practical part
Five exercises `MID-004-EX01` to `EX05` (the five concurrency-bug snippets) plus the lab. Pass: at least four snippets correct and a stress test that fails before and passes after each of the three fixes.
