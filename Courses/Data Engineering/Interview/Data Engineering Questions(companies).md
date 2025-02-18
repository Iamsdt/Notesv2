### Deloitte Data Engineer Interview Questions (2024)

---

#### **1. Can you explain your project flow and architecture?**

When answering this question:
- Start by outlining the **business problem** the project aimed to solve.
- Explain the **data flow**: from ingestion, processing, and storage to analytics and visualization.
- Highlight the tools and technologies you used.

Example:
"Our project aimed to build a real-time analytics dashboard for sales data. The architecture was:
- **Data Ingestion**: Used Kafka to collect data from multiple sources like POS systems and web platforms.
- **Processing**: Data was cleaned and transformed in Spark structured streaming.
- **Storage**: Processed data was stored in AWS S3 (parquet format) for batch analysis and DynamoDB for real-time queries.
- **Analytics**: Connected Tableau to S3 for visualization.
- Followed CI/CD pipelines using Jenkins to automate deployments and ensured data quality with Great Expectations."

---

#### **2. What is the default file format used in Spark?**

The default file format in Spark is **Parquet**. It is columnar and optimized for analytical queries. If not specified, Spark defaults to Parquet when writing data.

---

#### **3. Why is Parquet commonly used in Spark?**

- **Columnar Format**: Stores data by columns, enabling efficient retrieval.
- **Compression**: Provides better compression compared to row-based formats, reducing storage costs.
- **Schema Evolution**: Supports schema evolution without breaking existing workflows.
- **Predicate Pushdown**: Reads only relevant columns/rows, speeding up processing.

---

#### **4. What optimization techniques have you implemented in your projects?**

Common Spark optimizations include:
- **Partitioning**: Partitioned data by key fields to improve parallelism.
- **Broadcast Joins**: Used for small datasets to reduce shuffle overhead.
- **Caching**: Cached frequently used datasets using `cache()` or `persist()`.
- **Avoiding Skew**: Handled data skew by salting keys.
- **Repartitioning**: Adjusted the number of partitions with `repartition` and `coalesce` for optimal performance.
- **Cost-Based Optimizer (CBO)**: Enabled CBO for better query planning.
- **Vectorized UDFs**: Used Pandas UDFs for efficient row-wise operations.

---

#### **5. Can you explain the difference between `groupByKey` and `reduceByKey` in Spark? Which one is more efficient?**

- **`groupByKey`**:
  - Groups all values for a key and sends them to a single node.
  - Requires more memory as it transfers all values across the network.
  - Less efficient for large datasets.

- **`reduceByKey`**:
  - Performs aggregation locally before shuffling data.
  - Reduces data size during shuffling.
  - More efficient for large datasets.

**Example**: If summing values by key, use `reduceByKey` to minimize data transfer.

---

#### **6. What do you understand by rack awareness in Hadoop?**

Rack awareness ensures data is distributed across different racks in a Hadoop cluster:
- **Fault Tolerance**: Keeps replicas on different racks to prevent data loss in case of rack failure.
- **Network Optimization**: Places one replica on the same rack for faster access, while others are on different racks.

---

#### **7. What file formats do you typically use in your data processing workflows?**

- **Parquet**: Optimized for analytics, supports compression and predicate pushdown.
- **Avro**: Schema evolution and compact serialization format.
- **JSON**: Lightweight format, used for semi-structured data.
- **ORC**: Similar to Parquet but used with Hive.
- **CSV**: Simple, used for small datasets or temporary files.

---

#### **8. How does fault tolerance work in Spark?**

Spark achieves fault tolerance using:
- **RDD Lineage**: Maintains a DAG of transformations, allowing recreation of lost partitions.
- **Checkpointing**: Saves RDDs to stable storage for recovery.
- **Replication**: For streaming, data is replicated to multiple nodes.

---

#### **9. How would you handle and ignore null values while loading data?**

- Use Spark DataFrame methods:
  ```python
  df = spark.read.format("csv").option("header", "true").load("data.csv")
  df = df.na.drop()  # Drops rows with null values
  ```
- For selective columns:
  ```python
  df = df.na.fill({"column1": 0, "column2": "unknown"})  # Fill nulls with defaults
  ```

---

#### **10. How would you find the 3rd highest salary in a dataset?**

SQL Approach:
```sql
SELECT DISTINCT salary 
FROM employees 
ORDER BY salary DESC 
LIMIT 3;
```
Then fetch the last record programmatically.

Spark Approach:
```python
df = df.select("salary").distinct().orderBy("salary", ascending=False)
third_highest = df.collect()[2]["salary"]
```

---

#### **11. Given a dataset with positive and negative invoice values, how would you convert the positive values to negative while keeping the negative values unchanged?**

Spark Code:
```python
df = df.withColumn("invoice_value", 
    when(col("invoice_value") > 0, col("invoice_value") * -1).otherwise(col("invoice_value"))
)
```

---

#### **12. How can you convert a date like "20/04/1963" to an integer format?**

Use Spark's `unix_timestamp` or Python libraries:
```python
from pyspark.sql.functions import to_date, unix_timestamp

df = df.withColumn("date_as_int", unix_timestamp("date_column", "dd/MM/yyyy").cast("int"))
```

---

#### **13. Given a dataset containing alphanumeric values and integers, how would you extract specific alphanumeric sequences like "ML," "GM," and "LTR" and create a new DataFrame to view only these sequences in Spark?**

Spark Code:
```python
from pyspark.sql.functions import col, regexp_extract

df = df.withColumn("extracted", regexp_extract(col("column_name"), "(ML|GM|LTR)", 0))
filtered_df = df.filter(col("extracted") != "")
```

---

#### **14. What kind of questions have you encountered related to data modeling in your projects?**

- **Entity-Relationship Modeling**: Identifying relationships and designing schemas for normalized and denormalized datasets.
- **Star vs. Snowflake Schema**: Explaining trade-offs.
- **Fact and Dimension Tables**: Designing based on business needs.
- **Data Partitioning**: Partitioning tables for performance.
- **Historical Data Handling**: Using Slowly Changing Dimensions (SCDs).

For example, "We used a star schema for sales analytics where fact tables contained sales transactions, and dimension tables provided product, time, and customer information." 

--- 

# 10 Interview Questions For Data Engineer 

Question 1. Can you describe your experience with data engineering?

Employers look for: Depth of technical expertise, project complexity, and business impact.

Example answer: In my 5+ years as a data engineer, I've architected end-to-end data solutions focusing on three main areas:
- Built real-time streaming pipelines using Kafka and Spark Streaming, processing 1M+ events/second
- Designed cloud data lakes on AWS using S3, Athena, and Glue, reducing storage costs by 40%
- Implemented automated data quality frameworks using Great Expectations, achieving 99.9% data accuracy

Question 2. What programming languages are you proficient in?

Employers look for. Proficiency in relevant programming languages for data engineering.

Example answer. I am proficient in Python, SQL, and Java, which I use regularly for data manipulation, querying, and building data pipelines. Additionally, I have experience with Scala for working with Apache Spark. These languages have enabled me to efficiently handle large datasets and perform complex data transformations.

Question 3. How do you handle data quality issues?

Employers look for: Systematic approach to data quality management.

Example answer: I follow a comprehensive approach to data quality:
1. Prevention:
   - Schema validation using JSON/Avro schemas
   - Input validation at data ingestion points
   - Automated unit tests for data transformations
2. Detection:
   - Data quality rules in Great Expectations
   - Anomaly detection using statistical methods
   - Real-time monitoring with Prometheus/Grafana
3. Resolution:
   - Automated correction for known issues
   - Alert routing to responsible teams
   - Root cause analysis using lineage tools

Question 4. What is ETL, and how have you used it in your projects?

Employers look for. Understanding of ETL processes and practical experience.

Example answer. ETL stands for Extract, Transform, Load, and it’s a process used to move and transform data from various sources into a data warehouse. I have used ETL tools like Apache Nifi and Talend to automate data extraction, transformation, and loading processes. These tools have helped me streamline data workflows and ensure data consistency.

Question 5. Can you explain the difference between a data warehouse and a data lake?

Employers look for. Understanding of data storage concepts and their use cases.

Example answer. A data warehouse is a structured storage system optimized for querying and reporting, typically using SQL. A data lake, on the other hand, is a more flexible storage system that can handle unstructured, semi-structured, and structured data. Data lakes are often used for big data analytics and machine learning applications.

Question 6. How do you optimize SQL queries for performance?

Employers look for: Deep understanding of database internals and optimization techniques.

Example answer: My SQL optimization strategy involves:
1. Query Analysis:
   - Use EXPLAIN ANALYZE to understand execution plans
   - Identify full table scans and expensive joins
   - Monitor query statistics and resource usage
2. Optimization Techniques:
   - Implement appropriate indexing (B-tree, bitmap, partial)
   - Partition large tables by date/region
   - Materialize common computations
   - Use CTEs instead of nested subqueries
3. Data Model Optimization:
   - Denormalization for read-heavy workloads
   - Implement star schema for analytical queries
   - Regular table statistics updates

Question 7. What experience do you have with cloud platforms like AWS, Azure, or Google Cloud?

Employers look for. Experience with cloud-based data engineering tools and services.

Example answer. I have extensive experience with AWS, using services like S3 for storage, Redshift for data warehousing, and Glue for ETL processes. I have also worked with Azure Data Factory for data integration and Google BigQuery for analytics. These platforms have enabled me to build scalable and efficient data solutions.

Question 8. How do you ensure data security and privacy in your projects?

Employers look for: Comprehensive security knowledge and compliance awareness.

Example answer: I implement a multi-layered security approach:
1. Access Control:
   - Role-based access control (RBAC)
   - Column-level security for sensitive data
   - Just-in-time access using tools like AWS IAM
2. Data Protection:
   - Encryption at rest (AES-256)
   - TLS for data in transit
   - Automated key rotation
3. Compliance:
   - Data classification and tagging
   - Automated PII detection and masking
   - Audit logging and monitoring
4. Security Testing:
   - Regular penetration testing
   - Automated security scans
   - Third-party security audits

Question 9. Can you describe a challenging data engineering project you worked on and how you overcame the challenges?

Employers look for. Problem-solving skills and ability to handle complex projects.

Example answer. I worked on a project involving the migration of a large dataset to a new data warehouse. The challenge was ensuring data consistency and minimal downtime. I overcame this by using incremental data loading and thorough testing to validate data integrity before the final cutover.

Question 10. What tools and technologies do you use for data pipeline orchestration?

Employers look for. Familiarity with orchestration tools and their usage.

Example answer. I use tools like Apache Airflow and AWS Step Functions for data pipeline orchestration. These tools help me schedule, monitor, and manage complex data workflows. They provide robust features for error handling, retries, and logging, ensuring reliable and efficient data processing.