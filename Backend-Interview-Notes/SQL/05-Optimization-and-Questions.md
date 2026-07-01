# 5. Query Optimization + Common SQL Interview Questions

> 🔴 **Level:** Advanced | 🔥 **Interview Frequency:** Very High

---

## Part A — Query Optimization

### 🧠 Concept
**Query optimization** = making SQL run **faster** and use **fewer resources**.

### 🛠️ Top Optimization Tips
1. **Add indexes** on columns in `WHERE`, `JOIN`, `ORDER BY`.
2. **Select only needed columns** — avoid `SELECT *`.
3. Use **`EXPLAIN`** to see the query plan (spot full table scans).
4. **Avoid functions on indexed columns** in WHERE (e.g., `WHERE YEAR(date)=2024` skips index).
5. Replace **correlated subqueries** with **JOINs** when possible.
6. Use **`LIMIT`** for large result sets / pagination.
7. **Filter early** (WHERE before GROUP BY).
8. Avoid `OR` on different columns — consider `UNION` or indexes.
9. Watch out for the **N+1 problem** (many small queries in a loop).

```sql
EXPLAIN SELECT name FROM users WHERE email = 'a@mail.com';
```

### Signs of a slow query
- Full table scan (no index used).
- Too many joins on unindexed columns.
- Returning huge unbounded result sets.

---

## Part B — Common SQL Interview Questions (with answers)

**1. Find the 2nd highest salary.**
```sql
SELECT MAX(salary) FROM employees
WHERE salary < (SELECT MAX(salary) FROM employees);

-- OR using window function
SELECT DISTINCT salary FROM (
  SELECT salary, DENSE_RANK() OVER (ORDER BY salary DESC) rnk FROM employees
) t WHERE rnk = 2;
```

**2. Find duplicate records.**
```sql
SELECT email, COUNT(*) FROM users
GROUP BY email HAVING COUNT(*) > 1;
```

**3. Delete duplicate rows (keep one).**
```sql
DELETE FROM users
WHERE id NOT IN (SELECT MIN(id) FROM users GROUP BY email);
```

**4. Nth highest salary (general).**
```sql
SELECT salary FROM (
  SELECT salary, DENSE_RANK() OVER (ORDER BY salary DESC) r FROM employees
) t WHERE r = N;
```

**5. Employees earning more than their manager.**
```sql
SELECT e.name FROM employees e
JOIN employees m ON e.manager_id = m.id
WHERE e.salary > m.salary;
```

**6. Count employees per department.**
```sql
SELECT department, COUNT(*) FROM employees GROUP BY department;
```

**7. Get top 3 salaries per department.**
```sql
SELECT * FROM (
  SELECT name, department, salary,
         DENSE_RANK() OVER (PARTITION BY department ORDER BY salary DESC) r
  FROM employees
) t WHERE r <= 3;
```

**8. Difference between UNION and UNION ALL?**
UNION removes duplicates (slower); UNION ALL keeps all rows (faster).

**9. WHERE vs HAVING?**
WHERE filters rows before grouping; HAVING filters after grouping.

**10. Find customers who never placed an order.**
```sql
SELECT c.name FROM customers c
LEFT JOIN orders o ON c.id = o.customer_id
WHERE o.id IS NULL;
```

---

## 📋 More Rapid-Fire Q&A
| Question | Answer |
|----------|--------|
| DELETE vs TRUNCATE? | DELETE = rows + rollback; TRUNCATE = all rows, fast |
| Primary vs Unique key? | PK: not null, one; Unique: allows one null, many |
| CHAR vs VARCHAR? | CHAR fixed length; VARCHAR variable |
| INNER vs LEFT JOIN? | INNER = matches; LEFT = all left + matches |
| Clustered vs non-clustered index? | Clustered sorts rows (1); non-clustered = separate structure |
| What is a subquery? | A query inside another query |
| What is a CTE? | `WITH` — a named temporary result set |

---

## ✅ Best Practices
- Always test with `EXPLAIN` on big tables.
- Paginate large results with `LIMIT`/`OFFSET` (or keyset pagination).
- Keep queries readable; use CTEs for complex logic.

## ⚠️ Common Mistakes
- `SELECT *` in production code.
- Functions on indexed columns in WHERE.
- Ignoring the N+1 query problem in ORMs.

---

## ⚡ Quick Revision Notes
- Optimize: index WHERE/JOIN columns, avoid `SELECT *`, use EXPLAIN, LIMIT.
- 2nd highest salary = subquery or DENSE_RANK.
- Duplicates = GROUP BY + HAVING COUNT(*) > 1.
- UNION removes dups; UNION ALL keeps them.

## 🙋 FAQs
**Q: How to find slow queries?** Use EXPLAIN/EXPLAIN ANALYZE and the DB's slow query log.

## 📎 References
- Use The Index, Luke
- LeetCode Database problems

[⬅ Back to SQL Index](./README.md)

