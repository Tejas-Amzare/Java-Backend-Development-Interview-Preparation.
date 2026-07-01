# 7. Patterns: Sliding Window, Two Pointer & Binary Search

> 🟡 **Level:** Intermediate | 🔥 **Interview Frequency:** Very High

These 3 patterns solve a **huge** number of array/string problems efficiently.

---

## Part A — Two Pointer

### 🧠 Concept
Use **two indexes** (often start & end) that move toward each other or together, instead of
nested loops. Turns O(n²) into **O(n)**.

```java
// Check if a SORTED array has two numbers summing to target
boolean twoSum(int[] a, int target) {
    int i = 0, j = a.length - 1;
    while (i < j) {
        int sum = a[i] + a[j];
        if (sum == target) return true;
        if (sum < target) i++;      // need bigger → move left pointer right
        else j--;                   // need smaller → move right pointer left
    }
    return false;
}
```

Use when: array is **sorted**, or comparing from **both ends** (palindrome, pair sum, reverse).

---

## Part B — Sliding Window

### 🧠 Concept
Keep a **window** (range) over the array and **slide** it, adjusting size, instead of
recomputing from scratch. Perfect for **subarray / substring** problems.

```
[ a b c ] d e     window slides →   a [ b c d ] e
```

```java
// Max sum of any subarray of size k - O(n)
int maxSum(int[] a, int k) {
    int sum = 0, max;
    for (int i = 0; i < k; i++) sum += a[i];   // first window
    max = sum;
    for (int i = k; i < a.length; i++) {
        sum += a[i] - a[i - k];                // slide: add new, remove old
        max = Math.max(max, sum);
    }
    return max;
}
```

Two kinds: **fixed-size** window (size k) and **variable-size** window (grow/shrink to meet a condition).

Use when: "longest/shortest/max/min **subarray or substring** with some condition".

---

## Part C — Binary Search

### 🧠 Concept
On a **sorted** array, repeatedly check the **middle** and throw away half. **O(log n)**.

```java
int binarySearch(int[] a, int target) {
    int lo = 0, hi = a.length - 1;
    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;   // avoids overflow
        if (a[mid] == target) return mid;
        if (a[mid] < target) lo = mid + 1;   // go right
        else hi = mid - 1;                   // go left
    }
    return -1;   // not found
}
```

> ⚠️ Use `lo + (hi - lo)/2`, not `(lo+hi)/2`, to avoid integer overflow.

Advanced: **binary search on the answer** (e.g., min capacity, Koko eating bananas).

---

## 🌍 Real-World Use Cases
- **Two pointer** → merge sorted lists, remove duplicates.
- **Sliding window** → rate limiting, max traffic in a time window, longest unique substring.
- **Binary search** → search in databases/indexes, find version, autoscaling thresholds.

---

## ❓ Most Asked Interview Questions
1. When to use two pointers vs sliding window?
2. How does binary search achieve O(log n)?
3. Find the longest substring without repeating characters.
4. Find a pair with a given sum in a sorted array.
5. Search in a rotated sorted array.
6. Why prefer `mid = lo + (hi-lo)/2`?
7. Find first/last occurrence of an element.

---

## 🏆 Top LeetCode Problems
| # | Problem | Pattern | Difficulty |
|---|---------|---------|-----------|
| 167 | Two Sum II (sorted) | Two Pointer | Medium |
| 125 | Valid Palindrome | Two Pointer | Easy |
| 11 | Container With Most Water | Two Pointer | Medium |
| 3 | Longest Substring Without Repeating | Sliding Window | Medium |
| 424 | Longest Repeating Char Replacement | Sliding Window | Medium |
| 209 | Minimum Size Subarray Sum | Sliding Window | Medium |
| 704 | Binary Search | Binary Search | Easy |
| 33 | Search in Rotated Sorted Array | Binary Search | Medium |
| 153 | Find Minimum in Rotated Array | Binary Search | Medium |
| 875 | Koko Eating Bananas | Binary Search on Answer | Medium |

---

## ✅ Best Practices
- Confirm the array is **sorted** before binary search / two-pointer sum.
- For sliding window, clearly define **when to shrink** the window.

## ⚠️ Common Mistakes
- Integer overflow in `mid`.
- Infinite loops from wrong `lo`/`hi` updates.
- Recomputing the whole window instead of sliding.

---

## ⚡ Quick Revision Notes
- Two pointer → sorted arrays / both ends → O(n).
- Sliding window → subarray/substring with a condition → O(n).
- Binary search → sorted data, halve each step → O(log n).
- `mid = lo + (hi - lo) / 2`.

## 🙋 FAQs
**Q: Can binary search work on unsorted data?** No — data must be sorted (or monotonic).

## 📎 References
- LeetCode Two Pointers / Sliding Window / Binary Search tags

[⬅ Back to DSA Index](./README.md)

