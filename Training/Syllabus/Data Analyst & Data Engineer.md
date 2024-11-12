---
Created by: Shudipto Trafder
Created time: 2024-11-12T17:50:00
Last edited by: Shudipto Trafder
Last edited time: 2024-11-12T17:54:00
tags:
  - syllabus
---

**Course Duration**: 12 weeks
**Total Class Time per Week:** 10 hours

**Weeks 1-4: Foundational Data Skills (Data Analysis Focus)**

* **Week 1: Introduction to Data Analysis & Python (10 hours)**
    * **Data Analysis Lifecycle:** Data collection, cleaning, exploration, analysis, interpretation, visualization, communication. (2 hours)
    * **Python Basics:** Data types (int, float, string, bool), operators, variables, input/output. (2 hours)
    * **Data Structures:** Lists, tuples, dictionaries, sets; operations and use cases. (2 hours)
    * **Control Flow:** Conditional statements (if/elif/else), loops (for/while). (2 hours)
    * **NumPy Introduction:** Creating arrays, array operations, mathematical functions. (2 hours)
    * **Project:** Analyzing a public dataset (e.g., NYC taxi data) using basic Python – calculating average trip distance, fare, etc.

* **Week 2: Data Wrangling & Manipulation (10 hours)**
    * **Pandas Introduction:** Series and DataFrames, creating and manipulating data structures. (2 hours)
    * **Data Cleaning:** Handling missing values (imputation, deletion), identifying and removing duplicates. (2 hours)
    * **Data Transformation:**  Reshaping data (pivot tables, stack/unstack), merging and joining datasets. (2 hours)
    * **String Manipulation and Regular Expressions:** Cleaning and extracting information from text data. (2 hours)
    * **Data Aggregation:** Grouping and summarizing data using `groupby()`, applying aggregate functions. (2 hours)
    * **Project:** Cleaning and preparing a messy dataset (e.g., a real-world dataset with inconsistencies) for analysis.

* **Week 3: Data Visualization & Storytelling (10 hours)**
    * **Matplotlib Basics:** Creating various plot types (line, scatter, bar, histogram). (2 hours)
    * **Seaborn for Statistical Visualization:**  Distribution plots, relationship plots, categorical plots. (2 hours)
    * **Data Storytelling Principles:**  Choosing the right visualization, creating compelling narratives, focusing on key insights. (2 hours)
    * **Dashboarding:** Combining multiple visualizations to tell a comprehensive story. (2 hours)
    * **Presentation Skills:**  Communicating findings effectively, tailoring presentations to different audiences. (2 hours)
    * **Project:** Creating a data visualization dashboard using a cleaned dataset and presenting key findings.

* **Week 4: SQL for Data Analysis (10 hours)**
    * **Relational Databases:** Introduction to database concepts, tables, relationships, keys. (2 hours)
    * **SQL Syntax:** SELECT, FROM, WHERE, JOIN (inner, left, right, full outer), subqueries. (4 hours)
    * **Data Aggregation and Filtering:** GROUP BY, HAVING, aggregate functions (COUNT, SUM, AVG, MIN, MAX). (2 hours)
    * **Window Functions:**  Performing calculations across rows within a specified partition. (2 hours)
    * **Project:** Analyzing data from a relational database (e.g., a sample database of customers, orders, and products) using SQL queries.

**Weeks 5-8: Data Engineering Fundamentals (Data Engineering Focus)**

* **Week 5: Introduction to Data Engineering & Google Cloud Platform (GCP) (10 hours)**
    * **Data Engineering Principles:** Data warehousing concepts (schema design, ETL), data lake vs. data warehouse, data modeling. (2 hours)
    * **Introduction to GCP:** Core services overview (Compute Engine, Cloud Storage, BigQuery, Cloud Functions), navigating the GCP console. (2 hours)
    * **Cloud Storage:**  Storing and retrieving data, different storage classes, data lifecycle management. (2 hours)
    * **Compute Engine:** Creating and managing virtual machines, setting up a development environment. (2 hours)
    * **Working with the gcloud CLI:** Basic commands for interacting with GCP services. (2 hours)
    * **Project:** Setting up a GCP project, creating a Cloud Storage bucket, uploading and downloading data, launching a Compute Engine instance.

* **Week 6: Data Pipelines with Python and GCP (10 hours)**
    * **Shell Scripting Basics:**  Navigating the file system, executing commands, basic scripting. (2 hours)
    * **Working with APIs:**  Making HTTP requests, parsing JSON responses, interacting with RESTful APIs. (2 hours)
    * **Building ETL Pipelines with Python:**  Extracting data from various sources (APIs, databases, files), transforming data using Pandas, loading data into Cloud Storage or BigQuery. (4 hours)
    * **Introduction to Cloud Functions:** Serverless computing for data processing tasks. (2 hours)
    * **Project:** Building an ETL pipeline to ingest data from a public API (e.g., Twitter API) into a BigQuery table.

* **Week 7: Big Data Technologies (Spark) on GCP (10 hours)**
    * **Introduction to Distributed Computing:**  Concepts of distributed systems, map-reduce paradigm. (2 hours)
    * **Apache Spark Overview:**  Spark architecture, RDDs, DataFrames, Spark SQL. (2 hours)
    * **Spark on Dataproc:**  Creating and managing Dataproc clusters, submitting Spark jobs. (2 hours)
    * **Data Processing with Spark:**  Transforming and analyzing data using Spark transformations and actions. (2 hours)
    * **Connecting Spark to BigQuery:** Reading and writing data between Spark and BigQuery. (2 hours)
    * **Project:** Processing a large dataset (e.g., a public dataset on Google Cloud Storage) using Spark on Dataproc, performing aggregations and analysis, and saving the results to BigQuery.

* **Week 8: Orchestration and Workflow Management with GCP (10 hours)**
    * **Workflow Orchestration Concepts:**  DAGs, task dependencies, scheduling, and monitoring. (2 hours)
    * **Cloud Composer (Managed Airflow):** Creating and managing workflows using Cloud Composer. (4 hours)
    * **Defining DAGs in Python:**  Using Python to define tasks, dependencies, and schedules. (2 hours)
    * **Monitoring and Logging:**  Tracking workflow execution, troubleshooting errors. (2 hours)
    * **Project:** Building an orchestrated data pipeline using Cloud Composer to automate the ETL process from Week 6, incorporating error handling and logging.


**Weeks 9-12: Capstone Projects, Advanced Topics & Interview Preparations**

* **Week 9: Advanced Topics & Capstone Project Planning (10 hours)**
    * **Advanced Data Analysis Techniques:** Hypothesis testing, regression analysis, time series analysis (4 hours)
    * **Advanced Data Engineering Concepts:** Data warehousing, dimensional modeling, data lake house architecture. (4 hours)
    * Capstone Project: Planing

* **Week 10-11: Capstone Project Execution**
    * **Dual Capstone Project Execution:** Build the data pipeline/infrastructure (data engineering) and perform data analysis using the processed data.  This integrated approach reinforces the interconnections of the two disciplines.

* **Week 12: Interview Preparation and Mock Interview**
    * **Mock Interviews:**  Practice behavioral questions relevant to both roles, emphasizing communication, teamwork, and problem-solving skills.
    * **Interview Preparation:** This combined session addresses interview questions and challenges relevant to BOTH data analyst and data engineer roles. It includes:
        * **Technical Skills Review:** SQL, Python, cloud platform fundamentals, big data concepts.
        * **Case Studies:**  Data analysis case studies, system design scenarios for data engineering.
        * **Mock Interviews:** Practice answering technical and behavioral questions, receive feedback on communication and problem-solving skills.

