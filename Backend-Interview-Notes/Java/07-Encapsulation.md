# 7. Encapsulation

> 🟢 **Level:** Beginner | ⭐ **Interview Frequency:** High

---

## 🧠 Concept

**Encapsulation** = wrapping **data (fields)** and **methods** into one unit (class), and
**protecting** the data by making it `private`. Access is given only through **getters/setters**.

Also called **data hiding**.

---

## 💬 Simple Explanation

Think of a **medicine capsule** 💊 — the medicine (data) is safely wrapped inside a shell.
You can't touch it directly. Similarly, encapsulation keeps data safe inside the class.

---

## 🧩 Example

```java
class BankAccount {
    private double balance;   // hidden data

    public double getBalance() {         // controlled read
        return balance;
    }

    public void deposit(double amount) { // controlled write with rule
        if (amount > 0) {
            balance += amount;
        }
    }
}
```

Here `balance` cannot be set to a negative value from outside — data stays **valid**.

---

## 🌍 Real-World Use Case

User's `password` field is `private`. It can only be set via `setPassword()` which hashes it
first. Outside code can never read or set it directly → **security**.

---

## 🗺️ Diagram

```
   ┌──────────── BankAccount ────────────┐
   │  private balance   (hidden)         │
   │  ─────────────────────────────────  │
   │  getBalance()  ← controlled access  │
   │  deposit()     ← validation rules   │
   └──────────────────────────────────────┘
```

---

## ❓ Interview Questions

1. What is encapsulation? How to achieve it?
2. Why make fields `private`?
3. Difference between encapsulation and abstraction?
4. What is a POJO / Java Bean?
5. Benefits of getters/setters over public fields?

---

## ✅ Best Practices
- Make all fields `private`.
- Add validation inside setters.
- Provide getters/setters only where needed (don't expose everything blindly).

## ⚠️ Common Mistakes
- Making fields `public` "for convenience".
- Auto-generating setters that skip validation.

---

## ⚡ Quick Revision Notes
- Encapsulation = private data + public getters/setters.
- Also called **data hiding**.
- Gives control, security, and validation.

## 📋 Cheat Sheet

| Modifier | Access |
|----------|--------|
| `private` | Same class only |
| `default` | Same package |
| `protected` | Package + subclasses |
| `public` | Everywhere |

## 🙋 FAQs
**Q: Is encapsulation same as making a class?** No — it's specifically about hiding & protecting data.

## 📎 References
- Oracle Docs — Controlling Access to Members

[⬅ Back to Java Index](./README.md)

