# MID-001 · JVM architecture — Lecture scripts

**Video:** 68 min · **Analogy used throughout:** a restaurant kitchen: recipes (bytecode) are read by a cook (interpreter), and dishes ordered often get a prepared fast station (JIT).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-001-L01 · From `.class` file to running code (10 min)
**Goal:** trace a Java source file through compilation to execution.

**Key points**
- `javac` turns `.java` into `.class` files holding bytecode, a portable instruction set.
- The JVM loads classes on demand, verifies them, then runs the bytecode.
- Bytecode is not machine code; the JVM interprets it, then compiles hot parts to machine code.
- "Write once, run anywhere" works because the JVM, not your code, is platform-specific.

**Show**
```
Shop.java --javac--> Shop.class --JVM: load, link, init--> interpret / JIT --> CPU
```

**Check:** What does `javac` produce? *(Bytecode in `.class` files, not machine code.)*

---

## MID-001-L02 · Class loading and class loaders (12 min)
**Goal:** explain the three class-loading phases and the loader hierarchy.

**Key points**
- Phases: loading (read bytes), linking (verify, prepare, resolve), initialization (run static initializers).
- Hierarchy: bootstrap (core JDK), platform, application loader; each delegates to its parent first.
- Delegation prevents user code from replacing `java.lang.String`.
- `ClassNotFoundException`: a checked exception when code asks for a class by name and it is not found. `NoClassDefFoundError`: the class was present at compile time but is missing, or failed to initialize, at runtime.
- Frameworks and app servers use custom loaders for isolation.

**Show**
```java
System.out.println(Shop.class.getClassLoader());   // application loader
System.out.println(String.class.getClassLoader()); // null = bootstrap
```

**Check:** Which one is an `Error` raised during linking or use: `ClassNotFoundException` or `NoClassDefFoundError`? *(`NoClassDefFoundError`.)*

---

## MID-001-L03 · Reading bytecode with `javap` (12 min)
**Goal:** read the bytecode of a small method and map it to source.

**Key points**
- `javap -c -p Shop` disassembles a class, including private members.
- The JVM is a stack machine: instructions push and pop an operand stack.
- Common instructions: `iload`, `imul`, `invokevirtual`, `invokestatic`, `ireturn`.
- Local variables sit in numbered slots; slot 0 is `this` in instance methods.
- Lambdas appear as `invokedynamic`; modern JDKs also use it for string concatenation (verify version before recording).

**Show**
```java
static int total(int price, int qty) { return price * qty; }
```
```
iload_0
iload_1
imul
ireturn
```

**Check:** In `total`, what does `imul` consume? *(The two top operand-stack values.)*

---

## MID-001-L04 · Runtime data areas (10 min)
**Goal:** name where each kind of data lives at runtime.

**Key points**
- Heap: all objects and arrays, shared by threads, managed by the GC.
- Thread stacks: one per thread, holding frames with locals and call state.
- Metaspace: class metadata, in native memory (it replaced PermGen).
- Code cache: JIT-compiled machine code.
- There is also other native memory: direct buffers, thread stacks, GC structures. Heap size is not total process size.

**Show:** a diagram: heap and metaspace shared; N stacks; code cache; native memory around it.

**Check:** Where does `new Order()` live? *(On the heap; the reference variable is in a stack frame.)*

---

## MID-001-L05 · The JIT compiler and warm-up (12 min)
**Goal:** explain why performance changes after startup.

**Key points**
- The JVM starts by interpreting; it counts method calls and loop iterations.
- Tiered compilation: C1 compiles quickly with light optimization; C2 compiles hot code with heavy optimization.
- C2 uses profile data (inlining, escape analysis) and can deoptimize if its assumptions break.
- Result: first requests are slow, later ones fast. This is warm-up.
- Benchmarking cold code measures startup, not steady state.

**Show:** a latency curve: high for the first ~1,000 requests, dropping in steps as tiers kick in.

**Check:** Why is the first request slower? *(Code is interpreted and classes are still loading; hot code is not yet compiled.)*

---

## MID-001-L06 · Demo: watching the JIT with `-XX:+PrintCompilation` (12 min)
**Goal:** see compilation events live; prepares MID-001-LAB1.

**Steps**
1. Write a loop calling a small pricing method a million times, timing batches.
2. Run with `-XX:+PrintCompilation`; find the method's lines.
3. Read the tier column (levels 1-4; level 4 is C2) and notice `made not entrant` lines (deoptimization).
4. Print batch timings and match speed-ups to compilation events.
5. **Planned mistake:** time a single cold call and conclude the method is slow. Fix: warm up first, then measure many iterations (or use JMH).
6. Link to the lab: apply the same reasoning to the first 1,000 Shop checkout requests. Output format is version-specific; verify version before recording.
