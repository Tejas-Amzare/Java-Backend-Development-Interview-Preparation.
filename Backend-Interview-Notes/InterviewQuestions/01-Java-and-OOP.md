# 01 — Java & OOP Interview Questions (120+)

> Format: **Q → short answer.** Cover the answers and test yourself.

---

## 🧩 Core Java (1–30)

1. **What is Java?** A platform-independent, object-oriented programming language that runs on the JVM.
2. **Why is Java platform independent?** Code compiles to bytecode, which runs on any JVM.
3. **What is bytecode?** Intermediate code (`.class`) executed by the JVM.
4. **JDK vs JRE vs JVM?** JDK = develop+run, JRE = run, JVM = executes bytecode. JDK ⊃ JRE ⊃ JVM.
5. **Is Java 100% object-oriented?** No — it has primitive types (`int`, `char`, etc.).
6. **What are primitive types?** byte, short, int, long, float, double, char, boolean.
7. **Difference between `==` and `.equals()`?** `==` compares references; `equals()` compares values.
8. **What is autoboxing?** Auto-conversion between primitives and wrapper classes (`int` ↔ `Integer`).
9. **What is the `final` keyword?** Constant variable / no method override / no class inheritance.
10. **`final` vs `finally` vs `finalize`?** Constant / always-run block / pre-GC method.
11. **What is `static`?** Belongs to the class, not an instance; shared across all objects.
12. **Can we override static methods?** No — they're hidden, not overridden.
13. **What is the `this` keyword?** Reference to the current object.
14. **What is `super`?** Reference to the parent class.
15. **Difference between path and classpath?** PATH = OS executables; CLASSPATH = Java classes location.
16. **What is a package?** A namespace grouping related classes.
17. **What are access modifiers?** private, default, protected, public.
18. **Default value of an int / object?** 0 / null.
19. **What is a wrapper class?** Object version of a primitive (`Integer`, `Double`).
20. **What is the String pool?** A memory area that reuses identical String literals.
21. **Why are Strings immutable?** Security, caching, thread-safety, and the string pool.
22. **String vs StringBuilder vs StringBuffer?** Immutable / mutable fast / mutable thread-safe.
23. **What is `hashCode()`?** Returns an int used in hashing; equal objects must have equal hashCodes.
24. **Contract between equals() and hashCode()?** Equal objects → equal hashCodes.
25. **What is a marker interface?** An empty interface (e.g., `Serializable`, `Cloneable`).
26. **What is a POJO?** Plain Old Java Object — simple class with fields + getters/setters.
27. **What is an immutable class?** Its state can't change after creation (e.g., String).
28. **How to create an immutable class?** `final` class, `final` private fields, no setters, deep copy.
29. **What is a static block?** Runs once when the class loads.
30. **What is an instance initializer block?** Runs each time an object is created, before the constructor.

---

## 🏛️ OOP (31–60)

31. **4 pillars of OOP?** Abstraction, Polymorphism, Inheritance, Encapsulation.
32. **What is a class?** A blueprint for objects.
33. **What is an object?** A real instance of a class (in heap memory).
34. **What is encapsulation?** Wrapping data + methods, hiding data via private fields.
35. **What is abstraction?** Hiding complexity, showing only essentials.
36. **Abstraction vs encapsulation?** Hide complexity (design) vs hide data (implementation).
37. **What is inheritance?** Reusing parent class code via `extends`.
38. **Types of inheritance?** Single, multilevel, hierarchical (no multiple with classes).
39. **Why no multiple inheritance with classes?** To avoid the diamond problem.
40. **How to achieve multiple inheritance?** Using interfaces.
41. **What is polymorphism?** Same name, many forms.
42. **Overloading vs overriding?** Compile-time same class / runtime child redefines.
43. **What is dynamic method dispatch?** Runtime decision of which overridden method runs.
44. **Can we overload main()?** Yes, but JVM only calls `main(String[])`.
45. **What is a constructor?** Special method to initialize an object; same name as class, no return type.
46. **Types of constructors?** Default, parameterized, copy.
47. **Can a constructor be private?** Yes (used in Singleton).
48. **What is constructor chaining?** `this()` / `super()` calling other constructors.
49. **Constructor vs method?** Constructor initializes objects (no return type); method does actions.
50. **What is an interface?** A contract of abstract methods (and default/static since Java 8).
51. **What is an abstract class?** A partial class that can't be instantiated.
52. **Interface vs abstract class?** Contract/multiple vs shared-code/single.
53. **Can interfaces have method bodies?** Yes — default and static methods (Java 8+).
54. **What is a functional interface?** Exactly one abstract method (e.g., `Runnable`).
55. **Can an abstract class have a constructor?** Yes.
56. **What is composition?** "has-a" relationship (object holds another object).
57. **Composition vs inheritance?** has-a vs is-a; prefer composition for flexibility.
58. **What is the `instanceof` operator?** Checks if an object is of a given type.
59. **What is method hiding?** Static method in subclass with the same signature.
60. **What is a nested/inner class?** A class defined inside another class.

---

## 📦 Collections (61–90)

61. **What is the Collections Framework?** Classes/interfaces to store and manage groups of objects.
62. **Is Map part of Collection?** No — it's a separate hierarchy.
63. **List vs Set vs Map?** Ordered+dup / unique / key-value.
64. **ArrayList vs LinkedList?** Array (fast access) vs doubly linked list (fast insert/delete).
65. **ArrayList vs Vector?** Vector is synchronized (legacy, slower).
66. **How does HashMap work internally?** hashCode → bucket; equals → key match; treeify after 8 collisions.
67. **HashMap load factor?** 0.75 — resizes when 75% full.
68. **HashMap vs Hashtable?** Not synchronized/1 null key vs synchronized/no null (legacy).
69. **HashMap vs ConcurrentHashMap?** Not thread-safe vs thread-safe (segment/bucket locking).
70. **HashSet vs TreeSet?** No order (fast) vs sorted (O(log n)).
71. **HashSet vs LinkedHashSet?** No order vs insertion order.
72. **TreeMap ordering?** Sorted by keys (Red-Black tree).
73. **What is a PriorityQueue?** A heap — returns elements by priority.
74. **What is a Deque?** Double-ended queue (add/remove both ends).
75. **Comparable vs Comparator?** `compareTo` (1 natural order) vs `compare` (many custom orders).
76. **Fail-fast vs fail-safe iterators?** Throw ConcurrentModificationException vs work on a copy.
77. **How to avoid ConcurrentModificationException?** Use `Iterator.remove()` or `removeIf()`.
78. **Iterator vs ListIterator?** Forward only vs bidirectional (+ set/add).
79. **What is the initial capacity of HashMap?** 16.
80. **Why override equals & hashCode for map keys?** So the map finds keys correctly.
81. **How to make a list read-only?** `Collections.unmodifiableList()` / `List.of()`.
82. **How to synchronize a collection?** `Collections.synchronizedList()` or concurrent classes.
83. **Difference between Queue and Stack?** FIFO vs LIFO.
84. **What backs an ArrayList?** A dynamic array.
85. **Time complexity of HashMap get/put?** O(1) average.
86. **What is EnumMap?** A fast Map for enum keys.
87. **What is CopyOnWriteArrayList?** Thread-safe list, copies on write (read-heavy).
88. **Difference between peek, poll, offer?** View head / remove head / add tail.
89. **What is a WeakHashMap?** Keys removed when no longer referenced (GC-friendly).
90. **What collection for LRU cache?** LinkedHashMap (access order) or custom.

---

## 🧵 Multithreading (91–110)

91. **What is a thread?** The smallest unit of execution.
92. **Process vs thread?** Independent program vs lightweight unit within a process (shares memory).
93. **Ways to create a thread?** Extend `Thread` or implement `Runnable`/`Callable`.
94. **Runnable vs Thread?** Prefer Runnable — allows extending another class.
95. **start() vs run()?** start() creates a new thread; run() executes on the current thread.
96. **What is a race condition?** Threads competing on shared data → wrong result.
97. **What is synchronization?** Allowing one thread at a time on shared code.
98. **synchronized method vs block?** Whole method vs specific critical section.
99. **What is a deadlock?** Threads waiting on each other forever.
100. **How to avoid deadlock?** Lock in consistent order, use timeouts, minimize locking.
101. **What is `volatile`?** Ensures a variable's changes are visible across threads.
102. **wait() vs sleep()?** Releases lock (Object) vs keeps lock (Thread).
103. **What is `notify()` / `notifyAll()`?** Wake one / all waiting threads.
104. **Callable vs Runnable?** Callable returns a value and can throw a checked exception.
105. **What is a thread pool?** Reusable set of threads (via ExecutorService).
106. **Why ExecutorService over new Thread()?** Reuses threads, better resource management.
107. **What is Future?** A placeholder for a task's future result.
108. **What is a CompletableFuture?** Async programming with chaining/combining.
109. **What is thread starvation?** A thread never gets CPU due to others hogging it.
110. **What is the `synchronized` alternative?** `ReentrantLock`, `Atomic` classes, concurrent collections.

---

## ⚙️ JVM, Streams & Misc (111–125)

111. **JVM memory areas?** Heap, Stack, Method Area, PC Register, Native Stack.
112. **Heap vs Stack?** Objects (shared) vs method calls/locals (per thread).
113. **What is garbage collection?** Auto-freeing unreferenced objects.
114. **Can we force GC?** `System.gc()` is only a request, not guaranteed.
115. **What is a memory leak in Java?** Objects still referenced but never used.
116. **What is the JIT compiler?** Converts hot bytecode to native code for speed.
117. **What causes StackOverflowError?** Deep/infinite recursion.
118. **What causes OutOfMemoryError?** Heap full (too many/large objects).
119. **What is a lambda expression?** Anonymous function: `(x) -> x*2`.
120. **What is the Stream API?** Pipeline processing of collections (filter/map/collect).
121. **Intermediate vs terminal operations?** Lazy (filter/map) vs triggering (collect/forEach).
122. **What is Optional?** A container to avoid NullPointerException.
123. **map() vs flatMap()?** Transform each vs flatten nested structures.
124. **What is method reference?** Shorthand for a lambda: `String::toUpperCase`.
125. **Is a stream reusable?** No — single use after a terminal operation.

[⬅ Back to Questions Index](./README.md)

