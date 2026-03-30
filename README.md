# PostgreSQL Database Troubleshooting

## Project Overview

This project demonstrates how to investigate and resolve database performance issues in PostgreSQL.

A slow query was analyzed using `EXPLAIN ANALYZE` and optimized by creating an index.

---

## Problem

The following query was performing poorly because PostgreSQL had to scan the entire table.

```sql
SELECT * FROM customers WHERE city = 'abc';
```

---

## Slow Query Execution

![Slow Query](screenshots/slow_query.png)

Execution Plan: **Sequential Scan**

This indicates PostgreSQL scanned the full table, which is inefficient for large datasets.

---

## Investigating Database Activity

To inspect running queries we used:

```sql
SELECT pid, usename, datname, state, query
FROM pg_stat_activity;
```

![pg_stat_activity](screenshots/pg_stat_activity.png)

This helps database engineers monitor active sessions and identify problematic queries.

---

## Solution

To optimize the query we created an index on the `city` column.

```sql
CREATE INDEX idx_city ON customers(city);
```

---

## Optimized Query Execution

![Optimized Query](screenshots/optimized_query.png)

After indexing, PostgreSQL used an **Index Scan** instead of a sequential scan, significantly improving performance.

---

## Skills Demonstrated

- PostgreSQL performance troubleshooting
- Query execution plan analysis
- Index optimization
- Database monitoring with `pg_stat_activity`
- CLI database debugging
