# MID-001 · JVM architecture — Quiz

Outcomes: O1 class loading · O2 bytecode · O3 data areas · O4 JIT and warm-up.

**Q01 (O1)** The three class-loading phases are: A. Compile, link, run B. Parse, load, execute C. Load, link, initialize D. Verify, compile, run
**Q02 (O1)** Which loader loads `java.lang.String`? A. Application B. Platform C. Custom D. Bootstrap
**Q03 (O1)** A class compiled fine but is absent at runtime. You typically get: A. `NoClassDefFoundError` B. `ClassNotFoundException` always C. A compile error D. Nothing
**Q04 (O1)** `Class.forName("x.Missing")` with no such class throws: A. `NoClassDefFoundError` B. `ClassNotFoundException` C. `NullPointerException` D. `OutOfMemoryError`
**Q05 (O2)** The JVM executes bytecode using an: A. Operand stack model B. Register file only C. Heap-only model D. SQL engine
**Q06 (O2)** `iload_0; iload_1; iadd; ireturn` returns: A. A difference B. The product C. The sum D. A comparison result
**Q07 (O3)** Class metadata lives in: A. Young generation B. A thread stack C. Metaspace D. Code cache
**Q08 (O3)** JIT-compiled machine code lives in: A. Heap B. Metaspace C. Stack D. Code cache
**Q09 (O4)** In tiered compilation, which compiler applies the heaviest optimization? A. Interpreter B. C2 C. C1 D. `javac`
**Q10 (O4)** First requests after startup are slow mainly because: A. Code is interpreted and not yet compiled B. The network is cold C. The GC is disabled D. Bytecode is encrypted

## Answers
Q01 C · Q02 D · Q03 A · Q04 B · Q05 A · Q06 C · Q07 C · Q08 D · Q09 B · Q10 A

## Practical part
Six exercises `MID-001-EX01` to `EX06` plus the lab with its chart. Pass: at least five exercises correct and a lab explanation that names the JIT tiers.
