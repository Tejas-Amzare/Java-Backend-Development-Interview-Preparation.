# 11. Multithreading, Synchronization & Executor Service

> 🔴 **Level:** Advanced | ⭐ **Interview Frequency:** High

---

## 🧠 Concept

A **thread** is a small unit of work that runs independently. **Multithreading** means running
**many threads at the same time** so the program does more work faster.

---

## 💬 Simple Explanation

A restaurant with **one waiter** serves slowly (single thread).
Add **many waiters** and customers get served in parallel (multithreading).

---

## 🧩 Creating Threads — 2 ways

```java
// Way 1: extend Thread
class MyThread extends Thread {
    public void run() { System.out.println("Running..."); }
}
new MyThread().start();

// Way 2 (preferred): implement Runnable
Runnable task = () -> System.out.println("Running...");
new Thread(task).start();
```

> ✅ Prefer `Runnable` — a class can implement many interfaces but extend only one class.

---

## 🗺️ Thread Life Cycle

```
NEW → RUNNABLE → RUNNING → (BLOCKED/WAITING/TIMED_WAITING) → TERMINATED
```

| State | Meaning |
|-------|---------|
| NEW | Created, not started |
| RUNNABLE | Ready to run |
| RUNNING | Currently executing |
| WAITING/BLOCKED | Paused / waiting for lock |
| TERMINATED | Finished |

---

## 🔒 Synchronization

When many threads change the **same data**, results can go wrong (**race condition**).
`synchronized` allows **only one thread at a time**.

```java
class Counter {
    private int count = 0;
    public synchronized void increment() {   // only one thread enters
        count++;
    }
}
```

- **Race condition** — threads fight over shared data → wrong result.
- **Deadlock** — two threads wait for each other forever.
- **Lock** — a "key"; only the holder can run the protected code.

```
Deadlock:
Thread1 holds Lock A, wants Lock B
Thread2 holds Lock B, wants Lock A   → both stuck forever
```

---

## ⚙️ Executor Service (modern way)

Creating threads manually is costly. **Thread pools** reuse threads.

```java
ExecutorService pool = Executors.newFixedThreadPool(3);
pool.submit(() -> System.out.println("Task running"));
pool.shutdown();
```

| Class | Use |
|-------|-----|
| `newFixedThreadPool(n)` | Fixed number of threads |
| `newCachedThreadPool()` | Grows/shrinks as needed |
| `newSingleThreadExecutor()` | One thread, sequential |
| `newScheduledThreadPool(n)` | Run tasks later / repeatedly |

`Callable` + `Future` → run a task that **returns a result**:
```java
Future<Integer> f = pool.submit(() -> 2 + 3);
Integer result = f.get();   // 5
```

---

## 🌍 Real-World Use Case

A web server handles **thousands of requests** using a thread pool. Each request runs on a
separate thread so users don't wait in a single line.

---

## ❓ Interview Questions

1. Difference between process and thread?
2. `Runnable` vs `Thread` — which is better and why?
3. What is a race condition? How to prevent it?
4. What is a deadlock? How to avoid it?
5. Difference between `synchronized` method and block?
6. What is `volatile` keyword? (Ensures visibility of a variable across threads)
7. Difference between `wait()` and `sleep()`?
8. What is a thread pool and why use it?
9. Difference between `Callable` and `Runnable`? (Callable returns value + throws checked exception)
10. What is `ConcurrentHashMap` and how is it better than `Hashtable`?

---

## 📋 wait() vs sleep()

| wait() | sleep() |
|--------|---------|
| Releases lock | Keeps lock |
| From `Object` class | From `Thread` class |
| Needs synchronized block | Anywhere |
| Woken by `notify()` | Wakes after time |

---

## ✅ Best Practices
- Prefer **ExecutorService** over creating threads by hand.
- Keep synchronized blocks **small**.
- Use concurrent collections (`ConcurrentHashMap`) instead of manual locks.
- Always `shutdown()` your executor.

## ⚠️ Common Mistakes
- Calling `run()` instead of `start()` (runs on same thread, no new thread!).
- Forgetting to synchronize shared data → race conditions.
- Creating deadlocks by locking in different orders.

---

## ⚡ Quick Revision Notes
- Thread = smallest unit of execution; multithreading = parallel work.
- Use `Runnable` over `Thread`. Use `start()`, not `run()`.
- `synchronized` prevents race conditions.
- Deadlock = threads wait on each other forever.
- Use `ExecutorService` (thread pools) in real apps.

## 🙋 FAQs
**Q: Does more threads always mean faster?** No — too many threads cause context-switching overhead.

## 📎 References
- Oracle Docs — Concurrency
- *Java Concurrency in Practice* (advanced)

[⬅ Back to Java Index](./README.md)

