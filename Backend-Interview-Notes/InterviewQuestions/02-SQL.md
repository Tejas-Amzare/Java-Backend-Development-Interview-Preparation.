# 02 — SQL & Databases Interview Questions (80+)

> Cover the answers and test yourself.

---


## 🗄️ Basics & CRUD (1–20)

1. **What is SQL?** Structured Query Language to manage relational databases.
2. **What is CRUD?** Create, Read, Update, Delete.
3. **DDL vs DML vs DCL vs TCL?** Define / manipulate / control access / transaction control.
4. **Examples of DDL?** CREATE, ALTER, DROP, TRUNCATE.
5. **Examples of DML?** INSERT, UPDATE, DELETE, SELECT.
6. **What is a primary key?** Unique + not null identifier for a row.
7. **What is a foreign key?** A column referencing another table's primary key.
8. **Primary key vs unique key?** PK: one, not null; Unique: many, allows one null.
9. **What is a composite key?** A primary key made of multiple columns.
10. **What is a candidate key?** Any column(s) that could be a primary key.
11. **What are constraints?** Rules: NOT NULL, UNIQUE, CHECK, DEFAULT, PK, FK.
12. **DELETE vs TRUNCATE vs DROP?** Rows (rollback) / all rows (fast) / whole table.
13. **What is referential integrity?** FK values must match a real PK (or be null).
14. **CHAR vs VARCHAR?** Fixed vs variable length.
15. **What is NULL?** Absence of a value (not 0 or empty string).
16. **How to check for NULL?** `IS NULL` / `IS NOT NULL`.
17. **What is `DISTINCT`?** Removes duplicate rows.
18. **What is `LIKE`?** Pattern matching (`%` any chars, `_` one char).
19. **What is `BETWEEN`?** Range check (inclusive).
20. **What is `IN`?** Matches any value in a list.

---

## 🔗 Joins (21–35)

21. **What is a join?** Combines rows from multiple tables on a related column.
22. **INNER JOIN?** Only matching rows in both tables.
23. **LEFT JOIN?** All left rows + matching right (NULL if none).
24. **RIGHT JOIN?** All right rows + matching left.
25. **FULL OUTER JOIN?** All rows from both tables.
26. **CROSS JOIN?** Cartesian product (all combinations).
27. **SELF JOIN?** A table joined with itself.
28. **Default JOIN type?** INNER JOIN.
29. **JOIN vs UNION?** Combines columns vs combines rows.
30. **UNION vs UNION ALL?** Removes duplicates vs keeps all (faster).
31. **How to find employees with no manager?** LEFT JOIN + `WHERE manager IS NULL`.
32. **How to find customers with no orders?** LEFT JOIN orders `WHERE order.id IS NULL`.
33. **What is an equi join?** Join using equality (=).
34. **What is a natural join?** Auto-joins on same-named columns.
35. **Can you join more than 2 tables?** Yes, chain multiple JOINs.

---

## 📐 Normalization & Design (36–48)

36. **What is normalization?** Organizing tables to reduce redundancy.
37. **Why normalize?** Avoid data duplication and update anomalies.
38. **What is 1NF?** Atomic values, no repeating groups.
39. **What is 2NF?** 1NF + no partial dependency on part of a composite key.
40. **What is 3NF?** 2NF + no transitive dependency on non-key columns.
41. **What is BCNF?** Stricter 3NF.
42. **What is denormalization?** Adding redundancy for faster reads.
43. **When to denormalize?** Read-heavy/reporting systems.
44. **What is a surrogate key?** An artificial key (e.g., auto-increment id).
45. **SQL vs NoSQL?** Structured+ACID vs flexible+scalable.
46. **What is a schema?** The structure/definition of the database.
47. **What is an ER diagram?** A visual model of entities and relationships.
48. **One-to-many relationship example?** A user has many orders.

---

## 🔒 Transactions & Indexes (49–65)

49. **What is a transaction?** A group of operations treated as one unit.
50. **What is COMMIT?** Save changes permanently.
51. **What is ROLLBACK?** Undo changes since the last commit.
52. **What is SAVEPOINT?** A marker to roll back to partially.
53. **What are ACID properties?** Atomicity, Consistency, Isolation, Durability.
54. **What is atomicity?** All operations succeed or none do.
55. **What is isolation?** Transactions don't interfere with each other.
56. **What are isolation levels?** Read Uncommitted, Read Committed, Repeatable Read, Serializable.
57. **What is a dirty read?** Reading uncommitted data.
58. **What is a phantom read?** New rows appear between reads.
59. **What is an index?** A structure for faster lookups (usually B-tree).
60. **Do indexes have downsides?** Yes — slower writes and more storage.
61. **Clustered vs non-clustered index?** Sorts rows physically (1) vs separate pointer structure.
62. **When to add an index?** On columns in WHERE, JOIN, ORDER BY.
63. **What is a covering index?** Index that contains all columns a query needs.
64. **What is a deadlock in DB?** Two transactions each waiting on the other's lock.
65. **Optimistic vs pessimistic locking?** Version check vs lock the row.

---

## 🧮 Aggregates, Windows & Advanced (66–82)

66. **What are aggregate functions?** COUNT, SUM, AVG, MIN, MAX.
67. **GROUP BY?** Groups rows for aggregation.
68. **WHERE vs HAVING?** Filter rows before vs groups after grouping.
69. **What is a subquery?** A query inside another query.
70. **Correlated subquery?** A subquery that depends on the outer query.
71. **What is a CTE?** `WITH` — a named temporary result set.
72. **What is a view?** A virtual table from a saved query.
73. **Can you update through a view?** Simple views yes; complex ones usually no.
74. **What is a stored procedure?** A saved reusable block of SQL.
75. **Stored procedure vs function?** Procedure does actions; function returns a value.
76. **What is a trigger?** Code that auto-runs on INSERT/UPDATE/DELETE.
77. **What are window functions?** Calculations across related rows without collapsing them.
78. **RANK vs DENSE_RANK vs ROW_NUMBER?** Gaps on ties / no gaps / unique sequence.
79. **What does PARTITION BY do?** Splits rows into groups for window functions.
80. **How to find the 2nd highest salary?** Subquery with MAX or DENSE_RANK = 2.
81. **How to find duplicates?** GROUP BY column HAVING COUNT(*) > 1.
82. **How to optimize a slow query?** Index columns, avoid SELECT *, use EXPLAIN, limit rows.

[⬅ Back to Questions Index](./README.md)

