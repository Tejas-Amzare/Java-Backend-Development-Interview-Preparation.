# 4. Views, Procedures, Triggers, Aggregates & Window Functions

> 🔴 **Level:** Advanced | ⭐ **Interview Frequency:** High

---

## Part A — Views

### 🧠 Concept
A **view** is a **virtual table** based on a saved query. It doesn't store data itself — it shows
data from real tables. Great for hiding complexity and controlling access.

```sql
CREATE VIEW active_users AS
SELECT id, name, email FROM users WHERE status = 'ACTIVE';

SELECT * FROM active_users;   -- use it like a table
```

Benefits: simplify complex queries, security (hide columns), reusability.

---

## Part B — Stored Procedures

### 🧠 Concept
A **stored procedure** is a **saved block of SQL** you can run by name, optionally with inputs.
Runs on the database server.

```sql
CREATE PROCEDURE GetUserOrders(IN uid INT)
BEGIN
    SELECT * FROM orders WHERE user_id = uid;
END;

CALL GetUserOrders(1);
```

Benefits: reusable, faster (precompiled), less network traffic.

---

## Part C — Triggers

### 🧠 Concept
A **trigger** is code that runs **automatically** when an event happens (INSERT/UPDATE/DELETE)
on a table. Great for audit logs and auto-updates.

```sql
CREATE TRIGGER log_new_user
AFTER INSERT ON users
FOR EACH ROW
INSERT INTO audit_log(user_id, action) VALUES (NEW.id, 'CREATED');
```

`BEFORE`/`AFTER` + `INSERT`/`UPDATE`/`DELETE`. `NEW` = new row, `OLD` = old row.

---

## Part D — Aggregate Functions

### 🧠 Concept
Aggregate functions summarize many rows into **one value**.

```sql
SELECT COUNT(*), SUM(price), AVG(price), MIN(price), MAX(price)
FROM products;

-- Group and filter groups
SELECT city, COUNT(*) AS total
FROM users
GROUP BY city
HAVING COUNT(*) > 10;      -- HAVING filters groups
```

| Function | Meaning |
|----------|---------|
| COUNT | number of rows |
| SUM | total |
| AVG | average |
| MIN / MAX | smallest / largest |

> ⚠️ **WHERE** filters rows **before** grouping; **HAVING** filters **after** grouping.

---

## Part E — Window Functions (advanced, impressive!)

### 🧠 Concept
Window functions do calculations **across rows** related to the current row — **without**
collapsing them into one (unlike GROUP BY). Uses `OVER()`.

```sql
-- Rank employees by salary within each department
SELECT name, department, salary,
       RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS rank
FROM employees;
```

| Function | Meaning |
|----------|---------|
| `ROW_NUMBER()` | unique row number |
| `RANK()` | rank with gaps (1,2,2,4) |
| `DENSE_RANK()` | rank without gaps (1,2,2,3) |
| `LEAD()/LAG()` | next / previous row value |
| `SUM() OVER()` | running total |

---

## 🌍 Real-World Use Cases
- **View** → a "customer summary" screen.
- **Procedure** → monthly report generation.
- **Trigger** → auto-log every balance change in banking.
- **Window functions** → leaderboards, "top 3 per category", running totals.

---

## ❓ Interview Questions
1. What is a view? Advantages?
2. Can we update data through a view? (Simple views: yes; complex: usually no)
3. What is a stored procedure vs function?
4. What is a trigger? Give a use case.
5. Difference between WHERE and HAVING?
6. Difference between GROUP BY and window functions?
7. Difference between RANK, DENSE_RANK, and ROW_NUMBER?
8. What does PARTITION BY do?

---

## ✅ Best Practices
- Use views to simplify and secure data access.
- Keep triggers small — heavy triggers slow down writes.
- Prefer window functions for ranking/running totals over complex subqueries.

## ⚠️ Common Mistakes
- Using WHERE to filter aggregated results (use HAVING).
- Heavy logic in triggers causing hidden slowdowns.
- Expecting GROUP BY to keep individual rows (it collapses them).

---

## ⚡ Quick Revision Notes
- View = virtual table (saved query).
- Stored procedure = saved reusable SQL block.
- Trigger = auto-runs on INSERT/UPDATE/DELETE.
- Aggregates: COUNT/SUM/AVG/MIN/MAX + GROUP BY; HAVING filters groups.
- Window functions: `OVER(PARTITION BY ... ORDER BY ...)` keep all rows.

## 🙋 FAQs
**Q: RANK vs DENSE_RANK?** RANK skips numbers after ties (1,2,2,4); DENSE_RANK doesn't (1,2,2,3).

## 📎 References
- Mode SQL — Window Functions
- PostgreSQL docs

[⬅ Back to SQL Index](./README.md)

