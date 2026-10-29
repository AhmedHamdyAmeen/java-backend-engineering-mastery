# BEG-038 · Java memory basics — Lecture scripts

**Video:** 43 min · **Analogy used throughout:** a desk (stack) holding sticky notes, and a warehouse (heap) holding the real objects; a note holds the shelf address.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-038-L01 · Stack and heap: a picture (12 min)
**Goal:** draw where things live.

**Key points**
- The stack holds one frame per running method call. A frame holds that method's local variables.
- When the method ends, its frame disappears.
- Primitives (`int`, `double`) live directly in the frame.
- Objects live on the heap. A variable of object type holds a reference (an address) to the object.
- `new` creates an object on the heap.

**Show**
```java
public static void main(String[] args) {
    int age = 30;
    String name = new String("Ana");
}
```
Diagram: frame `main` with `age = 30` and `name -> [String "Ana"]` in the heap.

**Check:** Where does the object created by `new` live? *(On the heap.)*

---

## BEG-038-L02 · References and aliasing (10 min)
**Goal:** understand shared objects.

**Key points**
- Assigning `b = a` copies the reference, not the object. Now both point to one object.
- This is aliasing: changing the object through `a` shows through `b`.
- Passing an object to a method passes a copy of the reference; the method can change the same object.
- Primitives are copied by value; changes do not travel.
- `==` compares references; `.equals` compares content. `null` means "points to nothing".

**Show**
```java
List<String> a = new ArrayList<>();
List<String> b = a;
b.add("x");
System.out.println(a.size()); // 1
```

**Check:** After `b = a`, how many objects exist? *(One, with two references.)*

---

## BEG-038-L03 · Garbage collection, gently (8 min)
**Goal:** know when memory is freed.

**Key points**
- Java frees heap objects automatically; this is garbage collection (GC).
- An object is eligible when nothing can reach it any more: no reference from any running code.
- Setting a variable to `null`, or a method ending, can remove the last reference.
- You do not decide when GC runs. `System.gc()` is only a hint, not a command.
- You do not call `free`; but you can still leak memory by keeping references you no longer need (for example in a growing static list).

**Show:** a diagram where an object loses its last arrow and is marked for collection.

**Check:** Does `System.gc()` free memory on demand? *(No, it is only a request.)*

---

## BEG-038-L04 · `OutOfMemoryError` and `StackOverflowError` (5 min)
**Goal:** recognise the two memory errors.

**Key points**
- `StackOverflowError`: too many nested calls, usually infinite recursion. The stack is full.
- `OutOfMemoryError`: the heap is full of reachable objects.
- Both are `Error`s, not normal exceptions.
- Fix the cause: add a stopping condition, or stop keeping data you do not need.
- Memory size options and leak hunting come in later levels.

**Show**
```java
static void loop() { loop(); } // StackOverflowError
```

**Check:** Which error does infinite recursion cause? *(`StackOverflowError`.)*

---

## BEG-038-L05 · Demo: drawing stack and heap, then checking in the debugger (8 min)
**Goal:** verify a diagram with the debugger. Prepares `BEG-038-LAB1`.

**Steps**
1. Write a short program: create a `List`, assign it to a second variable, add through one, call a method that adds again.
2. Draw the stack frames and the heap on paper before running.
3. Set a breakpoint and step; watch the variables panel and compare with the drawing.
4. **Planned mistake:** the drawing shows two lists; the debugger shows the same object id for both. Correct the diagram.
5. Check what happens to a `null` reference after assigning it.
