### Medallion Architecture

![](https://www.databricks.com/sites/default/files/inline-images/building-data-pipelines-with-delta-lake-120823.png?v=1702318922)


The **Medallion Architecture** is a data design pattern commonly used in data lakehouse environments. Its primary objective is to organize and refine data systematically by passing it through three distinct layers, each with a specific purpose and quality standard. The layers are typically referred to as **Bronze**, **Silver**, and **Gold**.

#### 1. **Bronze Layer** (Raw Data)

- **Purpose**: Acts as the raw data repository.
- **Data Characteristics**:
    - Contains unprocessed, raw data ingested from various sources (e.g., logs, IoT devices, relational databases, APIs).
    - Includes data in its original format, often with duplicates and incomplete records.
- **Advantages**:
    - Provides an immutable, audit-friendly log of source data.
    - Serves as the foundation for downstream transformations.

#### 2. **Silver Layer** (Cleaned and Enriched Data)

- **Purpose**: Provides cleansed and semi-processed data for broader consumption.
- **Data Characteristics**:
    - Data is deduplicated, validated, and may include transformations like joins, aggregations, or applying business rules.
    - Intermediate quality, suitable for exploratory analysis or lightweight business use.
- **Advantages**:
    - Standardizes data for consistent usage.
    - Ensures the removal of corrupt or invalid data records.
    - Bridges the gap between raw and analytical-ready data.

#### 3. **Gold Layer** (Curated Data)

- **Purpose**: Serves highly processed, aggregated, and business-ready data.
- **Data Characteristics**:
    - Optimized for specific business use cases, such as reporting, dashboards, or machine learning models.
    - Enriched with domain-specific calculations and aggregations.
    - Generally aligns closely with KPIs or key business metrics.
- **Advantages**:
    - Enables fast and efficient access to insights.
    - Ensures data is in the most usable format for decision-making.

#### Benefits of Medallion Architecture

- **Incremental Transformation**: Improves data quality progressively, reducing reprocessing effort.
- **Scalability**: Adapts well to growing data volumes and diverse use cases.
- **Auditability**: Maintains a clear lineage from raw to refined data.
- **Flexibility**: Supports a variety of workflows, including ETL, data warehousing, and analytics.

#### Typical Workflow

1. Ingest raw data into the **Bronze** layer.
2. Cleanse, deduplicate, and transform data into the **Silver** layer.
3. Perform advanced processing or aggregation for the **Gold** layer.


## Other Architecture

### **1. Data Warehouse Architecture**
![](https://miro.medium.com/v2/resize:fit:1400/0*jr53rRe3YvkrdVKD)

- **Purpose**: Centralized repository optimized for structured data and analytical queries.
- **Components**:
    - **ETL Pipelines**: Extract, Transform, Load processes to prepare and load data.
    - **Schema Design**: Star or snowflake schemas for relational databases.
    - **Tools**: Snowflake, Amazon Redshift, Google BigQuery.
- **Use Cases**:
    - Business Intelligence (BI) and reporting.
    - Structured and consistent data storage.

---
### **2. Data Lake Architecture**

![](https://www.interviewbit.com/blog/wp-content/uploads/2022/06/Data-Lake-Architecture-1-1024x694.png)

- **Purpose**: Stores raw, unstructured, or semi-structured data at scale.
- **Components**:
    - **Storage**: Object stores (e.g., Amazon S3, Azure Data Lake, Hadoop HDFS).
    - **Processing Engines**: Apache Spark, Presto, or Hive for querying data.
    - **Cataloging**: Metadata management using tools like AWS Glue or Apache Atlas.
- **Use Cases**:
    - Big Data analytics.
    - Data science and machine learning (ML).

---

### **Comparison: Data Lake vs Data Warehouse**

| **Aspect**              | **Data Lake**                                                                 | **Data Warehouse**                                                   |
| ----------------------- | ----------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| **Purpose**             | Stores raw, unstructured, and semi-structured data for various use cases.     | Stores structured data optimized for analysis and reporting.         |
| **Data Type**           | Unstructured, semi-structured, and structured (e.g., JSON, images, videos).   | Structured data only (e.g., tables, relational formats).             |
| **Schema**              | Schema-on-read: Defined when data is accessed.                                | Schema-on-write: Defined when data is written.                       |
| **Cost**                | Cost-effective for large volumes due to inexpensive storage (e.g., S3, HDFS). | Higher storage and processing costs due to compute-optimized design. |
| **Performance**         | Slower for querying raw or complex data; needs processing/optimization.       | Faster for structured queries due to indexing and optimized storage. |
| **Use Cases**           | Data science, machine learning, exploratory analysis, and streaming data.     | Business intelligence, operational reporting, and analytics.         |
| **Processing Tools**    | Tools like Spark, Hive, Presto for big data analytics.                        | SQL-based tools for structured query processing.                     |
| **Data Governance**     | Challenging due to lack of structure; requires metadata management.           | Easier to govern due to predefined schemas and structured design.    |
| **Scalability**         | Highly scalable for raw data storage.                                         | Scales with cost and complexity for structured analytics.            |
| **Flexibility**         | High; supports diverse data formats and use cases.                            | Limited to structured, predefined use cases.                         |
| **Storage Technology**  | Cloud storage, distributed systems (e.g., Amazon S3, Hadoop HDFS).            | Data warehouse solutions (e.g., Snowflake, Redshift, BigQuery).      |
| **Accessibility**       | Accessible for all types of users but requires advanced tools for insights.   | Designed for business users with SQL expertise.                      |
| **Data Quality**        | Data is raw and may contain duplicates or errors.                             | Data is cleansed, deduplicated, and transformed for reliability.     |
| **Integration with ML** | Suited for machine learning pipelines and big data analytics.                 | Less suitable for unstructured ML workloads but great for BI.        |

- Use **Data Lakes** when you need to store vast amounts of raw data for diverse processing, including big data analytics and machine learning.
- Use **Data Warehouses** for structured data analysis, such as business intelligence and operational reporting.

---
### **3. Data Lakehouse Architecture**

![](https://cdn2.bitwiseglobal.com/bwglobalprod-cdn/2023/10/Databricks_Lakehouse_Cloud_Agnostic_Ref_Arc_-651fdc570d893.png)

- **Purpose**: Combines the scalability of a data lake with the reliability and structure of a data warehouse.
- **Components**:
    - **Unified Storage**: Stores raw and curated data.
    - **Query Engine**: Allows both SQL analytics and ML workloads.
    - **Tools**: Databricks, Delta Lake, Apache Iceberg.
- **Use Cases**:
    - Unified analytics and ML pipelines.
    - Single platform for structured and unstructured data.

---

### **4. Lambda Architecture**

![](https://hazelcast.com/wp-content/uploads/2021/12/19_Lambda-1.png)

- **Purpose**: Combines batch and real-time data processing.
- **Components**:
    - **Batch Layer**: Processes large historical datasets (e.g., Hadoop, Apache Spark).
    - **Speed Layer**: Handles real-time, low-latency data (e.g., Apache Kafka, Apache Flink).
    - **Serving Layer**: Combines results from batch and speed layers for queries.
- **Use Cases**:
    - Real-time analytics with historical context.
    - IoT and event-driven systems.

---

### **5. Kappa Architecture**

![](https://www.kai-waehner.de/wp-content/uploads/2021/07/Kappa-instead-of-Lambda-Architecture-with-Kafka-at-Uber-1024x547.png)

- **Purpose**: A simplified version of the Lambda architecture designed for real-time data processing.
- **Components**:
    - **Streaming Engine**: Handles both real-time and historical data (e.g., Apache Kafka, Apache Pulsar).
    - **Processing Frameworks**: Flink, Apache Beam, or Spark Structured Streaming.
- **Use Cases**:
    - Real-time analytics without complex batch processing.
    - Event-driven systems.
