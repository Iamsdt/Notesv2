Project: Use the `bigquery-public-data` project. 
Dataset: `bigquery-public-data.google_analytics_sample`.

## 1. Introduction to BigQuery SQL Enhancements

### Differences Between Standard SQL and BigQuery SQL

BigQuery supports both Standard SQL and Legacy SQL. However, Standard SQL is recommended for new projects due to its richer feature set and compatibility with ANSI SQL standards. Key differences include:

- **Syntax:** Standard SQL uses `JOIN` and `ON` for joins, while Legacy SQL uses `JOIN ON`.
- **Window Functions:** Standard SQL supports a broader range of window functions.
- **Data Types:** Standard SQL introduces new data types like `STRUCT` and `ARRAY`.

### Unique Features of BigQuery SQL

- **Nested and Repeated Fields:** Handle complex data structures.
- **Partitioning and Clustering:** Optimize query performance.
- **Window and Analytical Functions:** Perform advanced data analysis.
- **Data Manipulation Language (DML):** Supports `INSERT`, `UPDATE`, `DELETE`, and `MERGE`.

## 2. Exploration of Public Dataset

### Accessing the `bigquery-public-data` Project

BigQuery provides several public datasets for learning and experimentation. One of the popular datasets is `bigquery-public-data.google_analytics_sample`, which contains Google Analytics data.

#### Example Query

```sql
-- Access public dataset
SELECT * 
FROM `bigquery-public-data.google_analytics_sample.ga_sessions_20170801`
LIMIT 10;
```

**Explanation:**

- This query retrieves the first 10 records from the `ga_sessions_20170801` table.
- The dataset contains session-level data with nested and repeated fields.

### Use Cases: Aggregation, Analytics, and Insights Generation

- **Aggregation:** Summarize data to derive meaningful insights.
- **Analytics:** Perform complex analyses using window and analytical functions.
- **Insights Generation:** Identify trends and patterns in user behavior.

## 3. Key BigQuery SQL Features

### 1. Working with Nested and Repeated Fields

BigQuery allows you to work with nested and repeated fields, which are common in hierarchical data structures.

#### Example: Extracting Repeated Fields

```sql
-- Extract repeated fields
SELECT
    visitId,
    fullVisitorId,
    hit.page.pageTitle AS page_titles
FROM
    `bigquery-public-data.google_analytics_sample.ga_sessions_20170801` AS sessions,
    UNNEST(sessions.hits) AS hit
WHERE hit.page.pageTitle != 'Page Unavailable'
LIMIT 5;
```

**Explanation:**

- **Dot Notation:** Access nested fields using dot notation (e.g., `hit.page.pageTitle`).
- **UNNEST Function:** Flatten repeated fields into individual rows.

### 2. Using Arrays and Structs

Arrays and structs are powerful data types for handling complex data.

#### Arrays

**Example: Creating and Querying Arrays**

```sql
WITH sample_data AS (
  SELECT [1, 2, 3, 4, 5] AS num_array
)
SELECT
  num_array,
  ARRAY_LENGTH(num_array) AS array_length
FROM sample_data;
```

**Explanation:**

- **ARRAY_LENGTH:** Returns the number of elements in an array.
- **UNNEST Function:** Convert arrays into rows for easier querying.

**Example: UNNEST with Arrays**

```sql
WITH sample_data AS (
  SELECT [1, 2, 3, 4, 5] AS num_array
)
SELECT
  num,
  num * 2 AS doubled_value
FROM
  sample_data,
  UNNEST(num_array) AS num;
```

#### Structs

**Example: Creating a STRUCT in a Query**

```sql
SELECT
  STRUCT('John Doe' AS name, 29 AS age) AS person;
```

**Example: Using STRUCT in a WITH Clause**

```sql
WITH sample_data AS (
  SELECT
    STRUCT('Alice' AS name, 25 AS age) AS person
)
SELECT
  person.name,
  person.age
FROM
  sample_data;
```

**Example: Nesting STRUCT in an Array**

```sql
WITH sample_data AS (
  SELECT
    [STRUCT('Alice' AS name, 25 AS age), STRUCT('Bob' AS name, 30 AS age)] AS people
)
SELECT
  person.name,
  person.age
FROM
  sample_data,
  UNNEST(people) AS person;
```

### **Array vs. Struct in BigQuery: Key Differences**

| Feature         | **Array**                                                                                | **Struct**                                                                       |
| --------------- | ---------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| **Definition**  | A collection of values of the same type (e.g., integers, strings).                       | A single entity containing multiple named fields of potentially different types. |
| **Homogeneity** | All elements must be of the same type.                                                   | Fields can have different types (e.g., string, integer, array, etc.).            |
| **Use Case**    | Ideal for representing lists, repeated values, or multiple occurrences of the same type. | Used to represent grouped attributes or a record-like structure.                 |
| **Access**      | Access elements via `OFFSET()` (0-based index) or `ORDINAL()` (1-based index).           | Access fields via dot notation (e.g., `struct.field_name`).                      |
| **Example**     | `[1, 2, 3, 4]`                                                                           | `STRUCT('John Doe' AS name, 29 AS age)`                                          |

### **Detailed Comparison**
1. **Data Organization:**
    - **Array:** Used for lists or repeated fields.
        - Example: A customer's multiple order IDs: `[123, 456, 789]`.
    - **Struct:** Used for grouping logically related fields into one unit.
        - Example: A customer record: `STRUCT('John' AS name, 'john@example.com' AS email)`.
2. **Querying:**
    - **Array:** Requires functions like `UNNEST()` to work with individual elements.
        ```sql
        SELECT num FROM UNNEST([1, 2, 3]) AS num;
        ```
    - **Struct:** Accessed directly via dot notation.
        ```sql
        SELECT person.name FROM STRUCT('Alice' AS name, 25 AS age) AS person;
        ```
3. **Nested Structures:**
    - **Array:** Supports arrays of `STRUCT`s for hierarchical data.
    - **Struct:** Can include fields that are arrays or even other `STRUCT`s.
4. **Aggregation:**
    - **Array:** Suitable for handling multiple related values of the same type.
    - **Struct:** Suitable for encapsulating multiple attributes into a single unit.
5. **Storage and Performance:**
    - **Array:** Efficient for repeated data types but requires flattening for individual access.
    - **Struct:** Allows for logical grouping, making queries intuitive and well-structured without flattening.


### 3. Partitioning and Clustering
Partitioning and clustering optimize query performance by reducing the amount of data scanned.
#### Example: Partitioned Query

```sql
SELECT
  visitId,
  fullVisitorId
FROM
  `bigquery-public-data.google_analytics_sample.ga_sessions_20170801`
WHERE
  DATE(TIMESTAMP_SECONDS(visitStartTime)) = '2017-08-01';
```

**Explanation:**

- **Partition Pruning:** Use partition keys in the `WHERE` clause to scan only relevant data.
- **TIMESTAMP_SECONDS:** Converts Unix timestamp to a TIMESTAMP data type.

### 4. Window Functions
Window functions perform calculations over a set of rows related to the current row.
#### Example: Calculate Rank Based on Pageviews

```sql
SELECT
  fullVisitorId,
  SUM(totals.pageviews) AS total_pageviews,
  RANK() OVER (ORDER BY SUM(totals.pageviews) DESC) AS rank
FROM
  `bigquery-public-data.google_analytics_sample.ga_sessions_20170801`
GROUP BY
  fullVisitorId
LIMIT 10;
```

**Explanation:**

- **RANK() Function:** Assigns a rank to each row based on the sum of pageviews.
- **OVER Clause:** Defines the window over which the function is applied.

### 5. Analytical Functions

Analytical functions perform advanced aggregations and statistical analyses.

#### Example: Calculate Percentiles

```sql
SELECT
  APPROX_QUANTILES(CAST(totals.pageviews AS FLOAT64), 2)[OFFSET(1)] AS median_pageviews
FROM
  `bigquery-public-data.google_analytics_sample.ga_sessions_20170801`
WHERE
  totals.pageviews IS NOT NULL;
```

**Explanation:**

- **APPROX_QUANTILES:** Approximates quantiles for large datasets.
- **OFFSET:** Retrieves the value at a specific position in the array.

### 6. Data Manipulation Language (DML)

DML allows you to modify data in BigQuery tables.

#### Example: Insert Data

```sql
-- Insert data
INSERT INTO `project.dataset.table` (id, name)
VALUES (1, 'John Doe');
```

**Explanation:**

- **INSERT Statement:** Adds new rows to a table.
- **VALUES Clause:** Specifies the data to be inserted.

#### Example: Update Data

```sql
-- Update data
UPDATE `project.dataset.table`
SET name = 'Jane Doe'
WHERE id = 1;
```

#### Example: Delete Data

```sql
-- Delete data
DELETE FROM `project.dataset.table`
WHERE id = 1;
```

### 7. Query Optimization Tips

- **Select Only Required Columns:** Avoid using `SELECT *` to reduce data processed.
- **Leverage Table Preview:** Use `LIMIT` to minimize costs during development.
- **Partition Pruning:** Always filter on partition columns to reduce data scanned.
- **Query Caching:** Reuse cached results for identical queries.

## 8. Views vs. Materialized Views

### Views

- **Definition:** A virtual table based on a query.
- **Data Storage:** No data is stored; the query is executed each time the view is accessed.
- **Use Case:** Simplify complex queries or provide data abstraction.

**Example: Creating a View**

```sql
CREATE VIEW `project.dataset.view_name` AS
SELECT
  fullVisitorId,
  SUM(totals.pageviews) AS total_pageviews
FROM
  `bigquery-public-data.google_analytics_sample.ga_sessions_20170801`
GROUP BY
  fullVisitorId;
```

### Materialized Views

- **Definition:** A physical table that stores the result of a query.
- **Data Storage:** Data is stored and updated based on a refresh schedule.
- **Use Case:** Improve query performance for complex queries.

**Example: Creating a Materialized View**

```sql
CREATE MATERIALIZED VIEW `project.dataset.materialized_view_name` AS
SELECT
  fullVisitorId,
  SUM(totals.pageviews) AS total_pageviews
FROM
  `bigquery-public-data.google_analytics_sample.ga_sessions_20170801`
GROUP BY
  fullVisitorId;
```

**Explanation:**

- **Refresh Schedule:** Materialized views can be refreshed periodically to reflect changes in the source data.
- **Performance:** Materialized views can significantly improve query performance by storing precomputed results.

### Choosing Between Views and Materialized Views

- **Use Views:**
  - When real-time data is required.
  - For simple queries that do not benefit from precomputation.
- **Use Materialized Views:**
  - When query performance is critical.
  - For complex queries that are run frequently.