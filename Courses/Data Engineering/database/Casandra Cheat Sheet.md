## Cassandra and CQL: A Comprehensive Guide (Reimagined for Cassandra from SQL)

This guide reinterprets familiar database concepts from a PostgreSQL context and adapts them to Apache Cassandra, focusing on Cassandra Query Language (CQL) and its unique features.  The goal is to provide a comprehensive understanding of Cassandra without relying on any language than CQL.

### 1. DBML Commands (Database Markup Language) - CQL Equivalent

| PostgreSQL Command | Description                     | Cassandra CQL Equivalent                                                                                                        | Notes                                                                                                                                                              |
| :----------------- | :------------------------------ | :------------------------------------------------------------------------------------------------------------------------------ | :----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **SELECT**         | Retrieves data from a database. | `SELECT column1, column2 FROM keyspace_name.table_name WHERE condition;`                                                       | CQL requires explicit specification of columns unless `SELECT *` is used.                                                                                         |
| **INSERT**         | Adds new records to a table.    | `INSERT INTO keyspace_name.table_name (column1, column2) VALUES (value1, value2);`                                           | CQL uses `INSERT` similarly to SQL.                                                                                                                              |
| **UPDATE**         | Modifies existing records.      | `UPDATE keyspace_name.table_name SET column1 = value1, column2 = value2 WHERE primary_key_column = primary_key_value;`           | CQL updates require specifying the partition key in the `WHERE` clause.  Clustering columns may also be used in the `WHERE` clause to narrow the update scope. |
| **DELETE**         | Removes records.                | `DELETE FROM keyspace_name.table_name WHERE primary_key_column = primary_key_value;`                                             | CQL deletes require specifying the partition key.  You can delete specific columns or entire rows.                                                                 |

**Example:**

```cql
-- Select first_name and last_name from the customers table:
SELECT first_name, last_name FROM mykeyspace.customers;

-- Insert a new customer:
INSERT INTO mykeyspace.customers (customer_id, first_name, last_name, email, city) VALUES (UUID(), 'Mary', 'Doe', 'mary.doe@email.com', 'New York');

-- Update an existing customer's city:
UPDATE mykeyspace.customers SET city = 'Los Angeles' WHERE customer_id = UUID('your_customer_id_here');

-- Delete a customer:
DELETE FROM mykeyspace.customers WHERE customer_id = UUID('your_customer_id_here');
```

### 2. DDL Commands (Data Definition Language) - CQL

| PostgreSQL Command | Description                   | Cassandra CQL Equivalent                                                 | Notes                                                                                                                                                                   |
| :----------------- | :---------------------------- | :----------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| CREATE DATABASE    | Creates a new database.       | `CREATE KEYSPACE keyspace_name WITH replication = {...};`                 | In Cassandra, databases are called "keyspaces." Replication strategy is *required*.                                                                                    |
| CREATE TABLE       | Creates a new table.          | `CREATE TABLE keyspace_name.table_name (...);`                          | Table creation is similar, but primary key definition is crucial.                                                                                                      |
| ALTER TABLE        | Modifies an existing table.   | `ALTER TABLE keyspace_name.table_name ADD column_name data_type;`         | Limited `ALTER` operations compared to SQL.  You can add columns, but dropping columns is often best handled through schema evolution strategies.                      |
| DROP TABLE         | Deletes a table.              | `DROP TABLE keyspace_name.table_name;`                                  |                                                                                                                                                                       |
| CREATE INDEX       | Creates an index.             | `CREATE INDEX ON keyspace_name.table_name (column_name);`                | Secondary indexes are supported, but understanding their performance implications is critical.                                                                          |

**Example:**

```cql
-- Create a keyspace:
CREATE KEYSPACE mykeyspace WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 3};

-- Create a table:
CREATE TABLE mykeyspace.users (
    id UUID PRIMARY KEY,
    name text,
    email text
);

-- Add a column:
ALTER TABLE mykeyspace.users ADD age int;

-- Drop a table:
DROP TABLE mykeyspace.users;

-- Create an index on the name column:
CREATE INDEX ON mykeyspace.users (name);
```

### 3. DCL Commands (Data Control Language) - CQL

Cassandra's authorization model is more sophisticated and implemented differently. DCL is more suitable for database systems that comply with SQL standards. In Cassandra, it is accomplished through:

*   Roles: `CREATE ROLE`, `ALTER ROLE`, `DROP ROLE`
*   Permissions: `GRANT`, `REVOKE`

| PostgreSQL Command | Description                    | Cassandra CQL Equivalent                   | Notes                                                                                                                                         |
| :----------------- | :----------------------------- | :----------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------- |
| GRANT              | Grants privileges to users.    | `GRANT permission ON resource TO role;`    | Cassandra uses roles for access control.  Resources can be keyspaces, tables, functions, etc.  Permissions include SELECT, MODIFY, AUTHORIZE. |
| REVOKE             | Revokes privileges from users. | `REVOKE permission ON resource FROM role;` |                                                                                                                                               |

**Example:**

```cql
-- Create a role:
CREATE ROLE 'data_reader' WITH PASSWORD 'secure_password' AND LOGIN = TRUE;

-- Grant SELECT permission on the 'users' table to the 'data_reader' role:
GRANT SELECT ON mykeyspace.users TO 'data_reader';

-- Revoke SELECT permission:
REVOKE SELECT ON mykeyspace.users FROM 'data_reader';
```

### 4. Query Commands (DQL - Data Query Language) - CQL

| PostgreSQL Command | Description                                | Cassandra CQL Equivalent                                                         | Notes                                                                                                                                       |
| :----------------- | :----------------------------------------- | :------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------ |
| SELECT             | Retrieves data from a table.               | `SELECT * FROM keyspace_name.table_name WHERE ...;`                              |                                                                                                                                             |
| FROM               | Specifies the table to retrieve data from. | Implied in the `SELECT` statement.                                               |                                                                                                                                             |
| WHERE              | Filters data based on a condition.         | `SELECT ... FROM ... WHERE partition_key = value AND clustering_column = value;` | Requires the partition key.  Clustering columns can be used for further filtering.                                                          |
| ORDER BY           | Sorts the result set.                      | `SELECT ... FROM ... WHERE ... ORDER BY clustering_column ASC/DESC;`             | Allowed *only* on clustering columns and *requires* the partition key to be specified with an equality condition.                           |
| LIMIT              | Limits the number of rows returned.        | `SELECT ... FROM ... WHERE ... LIMIT n;`                                         |                                                                                                                                             |
| OFFSET             | Skips a specified number of rows.          | Not directly supported.  Requires alternative approaches (e.g., paging).         | Cassandra's distributed nature makes `OFFSET` inefficient.  Paging is the recommended approach for retrieving large datasets incrementally. |
| DISTINCT           | Returns only distinct values.              | Supported with restrictions.                                                     | Only supports `DISTINCT` on partition key (the first key) unless used with `clustering columns` and partition key is also defined.          |

**Example:**

```cql
-- Select all columns from the users table where id equals a UUID:
SELECT * FROM mykeyspace.users WHERE id = UUID('your_uuid_here');

-- Select users named 'John' (assuming 'name' is indexed):
SELECT * FROM mykeyspace.users WHERE name = 'John' ALLOW FILTERING; -- ALLOW FILTERING makes query possible but can be inefficient

-- Select users sorted by email:
SELECT * FROM mykeyspace.users WHERE id = UUID('your_uuid_here') ORDER BY email ASC;
```

### 5. Join Commands - CQL

Cassandra *does not* support standard SQL `JOIN` operations.  Data denormalization is the recommended approach.

*   **Denormalization:**  Duplicate data across tables to avoid joins.
*   **Application-Side Joins:**  Retrieve data from multiple tables separately and join them in the application code.
*   **Materialized Views (with limitations):** Materialized views can pre-compute some join-like operations, but they are limited to within a single keyspace.

**Example (Data Denormalization):**

Instead of joining orders and customers, store customer information (name, city) directly in the `orders` table.

### 6. Subqueries - CQL

Cassandra *does not* support subqueries in the same way as SQL.  Alternatives include:

*   **Multiple Queries:** Execute separate queries and combine the results in the application.
*   **Materialized Views:** Can sometimes pre-compute subquery results.

### 7. Aggregate Functions - CQL

| PostgreSQL Function | Description                                | Cassandra CQL Equivalent                                                                                                                  | Notes                                                                                                                                                     |
| :------------------ | :----------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------- |
| COUNT()             | Counts the number of rows.                 | `SELECT COUNT(*) FROM keyspace_name.table_name WHERE ...;`                                                                               |                                                                                                                                                         |
| SUM()               | Calculates the sum of a numeric column.   | `SELECT SUM(column_name) FROM keyspace_name.table_name WHERE ...;`                                                                       |  Requires allowing filtering using secondary indexes. Use with caution due to potential performance impacts.                                                                    |
| AVG()               | Calculates the average of a numeric column. | `SELECT AVG(column_name) FROM keyspace_name.table_name WHERE ...;`                                                                       | Requires allowing filtering using secondary indexes. Use with caution due to potential performance impacts.                                                                                                                                                  |
| MIN()               | Finds the minimum value in a column.      | `SELECT MIN(column_name) FROM keyspace_name.table_name WHERE ...;`                                                                       | Requires allowing filtering using secondary indexes. Use with caution due to potential performance impacts.                                                                                                                                                   |
| MAX()               | Finds the maximum value in a column.      | `SELECT MAX(column_name) FROM keyspace_name.table_name WHERE ...;`                                                                       | Requires allowing filtering using secondary indexes. Use with caution due to potential performance impacts.                                                                                                                                                   |

**Example:**

```cql
-- Count all users:
SELECT COUNT(*) FROM mykeyspace.users;

-- Calculate the sum of all order amounts (requires ALLOW FILTERING):
SELECT SUM(total_amount) FROM mykeyspace.orders ALLOW FILTERING;
```

### 8. String Commands - CQL

| PostgreSQL Function           | Description                              | Cassandra CQL Equivalent                     | Notes                            |        |                                               |
| :---------------------------- | :--------------------------------------- | :------------------------------------------- | :------------------------------- | ------ | --------------------------------------------- |
| LENGTH(str)                   | Returns the length of a string.          | `LENGTH(text)`                               | Returns the length of a text.    |        |                                               |
| LOWER(str)                    | Converts a string to lowercase.          | `LOWER(text)`                                | Converts a text to lowercase.    |        |                                               |
| UPPER(str)                    | Converts a string to uppercase.          | `UPPER(text)`                                | Converts a text to uppercase.    |        |                                               |
| SUBSTRING(str, start, length) | Extracts a substring from a string.      | `SUBSTR(text, start, length)`                | Returns the text of a substring. |        |                                               |
| REPLACE(str, from, to)        | Replaces all occurrences of a substring. | `REPLACE(text, searchText, replacementText)` | Returns the text of a substring. |        |                                               |
| CONCAT(str1, str2, ...)       | Concatenates two or more strings.        | `text1                                       |                                  | text2` | Returns the text concatenating multiple text. |

### 9. Date/Time Commands - CQL

| PostgreSQL Function | Description                                       | Cassandra CQL Equivalent                               | Notes                                                                                                                                                                         |
| :------------------ | :------------------------------------------------ | :----------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| NOW()               | Returns the current date and time.                | `NOW()` (Returns a UUID based on timestamp) |  Need to convert timestamp to date.  Returns current timestamp as UUID, which can be used for `timeuuid` columns.                                                                 |
| CURRENT_DATE        | Returns the current date.                         | Not directly available. Need to convert.                       |  Requires using a function or custom logic to extract the date from a timestamp or timeuuid.                                                                               |
| CURRENT_TIME        | Returns the current time.                         | Not directly available. Need to convert.                   | Requires using a function or custom logic.                                                                                                                         |
| EXTRACT(field FROM source)      | Extracts a specific part from date/time.                     | `dateOf(timeuuid)` to get date |  Need to convert timeuuid to date and extract. This will allow only Timeuuid based column.                                                                                           |
| DATE_PART(field, source)      | Extracts a specific part from date/time.                     | `dateOf(timeuuid)` to get date |  Need to convert timeuuid to date and extract.  This will allow only Timeuuid based column.                                                                                          |
| AGE(timestamp)   | Calculates the age (in years) from a timestamp.    | No direct equivalent.  Requires function.              | Requires creation of user defined function to achieve this.                                                                                                              |

**Example:**

```cql
-- Get date from timeuuid
SELECT dateOf(id) from mykeyspace.users LIMIT 1;

-- Insert a record with current time
INSERT INTO mykeyspace.users (id, name) VALUES (NOW(), 'Current Time');
```

### 10. Conditions - CQL

| PostgreSQL Operator | Description                    | Cassandra CQL Equivalent | Notes                                                                                                                                  |
| :------------------ | :----------------------------- | :----------------------- | :------------------------------------------------------------------------------------------------------------------------------------- |
| =                   | Equal to                       | `=`                    |                                                                                                                                      |
| <>                  | Not equal to                   | Not Recommended. `ALLOW FILTERING` |  Avoid using inequality operators without proper indexing, as it can lead to full table scans.                                                                        |
| !=                  | Not equal to (alternative)      | Not Recommended. `ALLOW FILTERING`    |  Avoid using inequality operators without proper indexing, as it can lead to full table scans.                                                                    |
| >                   | Greater than                   | Not Recommended. `ALLOW FILTERING`       |  Avoid using inequality operators without proper indexing, as it can lead to full table scans.                                                                     |
| <                   | Less than                      | Not Recommended. `ALLOW FILTERING`   |  Avoid using inequality operators without proper indexing, as it can lead to full table scans.                                                                     |
| >=                  | Greater than or equal to        |  Not Recommended. `ALLOW FILTERING`|   Avoid using inequality operators without proper indexing, as it can lead to full table scans.                                                                   |
| <=                  | Less than or equal to           |  Not Recommended. `ALLOW FILTERING` |   Avoid using inequality operators without proper indexing, as it can lead to full table scans.                                                                   |
| BETWEEN             | Between a range of values       |  Not Recommended. `ALLOW FILTERING` | Avoid using range operators without proper indexing, as it can lead to full table scans.   |
| LIKE                | Matches a pattern               |  Not Recommended. `ALLOW FILTERING`  | Requires `ALLOW FILTERING` and can be very inefficient.                                                                                                  |
| IN                  | In a list of values             | `IN (value1, value2)`    |                                                                                                                                      |
| IS NULL             | Checks for null values          | `column_name IS NULL`  |  Limited support. Requires `ALLOW FILTERING` and can be inefficient.                                                                                                 |
| IS NOT NULL         | Checks for non-null values       | `column_name IS NOT NULL` |  Limited support. Requires `ALLOW FILTERING` and can be inefficient.                                                                                                  |

**Conditional Expressions**

| PostgreSQL Operator | Description                             | Cassandra CQL Equivalent (Alternatives)                                                                      | Notes                                                                                                                                                                                                             |
| :------------------ | :-------------------------------------- | :------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| CASE                | Conditional logic within a query.         | Not directly supported.  Denormalization, multiple queries, or User-Defined Functions (UDFs) are alternatives. | Cassandra encourages denormalization to avoid complex logic in queries.  UDFs can provide some conditional logic on the server side, but should be used sparingly due to performance considerations.          |
| COALESCE            | Returns the first non-null value.       | `COALESCE(column1, column2)`                                                                                 |                                                                                                                                                                                                                 |
| NULLIF              | Returns null if expressions are equal. | No direct equivalent. Requires UDFs or denormalization.                                                      |                                                                                                                                                                                                                 |

**Example:**

```cql
-- Select users with name John or name Bob
SELECT * FROM mykeyspace.users WHERE name IN ('John', 'Bob');

--Select user where department is sales or HR and city is City0; Use Allow filtering due to not using partition key
SELECT * FROM mykeyspace.employees WHERE department IN ('Sales', 'HR') AND city = 'City0' ALLOW FILTERING;
```

### 11. Set Operations - CQL

Cassandra *does not* directly support `UNION`, `INTERSECT`, or `EXCEPT` operations in the same way as SQL.

**Alternatives:**

*   **Application-Side Logic:**  Execute separate queries and combine/filter the results in the application code.
*   **Data Modeling:**  Design your data model to avoid the need for set operations.  Consider creating a unified table that contains all the necessary data.

### 12. Indexes - CQL

**Purpose:** Improve the speed of data retrieval operations (SELECT queries) on *non-primary key* columns.

**How they work:** Cassandra indexes create a separate, distributed index table that maps indexed values to the rows containing those values.

**Syntax:**

```cql
CREATE INDEX index_name ON keyspace_name.table_name (column_name);  -- Standard index
CREATE INDEX index_name ON keyspace_name.table_name (KEYS(map_column));  -- Index on map keys
CREATE INDEX index_name ON keyspace_name.table_name (ENTRIES(map_column)); -- Index on map entries
```

**Types of Indexes:**

*   **Standard Index (Secondary Index):**  The most common type. Suitable for equality queries.
*   **COMPOSITE Index:** create index composite_index ON demokeyspace.demotable (field1, field2);
*   **KEYS Index:**  Indexes the *keys* of a map column.
*   **ENTRIES Index:**  Indexes both *keys and values* of a map column.
*   **VALUES Index:** Indexes the *values* of a list or set column.
*   **SAI (Storage-Attached Index):**  SAI is a new generation of indexing, and it offers significant performance advantages over the older secondary indexing.
```cql
    CREATE CUSTOM INDEX ON demokeyspace.products (price) USING 'org.apache.cassandra.index.sai.StorageAttachedIndex';
    ```

**Choosing the Right Index:**
*   **Equality Queries on Non-Primary Key Columns:** Standard indexes.
*   **Map Key/Value Search:**  `KEYS` or `ENTRIES` indexes.
*   **List/Set Value Search:** `VALUES` indexes.

**Important Considerations:**

*   **Index Cardinality:**  Avoid indexing columns with very low cardinality (e.g., boolean columns). Low cardinality indexes can lead to performance problems.
*   **`ALLOW FILTERING`:** Queries that use secondary indexes might still require `ALLOW FILTERING`, which can impact performance.  Design your data model carefully to minimize the need for `ALLOW FILTERING`.
*   **SAI:** For Cassandra 4.0 and later, consider using SAI as it offers performance and functionality improvements over standard secondary indexes.

### 13. Transactions - CQL

Cassandra provides lightweight transactions (LWT) for conditional updates but *does not* support full ACID transactions in the traditional sense.

**Lightweight Transactions (LWT):**

*   Implemented using the `IF` clause in `INSERT` or `UPDATE` statements.
*   Provide atomicity and isolation for single-row operations.
*   Rely on Paxos consensus, which can impact performance.

**Example:**

```cql
-- Insert only if a record with the same id does not already exist:
INSERT INTO mykeyspace.users (id, name, email) VALUES (UUID(), 'John', 'john@example.com') IF NOT EXISTS;

-- Update only if the current value of email is 'john@example.com':
UPDATE mykeyspace.users SET email = 'new.email@example.com' WHERE id = UUID('your_uuid') IF email = 'john@example.com';
```

**Important Notes:**

*   LWTs should be used sparingly due to their performance overhead.
*   Design your data model to minimize the need for conditional updates.

### 14. Window Functions - CQL

Cassandra *does not* support window functions directly as in SQL.  Alternatives:

*   **Data Denormalization:** Pre-calculate aggregates and store them directly in your tables.
*   **Spark or Other Processing Frameworks:** Use external processing frameworks like Apache Spark to perform windowed aggregations on Cassandra data.
*   **User Defined Functions (UDFs):** Write custom UDFs in Java to perform specific windowing logic.

### 15. WITH Keyword (Common Table Expressions - CTE) - CQL

Cassandra *does not* support CTEs.  Alternatives:

*   **Multiple Queries:** Break down complex queries into multiple simpler queries.
*   **Data Modeling:** Restructure your data model to simplify queries and avoid the need for CTEs.

### 16. Views - CQL

Cassandra supports materialized views.

**Materialized Views:**

*   Pre-computed tables automatically updated when the base table changes.
*   Enable efficient querying of pre-aggregated or transformed data.
*   Must have a primary key that includes the base table's partition key.

**Syntax:**

```cql
CREATE MATERIALIZED VIEW mykeyspace.mv_users_by_city AS
SELECT city, id, name, email
FROM mykeyspace.users
WHERE city IS NOT NULL AND id IS NOT NULL AND name IS NOT NULL AND email IS NOT NULL
PRIMARY KEY (city, id);
```

**Important Notes:**

*   Materialized views are automatically updated, but updates can introduce latency.
*   Carefully design your views to optimize for specific query patterns.

### 17. Materialized View:

**Purpose:**: Enable efficient querying of pre-aggregated or transformed data from base tables.

**Creating materialized views**

1. Materialized views must have a primary key that includes the base table's partition key

```cql
CREATE MATERIALIZED VIEW demokeyspace.customer_summary AS
SELECT
    customer_id,
    first_name,
    last_name,
    city,
    email
FROM demokeyspace.customers
WHERE customer_id IS NOT NULL and first_name IS NOT NULL and last_name IS NOT NULL and email IS NOT NULL and city IS NOT NULL
PRIMARY KEY (customer_id, first_name, last_name)
WITH CLUSTERING ORDER BY (first_name ASC)
AND gc_grace_seconds = 864000 ;
```

2. Materialized views always contains base table primary key, if clustering is not present

```cql
CREATE MATERIALIZED VIEW demokeyspace.customer_summary2 AS
SELECT
    customer_id,
    first_name,
    last_name,
    city,
    email
FROM demokeyspace.customers
WHERE customer_id IS NOT NULL and first_name IS NOT NULL and last_name IS NOT NULL and email IS NOT NULL and city IS NOT NULL
PRIMARY KEY ((city), customer_id, first_name, last_name)
WITH CLUSTERING ORDER BY (customer_id ASC, first_name ASC)
AND gc_grace_seconds = 864000 ;
```

Querying Materialized Views

```cql
SELECT * FROM demokeyspace.customer_summary WHERE customer_id = 2 AND first_name = 'First_190' AND last_name = 'Last_190';
SELECT * FROM demokeyspace.customer_summary2 WHERE city = 'City10' and customer_id = 2 and first_name = 'First_190' and last_name = 'Last_190' ;
```

Limitations and Considerations

*   **Data Duplication:** Stores a copy of data, increasing storage needs.
*   **Write Performance:** Updates to the base table triggers updates to the view, which can affect write performance.
*   **Key Selection**: View must include all base table keys, and adding clustering keys impacts query options.
*   **Strong consistency is not ensured**:  While updates are generally propagated quickly, strong consistency isn't guaranteed during view updates.
*   **Deletion Considerations**: Materialized views do not inherit TTL (Time-To-Live) settings from the base table, which can lead to inconsistencies when data is deleted. It is important to handle deletions and TTLs for Materialized views separately.

Materialized views in Cassandra are useful for creating views that can be queried to get specific data.

### 18. Query Analysis (Explain Plan) - CQL

Cassandra provides `TRACING` to analyze query execution.

**Tracing:**

*   Enables detailed logging of query execution steps.
*   Helps identify performance bottlenecks.

**Syntax:**

```cql
TRACING ON;
SELECT * FROM mykeyspace.users WHERE name = 'John' ALLOW FILTERING;
TRACING OFF;
```

The output will provide details about the nodes involved, the time spent in each stage, and any errors that occurred.

### 19. Partition - CQL

Partitioning is *fundamental* to Cassandra's data model. You *must* define a partition key when creating a table.

**Partitioning:**

*   Determines how data is distributed across nodes in the cluster.
*   The partition key is used to hash data and assign it to a specific node.
*   Queries *must* include the partition key for efficient data retrieval.

**Syntax (Table Creation):**

```cql
CREATE TABLE mykeyspace.orders (
    customer_id UUID,  -- Partition key
    order_id UUID,       -- Clustering column
    order_date timestamp,
    total_amount decimal,
    PRIMARY KEY (customer_id, order_id)
);
```

**Types of Partitioning (Logical):**

*   **Composite Partition Keys:** You can use multiple columns to form the partition key.
    ```cql
    CREATE TABLE mykeyspace.events (
        year int,
        month int,
        day int,
        event_id UUID,
        ...
        PRIMARY KEY ((year, month, day), event_id)
    );
    ```

### 20. Trigger - CQL
Cassandra doesn't have database triggers like in SQL, so let's talk about other ways to do similar things:

*   **Client-Side Logic**: The easiest way is to handle any extra work in your app. When you change something in the database, your app can also do other tasks if needed.

*   **Materialized Views**: Use these to keep data updated in another table automatically. However, these don't let you run special actions like triggers do.

*   **Kafka and Change Data Capture (CDC)**: CDC tools track changes in the database and send messages to a queue (like Kafka). Then, other apps can listen to these messages and act on them.

### Additional Concepts Relevant to Cassandra

1.  **Efficient Data Loading Techniques**:
    *   `COPY` is not directly supported in Cassandra. Use `sstableloader` for bulk loading from SSTable files (which can be generated from other sources). Or try loading from spark.

2.  **Advanced ETL Patterns**:
    *   Use `ON CONFLICT` (upsert) operations.  However, this is handled using Lightweight Transactions, use sparingly.

3.  **Performance Optimization Techniques**:
    *   Understand data locality.

4.  **Data Quality and Validation**:
    *   Constraints are limited in Cassandra. Data validation typically happens in the application layer.

5.  **Aggregate Operations**:
    *  Cassandra has built in aggregation and array operation.

6.  **Advance view techniue**
    *   In case of concurrent refreshes, materialized view are only allowed with one partition key index.

### Insert Data

Create table orders

```sql
CREATE TABLE IF NOT EXISTS demokeyspace.orders (
    order_id uuid,
    customer_id uuid,
    order_date timestamp,
    total_amount decimal,
    status text,
    PRIMARY KEY (customer_id, order_id)
) WITH CLUSTERING ORDER BY (order_id DESC);

-- Populate the demokeyspace.orders table with some example data.
INSERT INTO demokeyspace.orders (order_id, customer_id, order_date, total_amount, status) VALUES (uuid(), uuid(), toTimestamp(now()), 100.0, 'shipped');

-- Add 9 more sample order records to demokeyspace.orders.
INSERT INTO demokeyspace.orders (order_id, customer_id, order_date, total_amount, status) VALUES (uuid(), uuid(), toTimestamp(now()), 200.0, 'pending');
INSERT INTO demokeyspace.orders (order_id, customer_id, order_date, total_amount, status) VALUES (uuid(), uuid(), toTimestamp(now()), 300.0, 'delivered');
INSERT INTO demokeyspace.orders (order_id, customer_id, order_date, total_amount, status) VALUES (uuid(), uuid(), toTimestamp(now()), 400.0, 'cancelled');
INSERT INTO demokeyspace.orders (order_id, customer_id, order_date, total_amount, status) VALUES (uuid(), uuid(), toTimestamp(now()), 500.0, 'shipped');
INSERT INTO demokeyspace.orders (order_id, customer_id, order_date, total_amount, status) VALUES (uuid(), uuid(), toTimestamp(now()), 600.0, 'pending');
INSERT INTO demokeyspace.orders (order_id, customer_id, order_date, total_amount, status) VALUES (uuid(), uuid(), toTimestamp(now()), 700.0, 'delivered');
INSERT INTO demokeyspace.orders (order_id, customer_id, order_date, total_amount, status) VALUES (uuid(), uuid(), toTimestamp(now()), 800.0, 'cancelled');
INSERT INTO demokeyspace.orders (order_id, customer_id, order_date, total_amount, status) VALUES (uuid(), uuid(), toTimestamp(now()), 900.0, 'shipped');
INSERT INTO demokeyspace.orders (order_id, customer_id, order_date, total_amount, status) VALUES (uuid(), uuid(), toTimestamp(now()), 1000.0, 'pending');
```
