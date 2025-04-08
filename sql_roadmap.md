# SQL Roadmap 
## Index 
- Introduction 
- SELECT, INSERT, UPDATE, DELETE 
- DROP V/S TRUNCATE 
- JOIN's ( Inner join, Left Join, Outer Join, Full Join)
- The Use Of EXPLAIN
- Creating Indexes
- Aggregate Function 
- Ranking Function 
- Analytics function
- [The CTE's](https://hightouch.com/sql-dictionary/sql-common-table-expression-cte)
- Window Functions
- Performance Tuning 
- stored procedures
- Consider partitioning and sharding for MySQL and Postgres
- [Query Optimization](https://www.thoughtspot.com/data-trends/data-modeling/optimizing-sql-queries)
- Data Modeling 

## [The CTE's](https://hightouch.com/sql-dictionary/sql-common-table-expression-cte)
- Use to convert complex queries into smaller part or break down into smaller parts 
- Followed by with statement 
- Avoid wrtting multiple sub query 
- ``` WITH Supervisors AS (
    SELECT e.employee_id, e.employee_name, s.supervisor_name
    FROM employees e
    LEFT JOIN employees s ON e.supervisor_id = s.employee_id
)
SELECT employee_id, employee_name, supervisor_name
FROM Supervisors;```

## Window Function 
- Perform calculation accross set of ROW's 
- access data beyond the current row without grouping rows into a single output.
- whereas an aggregate operation groups query rows into a single result row, a window function produces a result for each query row
```
mysql> SELECT
         year, country, product, profit,
         SUM(profit) OVER() AS total_profit,
         SUM(profit) OVER(PARTITION BY country) AS country_profit
       FROM sales
       ORDER BY country, year, product, profit;
+------+---------+------------+--------+--------------+----------------+
| year | country | product    | profit | total_profit | country_profit |
+------+---------+------------+--------+--------------+----------------+
| 2000 | Finland | Computer   |   1500 |         7535 |           1610 |
| 2000 | Finland | Phone      |    100 |         7535 |           1610 |
| 2001 | Finland | Phone      |     10 |         7535 |           1610 |
| 2000 | India   | Calculator |     75 |         7535 |           1350 |
| 2000 | India   | Calculator |     75 |         7535 |           1350 |
| 2000 | India   | Computer   |   1200 |         7535 |           1350 |
| 2000 | USA     | Calculator |     75 |         7535 |           4575 |
| 2000 | USA     | Computer   |   1500 |         7535 |           4575 |
| 2001 | USA     | Calculator |     50 |         7535 |           4575 |
| 2001 | USA     | Computer   |   1200 |         7535 |           4575 |
| 2001 | USA     | Computer   |   1500 |         7535 |           4575 |
| 2001 | USA     | TV         |    100 |         7535 |           4575 |
| 2001 | USA     | TV         |    150 |         7535 |           4575 |
+------+---------+------------+--------+--------------+----------------+
```

## Performance tunning
- Performance tunning is checking and resolving issues potentially affecting the efficiency of a SQL database. 
- The key to good performance is ensuring queries execute quickly with minimal resources.
-  Common SQL performance tuning techniques:
Use indexes effectively
- Avoid SELECT (fetch only the columns you need)
- Use JOINs efficiently
- Avoid unnecessary subqueries
- Use WHERE clauses to filter data early
- Use EXPLAIN or EXPLAIN ANALYZE to understand how queries are executed
- Optimize database schema (e.g., normalization, denormalization when needed)
- Batch updates/inserts
- Use appropriate data types

## Data Modeling 
- Fact and Dimension tables -> A Fact table can be Orders and Customer , Addresses Can be dimension table 
- Star vs Snowflake schemas
- Slowly Changing Dimensions (SCDs) -> There might be some data in the database which is going to be changing lesser then the other for example the price of a product is not going to change after every order.
- 

