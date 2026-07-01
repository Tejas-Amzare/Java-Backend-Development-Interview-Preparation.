# 🎤 Detailed Spoken Answers — SQL & Databases

> Model answers written to **speak out loud** in an interview. Formula:
> `Definition → Example → Why it matters.` Speak calmly, 30–60 seconds each.

---

## 1. What is the difference between a primary key and a foreign key? 🔥

> "A **primary key** uniquely identifies each row in a table. It must be **unique** and
> **cannot be null**, and a table can have only **one** primary key — for example, the `id`
> column in a `users` table.
>
> A **foreign key** is a column in one table that **points to the primary key of another
> table**. It creates a **relationship** between the two tables and keeps the data consistent —
> this is called referential integrity. For example, in an `orders` table, a `user_id` foreign
> key links each order to a real user.
>
> So in short: the primary key identifies a row, and the foreign key connects rows across
> tables."

---

## 2. Explain the different types of JOINs 🔥

> "A JOIN combines rows from two or more tables based on a related column.
>
> An **INNER JOIN** returns only the rows that **match in both tables**. A **LEFT JOIN** returns
> **all rows from the left table**, plus matching rows from the right — and null where there's no
> match. A **RIGHT JOIN** is the opposite: all rows from the right table plus matches from the
> left. A **FULL OUTER JOIN** returns **all rows from both** tables. And a **SELF JOIN** is when
> a table is joined with itself — useful for things like employees and their managers.
>
> A practical example: to get all users **and** their orders, but still include users who
> haven't ordered anything, I'd use a **LEFT JOIN** from users to orders."

---

## 3. What is normalization? Explain 1NF, 2NF, 3NF 🔥

> "Normalization is the process of organizing tables to **reduce data redundancy** and avoid
> update problems, by splitting large tables into smaller related ones.
>
> **First Normal Form** means each cell holds a **single atomic value** — no repeating groups or
> lists in one column. **Second Normal Form** builds on that and removes **partial
> dependencies** — every non-key column must depend on the **whole** primary key, not just part
> of it. **Third Normal Form** removes **transitive dependencies** — no non-key column should
> depend on another non-key column.
>
> The benefit is clean, consistent data. But for read-heavy reporting systems, I sometimes
> **denormalize** on purpose to reduce joins and speed up reads — it's a trade-off between
> consistency and performance."

---

## 4. What are ACID properties? 🔥

> "ACID describes the four guarantees of a reliable database transaction.
>
> **Atomicity** means all-or-nothing — either every operation in the transaction succeeds, or
> none do. **Consistency** means the database moves from one valid state to another, keeping all
> rules intact. **Isolation** means concurrent transactions don't interfere with each other.
> And **Durability** means once a transaction is committed, it stays saved even if the system
> crashes.
>
> The classic example is a **bank transfer**: money is debited from one account and credited to
> another. Atomicity ensures that if the second step fails, the first is rolled back — so money
> is never lost."

---

## 5. What is an index and how does it improve performance? 🔥

> "An index is a data structure — usually a **B-tree** — that helps the database **find rows
> quickly**, similar to the index at the back of a book.
>
> Without an index, the database does a **full table scan**, checking every row, which is O(n).
> With an index on a column, it can jump straight to the data in about O(log n). So I add
> indexes on columns I frequently use in `WHERE`, `JOIN`, and `ORDER BY` clauses — like `email`
> in a users table.
>
> The trade-off is that indexes **slow down writes** — inserts, updates, and deletes — because
> the index also has to be updated, and they use extra storage. So I index selectively, not
> every column."

---

## 6. What is the difference between WHERE and HAVING? 🔥

> "Both filter data, but at different stages.
>
> **WHERE** filters **individual rows before** they are grouped. **HAVING** filters **groups
> after** a `GROUP BY` has been applied — so it's typically used with aggregate functions like
> COUNT or SUM.
>
> For example, if I want cities that have **more than 10 users**, I group by city and then use
> `HAVING COUNT(*) > 10`. I can't use WHERE for that because the count doesn't exist until after
> grouping. A simple rule: **WHERE before grouping, HAVING after grouping.**"

---

## 7. Difference between DELETE, TRUNCATE, and DROP? 🔥

> "All three remove data, but differently.
>
> **DELETE** removes **specific rows** based on a WHERE condition, and it can be **rolled back**
> because it's logged. **TRUNCATE** removes **all rows** at once — it's much faster because it
> doesn't log each row, but it usually **can't be rolled back** and it keeps the table
> structure. **DROP** removes the **entire table** — both data and structure.
>
> So: DELETE for selected rows with rollback, TRUNCATE to quickly empty a table, and DROP to
> remove the table completely."

---

## 8. How do you find the second highest salary? 🔥 (very common)

> "There are a couple of clean ways. The simplest is a subquery — I find the maximum salary
> that is **less than the overall maximum**:
>
> `SELECT MAX(salary) FROM employees WHERE salary < (SELECT MAX(salary) FROM employees);`
>
> A more scalable way, especially for the **Nth** highest, is a window function with
> `DENSE_RANK`: I rank salaries in descending order and pick where the rank equals 2.
> `DENSE_RANK` is better than `ROW_NUMBER` here because it correctly handles duplicate salaries.
> I'd mention both approaches to show I understand the trade-offs."

---

## 9. What are window functions? How are they different from GROUP BY? ⭐

> "Window functions perform calculations **across a set of rows related to the current row**,
> but **without collapsing** those rows into one — that's the key difference from `GROUP BY`.
>
> With `GROUP BY`, many rows become a single summary row. With a window function, each row keeps
> its identity **and** gets an extra calculated value, using the `OVER()` clause.
>
> For example, `RANK() OVER (PARTITION BY department ORDER BY salary DESC)` ranks employees
> within each department by salary, while still showing every employee. They're great for
> leaderboards, running totals, and 'top N per group' problems. Common ones are `ROW_NUMBER`,
> `RANK`, `DENSE_RANK`, and `LEAD`/`LAG`."

---

## 10. What is the difference between UNION and UNION ALL? ⭐

> "Both combine the results of two queries by **stacking rows**, and both need the same number
> and types of columns.
>
> The difference is that **UNION removes duplicate rows**, which means the database does extra
> work to sort and de-duplicate. **UNION ALL keeps all rows**, including duplicates, so it's
> **faster**.
>
> So if I know there are no duplicates, or I don't care about them, I use **UNION ALL** for
> better performance."

---

## 11. What is a transaction and how do you use it? ⭐

> "A transaction is a **group of SQL operations treated as one single unit** — they all succeed
> or all fail together.
>
> I start it with `BEGIN`, run my statements, and then either `COMMIT` to save everything
> permanently, or `ROLLBACK` to undo everything if something goes wrong. I can also set a
> `SAVEPOINT` to roll back partially.
>
> The classic use case is a money transfer — debit one account and credit another inside one
> transaction, so the database is never left in a half-finished state."

---

## 12. What is a deadlock in a database and how do you avoid it? ⭐

> "A deadlock happens when **two transactions each hold a lock the other needs**, so both wait
> forever. For example, transaction A locks row 1 and wants row 2, while transaction B locks
> row 2 and wants row 1.
>
> To avoid deadlocks, I **access resources in a consistent order**, keep transactions **short**,
> and use appropriate **isolation levels**. Most databases also detect deadlocks automatically
> and kill one transaction so the other can proceed — and my application should be ready to
> **retry** the failed one."

---

## 13. How would you optimize a slow SQL query? ⭐

> "First, I'd run `EXPLAIN` to see the query plan and check whether it's doing a **full table
> scan**. Then I'd apply the usual optimizations:
>
> I **add indexes** on the columns used in WHERE, JOIN, and ORDER BY. I **select only the
> columns I need** instead of `SELECT *`. I **avoid functions on indexed columns** in the WHERE
> clause, because that prevents the index from being used. I **replace correlated subqueries with
> joins** where possible, and I use **pagination with LIMIT** for large result sets.
>
> I'd also watch out for the **N+1 query problem** if an ORM is involved, and fix it with a join
> fetch. The goal is fewer scans and fewer round trips to the database."

---

## 🗣️ Speaking Tips for SQL Rounds
- When asked "difference between X and Y", **always give a verbal comparison** (X does this, Y
  does that).
- **Offer to write the query** — interviewers love when you volunteer code.
- Mention **performance/indexing** even in design questions — shows senior thinking.
- For tricky queries, **think out loud**: "First I'll group, then filter with HAVING…".

[⬅ Back to Questions Index](./README.md) · [Full SQL Q Bank](./02-SQL.md)

