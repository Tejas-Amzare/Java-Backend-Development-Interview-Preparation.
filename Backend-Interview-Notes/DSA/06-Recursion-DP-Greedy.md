# 6. Recursion, Backtracking, DP & Greedy

> 🔴 **Level:** Advanced | 🔥 **Interview Frequency:** Very High

---

## Part A — Recursion

### 🧠 Concept
**Recursion** = a function that **calls itself** to solve a smaller version of the problem,
until it hits a **base case** (stopping point).

Every recursion needs: **(1) base case** + **(2) recursive call** that moves toward the base.

```java
int factorial(int n) {
    if (n <= 1) return 1;          // base case
    return n * factorial(n - 1);   // recursive call
}
```

```
factorial(3)
 = 3 * factorial(2)
 = 3 * 2 * factorial(1)
 = 3 * 2 * 1 = 6
```

> ⚠️ No base case = infinite recursion → `StackOverflowError`.

---

## Part B — Backtracking

### 🧠 Concept
**Backtracking** = try a choice → if it fails, **undo (backtrack)** and try another.
Used for problems asking for **all combinations/permutations/paths**.

Template:
```
choose → explore → un-choose (backtrack)
```

```java
void permute(List<Integer> nums, List<Integer> current, boolean[] used, List<List<Integer>> res) {
    if (current.size() == nums.size()) {
        res.add(new ArrayList<>(current));
        return;
    }
    for (int i = 0; i < nums.size(); i++) {
        if (used[i]) continue;
        used[i] = true; current.add(nums.get(i));   // choose
        permute(nums, current, used, res);          // explore
        used[i] = false; current.remove(current.size()-1); // un-choose
    }
}
```

Classic: N-Queens, Sudoku solver, subsets, permutations, word search.

---

## Part C — Dynamic Programming (DP)

### 🧠 Concept
**DP** = break a problem into **overlapping sub-problems**, solve each **once**, and **store**
the result (so you don't recompute). Great when brute force repeats the same work.

Two styles:
- **Top-down (Memoization)** → recursion + cache.
- **Bottom-up (Tabulation)** → fill a table from small to big.

```java
// Fibonacci with memoization - O(n) instead of O(2^n)
int[] memo = new int[100];
int fib(int n) {
    if (n <= 1) return n;
    if (memo[n] != 0) return memo[n];
    return memo[n] = fib(n-1) + fib(n-2);
}

// Bottom-up
int fibDP(int n) {
    int[] dp = new int[n+1];
    dp[1] = 1;
    for (int i = 2; i <= n; i++) dp[i] = dp[i-1] + dp[i-2];
    return dp[n];
}
```

**When to use DP?** Problem asks for **min/max/count of ways** AND has **overlapping subproblems +
optimal substructure**.

---

## Part D — Greedy

### 🧠 Concept
**Greedy** = at each step, pick the **best choice right now** and hope it leads to the overall best.
Works only when **local best = global best**.

```java
// Coin change (greedy works for standard coin systems)
int coins(int amount, int[] coins) {  // coins sorted desc
    int count = 0;
    for (int c : coins) {
        count += amount / c;
        amount %= c;
    }
    return count;
}
```

Classic: activity selection, Huffman coding, Dijkstra, interval scheduling.

> ⚠️ Greedy doesn't always work! (e.g., coins `[1,3,4]` for amount `6` — greedy fails, DP needed.)

---

## 📋 Recursion vs DP vs Greedy vs Backtracking

| Approach | Idea | Use when |
|----------|------|----------|
| Recursion | Solve smaller subproblem | Naturally self-similar |
| Backtracking | Try + undo | All solutions / combinations |
| DP | Store subproblem results | Overlapping subproblems |
| Greedy | Best local choice | Local = global optimal |

---

## 🌍 Real-World Use Cases
- **Recursion** → tree/graph traversal, file system walk.
- **Backtracking** → puzzle solvers, route finding.
- **DP** → text diff, spell-check, resource allocation, caching.
- **Greedy** → scheduling, compression, routing.

---

## ❓ Most Asked Interview Questions
1. What is recursion? Base case importance?
2. Difference between recursion and iteration?
3. What is backtracking? Give an example.
4. What is dynamic programming? Memoization vs tabulation?
5. When does greedy fail?
6. Optimal substructure & overlapping subproblems?
7. Solve Fibonacci in O(n).
8. Explain the knapsack problem.

---

## 🏆 Top LeetCode Problems
| # | Problem | Type | Difficulty |
|---|---------|------|-----------|
| 509 | Fibonacci Number | DP | Easy |
| 70 | Climbing Stairs | DP | Easy |
| 322 | Coin Change | DP | Medium |
| 300 | Longest Increasing Subsequence | DP | Medium |
| 1143 | Longest Common Subsequence | DP | Medium |
| 198 | House Robber | DP | Medium |
| 39 | Combination Sum | Backtracking | Medium |
| 46 | Permutations | Backtracking | Medium |
| 78 | Subsets | Backtracking | Medium |
| 51 | N-Queens | Backtracking | Hard |
| 55 | Jump Game | Greedy | Medium |
| 435 | Non-overlapping Intervals | Greedy | Medium |

---

## ✅ Best Practices
- Always write the **base case first**.
- For DP: define the **state** and **recurrence** clearly.
- Try recursion → add memoization → convert to tabulation.

## ⚠️ Common Mistakes
- Missing/wrong base case → StackOverflow.
- Not caching in DP → exponential time.
- Assuming greedy always works.

---

## ⚡ Quick Revision Notes
- Recursion = self-call + base case.
- Backtracking = choose → explore → un-choose.
- DP = store subproblem answers (memoization/tabulation).
- Greedy = best local pick; only works when local = global.

## 🙋 FAQs
**Q: How to know it's a DP problem?** Overlapping subproblems + asks min/max/count of ways.

## 📎 References
- LeetCode DP / Backtracking tags
- Striver DP playlist

[⬅ Back to DSA Index](./README.md)

