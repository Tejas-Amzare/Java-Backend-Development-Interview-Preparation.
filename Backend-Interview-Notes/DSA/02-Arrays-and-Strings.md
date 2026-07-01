# 2. Arrays & Strings

> 🟢 **Level:** Beginner | 🔥 **Interview Frequency:** Very High

---

## Part A — Arrays

### 🧠 Concept
An **array** is a fixed-size box of elements of the **same type**, stored **next to each other**
in memory. Access by **index** is instant — **O(1)**.

```
index:  0    1    2    3
      [10] [20] [30] [40]
```

### 🧩 Java Basics
```java
int[] arr = {10, 20, 30, 40};
arr[0];               // 10  (O(1) access)
arr.length;           // 4
for (int x : arr) System.out.println(x);

int[][] grid = new int[3][3];   // 2D array
```

### Key Facts
- Fixed size (can't grow). Use `ArrayList` for dynamic size.
- Access O(1), search O(n), insert/delete O(n).

---

## Part B — Strings

### 🧠 Concept
A **String** is a sequence of characters. In Java, Strings are **immutable** (cannot be changed
after creation). For heavy editing, use `StringBuilder`.

### 🧩 Java Basics
```java
String s = "hello";
s.length();            // 5
s.charAt(0);           // 'h'
s.substring(1, 3);     // "el"
s.toUpperCase();       // "HELLO"
s.equals("hello");     // true  (use equals, NOT ==)

// Editing efficiently
StringBuilder sb = new StringBuilder();
sb.append("a").append("b");
sb.reverse();
String result = sb.toString();
```

### String vs StringBuilder vs StringBuffer

| | String | StringBuilder | StringBuffer |
|-|--------|---------------|--------------|
| Mutable | ❌ No | ✅ Yes | ✅ Yes |
| Thread-safe | ✅ | ❌ | ✅ |
| Speed | slow (edits) | fast | slower than SB |

> ⚠️ Use `equals()` to compare String **values**; `==` compares **references**.

---

## 🌍 Real-World Use Case
- Arrays store fixed data like days of the week or pixel values.
- Strings handle names, emails, JSON — everywhere in backend.

---

## ❓ Most Asked Interview Questions
1. Why are Strings immutable in Java? (Security, caching, thread-safety, string pool)
2. Difference between `==` and `equals()`?
3. String vs StringBuilder vs StringBuffer?
4. What is the String Constant Pool?
5. How to reverse a string / check palindrome?
6. Find duplicate / missing number in an array.
7. How to rotate an array?
8. Difference between array and ArrayList?

---

## 💻 Coding Examples

```java
// Reverse an array in-place - O(n)
void reverse(int[] a) {
    int i = 0, j = a.length - 1;
    while (i < j) { int t = a[i]; a[i] = a[j]; a[j] = t; i++; j--; }
}

// Check palindrome string
boolean isPalindrome(String s) {
    int i = 0, j = s.length() - 1;
    while (i < j) if (s.charAt(i++) != s.charAt(j--)) return false;
    return true;
}

// Find the missing number 1..n
int missing(int[] a, int n) {
    int total = n * (n + 1) / 2;
    for (int x : a) total -= x;
    return total;
}
```

---

## 🏆 Top LeetCode Problems
| # | Problem | Difficulty |
|---|---------|-----------|
| 1 | Two Sum | Easy |
| 121 | Best Time to Buy and Sell Stock | Easy |
| 217 | Contains Duplicate | Easy |
| 53 | Maximum Subarray (Kadane) | Medium |
| 238 | Product of Array Except Self | Medium |
| 15 | 3Sum | Medium |
| 242 | Valid Anagram | Easy |
| 5 | Longest Palindromic Substring | Medium |
| 49 | Group Anagrams | Medium |
| 76 | Minimum Window Substring | Hard |

---

## ✅ Best Practices
- Use `StringBuilder` in loops, never `+` for many concatenations.
- Prefer `ArrayList` when size is unknown.

## ⚠️ Common Mistakes
- Comparing Strings with `==`.
- Off-by-one errors (`<=` vs `<` with `length`).
- `ArrayIndexOutOfBoundsException` — going past the last index.

---

## ⚡ Quick Revision Notes
- Array: fixed size, O(1) access, same type.
- String: immutable → use StringBuilder for edits.
- Compare Strings with `equals()`, not `==`.
- Kadane's algorithm → max subarray in O(n).

## 🙋 FAQs
**Q: Why StringBuilder over String in loops?** String creates a new object each time (slow, O(n²)).

## 📎 References
- LeetCode Arrays & Strings tag
- Oracle Docs — String, StringBuilder

[⬅ Back to DSA Index](./README.md)

