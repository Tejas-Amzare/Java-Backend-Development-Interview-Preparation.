# 10. Exception Handling

> 🟢 **Level:** Beginner | 🔥 **Interview Frequency:** Very High

---

## 🧠 Concept

An **exception** is a problem that happens **while the program runs** (e.g., dividing by zero,
file not found). Exception handling lets us **catch these errors** and keep the program from crashing.

Keywords: `try`, `catch`, `finally`, `throw`, `throws`.

---

## 💬 Simple Explanation

Imagine driving with a **spare tyre** 🚗. If a tyre bursts (error), you don't abandon the car —
you handle it and continue. `try-catch` is that spare tyre for your code.

---

## 🧩 Example

```java
try {
    int result = 10 / 0;             // risky code
} catch (ArithmeticException e) {    // catch the specific error
    System.out.println("Cannot divide by zero");
} finally {
    System.out.println("Always runs (cleanup)");
}
```

---

## 🗺️ Exception Hierarchy

```
              Throwable
             /         \
        Error          Exception
     (JVM issues,      /         \
      don't catch) Checked     Unchecked (RuntimeException)
                   (IOException) (NullPointer, ArithmeticException,
                    SQLException)  ArrayIndexOutOfBounds)
```

| Type | Checked | Unchecked |
|------|---------|-----------|
| When known | Compile time | Runtime |
| Must handle? | Yes (compiler forces) | No |
| Examples | IOException, SQLException | NullPointerException, ArithmeticException |

---

## 🔑 Keyword Meanings

| Keyword | Meaning |
|---------|---------|
| `try` | Wrap risky code |
| `catch` | Handle the error |
| `finally` | Always runs (cleanup, close resources) |
| `throw` | Manually throw an exception |
| `throws` | Declares a method **might** throw an exception |

```java
void checkAge(int age) {
    if (age < 18) {
        throw new IllegalArgumentException("Must be 18+");   // throw
    }
}
```

---

## 🆕 Custom Exception + try-with-resources

```java
class InsufficientBalanceException extends RuntimeException {
    public InsufficientBalanceException(String msg) { super(msg); }
}

// try-with-resources auto-closes the resource (no finally needed)
try (BufferedReader br = new BufferedReader(new FileReader("data.txt"))) {
    System.out.println(br.readLine());
} catch (IOException e) {
    e.printStackTrace();
}
```

---

## 🌍 Real-World Use Case

In a REST API, if the database is down, we **catch** the exception and return a clean
`503 Service Unavailable` response instead of crashing the whole app.

---

## ❓ Interview Questions

1. Difference between checked and unchecked exceptions?
2. Difference between `throw` and `throws`?
3. Difference between `final`, `finally`, and `finalize`?
4. Can `finally` block be skipped? (Only if `System.exit()` or JVM crash)
5. Difference between Error and Exception?
6. What is try-with-resources?
7. Can we have try without catch? (Yes — with `finally` or resources)
8. What happens if an exception is thrown in `finally`?

---

## 📋 final vs finally vs finalize

| Term | What |
|------|------|
| `final` | Keyword — constant / no override / no inherit |
| `finally` | Block that always runs |
| `finalize()` | Old method called before GC (deprecated) |

---

## ✅ Best Practices
- Catch **specific** exceptions, not just `Exception`.
- Never leave a catch block empty (swallowing errors).
- Use **try-with-resources** to close files/connections.
- Create meaningful **custom exceptions** for business rules.

## ⚠️ Common Mistakes
- `catch (Exception e) {}` — hides real problems.
- Catching an exception you can't handle.
- Using exceptions for normal flow control.

---

## ⚡ Quick Revision Notes
- Exception = runtime problem; handle with `try-catch-finally`.
- Checked = compile-time (must handle); Unchecked = runtime.
- `throw` = throw now; `throws` = might throw.
- `finally` always runs; try-with-resources auto-closes.

## 🙋 FAQs
**Q: Is NullPointerException checked or unchecked?** Unchecked (RuntimeException).

## 📎 References
- Oracle Docs — Exceptions

[⬅ Back to Java Index](./README.md)

