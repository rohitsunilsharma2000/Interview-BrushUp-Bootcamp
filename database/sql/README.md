Below is a Markdown file layout with each question indexed and with a structure for answering each one.


# Database & SQL Queries FAQ

This document contains answers to frequently asked questions on database management, SQL queries, performance tuning, and more.

---

## Table of Contents

1. [Truncate Vs Delete](#truncate-vs-delete)
2. [Delete Vs Drop](#delete-vs-drop)
3. [How to Improve Database Performance and Which DB to Choose for High Performance](#improve-performance-db-choice)
4. [Migration from Oracle to SQL Server in JPA-based Application](#migration-oracle-to-sql-server-jpa)
5. [Optimizing Performance (Other than Caching and Indexing)](#optimizing-performance)
6. [How to Decide on Tomcat Thread Pools Size](#tomcat-thread-pools)
7. [Speed-up DB Processing - Indexing, Query Optimization, and Stored Procedures](#speed-up-db-processing)
8. [Oracle Performance Tuning & Indexing](#oracle-performance-tuning)
9. [Deadlock: What Is It and How to Resolve](#deadlock-resolution)
10. [Inner and Outer Join](#inner-outer-join)
11. [What is an Index?](#what-is-an-index)
12. [Database Connection Pooling](#database-connection-pooling)
13. [How to Fix Slow Queries](#fix-slow-queries)
14. [Left Outer Join Vs Right Outer Join](#left-outer-vs-right-outer-join)
15. [CAP Database Theorem](#cap-database-theorem)
16. [MySQL vs PostgreSQL vs MongoDB](#mysql-vs-postgresql-vs-mongodb)
17. [When to Use NoSQL vs RDBMS](#when-to-use-nosql-vs-rdbms)
18. [Types of Joins in MySQL](#types-of-joins-mysql)
19. [Nth Largest Value Query](#nth-largest-value-query)
20. [Write SQL Query for Joins (Person and Answers Tables)](#sql-query-joins-person-answers)
21. [Database Indexing](#database-indexing)
22. [How Indexing Works Internally](#how-indexing-works-internally)
23. [How to Avoid Duplicate Insert in DB](#avoid-duplicate-insert)
24. [Handling Duplicate Records in Database](#handling-duplicate-records)
25. [What Is a Query Plan](#query-plan)
26. [Database Connection Pooling](#database-connection-pooling)
27. [How to Improve Queries Fetching Data from Multiple Tables](#improve-query-fetching-multiple-tables)

---

## 1. Truncate Vs Delete
- **Truncate** removes all rows from a table without logging individual row deletions. It's faster but doesn't allow for rollback.
- **Delete** removes rows one by one and logs each row deletion, making it slower but allowing for rollback.

## 2. Delete Vs Drop
- **Delete** removes data from a table but keeps the table structure.
- **Drop** removes the entire table, including its data and structure.

## 3. How to Improve Database Performance and Which DB to Choose for High Performance
- You can improve performance through techniques like optimizing queries, using indexing, and partitioning tables.
- For high-performance databases, consider **PostgreSQL**, **MySQL**, or **SQL Server** for SQL-based workloads, and **MongoDB** or **Cassandra** for NoSQL.

## 4. Migration from Oracle to SQL Server in JPA-based Application
- Changes to **dialects** for SQL generation.
- Adjust **JPA queries** and **native SQL queries** as per SQL Server syntax.
- Test the application thoroughly for **performance** after migration.

## 5. Optimizing Performance (Other than Caching and Indexing)
- Use **partitioning** and **sharding** for large datasets.
- Optimize **queries** by eliminating subqueries, using **joins** efficiently, and avoiding unnecessary columns.
- Use **stored procedures** for repetitive tasks.

## 6. How to Decide on Tomcat Thread Pools Size
- Set thread pool size based on the number of **user connections** and **request load**.
- Start with default values, monitor the server's performance, and adjust accordingly to avoid resource exhaustion.

## 7. Speed-up DB Processing - Indexing, Query Optimization, and Stored Procedures
- Ensure **proper indexing** for frequent queries.
- Optimize **joins** and **subqueries**.
- Use **stored procedures** for common tasks and to reduce query parsing time.

## 8. Oracle Performance Tuning & Indexing
- Use **B-tree indexing**, **Bitmap indexing**, and **Clustered indexing** for performance optimization.
- Consider **partitioning** tables for large datasets.
- Ensure that **statistics** are updated regularly.

## 9. Deadlock: What Is It and How to Resolve
- **Deadlock** occurs when two or more transactions block each other, causing the system to freeze.
- **Resolution:** Use **transaction isolation levels**, optimize queries, and break transactions into smaller ones.

## 10. Inner and Outer Join
- **Inner Join** returns rows where there is a match in both tables.
- **Outer Join** returns all rows from one table and matched rows from another, filling with `NULL` where no match exists.

## 11. What is an Index?
An **index** in a database is a data structure that improves query speed by allowing the database to find rows more efficiently without scanning the entire table.

## 12. Database Connection Pooling
- Connection pooling is the practice of reusing a set of database connections instead of opening a new one for each request, which improves performance.

## 13. How to Fix Slow Queries
- Use **EXPLAIN** to analyze query execution plans.
- Ensure proper **indexing** and avoid unnecessary joins.
- Refactor queries to be more efficient.

## 14. Left Outer Join Vs Right Outer Join
- **Left Outer Join** returns all rows from the left table and matched rows from the right table.
- **Right Outer Join** returns all rows from the right table and matched rows from the left table.

## 15. CAP Database Theorem
- The **CAP theorem** states that in a distributed database system, you can have only **two** of the following: **Consistency**, **Availability**, or **Partition Tolerance**.

## 16. MySQL vs PostgreSQL vs MongoDB
- **MySQL** is fast and suitable for relational data.
- **PostgreSQL** supports complex queries and is known for its ACID compliance and extensibility.
- **MongoDB** is a NoSQL database, ideal for unstructured data and horizontal scaling.

## 17. When to Use NoSQL vs RDBMS
- Use **NoSQL** for unstructured, flexible data that needs high scalability.
- Use **RDBMS** for structured data with complex relationships and ACID requirements.

## 18. Types of Joins in MySQL
- **INNER JOIN**: Matches rows in both tables.
- **LEFT JOIN**: Includes all rows from the left table and matched rows from the right.
- **RIGHT JOIN**: Includes all rows from the right table and matched rows from the left.
- **FULL JOIN**: Includes rows from both tables.

## 19. Nth Largest Value Query
```sql
SELECT value FROM table ORDER BY value DESC LIMIT 1 OFFSET N-1;
```

## 20. Write SQL Query for Joins (Person and Answers Tables)
```sql
SELECT p.name
FROM Person p
JOIN Answers a ON p.id = a.person_id
GROUP BY p.name
ORDER BY COUNT(a.answer_id) DESC
LIMIT 1;
```

## 21. Database Indexing
- **Indexing** is the technique of creating a separate data structure to speed up data retrieval operations.
- Common types include **B-tree**, **hash indexing**, and **bitmap indexing**.

## 22. How Indexing Works Internally
- Indexes are created using **B-trees** or **hashes**, allowing the database to quickly locate rows based on key values.
- **B-trees** maintain a balanced structure for fast search and retrieval.

## 23. How to Avoid Duplicate Insert in DB
- Use **unique constraints** on columns.
- Use **UPSERT** or **INSERT ON DUPLICATE KEY UPDATE** for controlled insertion.

## 24. Handling Duplicate Records in Database
- Use **DISTINCT** to select unique rows.
- Use **GROUP BY** to eliminate duplicates based on certain columns.

## 25. What Is a Query Plan
A **query plan** is an execution strategy for a database query, showing how the database will access the data (e.g., using indexes, joins, etc.).

## 26. Database Connection Pooling (Duplicate Entry)
- Ensure **max connections** and **connection reuse** are tuned to avoid frequent open-close operations that slow down performance.

## 27. How to Improve Queries Fetching Data from Multiple Tables
- Use **proper indexes** for columns used in joins.
- **Avoid subqueries**; use **joins** where possible.
- Filter data as early as possible in the query.

---

## Additional References
- **Oracle Performance Tuning Guide**: [Oracle Documentation](https://docs.oracle.com/en/)
- **PostgreSQL Performance Optimization**: [PostgreSQL Docs](https://www.postgresql.org/docs/current/performance-optimization.html)
```

Each question has been given a specific index and structured answer. You can expand the answers as needed with more detailed explanations.