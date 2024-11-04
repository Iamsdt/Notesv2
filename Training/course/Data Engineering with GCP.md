
**Program Overview:** This program equips learners with the skills to design, build, and manage data processing systems on Google Cloud Platform (GCP), while also introducing comparable tools and services from AWS and Apache ecosystems.  Students will learn to work with massive datasets, build data lakes, automate data pipelines, and develop proficiency in core data engineering tools.

**Prerequisites:** Intermediate Python, Intermediate SQL, and command line skills.

**Estimated Time:** 4 months (5-10 hours/week)

**Required Hardware/Software:**  All coursework and projects can be completed via online workspaces.


**Course 1: Data Modeling**

* **Course Project:** Designing a Data Model for a Ride-Sharing Application (using GCP Bigtable and Cloud Spanner as primary examples, discussing alternatives like AWS DynamoDB and Apache Cassandra)
* **Lesson 1: Introduction to Data Modeling**
    * Purpose of data modeling
    * Strengths and weaknesses of different database types (relational, NoSQL – document, key-value, graph, wide-column)
    * Introduction to Bigtable (GCP) - creating a table, comparing with DynamoDB (AWS) and Cassandra (Apache)
* **Lesson 2: Relational Data Models**
    * When to use relational databases
    * OLAP vs. OLTP databases
    * Data normalization and denormalization (STAR, Snowflake schemas)
    * Introduction to Cloud Spanner (GCP) - distributed SQL database, comparing with Aurora (AWS) and CockroachDB (Apache)
* **Lesson 3: NoSQL Data Models**
    * When to use NoSQL databases
    * Choosing primary keys and clustering columns
    * Creating a NoSQL database in Bigtable, comparing data modeling approaches with DynamoDB and Cassandra


**Course 2: Cloud Data Warehouses**

* **Course Project:** Building a Data Warehouse for E-commerce Analytics (using BigQuery, discussing alternatives like AWS Redshift and Apache Hive)
* **Lesson 1: Introduction to Data Warehouses**
    * OLAP for business users
    * ETL for OLAP transformations with SQL
    * Data warehouse architecture
    * OLAP cubes: slice, dice, roll-up, drill-down
    * Columnar vs. row-oriented storage
* **Lesson 2: ELT and Data Warehouse Technology in the Cloud**
    * ETL vs. ELT
    * Cloud data storage solutions (GCP Cloud Storage, AWS S3, Apache HDFS)
    * Cloud pipeline solutions (GCP Dataflow, AWS Glue, Apache Spark)
    * Cloud data warehouse solutions (BigQuery, Redshift, Hive)
* **Lesson 3: GCP Data Technologies**
    * BigQuery architecture and features
    * Creating and configuring GCP storage resources
    * Implementing infrastructure as code for BigQuery
* **Lesson 4: Implementing Data Warehouses on GCP**
    * Loading data into BigQuery from various sources
    * Partitioning and clustering tables for performance
    * Query optimization techniques


**Course 3: Spark and Data Lakes**

* **Course Project:** Building a Data Lakehouse for IoT Sensor Data (using Dataproc, Dataflow, and Cloud Storage, discussing alternatives like AWS EMR, Glue, and S3)
* **Lesson 1: Big Data Ecosystem, Data Lakes, and Spark**
    * Big data ecosystem components
    * Purpose and evolution of data lakes
    * Spark vs. Hadoop
    * Lakehouse architecture
* **Lesson 2: Spark Essentials**
    * Data wrangling with Spark and functional programming
    * Spark DataFrames and Spark SQL
    * Processing CSV and JSON data
    * Spark RDDs API
* **Lesson 3: Using Spark and Data Lakes in GCP**
    * Distributed data storage with Cloud Storage
    * Running Spark on Dataproc and Dataflow
    * Configuring and using Dataproc clusters
* **Lesson 4: Building a Lakehouse on GCP**
    * Implementing ELT pipelines with Spark and Dataflow
    * Creating a data catalog with Data Catalog
    * Querying data with Athena (AWS equivalent) and BigQuery
    * Data lakehouse zones (raw, curated, refined)


**Course 4: Automating Data Pipelines**

* **Course Project:** Building a Data Pipeline for a Gaming Platform (using Cloud Composer and Cloud Functions, discussing alternatives like AWS Airflow and Lambda)
* **Lesson 1: Data Pipelines**
    * Defining data pipelines and their uses
    * DAGs (Directed Acyclic Graphs)
    * Tasks and operators
    * Task dependencies and workflow orchestration
* **Lesson 2: Cloud Composer and GCP**
    * Creating and managing Cloud Composer environments
    * Connecting to GCP services using connections and hooks
    * Building DAGs with Python
* **Lesson 3: Data Quality and Pipeline Monitoring**
    * Data lineage and error tracking
    * Data quality checks and validation
    * Monitoring pipeline execution and performance
* **Lesson 4: Production Data Pipelines**
    * Building reusable operators and plugins
    * Implementing task boundaries and error handling
    * Scheduling and managing pipelines in production

