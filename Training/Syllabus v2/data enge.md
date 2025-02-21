# Advanced Data Engineering Course (1.5 Months)

## Module 1: Database Systems & Data Modeling (1 Week)

### Class 1: Advanced PostgreSQL
- Performance tuning and optimization
- Partitioning strategies
- Advanced indexing techniques
- Query optimization and execution plans
- Concurrent transactions and MVCC
- Hands-on: Complex query optimization
- Practice: Performance tuning

### Class 2: MongoDB at Scale
- Sharding and replication
- Index strategies and optimization
- Aggregation pipeline optimization
- Change streams
- Transaction management
- Hands-on: Scaling MongoDB
- Practice: Complex aggregations

### Class 3: Data Modeling & Architecture
- Dimensional modeling
- Data vault modeling
- Schema design patterns
- Data normalization vs denormalization
- Real-time vs batch processing
- Hands-on: Data model design
- Practice: Model implementation

### Class 4: Data Lake Architecture
- Data lake vs data warehouse
- Storage layers (Raw, Cleansed, Curated)
- Data governance and metadata
- Security and access patterns
- Delta Lake implementation
- Hands-on: Data lake setup
- Practice: Data organization

### Class 5: Modern Data Warehouse
- Snowflake architecture
- BigQuery optimization
- Materialized views
- Partitioning and clustering
- Cost optimization
- Hands-on: Warehouse implementation
- Practice: Query optimization

## Module 2: Big Data Processing (2 Weeks)

### Week 1: Distributed Computing

#### Class 1: Hadoop Ecosystem
- HDFS architecture
- YARN resource management
- MapReduce paradigm
- HBase and Hive integration
- Performance optimization
- Hands-on: Hadoop cluster
- Practice: MapReduce jobs

#### Class 2: Apache Spark
- RDD operations
- Spark SQL optimization
- DataFrame and Dataset APIs
- Memory management
- Spark UI analysis
- Hands-on: Spark applications
- Practice: Performance tuning

#### Class 3: Advanced Spark
- Custom partitioning
- Broadcast variables
- Accumulators
- Catalyst optimizer
- Tungsten execution
- Hands-on: Advanced optimizations
- Practice: Complex transformations

#### Class 4: Stream Processing
- Structured Streaming
- Watermarking
- State management
- Checkpointing
- Fault tolerance
- Hands-on: Streaming pipeline
- Practice: Real-time processing

#### Class 5: Apache Flink
- Stream processing model
- State backends
- Event time processing
- CEP patterns
- Exactly-once semantics
- Hands-on: Flink applications
- Practice: Stream analytics

### Week 2: Data Pipeline & Integration

#### Class 1: Apache Kafka
- Advanced producer/consumer patterns
- Kafka Connect framework
- Kafka Streams
- Schema registry
- Security implementation
- Hands-on: Kafka cluster
- Practice: Stream processing

#### Class 2: Apache Beam
- Pipeline design patterns
- Windowing strategies
- Triggers and watermarks
- Custom transforms
- Runner optimization
- Hands-on: Beam pipelines
- Practice: Data processing

#### Class 3: Data Integration
- CDC patterns
- ETL vs ELT
- Real-time integration
- Data quality frameworks
- Error handling
- Hands-on: Integration patterns
- Practice: Pipeline implementation

#### Class 4: Workflow Orchestration
- Airflow architecture
- DAG optimization
- Custom operators
- Sensor patterns
- XCom and branching
- Hands-on: Workflow design
- Practice: Pipeline orchestration

#### Class 5: Performance & Monitoring
- Pipeline monitoring
- Resource optimization
- Cost management
- Debugging strategies
- Performance tuning
- Hands-on: Monitoring setup
- Practice: Optimization

## Module 3: Cloud Data Platforms (2 Weeks)

### Week 1: Google Cloud Platform

#### Class 1: DataProc & GCS
- Cluster management
- Storage classes
- IAM and security
- Cost optimization
- Migration strategies
- Hands-on: GCP setup
- Practice: Cloud operations

#### Class 2: Advanced BigQuery
- Query optimization
- Materialized views
- Capacity planning
- ML integration
- Cost control
- Hands-on: BigQuery features
- Practice: Analytics queries

#### Class 3: Data Pipeline Tools
- Cloud Composer
- Cloud Data Fusion
- Dataflow templates
- Pub/Sub patterns
- Cloud Functions
- Hands-on: Pipeline tools
- Practice: Tool integration

#### Class 4: Security & Governance
- Data governance
- Security patterns
- Compliance frameworks
- Audit logging
- Access management
- Hands-on: Security setup
- Practice: Governance implementation

#### Class 5: Performance Optimization
- Query optimization
- Cost analysis
- Resource planning
- Monitoring setup
- Alert management
- Hands-on: Performance tuning
- Practice: Optimization

### Week 2: Modern Data Platforms

#### Class 1: Databricks
- Delta Lake optimization
- Unity Catalog
- MLflow integration
- Photon engine
- Auto-scaling
- Hands-on: Databricks setup
- Practice: Platform usage

#### Class 2: Advanced Snowflake
- Virtual warehouses
- Zero-copy cloning
- Time travel
- Data sharing
- Resource monitoring
- Hands-on: Snowflake features
- Practice: Warehouse management

#### Class 3: Cassandra
- Data modeling
- Partition strategies
- Consistency levels
- Performance tuning
- Monitoring
- Hands-on: Cassandra setup
- Practice: NoSQL implementation

#### Class 4: Real-time Analytics
- Streaming analytics
- Real-time dashboards
- Complex event processing
- Alert mechanisms
- Performance optimization
- Hands-on: Analytics setup
- Practice: Real-time systems

#### Class 5: Modern Architecture
- Lambda architecture
- Kappa architecture
- Data mesh principles
- Microservices integration
- Event-driven patterns
- Hands-on: Architecture design
- Practice: Implementation

# Assignments: 

## Advanced Data Manipulation and Predictive Analysis with Apache Spark
**Objective**: This assignment will test your ability to conduct exploratory data analysis (EDA), clean data, and transform it into a format suitable for predictive analysis and aggregation tasks. [MBA](https://github.com/Training10x/DataEngineering/blob/main/Data/MBA.csv) Datasets.
#### Dataset Fields
The dataset includes the following fields:
- **application_id**: Unique identifier for each application
- **gender**: Applicant's gender (Male, Female)
- **international**: International student status (TRUE/FALSE)
- **gpa**: Grade Point Average on a 4.0 scale
- **major**: Undergraduate major (Business, STEM, Humanities)
- **race**: Racial background (e.g., White, Black, Asian, Hispanic, Other, or null for international students)
- **gmat**: GMAT score (out of 800)
- **work_exp**: Years of work experience
- **work_industry**: Industry of previous work experience (Consulting, Finance, Technology, etc.)
- **admission**: Admission status (Admit, Waitlist, or Null for Deny)

#### Assignment Tasks
1. **Data Loading and Inspection**:
   - Load the dataset into a Spark DataFrame.
   - Display a summary of the dataset to inspect field names, data types, and the first few rows.

2. **Data Cleaning and Transformation**:
   - **Rename Columns**: Rename `work_exp` to `experience_years` and `gmat` to `gmat_score`.
   - **Handle Null Values**:
     - For `gpa`, `gmat_score`, and `work_exp` columns, replace nulls with the median of each column.
     - Fill missing values in the `admission` column with `Deny`.
     - Assume null values in `race` are `International`.
   - **Add Conditional Columns**:
     - Create a column `admission_numeric` with values: 1 for Admit, 0 for Waitlist, and -1 for Deny.
     - Create a column `experience_level` based on `experience_years`:
       - `Entry-level` if experience is 0–2 years
       - `Mid-level` if experience is 3–6 years
       - `Senior` if experience is more than 6 years

3. **Exploratory Data Analysis**:
   - Calculate the average GMAT score and GPA for each `major`.
   - Find the percentage of applicants admitted by `work_industry`.
   - Determine the distribution of `experience_level` among applicants by `gender`.
   - Show the average GPA and GMAT scores by `race` and `international` status.

4. **Aggregation and Insights**:
   - Calculate the admission rate for international vs. domestic applicants.
   - Find the top 3 undergraduate majors with the highest admission rates.
   - Show the average work experience and GPA for admitted vs. denied applicants.
   - Calculate the overall average GPA and GMAT score by `admission` status.

5. **Prediction Dataset Preparation**:
   - Create a final dataset with the following features to predict `admission_numeric`: 
     - `gpa`, `gmat_score`, `experience_years`, `major`, `gender`, and `work_industry`.
   - Save the final dataset as a CSV file for future predictive modeling.

6. **Save the Results**:
   - Save the cleaned DataFrame as a CSV file.
   - Save each of the key aggregations (admission rates, averages, distributions) as separate CSV files.

#### Submission
1. Submit the cleaned DataFrame in CSV format.
2. Submit CSV files for each of the aggregations and insights derived from the dataset.
3. Provide your code in a `.py` file or Jupyter notebook with detailed comments explaining each step.
