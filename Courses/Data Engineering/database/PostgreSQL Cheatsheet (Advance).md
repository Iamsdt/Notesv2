---
Created by: Shudipto Trafder
Created time: 2024-11-12T17:50:00
Last edited by: Shudipto Trafder
Last edited time: 2024-11-14T17:54:00
tags:
  - sql
  - psql
  - database
---

### 1. DBML Commands (Database Markup Language)

| Command    | Description                           | Example                                                                                                              |
| ---------- | ------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| **SELECT** | Retrieves data from a database.       | `SELECT first_name, last_name FROM customers;`                                                                       |
| **INSERT** | Adds new records to a table.          | `INSERT INTO customers (first_name, last_name, email, city) VALUES ('Mary', 'Doe', 'marydoe@email.com', 'newyork');` |
| **UPDATE** | Modifies existing records in a table. | `UPDATE employees SET first_name = 'John', department = 'Marketing';`                                         |
| **DELETE** | Removes records from a table.         | `DELETE FROM employees WHERE first_name = 'John';`                                                            |

### 2. DDL Commands (Data Definition Language)

| Command         | Description                            | Example                                                  |
| --------------- | -------------------------------------- | -------------------------------------------------------- |
| CREATE DATABASE | Creates a new database.                | `CREATE DATABASE mydatabase;`                            |
| CREATE TABLE    | Creates a new table.                   | `CREATE TABLE users (id SERIAL PRIMARY KEY, name TEXT);` |
| ALTER TABLE     | Modifies an existing table.            | `ALTER TABLE users ADD COLUMN email TEXT;`               |
| DROP TABLE      | Deletes a table.                       | `DROP TABLE users;`                                      |
| CREATE INDEX    | Creates an index (speeds up searches). | `CREATE INDEX users_name_idx ON users (name);`           |

### 3. DCL Commands (Data Control Language)

| Command   | Description                                          | Example                     |
|-----------|------------------------------------------------------|------------------------------|
| GRANT      | Grants privileges to users.                        | `GRANT SELECT ON users TO public;` |
| REVOKE     | Revokes privileges from users.                       | `REVOKE SELECT ON users FROM public;` |

### 4. Query Commands (DQL - Data Query Language)

| Command  | Description                                             | Example                                  |
| -------- | ------------------------------------------------------- | ---------------------------------------- |
| SELECT   | Retrieves data from a table.                            | `SELECT * FROM users;`                   |
| FROM     | Specifies the table to retrieve data from.              | `SELECT name FROM users;`                |
| WHERE    | Filters data based on a condition.                      | `SELECT * FROM users WHERE id = 1;`      |
| ORDER BY | Sorts the result set.                                   | `SELECT * FROM users ORDER BY name ASC;` |
| LIMIT    | Limits the number of rows returned.                     | `SELECT * FROM users LIMIT 10;`          |
| OFFSET   | Skips a specified number of rows before returning rows. | `SELECT * FROM users OFFSET 5;`          |
| DISTINCT | Returns only distinct (different) values.               | `SELECT DISTINCT city FROM customers;`   |

### 5. Join Commands

| Join Type  | Description                                                                  | Example                                                                                    |
| ---------- | ---------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| INNER JOIN | Returns rows only when there is a match in both tables.                      | `SELECT * FROM orders INNER JOIN customers ON orders.customer_id = customers.customer_id;` |
| LEFT JOIN  | Returns all rows from the left table and matching rows from the right table. | `SELECT * FROM orders LEFT JOIN customers ON orders.customer_id = customers.customer_id;`                       |
| RIGHT JOIN | Returns all rows from the right table and matching rows from the left table. | `SELECT * FROM orders RIGHT JOIN customers ON orders.customer_id = customers.customer_id;`                      |
| FULL JOIN  | Returns all rows from both tables, regardless of a match.                    | `SELECT * FROM orders FULL JOIN customers ON orders.customer_id = customers.customer_id;`|

### 6. Subquery
| Command | Description                                                        | Example                                                                                                                                                                               |
| ------- | ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **IN**  | Determines whether a value matches any value in a subquery result. | `SELECT first_name, last_name FROM customers WHERE customer_id IN (SELECT customer_id FROM orders);`                                                                                  |
| **ANY** | Compares a value to any value returned by a subquery.              | `SELECT order_id, total_amount FROM orders WHERE total_amount > ANY (SELECT total_amount FROM orders WHERE customer_id = 1);`                                                         |
| **ALL** | Compares a value to all values returned by a subquery.             | `SELECT first_name, last_name FROM customers WHERE customer_id IN (SELECT customer_id FROM orders WHERE total_amount > ALL (SELECT total_amount FROM orders WHERE customer_id = 1));` |

### 7. Aggregate Functions

| Function | Description                               | Example                               |
|----------|-------------------------------------------|---------------------------------------|
| COUNT()  | Counts the number of rows.                | `SELECT COUNT(*) FROM customers;`         |
| SUM()    | Calculates the sum of a numeric column.    | `SELECT SUM(price) FROM orders;`      |
| AVG()    | Calculates the average of a numeric column. | `SELECT AVG(price) FROM orders;`         |
| MIN()    | Finds the minimum value in a column.       | `SELECT MIN(price) FROM orders;`  |
| MAX()    | Finds the maximum value in a column.       | `SELECT MAX(price) FROM products;`     |

### 8. String Commands

| Function     | Description                                                | Example                                          |
|--------------|------------------------------------------------------------|---------------------------------------------------|
| LENGTH(str) | Returns the length of a string.                        | `SELECT LENGTH('Hello');` --> 5                |
| LOWER(str)  | Converts a string to lowercase.                          | `SELECT LOWER('PostgreSQL');` --> postgresql |
| UPPER(str)  | Converts a string to uppercase.                          | `SELECT UPPER('PostgreSQL');` --> POSTGRESQL |
| SUBSTRING(str, start, length) | Extracts a substring from a string.             | `SELECT SUBSTRING('PostgreSQL', 1, 4);` --> Post |
| REPLACE(str, from, to) | Replaces all occurrences of a substring.          | `SELECT REPLACE('Hello World', 'World', 'PostgreSQL');` |
| CONCAT(str1, str2, ...) | Concatenates two or more strings.               | `SELECT CONCAT('Hello', ' ', 'World');` --> Hello World |

### 9. Date/Time Commands

| Function         | Description                                         | Example                                              |
|------------------|-----------------------------------------------------|-------------------------------------------------------|
| NOW()           | Returns the current date and time.                  | `SELECT NOW();`                                       |
| CURRENT_DATE   | Returns the current date.                           | `SELECT CURRENT_DATE;`                               |
| CURRENT_TIME   | Returns the current time.                           | `SELECT CURRENT_TIME;`                               |
| EXTRACT(field FROM source) | Extracts a specific part (year, month, day) from a date/time value. | `SELECT EXTRACT(YEAR FROM NOW());`                      |
| DATE_PART(field, source) | Extracts a specific part (year, month, day) from a date/time value. | `SELECT DATE_PART('year', NOW());`                    |
| AGE(timestamp) | Calculates the age (in years) from a timestamp.    | `SELECT AGE(hire_date) FROM employees;`             |

### 10. Conditions

| Operator  | Description                     |
|-----------|---------------------------------|
| =         | Equal to                        |
| <>        | Not equal to                    |
| !=        | Not equal to (alternative)       |
| >         | Greater than                    |
| <         | Less than                       |
| >=        | Greater than or equal to         |
| <=        | Less than or equal to            |
| BETWEEN    | Between a range of values        |
| LIKE      | Matches a pattern                |
| IN        | In a list of values              |
| IS NULL   | Checks for null values           |
| IS NOT NULL | Checks for non-null values        |

Conditional Expressions

| Command  | Description                                                                     | Example                                                                                                                                                                                          |
| -------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| CASE     | The CASE statement allows you to perform conditional logic within a query.      | `SELECT order_id, total_amount, CASE WHEN total_amount > 1000 THEN 'High Value Order' WHEN total_amount > 500 THEN 'Medium Value Order' ELSE 'Low Value Order' END AS order_status FROM orders;` |
| COALESCE | The COALESCE() function returns the first non-null value from a list of values. | `SELECT COALESCE(first_name, last_name) AS preferred_name FROM customers;`                                                                                                                       |
| NULLIF   | The NULLIF() function returns null if two specified expressions are equal       | `SELECT NULLIF(total_amount, discounted_amount) AS diff_amount FROM orders;`                                                                                                                     |

### 11. Set Operations

| Operator  | Description                                         | Example                                                                                              |
| --------- | --------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| UNION     | Combines the results of two or more queries.        | `SELECT first_name, last_name FROM customers UNION SELECT first_name, last_name FROM employees;`     |
| INTERSECT | Returns rows common to both queries.                | `SELECT first_name, last_name FROM customers INTERSECT SELECT first_name, last_name FROM employees;` |
| EXCEPT    | Returns rows in the first query but not the second. | `SELECT first_name, last_name FROM customers EXCEPT SELECT first_name, last_name FROM employees;`    |

### 12. Indexes

**Purpose:** Improve the speed of data retrieval operations (SELECT queries) on tables.

**How they work:** Indexes create a separate data structure that stores a subset of table data in a sorted order or a hash structure. This allows the database to locate matching rows much faster than scanning the entire table.

**Syntax:**

```sql
CREATE [UNIQUE] INDEX index_name
ON table_name (column_name [ASC | DESC], ...);
```

Create index in order table on order_date
```sql
CREATE INDEX order_date_idx ON orders (order_date);
```

**Types of Indexes:**

| Index Type             | Description                                                                                        |
|-------------------------|----------------------------------------------------------------------------------------------------|
| **B-tree (Default)**      | Suitable for equality and range queries, as well as sorting. Most common index type.            |
| **Hash**                | Very fast for equality comparisons, but not suitable for range queries or sorting.                 |
| **GIN (Generalized Inverted Index)** | Efficient for searching arrays and other composite data types. Useful for full-text search.   |
| **GiST (Generalized Search Tree)**   | Used for geometric and spatial data types, as well as full-text search. Provides flexible indexing. |
| **SP-GiST (Space-Partitioned GiST)** |  Variant of GiST optimized for multidimensional data.                                                |
| **BRIN (Block Range Index)**       | Designed for very large tables, storing index data at a block level to save space.                |

**Choosing the Right Index:**

- **Equality Queries:** Use B-tree or Hash indexes on frequently queried columns.
- **Range Queries:** B-tree is the best choice.
- **Sorting:** B-tree indexes can speed up sorting on indexed columns.
- **Full-Text Search:** Use GIN or GiST indexes depending on your specific requirements.
- **Multi-Column Indexes (Composite Indexes):** Create indexes on multiple columns to optimize complex queries. The order of columns in the index definition matters!

### 13. Transaction

| Command  | Description                      | Example                                                                                                                                                                                                                 |
| -------- | -------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| COMMIT   | Commits the current transaction. | BEGIN TRANSACTION;  <br/> -- SQL statements and changes within the transaction <br/>INSERT INTO users (name) VALUES ('Alice'); <br/>UPDATE products SET unit_price = 25.00 WHERE category = 'Electronics'; <br/>COMMIT; |
| ROLLBACK | Reverts the current transaction. | BEGIN TRANSACTION; <br/>-- SQL statements and changes within the transaction <br/>INSERT INTO users (name) VALUES ('Bob'); <br/>UPDATE products SET unit_price = 30.00 WHERE category = 'Electronics'; <br/>ROLLBACK;   |

### 14. Window Function
* Performs a calculation across a set of table rows. 
* Example: `SELECT name, salary, AVG(salary) OVER () AS avg_salary FROM employees;`

```sql
function_name(arguments) OVER ( [PARTITION BY column] [ORDER BY column] [frame_clause] )
```

**Components:**

- **`function_name`:**  Aggregate function (SUM, AVG, COUNT, etc.), ranking function (RANK, DENSE_RANK, ROW_NUMBER), or others.
- **`arguments`:** Columns or expressions used by the function.
- **`OVER clause`:** Defines the window:
    - **`PARTITION BY column`:** (Optional) Divides rows into groups (partitions).
    - **`ORDER BY column`:** (Optional) Specifies the order within each partition.
    - **`frame_clause`:** (Optional) Further defines the window using keywords like `ROWS`, `RANGE`, `PRECEDING`, `FOLLOWING`.

**Common Window Functions:**

| Function                   | Description                                                          |
| -------------------------- | -------------------------------------------------------------------- |
| **`ROW_NUMBER()`**         | Assigns a unique sequential number to each row within its partition. |
| **`RANK()`**               | Assigns a rank to each row, with ties receiving the same rank.       |
| **`DENSE_RANK()`**         | Similar to `RANK()`, but ties don't create gaps in rank values.      |
| **`SUM(column)`**          | Calculates the sum of `column` over the window.                      |
| **`AVG(column)`**          | Calculates the average of `column` over the window.                  |
| **`COUNT(column)`**        | Counts the number of non-null values in `column` over the window.    |
| **`FIRST_VALUE(column)`**  | Returns the first value of `column` in the window.                   |
| **`LAST_VALUE(column)`**   | Returns the last value of `column` in the window.                    |
| **`LAG(column, offset)`**  | Accesses data from a previous row within the partition.              |
| **`LEAD(column, offset)`** | Accesses data from a following row within the partition.             |

**Example:**

```sql
SELECT department, first_name, last_name,
AVG(salary) OVER (PARTITION BY department) AS avg_salary_dept
FROM employees;
```

This query calculates the average salary for each department using a window function and displays it alongside each employee's information. 

### 15. WITH Keyword (Common Table Expressions - CTE)

* Defines a temporary named result set.
* Example:
```sql
WITH top_order AS (
	SELECT order_id, SUM(total_amount) AS total_sold
	FROM orders
	GROUP BY order_id
	ORDER BY total_sold DESC
	LIMIT 10
)
SELECT * FROM top_order;
```

### 16. View

* A virtual table based on a stored query.
* Created with `CREATE VIEW view_name AS SELECT ...`.
```sql
CREATE OR REPLACE VIEW order_summary AS
SELECT
	c.first_name,
	c.last_name,
	COUNT(o.order_id) AS order_count,
	SUM(o.total_amount) AS total_spent
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_id, c.first_name, c.last_name;
```

### 17. Materialized View

* A pre-computed view that stores data physically.
* Created with `CREATE MATERIALIZED VIEW view_name AS SELECT ...`.
```sql
CREATE MATERIALIZED VIEW order_summary_materilized AS
SELECT
	c.first_name,
	c.last_name,
	COUNT(o.order_id) AS order_count,
	SUM(o.total_amount) AS total_spent
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_id, c.first_name, c.last_name;
```

### 18. Query Analysis (Explain Plan)

* Use `EXPLAIN` or `EXPLAIN ANALYZE` to understand the query plan.
```sql
EXPLAIN ANALYSE SELECT c.first_name, SUM(o.total_amount)
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
where city = 'City11'
GROUP BY c.customer_id, c.first_name;
```

### 19. Partition
**Purpose:** Improve performance for large tables by dividing them into logical parts.
* Divides a table into logical parts for performance.
* Created with `CREATE TABLE ... PARTITION BY ...`.

**Types:**
- **Range Partitioning:** Partitions are based on a range of values in a specified column (e.g., dates, numbers).
- **List Partitioning:** Partitions contain a specific list of values for a column.
- **Hash Partitioning:** Partitions are determined by a hash function applied to a column.

**Creating Partitioned Tables:**

1. **Create the Master Table (Partitioned Table):**
   ```sql
   CREATE TABLE table_name (
       -- Column definitions
   ) PARTITION BY RANGE (partition_column);
   ```

2. **Create Partitions:**
   ```sql
   CREATE TABLE partition_name PARTITION OF table_name
   FOR VALUES FROM (start_value) TO (end_value);
   ```

**Example: Range Partitioning (Orders by Year)**

```sql
-- Create the master table partitioned by order date
CREATE TABLE orders_partitioned (
	order_id SERIAL,
	customer_id INT REFERENCES customers(customer_id),
	order_date DATE,
	total_amount NUMERIC(10, 2),
	status VARCHAR(20) CHECK (status IN ('Pending', 'Shipped', 'Delivered', 'Cancelled')),
	PRIMARY KEY (order_id, order_date)
) PARTITION BY RANGE (order_date);

-- Create partitions for specific years
CREATE TABLE orders_2023 PARTITION OF orders_partitioned
FOR VALUES FROM ('2023-01-01') TO ('2024-01-01');

CREATE TABLE orders_2024 PARTITION OF orders_partitioned
FOR VALUES FROM ('2024-01-01') TO ('2025-01-01');
```

Insert Data from `orders` table
```sql
INSERT INTO orders_partitioned (order_id, customer_id, order_date, total_amount, status)
SELECT order_id, customer_id, order_date, total_amount, status
FROM orders;
```

Query data
```sql
select * from orders_partitioned;
explain select * from orders_partitioned;
```

Date based query
```sql
select * from orders_partitioned where order_date BETWEEN '2024-01-01' AND '2024-12-31';
explain select * from orders_partitioned where order_date BETWEEN '2024-01-01' AND '2024-12-31';
```

**Benefits:**

- **Improved Query Performance:** Queries targeting specific partitions can be processed much faster.
- **Faster Data Loads and Deletes:** Operations on individual partitions are generally more efficient.
- **Easier Maintenance:** Archiving or deleting old data is simplified by dropping or truncating partitions.

**Important Considerations:**
- Choose appropriate partition keys for your queries.
- Ensure that data is distributed evenly across partitions to avoid "partition skew."
- Test queries with `EXPLAIN` to verify that partitions are being used effectively. 

### 20. Trigger
**Purpose:** Define actions that automatically execute before or after specific database events (e.g., INSERT, UPDATE, DELETE).
* A stored procedure that automatically executes when an event occurs.
* Created with `CREATE TRIGGER trigger_name ... ON table_name ...`. 

**Types:**
- **Statement-Level Triggers:** Execute once per SQL statement, regardless of the number of rows affected.
- **Row-Level Triggers:** Execute once for each row affected by the statement.

**Syntax:**

```sql
CREATE [OR REPLACE] TRIGGER trigger_name
{ BEFORE | AFTER } { INSERT | UPDATE | DELETE } [OR ...]
ON table_name
[ FOR EACH { ROW | STATEMENT } ]
[ WHEN (condition) ]
EXECUTE FUNCTION function_name();
```

**Example: Updating Order Total using a Trigger**

```sql
-- 1. Table for order items
CREATE TABLE order_items (
    order_id INT REFERENCES orders(order_id),
    product_id INT REFERENCES products(product_id),
    quantity INT,
    price DECIMAL(10, 2)
);

-- 2. Function to calculate and update the order total 
CREATE OR REPLACE FUNCTION update_order_total()
RETURNS TRIGGER AS $$
BEGIN
    UPDATE orders
    SET total_amount = (
        SELECT SUM(quantity * price)
        FROM order_items
        WHERE order_id = NEW.order_id
    )
    WHERE order_id = NEW.order_id;
    RETURN NEW; 
END;
$$ LANGUAGE plpgsql;

-- 3. Trigger to call the function after changes to order_items
CREATE OR REPLACE TRIGGER update_order_total_trigger
AFTER INSERT OR UPDATE OR DELETE ON order_items
FOR EACH ROW 
EXECUTE FUNCTION update_order_total(); 
```

Add Data
```sql
INSERT INTO products (name, category, unit_price, stock)
VALUES
('Laptop', 'Electronics', 1200.00, 50),
('Phone', 'Electronics', 800.00, 100),
('Book', 'Stationery', 20.00, 200);

select * from products;
```

Now Insert into `order_items`
```sql
INSERT INTO order_items (order_id, product_id, quantity, price)
VALUES
(1, 1, 2, 1200.00), -- 2 Laptops
(1, 2, 1, 800.00); -- 1 Phone

-- verify total_amount
SELECT * FROM orders WHERE order_id = 1;
```

Update quantity
```sql
UPDATE order_items
SET quantity = 3
WHERE order_id = 1 AND product_id = 1;
```

Delete records
```sql
DELETE FROM order_items
WHERE order_id = 1 AND product_id = 2;
```

**Explanation:**
- **`update_order_total()` Function:** 
    - Calculates the total amount for the given `order_id` from `order_items`.
    - Updates the `total_amount` in the `orders` table.
- **`update_order_total_trigger` Trigger:**
    - Executes **after** any `INSERT`, `UPDATE`, or `DELETE` operation on the `order_items` table.
    - It's a **row-level trigger** ( `FOR EACH ROW`), so it runs for every row changed.
    - It calls the `update_order_total()` function to recalculate and update the order's total amount.


### Table and Data:
Please Create These tables first and generate data
Table: customers
```sql
CREATE TABLE customers (
    customer_id SERIAL PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    city VARCHAR(50),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
Table: employees
```sql
CREATE TABLE employees (
    employee_id SERIAL PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    department VARCHAR(50),
    hire_date DATE,
    salary NUMERIC(10, 2),
    is_active BOOLEAN DEFAULT TRUE,
    manager_id INT REFERENCES employees(employee_id) -- Self-referencing foreign key
);
```
Table: users
```sql
CREATE TABLE users (id SERIAL PRIMARY KEY, name TEXT);
```

Table: products
```sql
CREATE TABLE products (
    product_id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    category VARCHAR(50),
    unit_price NUMERIC(10, 2) NOT NULL,
    stock INT CHECK (stock >= 0)
);
```
Table: orders
```sql
CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    customer_id INT REFERENCES customers(customer_id),
    order_date DATE DEFAULT CURRENT_DATE,
    total_amount NUMERIC(10, 2) NOT NULL,
    status VARCHAR(20) CHECK (status IN ('Pending', 'Shipped', 'Delivered', 'Cancelled'))
);
```

#### Insert Data
Table: customers
```sql
INSERT INTO customers (first_name, last_name, email, city)
SELECT 
    'John' || i, 'Doe' || i, 
    'john.doe' || i || '@example.com', 
    'City' || (i % 100) 
FROM generate_series(1, 10000) AS s(i);
```

Table: orders
```sql
INSERT INTO orders (customer_id, order_date, total_amount, status)
SELECT 
    (random() * 1000 + 1)::int AS customer_id,
    CURRENT_DATE - (random() * 365)::int AS order_date,
    round((random() * 980 + 20)::numeric, 2) AS total_amount,
    CASE 
        WHEN random() < 0.25 THEN 'Pending'
        WHEN random() < 0.5 THEN 'Shipped'
        WHEN random() < 0.75 THEN 'Delivered'
        ELSE 'Cancelled'
    END AS status
FROM generate_series(1, 10000);
```

Table: employees
```sql
-- Randomize manager assignments for this example, assigning each employee a manager randomly (except for top-level employees).
WITH employee_data AS (
    SELECT 
        gs AS employee_id,  -- Use the series as the employee_id
        'First_' || gs AS first_name, 
        'Last_' || gs AS last_name,
        CASE 
            WHEN gs % 4 = 0 THEN 'Engineering'
            WHEN gs % 4 = 1 THEN 'Marketing'
            WHEN gs % 4 = 2 THEN 'Sales'
            ELSE 'HR'
        END AS department,
        NOW() - INTERVAL '1 day' * (gs % 365) AS hire_date, -- Randomize hire dates within the last year
        ROUND((40000 + (random() * 60000))::numeric, 2) AS salary, -- Salary between 40,000 and 100,000
        NULL AS manager_id  -- We'll assign managers in a second step
    FROM generate_series(1, 10000) AS gs
)
-- Insert employee data into employees table.
INSERT INTO employees (employee_id, first_name, last_name, department, hire_date, salary, manager_id)
SELECT 
    ed.employee_id, 
    ed.first_name, 
    ed.last_name, 
    ed.department, 
    ed.hire_date, 
    ed.salary,
    CASE
        WHEN ed.employee_id = 1 THEN NULL  -- Alice (id = 1) has no manager (top-level employee)
        ELSE FLOOR(random() * 10000) + 1  -- Randomly assign a manager from the list
    END AS manager_id
FROM employee_data ed;

```

## Advance Concepts

### 1. Efficient Data Loading Techniques

#### Using the `COPY` Command
The `COPY` command is efficient for loading data from external files:

```sql
COPY customers(first_name, last_name, email, city)
FROM '/path/to/customers.csv' 
WITH (FORMAT CSV, HEADER TRUE);
```

#### Temporary Table for Staging and Data Validation
```sql
CREATE TEMPORARY TABLE temp_customers (LIKE customers);

COPY temp_customers FROM '/path/to/customers_staging.csv' WITH (FORMAT CSV);

INSERT INTO customers
SELECT * FROM temp_customers
ON CONFLICT (email) DO NOTHING;  -- Avoid duplicate emails
```

### 2. Advanced ETL Patterns

#### Merge (Upsert) Operations
Use `ON CONFLICT` to handle upsert operations in PostgreSQL:

```sql
INSERT INTO customers (first_name, last_name, email, city)
VALUES ('John', 'Doe', 'john@example.com', 'New City')
ON CONFLICT (email) DO UPDATE 
SET 
    first_name = EXCLUDED.first_name,
    last_name = EXCLUDED.last_name,
    city = EXCLUDED.city;
```

### 3. Performance Optimization Techniques

#### Parallel Query Execution
Check current parallel workers
```sql
SHOW max_parallel_workers_per_gather;
```

```sql
-- Enable parallel workers for optimized aggregation
SET max_parallel_workers_per_gather = 4;

SELECT customer_id, COUNT(*)
FROM orders
GROUP BY customer_id;
```

### 4. Data Quality and Validation
#### Adding Constraints and Checks
```sql
ALTER TABLE orders
ADD CONSTRAINT check_amount CHECK (total_amount > 0),
ADD CONSTRAINT check_status CHECK (status IN ('Pending', 'Shipped', 'Delivered', 'Cancelled'));
```

### 5. Aggregate Operations
#### 5.1 json_agg
```sql
SELECT 
    c.customer_id,
    c.first_name,
    c.last_name,
    c.email,
    json_agg(
        json_build_object(
            'order_id', o.order_id,
            'order_date', o.order_date,
            'total_amount', o.total_amount,
            'status', o.status
        )
    ) AS orders
FROM 
    customers c
LEFT JOIN 
    orders o ON c.customer_id = o.customer_id
GROUP BY 
    c.customer_id;
```

#### 5.2 array_agg
```sql
SELECT 
    c.customer_id,
    c.first_name,
    c.last_name,
    c.email,
    array_agg(o.status) AS order_statuses
FROM 
    customers c
LEFT JOIN 
    orders o ON c.customer_id = o.customer_id
GROUP BY 
    c.customer_id;

```

Get all unique numbers
```sql
SELECT 
    c.customer_id,
    c.first_name,
    c.last_name,
    array_agg(DISTINCT o.order_date) AS unique_order_dates
FROM 
    customers c
LEFT JOIN 
    orders o ON c.customer_id = o.customer_id
GROUP BY 
    c.customer_id;

```

#### 5.3 string_agg
```sql
SELECT
	department,
	STRING_AGG(DISTINCT concat(first_name, last_name), ', ' ORDER BY concat(first_name, last_name)) as employee_list
FROM employees
GROUP BY department;
```
### 6. Window Functions for Analytics
```sql
WITH daily_totals AS (
	SELECT
	order_date,
	SUM(total_amount) AS daily_total_amount
	FROM
	orders
	GROUP BY
	order_date
	ORDER BY
	order_date
)
SELECT 
    order_date,
    daily_total_amount,
    AVG(daily_total_amount) OVER (
        ORDER BY order_date 
        ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
    ) AS moving_avg_7day,
    SUM(daily_total_amount) OVER (
        ORDER BY order_date
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS running_total
FROM 
    daily_totals;

```

Percentile Calculation
```sql
SELECT
	department,
	concat(first_name, last_name) as name,
	salary,
	PERCENT_RANK() OVER (PARTITION BY department ORDER BY salary) as salary_percentile,
	NTILE(4) OVER (PARTITION BY department ORDER BY salary) as salary_quartile
FROM employees;
```
Note: 
- `PERCENT_RANK() OVER (PARTITION BY department ORDER BY salary)` calculates the percentile rank of each employee’s salary within their department, giving a relative ranking from 0 to 1.
- `NTILE(4) OVER (PARTITION BY department ORDER BY salary)` divides employees in each department into four equal groups (quartiles) based on their salary.
- This is useful for understanding the distribution of salaries within each department, where 1 is the lowest quartile and 4 is the highest.


### 7. Advance View Technique
#### 7.1 Materialized View with concurrent Refresh

Lets create the view first
```sql
CREATE MATERIALIZED VIEW customer_order_summary AS
	SELECT
		c.customer_id,
		c.first_name,
		c.last_name,
		c.city,
		COUNT(o.order_id) AS total_orders,
		SUM(o.total_amount) AS total_spent,
		MAX(o.order_date) AS last_order_date,
		json_agg(
			json_build_object(
				'order_id', o.order_id,
				'order_date', o.order_date,
				'total_amount', o.total_amount,
				'status', o.status
			)
		) AS orders
FROM
customers c
LEFT JOIN
orders o ON c.customer_id = o.customer_id
GROUP BY
c.customer_id, c.first_name, c.last_name, c.city
ORDER BY total_orders DESC
WITH DATA;
```

Create Index
```sql
-- Step 2: Refresh Materialized View Concurrently -- You need to add an index to use CONCURRENTLY with the REFRESH 
CREATE UNIQUE INDEX idx_customer_order_summary ON customer_order_summary (customer_id);
```

Allow concurrent refresh
```sql
-- To update the view data while allowing concurrent access: 
REFRESH MATERIALIZED VIEW CONCURRENTLY customer_order_summary;
```

Validate
```sql
select * from customer_order_summary where customer_id = 354;

UPDATE customers set first_name = 'Jhon#354'
where customer_id = 354;

REFRESH MATERIALIZED VIEW CONCURRENTLY customer_order_summary;
select * from customer_order_summary where customer_id = 354;
```
##### Important Notes:
- **Concurrent Refresh Restrictions**: Concurrent refresh requires a unique index on at least one column in the materialized view.
- **Performance Considerations**: Regularly refreshing the materialized view, especially concurrently, may impact performance depending on the data size and the complexity of the view query.

Additional Notes: You can create a function and trigger. If anything changes, you can update the materialized view as well to keep all the data refreshed.

#### 7.2 Recursive Views
```sql
-- Create the Recursive View for Employee-Manager Hierarchy
CREATE VIEW employee_manager_hierarchy AS
WITH RECURSIVE manager_hierarchy AS (
    -- Base case: Select top-level employees (those with no manager)
    SELECT 
        e.employee_id,
        e.first_name,
        e.last_name,
        e.department,
        e.hire_date,
        e.salary,
        e.manager_id,
        1 AS level -- Top-level employees have level 1
    FROM employees e
    WHERE e.manager_id IS NULL

    UNION ALL

    -- Recursive case: Get employees who report to managers
    SELECT 
        e.employee_id,
        e.first_name,
        e.last_name,
        e.department,
        e.hire_date,
        e.salary,
        e.manager_id,
        mh.level + 1 AS level -- Increment the level for subordinates
    FROM employees e
    JOIN manager_hierarchy mh ON e.manager_id = mh.employee_id
)
-- Final select to get the complete hierarchy
SELECT 
    mh.employee_id,
    mh.first_name,
    mh.last_name,
    mh.department,
    mh.hire_date,
    mh.salary,
    mh.manager_id,
    mh.level,
    m.first_name AS manager_first_name,
    m.last_name AS manager_last_name
FROM 
    manager_hierarchy mh
LEFT JOIN 
    employees m ON mh.manager_id = m.employee_id
ORDER BY mh.level, mh.manager_id, mh.employee_id;

```

Lets verify
```sql
SELECT * FROM employee_manager_hierarchy;
```

#### 7.3 Parameterized View
Create a Custom Type for Parameters - This type will store the parameters for filtering the orders.
```sql
CREATE TYPE order_params AS (
    start_date date,
    end_date date,
    status_filter VARCHAR(20)
);

```

Create the Function -> Now, we define the function that returns a table. This function will accept `order_params` as input and return the filtered results from the `orders` table.
```sql
CREATE OR REPLACE FUNCTION filtered_orders(params order_params)
RETURNS TABLE (
    order_id INT,
    customer_id INT,
    order_date DATE,
    total_amount NUMERIC(10, 2),
    status VARCHAR(20)
) AS $$
BEGIN
    RETURN QUERY
    SELECT 
        o.order_id,
        o.customer_id,
        o.order_date,
        o.total_amount,
        o.status
    FROM orders o
    WHERE o.order_date BETWEEN params.start_date AND params.end_date
    AND (params.status_filter IS NULL OR o.status = params.status_filter);
END;
$$ LANGUAGE plpgsql;
```

Create the View Using the Function
```sql
CREATE OR REPLACE VIEW filtered_orders_view AS
SELECT *
FROM filtered_orders(
    (CURRENT_DATE - interval '30 days', 
     CURRENT_DATE, 
     'Shipped')::order_params
);
```

Query:
```sql
SELECT * FROM filtered_orders_view;
```

```sql
SELECT * 
FROM filtered_orders(
    ('2024-10-01', '2024-11-01', 'Delivered')::order_params
);
```

#### 7.4 View Performance Optimization
```sql
CREATE INDEX idx_mv_customer_activity_customer 
ON mv_customer_activity(customer_id);
```

```sql
CREATE INDEX idx_mv_customer_activity_high_value 
ON mv_customer_activity(customer_id)
WHERE total_spend > 1000;
```