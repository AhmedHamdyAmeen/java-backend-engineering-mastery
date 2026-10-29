# MID-001 · JVM architecture — Exercises and lab

## Lab
### MID-001-LAB1 · Warm-up effect
**Outcomes:** 1–4 · **Time:** ~3 h
Start Shop and send 5,000 checkout requests with a simple load tool, recording each latency. Plot the first 1,000 requests against steady state. Repeat with `-XX:+PrintCompilation` and mark compilation events on the timeline. Explain the curve.
**Acceptance:** chart plus explanation referencing JIT tiers.

## Exercises (assessment: bytecode-reading quiz, a class-loading scenario, and the lab)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-001-EX01 | 1 | Print the class loader of `String`, a Shop class, and `java.sql.Connection`; explain each result. |
| MID-001-EX02 | 2 | Run `javap -c -p` on a class with `total(int,int)` and annotate each instruction. |
| MID-001-EX03 | 2 | Compile `if (qty > 0) return price * qty; else return 0;` and identify the branch instruction. |
| MID-001-EX04 | 3 | Draw the runtime data areas and place: an `Order` object, a local `int`, a class's method table, JIT output. |
| MID-001-EX05 | 4 | Run a timing loop with and without warm-up; explain the difference. |
| MID-001-EX06 | 1 | Scenario: `NoClassDefFoundError` after deploy though the build passed. Give two likely causes. |

## Solutions
- **EX01** `String` gives `null` (bootstrap); the Shop class gives the application loader; `java.sql.Connection` gives the platform loader.
- **EX02** `iload_0`/`iload_1` push arguments, `imul` multiplies, `ireturn` returns the top value.
- **EX03** A conditional jump such as `ifle` skips to the `return 0` path.
- **EX04** Object on heap; local `int` in the thread's stack frame; method table in metaspace; JIT output in the code cache.
- **EX05** The cold loop includes interpretation and compilation; after warm-up the same code is much faster.
- **EX06** A dependency JAR missing from the runtime classpath (compile vs runtime scope mismatch), or a static initializer that threw earlier. `ClassNotFoundException` would instead be a failed by-name lookup.
- Outcome 4 is also covered by the lab and Q09-Q10.
