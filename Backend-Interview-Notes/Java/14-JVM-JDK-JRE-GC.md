# 14. JVM, JDK, JRE & Garbage Collection

> 🟡 **Level:** Intermediate | 🔥 **Interview Frequency:** Very High

---

## 🧠 Concept

- **JDK** (Java Development Kit) → tools to **write + compile + run** Java. (JDK = JRE + compiler + tools)
- **JRE** (Java Runtime Environment) → tools to **run** Java. (JRE = JVM + libraries)
- **JVM** (Java Virtual Machine) → actually **runs** the bytecode. Makes Java **platform independent**.

```
JDK ⊃ JRE ⊃ JVM
```

---

## 💬 Simple Explanation

- **JVM** = the engine that runs your code.
- **JRE** = engine + fuel + parts needed to run (but can't build).
- **JDK** = full garage: build + run everything.

---

## 🗺️ How Java Runs (Very Important!)

```
Source.java  --javac-->  Bytecode (.class)  --JVM-->  Machine code
                          (platform independent)      (runs anywhere)
```

**"Write Once, Run Anywhere"** — bytecode runs on any OS that has a JVM.

---

## 🧩 JVM Architecture

```
┌──────────────── JVM ────────────────┐
│ 1. ClassLoader   (loads .class)      │
│ 2. Memory Areas:                     │
│    - Heap    (objects)               │
│    - Stack   (method calls, locals)  │
│    - Method Area (class metadata)    │
│    - PC Register, Native Stack       │
│ 3. Execution Engine                  │
│    - Interpreter                     │
│    - JIT Compiler (speeds up)        │
│    - Garbage Collector               │
└──────────────────────────────────────┘
```

- **Heap** → where all objects live (shared).
- **Stack** → each thread's method calls & local variables.
- **JIT (Just-In-Time)** compiler → converts hot bytecode to native code for speed.

---

## ♻️ Garbage Collection (GC)

Java **automatically frees memory** of objects no longer used. No manual `free()` like C++.

An object becomes eligible for GC when **nothing references it**.

```java
Student s = new Student();
s = null;   // old object now has no reference → eligible for GC
```

### Heap Generations

```
Young Generation → Eden + Survivor (new objects, minor GC)
Old Generation   → long-lived objects (major GC)
```

- Most objects **die young** → cleaned in the Young Gen quickly.
- Survivors move to **Old Gen**.

### GC Algorithms
| GC | Notes |
|----|-------|
| Serial GC | Single thread, small apps |
| Parallel GC | Multiple threads (throughput) |
| G1 GC | Default (Java 9+), balanced |
| ZGC / Shenandoah | Very low pause, large heaps |

---

## 🌍 Real-World Use Case

In a long-running backend server, GC quietly cleans unused objects so memory doesn't fill up.
Tuning GC (heap size, GC type) improves performance under heavy load.

---

## ❓ Interview Questions

1. Difference between JDK, JRE, and JVM?
2. Why is Java platform independent?
3. What is bytecode?
4. Explain JVM memory areas (heap vs stack).
5. What is the JIT compiler?
6. How does garbage collection work?
7. Can we force garbage collection? (`System.gc()` — only a *request*, not guaranteed)
8. What is a memory leak in Java? (Objects still referenced but never used)
9. What is `finalize()`? (Deprecated cleanup method before GC)
10. Difference between stack and heap memory?

---

## 📋 Stack vs Heap

| Stack | Heap |
|-------|------|
| Stores method calls, local vars | Stores objects |
| Per thread | Shared by all threads |
| Fast, auto freed | Managed by GC |
| `StackOverflowError` | `OutOfMemoryError` |

---

## ✅ Best Practices
- Let GC do its job — don't rely on `System.gc()`.
- Avoid holding references longer than needed (prevents leaks).
- Close resources (use try-with-resources).

## ⚠️ Common Mistakes
- Thinking `System.gc()` forces immediate collection.
- Keeping static references to big objects (memory leak).

---

## ⚡ Quick Revision Notes
- JDK ⊃ JRE ⊃ JVM.
- `.java` → (javac) → bytecode `.class` → (JVM) → machine code.
- Heap = objects; Stack = method calls/locals.
- GC auto-frees unreferenced objects (Young → Old generations).
- JIT speeds up execution.

## 🙋 FAQs
**Q: Is JVM platform independent?** No — JVM is platform **specific**; **bytecode** is platform independent.

## 📎 References
- Oracle Docs — JVM Specification

[⬅ Back to Java Index](./README.md)

