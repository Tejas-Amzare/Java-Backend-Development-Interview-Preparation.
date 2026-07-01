# 1. Time & Space Complexity (Big-O)

> 🟢 **Level:** Beginner | 🔥 **Interview Frequency:** Very High

---

## 🧠 Concept

**Big-O** tells us how fast an algorithm's **time** or **memory** grows as the input size (n) grows.
It measures **efficiency**, ignoring exact machine speed.

- **Time complexity** = how many steps.
- **Space complexity** = how much extra memory.

---

## 💬 Simple Explanation

If you search a name in a phonebook:
- Checking every page one by one = **O(n)** (slow for big books).
- Opening the middle and halving each time = **O(log n)** (fast).

Big-O answers: *"When data doubles, how much slower do we get?"*

---

## 📊 Common Complexities (best → worst)

```
O(1)      Constant     ⚡ fastest — array access
O(log n)  Logarithmic  🚀 binary search
O(n)      Linear       🙂 one loop
O(n log n) Linearithmic 👍 good sorting (merge/quick)
O(n²)     Quadratic    😐 nested loops
O(2ⁿ)     Exponential  🐢 recursion (subsets)
O(n!)     Factorial    💀 permutations
```

```
steps
 │        O(n!)  O(2ⁿ)
 │       /      /
 │      /     /    O(n²)
 │     /    /    /
 │    /   /   / _____ O(n log n)
 │   /  / _/_______ O(n)
 │  /_/____________ O(log n)
 │_________________ O(1)
 └──────────────────► input size (n)
```

---

## 🧩 Examples

```java
// O(1) - constant
int first = arr[0];

// O(n) - linear
for (int x : arr) sum += x;

// O(n²) - quadratic (nested loop)
for (int i = 0; i < n; i++)
    for (int j = 0; j < n; j++)
        System.out.println(i + "," + j);

// O(log n) - halving each step
while (n > 1) n = n / 2;
```

---

## 🧮 How to Find Complexity (quick rules)
1. Single loop over n → **O(n)**.
2. Nested loops → **O(n²)**.
3. Halving each step → **O(log n)**.
4. Drop constants: O(2n) → **O(n)**.
5. Keep the biggest term: O(n² + n) → **O(n²)**.

---

## 🌍 Real-World Use Case

Choosing HashMap (O(1) lookup) over scanning a list (O(n)) makes an API respond in
milliseconds instead of seconds when data is large.

---

## ❓ Interview Questions
1. What is Big-O notation?
2. Difference between time and space complexity?
3. Complexity of binary search? (**O(log n)**)
4. Complexity of HashMap get/put? (**O(1)** average)
5. What is the worst case of QuickSort? (**O(n²)**)
6. Difference between O(n) and O(log n)?
7. What does "amortized" complexity mean? (Average over many operations, e.g., ArrayList add)

---

## 📋 Data Structure Complexity Cheat Sheet

| Structure | Access | Search | Insert | Delete |
|-----------|--------|--------|--------|--------|
| Array | O(1) | O(n) | O(n) | O(n) |
| ArrayList | O(1) | O(n) | O(1)* | O(n) |
| LinkedList | O(n) | O(n) | O(1) | O(1) |
| HashMap | — | O(1) | O(1) | O(1) |
| TreeMap | — | O(log n) | O(log n) | O(log n) |
| Stack/Queue | O(n) | O(n) | O(1) | O(1) |

*amortized

---

## ✅ Best Practices
- Always state complexity when solving an interview problem.
- Optimize the **bottleneck** (biggest term) first.

## ⚠️ Common Mistakes
- Forgetting that nested loops = O(n²).
- Ignoring space complexity (recursion uses stack space!).

---

## ⚡ Quick Revision Notes
- Big-O = growth rate of time/memory vs input.
- Order: O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2ⁿ) < O(n!).
- Drop constants, keep the biggest term.
- HashMap = O(1); Binary search = O(log n); nested loop = O(n²).

## 🙋 FAQs
**Q: Is O(n) always slower than O(1)?** For large n, yes; for tiny n it may not matter.

## 📎 References
- *Cracking the Coding Interview* — Big-O chapter
- bigocheatsheet.com

[⬅ Back to DSA Index](./README.md)

