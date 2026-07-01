# 8. Sorting Algorithms

> 🟢 **Level:** Beginner | ⭐ **Interview Frequency:** High

---

## 🧠 Concept

**Sorting** = arranging data in order (ascending/descending). Knowing how sorts work and their
complexity is a classic interview topic.

---

## 📊 Comparison Table (memorize this!)

| Algorithm | Best | Average | Worst | Space | Stable? |
|-----------|------|---------|-------|-------|---------|
| Bubble Sort | O(n) | O(n²) | O(n²) | O(1) | ✅ |
| Selection Sort | O(n²) | O(n²) | O(n²) | O(1) | ❌ |
| Insertion Sort | O(n) | O(n²) | O(n²) | O(1) | ✅ |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) | ✅ |
| Quick Sort | O(n log n) | O(n log n) | O(n²) | O(log n) | ❌ |
| Heap Sort | O(n log n) | O(n log n) | O(n log n) | O(1) | ❌ |
| Counting Sort | O(n+k) | O(n+k) | O(n+k) | O(k) | ✅ |

> **Stable** = keeps the original order of equal elements.

---

## 🧩 Key Algorithms

### Bubble Sort (simple, slow)
Repeatedly swap adjacent out-of-order elements — biggest "bubbles" to the end.
```java
for (int i = 0; i < n-1; i++)
    for (int j = 0; j < n-1-i; j++)
        if (a[j] > a[j+1]) { int t=a[j]; a[j]=a[j+1]; a[j+1]=t; }
```

### Merge Sort (divide & conquer, reliable O(n log n))
Split in half → sort each half → **merge** them.
```
[5,2,8,1] → [5,2] [8,1] → [2,5] [1,8] → [1,2,5,8]
```

### Quick Sort (fast in practice)
Pick a **pivot**, put smaller left & bigger right, then sort each side.
Average O(n log n), worst O(n²) (bad pivot).

---

## 🏭 Sorting in Java
```java
int[] a = {5, 2, 8, 1};
Arrays.sort(a);                          // dual-pivot quicksort (primitives)

List<Integer> list = new ArrayList<>(List.of(5, 2, 8));
Collections.sort(list);                  // merge sort (objects)
list.sort(Comparator.reverseOrder());    // descending
list.sort(Comparator.comparingInt(x -> x));  // custom
```

> Java uses **Dual-Pivot QuickSort** for primitives and **TimSort** (merge+insertion) for objects.

---

## 🌍 Real-World Use Cases
- Sorting search results, leaderboards, product prices.
- Merge sort idea → external sorting of huge files.
- Counting sort → sort ages, small-range numbers fast.

---

## ❓ Most Asked Interview Questions
1. Which sort is fastest and why?
2. Difference between merge sort and quick sort?
3. What is a stable sort? Why does it matter?
4. Worst case of quick sort and how to avoid it? (Random/median pivot)
5. Which sort does `Arrays.sort()` use?
6. When is insertion sort a good choice? (Small or nearly-sorted data)
7. Explain merge sort's O(n log n).

---

## ✅ Best Practices
- Use built-in `Arrays.sort()` / `Collections.sort()` in real code.
- Use `Comparator` for custom ordering.
- Prefer merge sort when **stability** matters.

## ⚠️ Common Mistakes
- Assuming quick sort is always O(n log n) (worst is O(n²)).
- Forgetting merge sort needs O(n) extra space.

---

## ⚡ Quick Revision Notes
- Best general sorts: merge, quick, heap → O(n log n).
- Merge = stable, O(n) space; Quick = fast, worst O(n²); Heap = O(1) space.
- Java: primitives → dual-pivot quicksort; objects → TimSort.
- Stable = preserves equal-element order.

## 🙋 FAQs
**Q: Fastest comparison sort possible?** O(n log n) is the theoretical lower bound.

## 📎 References
- visualgo.net/sorting (visual)
- Oracle Docs — Arrays.sort

[⬅ Back to DSA Index](./README.md)

