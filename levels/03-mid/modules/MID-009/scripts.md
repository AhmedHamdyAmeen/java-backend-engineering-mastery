# MID-009 · Advanced generics and reflection — Lecture scripts

**Video:** 60 min · **Analogy used throughout:** shipping labels: generics are labels checked at the warehouse door (compile time) and thrown away on the truck (erasure); reflection is opening the box to read what is inside; a proxy is a courier who signs for the parcel and adds a stamp.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-009-L01 · Type erasure (10 min)
**Goal:** explain what generics are at runtime and the consequences.

**Key points**
- Generic type arguments are checked at compile time, then erased; at runtime `List<String>` is a `List`.
- Consequences: no `new T()`, no `instanceof List<String>`, no generic arrays, no overloads differing only in type arguments.
- The compiler inserts casts and generates bridge methods to keep overriding working.
- Heap pollution: raw types or unchecked casts let a wrong element enter a list; the failure appears later as `ClassCastException`.
- Workaround for runtime type info: pass a `Class<T>` token.

**Show**
```java
static <T> T create(Class<T> type) throws Exception {
    return type.getDeclaredConstructor().newInstance(); // instead of new T()
}
```

**Check:** Why does `new T()` not compile? *(`T` is erased; the JVM does not know the class at runtime.)*

---

## MID-009-L02 · Wildcards and PECS (10 min)
**Goal:** write flexible generic method signatures.

**Key points**
- `List<Integer>` is not a `List<Number>`: generics are invariant.
- `? extends T`: a producer; you can read `T`, not add.
- `? super T`: a consumer; you can add `T`, reading gives `Object`.
- PECS: Producer Extends, Consumer Super.
- Do not use wildcards in return types; they burden callers.

**Show**
```java
static <T> void copy(List<? extends T> src, List<? super T> dst) {
    for (T t : src) dst.add(t);
}
```

**Check:** What does PECS stand for? *(Producer Extends, Consumer Super.)*

---

## MID-009-L03 · Reflection (10 min)
**Goal:** inspect and invoke code at runtime.

**Key points**
- `Class<?>` gives fields, methods, constructors, annotations, and modifiers.
- Invoke with `Method.invoke`; read fields with `Field.get` (needs `setAccessible(true)` for private members, and may be blocked by modules).
- Frameworks use it for dependency injection, serialization, and mapping.
- Costs: slower than direct calls, bypasses compile-time checks, and can break encapsulation.
- Avoid in hot paths; cache `Method` objects or use `MethodHandle`.

**Show**
```java
for (Method m : Product.class.getDeclaredMethods()) {
    System.out.println(m.getName() + " " + m.getReturnType());
}
```

**Check:** Why avoid reflection in hot loops? *(Slower, and checks move from compile time to runtime.)*

---

## MID-009-L04 · Custom annotations (8 min)
**Goal:** define and read a runtime annotation.

**Key points**
- Declare with `@interface`; elements look like methods.
- Meta-annotations: `@Retention(RUNTIME)` so reflection can see it; `@Target` limits where it applies.
- Without RUNTIME retention the annotation is invisible at runtime.
- Read with `method.isAnnotationPresent` or `getAnnotation`.
- Frameworks pair annotations with reflection or proxies.

**Show**
```java
@Retention(RetentionPolicy.RUNTIME) @Target(ElementType.METHOD)
@interface Audited { String action() default ""; }
```

**Check:** What happens with `@Retention(SOURCE)`? *(The annotation is dropped before runtime, so reflection cannot see it.)*

---

## MID-009-L05 · Dynamic proxies (10 min)
**Goal:** explain how Spring adds behavior around beans.

**Key points**
- `java.lang.reflect.Proxy` creates an object implementing interfaces; each call goes to an `InvocationHandler`.
- The handler can add behavior (timing, transactions) and call the real object.
- Spring uses JDK proxies for interfaces and CGLIB subclass proxies for classes (verify details for your Spring version).
- Only calls through the proxy are intercepted. A call from one method to another on `this` bypasses it, so `@Transactional` self-invocation does not start a transaction.
- Fix: move the method to another bean, or inject the proxy.

**Show**
```java
Svc proxy = (Svc) Proxy.newProxyInstance(loader, new Class<?>[]{Svc.class},
    (p, m, args) -> { log(m); return m.invoke(target, args); });
```

**Check:** Why does `this.save()` skip `@Transactional`? *(`this` is the raw object, not the proxy.)*

---

## MID-009-L06 · Demo: building a mini `@Timed` with a proxy (12 min)
**Goal:** build an annotation-driven interceptor; prepares MID-009-LAB1.

**Steps**
1. Define `@Timed` (RUNTIME, METHOD) and an interface `PriceService` with an implementation.
2. Write a `Proxy.newProxyInstance` handler that checks the annotation on the target method and logs elapsed time.
3. Call through the proxy; see the timing log.
4. **Planned mistake:** annotate only the interface method and read the annotation from the implementation class (not found). Fix: look up the annotation on the target class method (and note Spring's own lookup rules).
5. Add an internal call between two methods; show it is not timed (self-invocation).
6. Discuss reflection cost and caching `Method` lookups.
