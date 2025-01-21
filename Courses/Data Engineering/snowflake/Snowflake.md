---
Created by: Shudipto Trafder
Last edited time: 2025-01-21T21:24:00
tags:
  - de
  - snowflake
---


Snowflake is a cloud-based data warehousing company that provides a platform for data storage, processing, and analytics.  It's known for its unique architecture that separates storage from compute, allowing for flexible scaling and performance. Here's a breakdown:

**Key Features and Characteristics:**

* **Cloud-Based Data Warehouse:** Snowflake operates entirely in the cloud and is available on major cloud platforms like AWS, Azure, and Google Cloud.  This eliminates the need for users to manage hardware or software.
* **Storage-Compute Separation:** This is a defining feature. Storage and compute resources are independent, meaning you can scale them up or down individually based on your needs.  This flexibility allows for optimized performance and cost efficiency.
* **Data Sharing:** Snowflake enables easy and secure data sharing with other Snowflake accounts or even external partners, facilitating collaboration and data monetization.
* **Support for Diverse Data Types:** Snowflake can handle structured, semi-structured, and unstructured data, making it suitable for a wide range of analytics workloads.
* **SQL-Based Query Engine:**  Snowflake uses a variant of SQL, making it easy for users familiar with traditional databases to get started.
* **Automatic Performance Optimization:** Snowflake incorporates various optimization techniques, such as automatic clustering and caching, to ensure fast query performance.
* **Security and Compliance:** Snowflake offers robust security features, including data encryption, access controls, and compliance certifications, to protect sensitive data.
* **Data Marketplace:**  Snowflake Data Marketplace allows users to access and share data sets from various providers, enriching their own analytics initiatives.


**Benefits of using Snowflake:**

* **Scalability and Elasticity:**  Easily adjust resources based on demand, avoiding performance bottlenecks and overspending.
* **Performance:**  The separated architecture and optimization features contribute to fast query processing.
* **Ease of Use:**  The cloud-based nature and SQL support simplify deployment and management.
* **Cost-Effectiveness:**  Pay-as-you-go pricing model and resource optimization help control costs.
* **Data Sharing and Collaboration:**  Seamlessly share data with internal and external parties.
* **Support for Diverse Data and Workloads:** Handle various data types and analytics tasks on a single platform.


**Use Cases:**

* **Data Warehousing and Business Intelligence:**  Consolidating data from various sources for reporting and analysis.
* **Data Lakes:**  Storing and analyzing large volumes of raw data.
* **Data Engineering:**  Building and managing data pipelines.
* **Data Science and Machine Learning:**  Training and deploying machine learning models.


# Concepts & Architecture

![](https://docs.snowflake.com/en/_images/architecture-overview.png)

Snowflake's architecture is a unique hybrid approach combining elements of shared-disk and shared-nothing database architectures. This innovative design results in a three-layer architecture:

*   **Storage Layer:**  This layer houses all data loaded into Snowflake.  Snowflake restructures this data into its internal optimized, compressed, and columnar format for efficient storage and query processing.  This layer resides within the chosen cloud provider's storage (e.g., Amazon S3, Azure Blob Storage, Google Cloud Storage) and is managed entirely by Snowflake.  Users don't directly interact with this layer; Snowflake handles data organization, file size, structure, compression, metadata, statistics, and all other aspects of data storage.  This centralized repository ensures data consistency and accessibility across all compute nodes.

*   **Compute Layer (Query Processing):**  This layer is responsible for executing user queries and performing data processing tasks.  It uses independent compute clusters called "virtual warehouses." These warehouses can be scaled independently of the storage layer, allowing users to adjust compute power based on their needs.  Multiple virtual warehouses can operate concurrently on the same data without impacting each other's performance.  This allows for high concurrency and efficient resource utilization. The compute layer employs Massively Parallel Processing (MPP) to distribute query execution across the nodes of a virtual warehouse, resulting in fast query performance, especially for large datasets.

*   **Cloud Services Layer:**  This layer acts as the central management and coordination service for the entire Snowflake platform.  It handles various critical functions, including:
    *   **Metadata Management:**  Tracks information about data, such as table schemas, data types, and statistics.
    *   **Authentication and Authorization:**  Manages user access and permissions.
    *   **Query Optimization and Execution:**  Optimizes query plans and distributes tasks to the compute layer.
    *   **Transaction Management:** Ensures data consistency and integrity.
    *   Infrastructure Management:**  Handles tasks such as virtual warehouse provisioning and scaling.

## Snowflake vs. BigQuery

| Feature           | Snowflake                                                                                                                     | BigQuery                                                                                                                            |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Architecture      | Multi-cluster, shared data architecture; separates storage and compute.                                                       | Columnar storage, serverless, fully managed; compute tied to storage within Google's infrastructure.                                |
| Scaling           | Manual and automatic scaling options; independent scaling of storage and compute.                                             | Automatic scaling; less direct control over scaling parameters.                                                                     |
| Performance       | Generally faster for simpler queries and standard benchmarks (like TPC-H).                                                    | Highly performant for large, complex queries and optimized for analytical workloads.                                                |
| Data Sharing      | Advanced data sharing features without data movement.                                                                         | Data sharing through Google Cloud's IAM; less flexible than Snowflake's native sharing.                                             |
| Cloud Integration | Multi-cloud support (AWS, Azure, GCP).                                                                                        | Deeply integrated with Google Cloud Platform (GCP) services.                                                                        |
| Pricing           | Storage and compute usage based.                                                                                              | Primarily based on data processed (queries) and storage consumed.                                                                   |
| Security          | Granular object-level permissions (not column-level); network security via cloud provider integration (e.g. AWS PrivateLink). | Dataset-level permissions (not table or column-level); utilizes VPC Service Controls for network security.                          |
| External Tables   | Supports external tables; requires manual or automated metadata refreshes.                                                    | Supports external tables and query federation within GCP; uses BigLake for external storage connectivity.                           |
| Data Partitioning | Automatic micro-partitioning based on data loaded; optimized for complex queries across wider datasets.                       | Automatic partitioning based on specified columns (often timestamp); suitable for time-series data and targeted time-based queries. |


**Choosing the right platform depends on your specific needs:**

* **Snowflake:** Offers more flexibility in scaling, cross-cloud deployments, and data sharing. Its performance shines on diverse workloads, although it requires more manual configuration and can become more expensive with complex scaling needs.
* **BigQuery:** Tight integration with the Google Cloud ecosystem, automatic scaling, and competitive pricing make it a good choice for organizations heavily invested in GCP.  It excels at handling large, complex analytical queries and provides a simplified, serverless experience.  However, it offers less flexibility in multi-cloud deployments and data sharing compared to Snowflake.

# Data LifeCycle

![Data Life Cycle](https://docs.snowflake.com/en/_images/data-lifecycle.png)

The Snowflake Data Lifecycle diagram illustrates the stages of managing data within the Snowflake environment.  It highlights key actions and corresponding SQL commands categorized by their purpose:

* **Organizing Data (DDL):**  This phase involves setting up the fundamental structure for storing data, including creating and modifying databases, schemas, and tables.  These actions use Data Definition Language (DDL) commands.
* **Storing Data (DML):** This stage focuses on loading data into the established tables using commands like `INSERT INTO` and `COPY INTO`. These are Data Manipulation Language (DML) commands.
* **Querying Data (DML):**  Retrieving and analyzing data is performed in this phase with the `SELECT` statement, another DML command. This is the core function of a data warehouse.
* **Working with Data (DML):**  This phase encompasses manipulating existing data through updates, merges, and deletions (`UPDATE`, `MERGE INTO`, `DELETE FROM`).  Cloning tables and schemas for testing or analysis is also part of this stage. These are also DML commands, with `CLONE` being a Snowflake-specific operation.
* **Removing Data (DDL):** This stage involves removing data objects, starting from tables and schemas and extending to entire databases. This uses DDL commands to clean up and manage the environment.


## Snowflake schema
A Snowflake schema is a logical arrangement of tables in a multi-dimensional database, like a data warehouse, designed to optimize analytical querying. It's a variant of the star schema, but with further normalized dimension tables.  Think of it as a star schema with more intricate, snowflake-like branches.

![Snowflake Schema](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b2/Snowflake-schema.png/1200px-Snowflake-schema.png)

Here's a breakdown:

* **Fact Table:** This central table holds the core metrics or measurements you're analyzing.  Examples include sales amount, order quantity, website clicks, or sensor readings.  It contains numerical data and foreign keys linking to the dimension tables.

* **Dimension Tables:** These tables provide descriptive context for the facts. They contain attributes related to the measurements.  Common examples include customer information (name, location, demographics), product details (name, category, price), time (date, month, year), or location (city, state, country).

* **Snowflaking (Normalization):** This is the key difference between a star schema and a snowflake schema.  In a star schema, dimension tables are denormalized (contain some redundant data) for simplicity and query performance.  In a snowflake schema, dimension tables are normalized.  This means breaking down large dimension tables into smaller, more specialized tables.  For example, a "customer" dimension table might be split into "customer demographics," "customer address," and "customer contact information" tables.  These smaller tables are then linked through foreign keys.

**Example:**

Imagine an e-commerce business.  A simplified Snowflake schema might look like this:

* **Fact Table:** `Sales` (Sales Amount, Order ID, Customer ID, Product ID, Date ID)
* **Dimension Tables:**
    * `Customer` (Customer ID, Location ID)
    * `Location` (Location ID, City, State, Country)
    * `Product` (Product ID, Category ID)
    * `Category` (Category ID, Category Name)
    * `Date` (Date ID, Date, Month, Year)

Notice how the `Customer` and `Product` dimensions are further normalized into `Location` and `Category` tables, respectively.  This normalization creates the "snowflake" effect.

**Advantages of Snowflake Schema:**

* **Reduced Data Redundancy:** Normalization eliminates data duplication in dimension tables, saving storage space and improving data integrity.
* **Improved Data Consistency:** Changes to a dimension attribute only need to be made in one place, minimizing inconsistencies.

**Disadvantages of Snowflake Schema:**

* **Increased Query Complexity:** Queries often require joining multiple tables due to the normalization, which can slightly reduce query performance compared to a star schema.
* **More Complex Design:** Designing and maintaining a snowflake schema can be more complex than a star schema.

**When to Use a Snowflake Schema:**

* **Storage Space is a Major Concern:** When storage is expensive or limited, the reduced redundancy of a Snowflake schema can be beneficial.
* **Data Integrity is Paramount:**  If maintaining data consistency is crucial, a Snowflake schema helps prevent anomalies.
* **Query Performance is Less Critical:** If query performance is not the absolute top priority, the slight performance overhead of joins in a Snowflake schema might be acceptable.


# Snowflake vs Star schemas:

| Feature           | Star Schema                                 | Snowflake Schema                                         |
| ----------------- | ------------------------------------------- | -------------------------------------------------------- |
| Structure         | Central fact table, denormalized dimensions | Central fact table, normalized dimensions                |
| Normalization     | Dimensions are denormalized (redundancy)    | Dimensions are normalized (minimal redundancy)           |
| Query Performance | Generally faster due to fewer joins         | Can be slower due to more joins between dimension tables |
| Storage Space     | Can require more storage due to redundancy  | More efficient storage due to less redundancy            |
| Data Integrity    | Potential for data inconsistencies          | Higher data integrity due to normalization               |
| Schema Complexity | Simpler to design and understand            | More complex to design and understand                    |
| ETL Process       | Simpler ETL process                         | More complex ETL process due to normalization needs      |
| Example           | Single "Customer" table with address, etc.  | "Customer" table linked to separate "Address" table      |


# SnowFlake Keywords
Those options within the Snowflake UI offer different ways to interact with and manage your data and workflows. Here's a breakdown:

1. **Worksheets:**  This is the core interface for interacting with Snowflake's data. Worksheets are where you write and execute SQL queries, view results, and perform various data manipulation tasks.  Think of them as your SQL editor and interactive workspace within Snowflake.  You can have multiple worksheets open simultaneously.

2. **Notebooks (Snowsight):**  Snowflake Notebooks (previously known as Worksheets in Snowsight) provide an integrated development environment where you can combine SQL, Python, Markdown, and other code to create interactive data analyses, reports, and data pipelines. They are useful for more complex data exploration, visualization, and sharing insights with others.

3. **Streamlit (in Snowpark Python):**  Streamlit within Snowpark Python allows you to build interactive web applications for data visualization and exploration directly within Snowflake. Snowpark is Snowflake's framework for running Python code within the platform. Streamlit simplifies the process of creating user-friendly interfaces for data apps powered by Snowflake data. *Note that Streamlit itself isn't a direct UI element like Worksheets, but a library used within Snowpark*.

4. **Dashboards (Snowsight):** Dashboards in Snowsight let you visually present data insights and key metrics from your Snowflake data. You can create charts, graphs, and other visualizations, combine them on a single dashboard, and share them with others to provide a quick overview of important data trends.

5. **Folders (for organization):** Folders are used for organizing your Snowflake objects like worksheets, dashboards, tables, and stored procedures. You can create a hierarchical structure of folders to keep your Snowflake environment well-organized and easier to navigate, especially in larger deployments with many objects.


## Understanding Snowflake Database

In Snowflake, a database contains one or more schemas. Schemas act as logical containers for database objects like tables, views, and other related components. They help organize your data and control access permissions. The PUBLIC schema is the default schema created automatically in every Snowflake database.

The options under "Create" allow you to create various database objects within the currently selected schema (in this case, PUBLIC):
- **Table:** Creates a standard relational table to store data. This is the most common object you'll create. Tables store data in rows and columns.

- **Dynamic Table:** Creates a table that automatically updates its contents based on a query against other tables or views. This is useful for creating materialized views or maintaining aggregated data sets.

- **View:** Creates a virtual table based on the results of a SQL query. Views don't store data themselves but provide a customized way to look at data from underlying tables. A secure view in Snowflake is a type of view that allows you to control access to the underlying data in a more granular and secure way. It's particularly useful for sharing data with others while protecting sensitive information.

- **Stage:** Creates a named storage location within Snowflake for loading and unloading data. Stages can be internal (within Snowflake's storage) or external (pointing to cloud storage like AWS S3, Azure Blob Storage, or Google Cloud Storage). They are crucial for data ingestion and extraction. In Snowflake, stages are used to store files before they are loaded into tables. The type of data you store in a stage (raw or semi-structured) depends on your data loading process and the format of your data. Data volume is a separate concern related to your overall data warehousing strategy.

- **Storage Integration:** Creates an object that defines how Snowflake connects to an external cloud storage service. This is a prerequisite for creating external stages.
```sql
create storage integration <storage_integration_name>
    type = external_stage
    storage_provider = gcs
    enabled = true
    storage_allowed_locations = ( 'gcs://<location1>', 'gcs://<location2>' )
    -- storage_blocked_locations = ( 'gcs://<location1>', 'gcs://<location2>' )
    -- comment = '<comment>';
```

- **File Format:** Defines how data files are structured (e.g., CSV, JSON, Parquet) when loading or unloading data from stages. This ensures that Snowflake correctly interprets the data.
```sql
create file format <name>
    type = { CSV | JSON | AVRO | ORC | PARQUET | XML }
    --  [ formatTypeOptions ]
    -- comment = '<comment>'
```

- **Sequence:** Creates a sequence object, which generates unique sequential numbers. Useful for generating primary keys or other auto-incrementing values.

```sql
create sequence <name>
    -- start = <integer>
    -- increment = <integer>
    -- comment = '<comment>';
```

- **Pipe:** Creates a named pipe object that simplifies the process of continuously loading data from a stage. Pipes automate data ingestion and handle file management.

```sql
create pipe <name>
    --  auto_ingest = <true or false>
    --  aws_sns_topic = '<string>'
    --  integration = '<string>' 
    -- comment = '<comment>'
      as <copy_statement>;

CREATE OR REPLACE PIPE my_pipe
  AUTO_INGEST = TRUE
  COMMENT = 'Pipe to load data from S3'
AS
  COPY INTO my_table
  FROM @my_s3_stage
  FILE_FORMAT = (TYPE = CSV);
```

- **Stream:** Creates a stream object that captures changes made to a table (inserts, updates, deletes). Streams are used for change data capture and building data pipelines. Snowflake Streams are best used in scenarios where you need to capture and process changes made to a table in real-time or near real-time

```sql
CREATE OR REPLACE STREAM mba_stream
  ON TABLE mba
  APPEND_ONLY = TRUE
  COMMENT = 'Stream capturing changes to the MBA table';
```

- **Task:** Creates a task object, which is a scheduled unit of work in Snowflake. Tasks can automate various operations, such as data loading, transformations, or other maintenance procedures. In Snowflake, a task is a scheduled or on-demand unit of work that executes a specified SQL statement or stored procedure.

```sql
CREATE OR REPLACE TASK refresh_summary_table
  WAREHOUSE = my_warehouse
  SCHEDULE = '15 minute' -- Runs every 15 minutes
  COMMENT = 'Refreshes a summary table'
AS
  CALL refresh_summary_procedure();  -- Calls a stored procedure or use a SQL Statement directly
```

- **Function:** Creates a user-defined function (UDF), which encapsulates reusable SQL or JavaScript code that can be called within queries.

- **Procedure:** Creates a stored procedure, a block of SQL or JavaScript code that can perform more complex operations, including multiple SQL statements, conditional logic, and looping.

- **Git Repository:** Integrate Snowflake with a Git repository for version control of your code (functions, procedures, tasks). This facilitates collaboration and code management.

### Table
External Table: An external table in Snowflake is a table whose data resides *outside* of Snowflake's internal storage.  It provides a way to query data directly from files located in external cloud storage (like AWS S3, Azure Blob Storage, or Google Cloud Storage) *without* first loading the data into Snowflake.

Here's a breakdown:

**Key Characteristics:**

* **Data Location:** Data files reside in external cloud storage, not within Snowflake's managed storage.
* **Query Access:** You can query data directly from the external files using standard SQL, just like querying any other table in Snowflake.
* **Data Ownership:** You maintain ownership and control of the data files in your external storage.
* **Metadata in Snowflake:** Snowflake stores metadata about the external table (schema, location of files, file format) but not the actual data.
* **Performance:** Query performance can depend on factors like the file format, size of the data, and the connection to your external storage.  Generally, optimized file formats like Parquet provide better performance than formats like CSV.
* **Cost-Effectiveness:** Can be cost-effective for querying infrequently accessed data or for exploring large datasets without incurring Snowflake storage costs.  You primarily pay for the compute resources used to query the data and the storage costs within your cloud provider.

**How it Works:**

1. **External Stage:** You create an external stage in Snowflake that points to the location of your data files in external storage.
2. **File Format:** You define a file format (e.g., CSV, JSON, Parquet, Avro) that describes the structure of the data files.
3. **External Table Definition:** You create the external table in Snowflake. The definition includes the table schema, the location of the external stage, and the file format.
4. **Querying:** You can then query the external table using standard SQL. Snowflake retrieves the data directly from the external files when you execute a query.

**When to Use External Tables:**

* **Infrequently Accessed Data:** Data that is not queried regularly can be kept in external storage and accessed as needed.
* **Large Datasets for Exploration:**  Quickly explore large datasets without the upfront cost and time of loading them into Snowflake.
* **Data Lake Querying:**  Directly query data residing in a data lake.
* **Simplified Data Sharing:** Share data easily by granting access to the external stage and table.


**Example Scenario:**

Let's say you have large log files stored in AWS S3. Instead of loading these logs into Snowflake, you could create an external table in Snowflake pointing to the S3 location.  This allows you to query the log data directly from S3 without having to copy it into Snowflake, potentially saving significant storage costs and simplifying your data pipeline.

[Supported Datatypes](https://docs.snowflake.com/en/sql-reference/intro-summary-data-types)


## Dynamic Table vs View vs Material View

| Feature        | View                     | Materialized View          | Dynamic Table (Snowflake)                              |
| -------------- | ------------------------ | -------------------------- | ------------------------------------------------------ |
| Data Storage   | Virtual (no data stored) | Physical (data stored)     | Physical (data stored)                                 |
| Refresh        | On every query           | Manual/Scheduled/On Demand | Automatic (based on base table changes)                |
| Performance    | Slower (query execution) | Faster (pre-computed)      | Faster (pre-computed)                                  |
| Storage Cost   | None                     | Yes                        | Yes                                                    |
| Data Freshness | Always up-to-date        | Can be stale               | Can be slightly stale, but configurable refresh        |
| Data Latency   | None                     | Can have latency           | Can have some latency, but less than Materialized View |

# Explore SQL

#### **Semi-Structured Data Handling (VARIANT, PARSE_JSON)**
- Snowflake natively supports JSON, XML, etc., using the `VARIANT` type.

```sql
-- Add a JSON column to the MBA table
ALTER TABLE TESTING.PUBLIC.MBA ADD COLUMN EXTRA_DATA VARIANT;

-- Insert semi-structured data
UPDATE TESTING.PUBLIC.MBA 
SET EXTRA_DATA = PARSE_JSON('{"recommendations": 3, "essay_score": 9.5}') 
WHERE APPLICATION_ID = 1001;

-- Query nested JSON data
SELECT APPLICATION_ID, EXTRA_DATA:recommendations AS recommendations 
FROM TESTING.PUBLIC.MBA;
```

####  **Time Travel**
- Query historical data (up to 90 days) using `AT` or `BEFORE`.

```sql
-- See data as it looked 1 hour ago
SELECT * FROM TESTING.PUBLIC.MBA AT(TIMESTAMP => DATEADD(hour, -1, CURRENT_TIMESTAMP()));

-- Query data as it existed at a specific statement ID or Query ID
SELECT * FROM TESTING.PUBLIC.MBA BEFORE(STATEMENT => '01b9dc7d-0000-74b9-0000-0bc1000237d2');

-- Restore a deleted row
CREATE TABLE TESTING.PUBLIC.MBA_RESTORED 
CLONE TESTING.PUBLIC.MBA 
BEFORE(TIMESTAMP => '2023-10-01 12:00:00');

-- Data retention period is configurable (up to 90 days for Enterprise edition)
ALTER TABLE TESTING.PUBLIC.MBA SET DATA_RETENTION_TIME_IN_DAYS = 7; -- Keep 7 days of history
```

#### **Zero-Copy Cloning**
- Create instant, storage-efficient copies of tables.

```sql
CREATE TABLE TESTING.PUBLIC.MBA_CLONE 
CLONE TESTING.PUBLIC.MBA;
```

Clone Entire Database
```sql
-- Create a clone of an entire database 
CREATE DATABASE MY_CLONE_DB CLONE MY_SOURCE_DB;
```

#### **Querying Semi-Structured Data with FLATTEN**

```sql
UPDATE TESTING.PUBLIC.MBA 
SET EXTRA_DATA = PARSE_JSON('{"recommendations": 3, "essay_score": 9.5, "interviews": ["John", "Jane"]}') 
WHERE APPLICATION_ID > 10;


SELECT APPLICATION_ID, f.value AS interviewer
FROM TESTING.PUBLIC.MBA,
LATERAL FLATTEN(INPUT => EXTRA_DATA:interviews) f;
```

#### **Dynamic Parameterized Queries**
- Use `LIMIT` with subqueries or session variables.

```sql
SET limit_var = 10;
SELECT * 
FROM TESTING.PUBLIC.MBA 
LIMIT $limit_var;
```

#### **Window Functions with QUALIFY**
- Filter results of window functions without subqueries.
```sql
SELECT APPLICATION_ID, GPA, 
       RANK() OVER (ORDER BY GPA DESC) AS rank
FROM TESTING.PUBLIC.MBA
QUALIFY rank <= 5; -- Show top 5 GPAs
```

#### **Snowflake Scripting (Procedural SQL)**
- Write stored procedures with SQL/JavaScript.

A **procedure** (also called a **stored procedure**) is a reusable set of SQL statements that you store in a database. It is used to perform specific tasks or operations, such as updating data, executing complex logic, or automating repetitive database operations.

**Advantages of Procedures**
- **Automation**: Automate repetitive tasks (e.g., updating admissions, sending reminders).
- **Consistency**: Centralize logic to avoid duplication and ensure uniformity across applications.
- **Security**: Grant permissions to execute the procedure without exposing the underlying tables.
- **Maintainability**: Simplify updates by changing the procedure logic in one place.

```sql
CREATE OR REPLACE PROCEDURE update_admission()
RETURNS STRING
LANGUAGE SQL
AS
BEGIN
   UPDATE TESTING.PUBLIC.MBA
   SET ADMISSION = CASE 
                     WHEN GPA > 3.5 AND GMAT > 700 THEN 'Accepted' 
                     ELSE 'Rejected' 
                   END;
   RETURN 'Admissions updated!';
END;
```

Lets use this

```sql
CALL update_admission();
```

Now verify

```sql
SELECT APPLICATION_ID, GPA, GMAT, ADMISSION
FROM TESTING.PUBLIC.MBA;
```

#### **Data Sharing**
- Securely share data across Snowflake accounts.

```sql
CREATE SHARE MBA_DATA_SHARE;
```
A **share** is a Snowflake object that allows you to share specific database objects (like tables, views, and schemas) with other Snowflake accounts.

```sql
GRANT USAGE ON DATABASE TESTING TO SHARE MBA_DATA_SHARE;
```

The `USAGE` privilege on the database allows the recipients of the share to "see" and access the database structure but not the data itself. Without this privilege, the recipient cannot navigate the database hierarchy (schemas, tables, etc.).

Grant SELECT on the Table
```sql
GRANT SELECT ON TABLE TESTING.PUBLIC.MBA TO SHARE MBA_DATA_SHARE;
```

The `SELECT` privilege on the `TESTING.PUBLIC.MBA` table allows recipients to query the data in this specific table. You can also grant privileges on other database objects (e.g., views or schemas) if needed.

### Stream and Tasks for Data Pipelines

**Create the `ADMISSIONS_DATA` Table**
- **Purpose**: This table stores the admissions data for applicants.
- **Columns**:
  - `APPLICATION_ID`: Unique identifier for each application (NUMBER).
  - `GENDER`: Gender of the applicant (VARCHAR).
  - `INTERNATIONAL`: Boolean flag indicating if the applicant is international.
  - `GPA`: Grade Point Average of the applicant (NUMBER with 2 decimal places).
  - `MAJOR`: Major field of study (VARCHAR).
  - `RACE`: Race of the applicant (VARCHAR).
  - `GMAT`: GMAT score of the applicant (NUMBER with 1 decimal place).
  - `WORK_EXP`: Work experience in years (NUMBER with 1 decimal place).
  - `WORK_INDUSTRY`: Industry of work experience (VARCHAR).
  - `ADMISSION`: Admission status (VARCHAR, e.g., "Accepted" or "Rejected").
  - `EXTRA_DATA`: Optional field for additional data (VARIANT type).

```sql
CREATE OR REPLACE TABLE TESTING.PUBLIC.ADMISSIONS_DATA (
    APPLICATION_ID NUMBER(38,0),
    GENDER VARCHAR(16777216),
    INTERNATIONAL BOOLEAN,
    GPA NUMBER(38,2),
    MAJOR VARCHAR(16777216),
    RACE VARCHAR(16777216),
    GMAT NUMBER(38,1),
    WORK_EXP NUMBER(38,1),
    WORK_INDUSTRY VARCHAR(16777216),
    ADMISSION VARCHAR(16777216),
    EXTRA_DATA VARIANT
);
```

**Insert Sample Data into `ADMISSIONS_DATA`**
- **Purpose**: Populate the table with sample admissions data.
- **Rows Inserted**: 5 rows with varying attributes for testing purposes.

```sql
INSERT INTO TESTING.PUBLIC.ADMISSIONS_DATA (
    APPLICATION_ID, GENDER, INTERNATIONAL, GPA, MAJOR, RACE, GMAT, WORK_EXP, WORK_INDUSTRY, ADMISSION, EXTRA_DATA
) VALUES
(1, 'Male', TRUE, 3.8, 'Engineering', 'Asian', 720, 5, 'Technology', 'Accepted', NULL),
(2, 'Female', FALSE, 3.5, 'Business', 'Hispanic', 680, 3, 'Finance', 'Rejected', NULL),
(3, 'Male', TRUE, 3.9, 'Economics', 'White', 740, 6, 'Consulting', 'Accepted', NULL),
(4, 'Female', FALSE, 3.4, 'Science', 'Black', 650, 2, 'Education', 'Rejected', NULL),
(5, 'Non-binary', TRUE, 3.7, 'Arts', 'Asian', 700, 4, 'Media', 'Accepted', NULL);
```

 **Query the `ADMISSIONS_DATA` Table**
- **Purpose**: Verify the data inserted into the table.
- **Query**:
```sql
SELECT * FROM ADMISSIONS_DATA;
```

**Create a Stream on the `ADMISSIONS_DATA` Table**
- **Purpose**: A stream tracks changes (inserts, updates, deletes) made to the `ADMISSIONS_DATA` table.
- **Stream Name**: `ADMISSIONS_DATA_STREAM`.
- **Usage**: The stream will be used to capture changes and load them into a history table.

```sql
CREATE OR REPLACE STREAM ADMISSIONS_DATA_STREAM ON TABLE TESTING.PUBLIC.ADMISSIONS_DATA;
```

**Create the `ADMISSIONS_DATA_HISTORY` Table**
- **Purpose**: This table stores historical changes to the `ADMISSIONS_DATA` table.
- **Additional Column**:
  - `CHANGE_TIME`: Timestamp indicating when the change was recorded (defaults to the current timestamp).
```sql
CREATE OR REPLACE TABLE TESTING.PUBLIC.ADMISSIONS_DATA_HISTORY (
    APPLICATION_ID NUMBER(38,0),
    GENDER VARCHAR(16777216),
    INTERNATIONAL BOOLEAN,
    GPA NUMBER(38,2),
    MAJOR VARCHAR(16777216),
    RACE VARCHAR(16777216),
    GMAT NUMBER(38,1),
    WORK_EXP NUMBER(38,1),
    WORK_INDUSTRY VARCHAR(16777216),
    ADMISSION VARCHAR(16777216),
    EXTRA_DATA VARIANT,
    CHANGE_TIME TIMESTAMP DEFAULT CURRENT_TIMESTAMP()
);
```

**Query the `ADMISSIONS_DATA_HISTORY` Table**
- **Purpose**: Verify the structure of the history table.
- **Query**:
```sql
SELECT * FROM ADMISSIONS_DATA_HISTORY;
```

**Create a Task to Load Changes into the History Table**
- **Purpose**: Automate the process of loading changes from the stream into the history table.
- **Task Name**: `LOAD_ADMISSIONS_DATA`.
- **Schedule**: Runs every minute.
- **Action**: Inserts data from the stream (`ADMISSIONS_DATA_STREAM`) into the history table (`ADMISSIONS_DATA_HISTORY`).

```sql
CREATE OR REPLACE TASK LOAD_ADMISSIONS_DATA
    SCHEDULE = '1 minute' -- Run every minute
AS
    INSERT INTO TESTING.PUBLIC.ADMISSIONS_DATA_HISTORY (
        APPLICATION_ID, GENDER, INTERNATIONAL, GPA, MAJOR, RACE, GMAT, WORK_EXP, WORK_INDUSTRY, ADMISSION, EXTRA_DATA
    )
    SELECT 
        APPLICATION_ID, 
        GENDER, 
        INTERNATIONAL, 
        GPA, 
        MAJOR, 
        RACE, 
        GMAT, 
        WORK_EXP, 
        WORK_INDUSTRY, 
        ADMISSION, 
        EXTRA_DATA
    FROM TESTING.PUBLIC.ADMISSIONS_DATA_STREAM;
```

**Resume the Task**
- **Purpose**: Start the task so it can execute according to the defined schedule.
- **Command**:
```sql
ALTER TASK LOAD_ADMISSIONS_DATA RESUME;
```

**Show Task Details**
- **Purpose**: Verify the task's existence and configuration.
- **Query**:
```sql
SHOW TASKS LIKE 'LOAD_ADMISSIONS_DATA';
```

**Describe the Stream and History Table**
- **Purpose**: View metadata about the stream and history table.
- **Commands**:
```sql
DESCRIBE STREAM ADMISSIONS_DATA_STREAM;
DESCRIBE TABLE ADMISSIONS_DATA_HISTORY;
```

**Check Task Execution History**
- **Purpose**: Monitor the execution history of the task.
- **Query**:
```sql
SELECT *
FROM TABLE(INFORMATION_SCHEMA.TASK_HISTORY())
WHERE NAME = 'LOAD_ADMISSIONS_DATA';
```

**Insert Additional Data into `ADMISSIONS_DATA`**
- **Purpose**: Test the stream and task by inserting new data.
- **Rows Inserted**: Same as the initial data for testing purposes.

```sql
INSERT INTO TESTING.PUBLIC.ADMISSIONS_DATA (
    APPLICATION_ID, GENDER, INTERNATIONAL, GPA, MAJOR, RACE, GMAT, WORK_EXP, WORK_INDUSTRY, ADMISSION, EXTRA_DATA
) VALUES
(1, 'Male', TRUE, 3.8, 'Engineering', 'Asian', 720, 5, 'Technology', 'Accepted', NULL),
(2, 'Female', FALSE, 3.5, 'Business', 'Hispanic', 680, 3, 'Finance', 'Rejected', NULL),
(3, 'Male', TRUE, 3.9, 'Economics', 'White', 740, 6, 'Consulting', 'Accepted', NULL),
(4, 'Female', FALSE, 3.4, 'Science', 'Black', 650, 2, 'Education', 'Rejected', NULL),
(5, 'Non-binary', TRUE, 3.7, 'Arts', 'Asian', 700, 4, 'Media', 'Accepted', NULL);
```

**Query the `ADMISSIONS_DATA` Table**
- **Purpose**: Verify the new data inserted.
- **Query**:
```sql
SELECT * FROM ADMISSIONS_DATA;
```

**Query the `ADMISSIONS_DATA_HISTORY` Table**
- **Purpose**: Verify that changes were captured and loaded into the history table.
- **Query**:
```sql
SELECT * FROM TESTING.PUBLIC.ADMISSIONS_DATA_HISTORY;
```

