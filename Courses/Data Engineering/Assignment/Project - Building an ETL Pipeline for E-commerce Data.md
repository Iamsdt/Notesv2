## Objectives

This project aims to design and implement a scalable ETL pipeline for processing and analyzing e-commerce data. The system will ingest data from multiple sources, process it, and store it in a cloud data warehouse for analytics and reporting.

---

## Data Collection

### Sources:

1. **API (Order Data)**: Data will be fetched every 10 minutes using PySpark.
2. **SQL Database (Product and User Data)**: Data will be fetched every 30 minutes using PySpark.
3. **Streaming Events (User Behavior Data)**:
   - Events such as views, orders, wishlists, and returns will be streamed via Pub/Sub or Kafka.
   - Data will be processed using PySpark Streaming or Apache Beam.

### Output:

Data from all sources will be saved into a cloud data lake (e.g., Google Cloud Storage) for further processing.

---

## ETL Pipeline

The ETL pipeline will process the data collected from the data lake and perform transformations before saving it into the data warehouse.

### Pipeline Details:

1. **Scheduling and Orchestration**:

   - The pipeline will be scheduled to run every hour using Apache Airflow (managed by Google Cloud Composer).
   - Data processing jobs will be triggered on Google Dataproc clusters.

2. **Data Transformation Steps**:

   - **Event Data**:
     - Aggregate user behavior data (views, orders, wishlists, returns).
     - Calculate traffic and engagement metrics.
   - **Order Data**:
     - Join with product data to enrich order details.
     - Add derived metrics (e.g., total amount spent per order).
   - **Product Data**:
     - Perform deduplication and normalization.
     - Enrich product data with category-level summaries.
   - **User Data**:
     - Enrich user profiles with aggregated behavioral metrics.

3. **Monitoring**:

   - Pipeline jobs will be monitored using Airflow’s UI.
   - Alerts will be configured for failures or performance degradation.

4. **Output**:

   - Transformed data will be saved into a cloud data warehouse (e.g., Google BigQuery).

---

## Data Warehouse Schema

### Unified Table: User Behavior Table

| Column        | Description                                   |
| ------------- | --------------------------------------------- |
| date          | Date of the event                             |
| event\_id     | Unique ID for the event                       |
| event\_name   | Type of event (view, order, wishlist, return) |
| price         | Price associated with the event               |
| product\_id   | Unique ID of the product                      |
| product\_name | Name of the product                           |
| user\_id      | Unique ID of the user                         |
| user\_name    | Name of the user                              |
| order\_id     | Unique ID of the order                        |

---

## Challenges

1. **Airflow (Composer) to Dataproc Integration**:
   - Ensuring seamless communication between Airflow and Dataproc.
   - Handling retries and resource allocation for Dataproc jobs.
2. **Data Deduplication**:
   - Managing duplicate entries from streaming and batch sources.
3. **Real-time Processing**:
   - Handling large-scale event data in near real-time with PySpark Streaming or Beam.

---

## Datasets

### Event Table

| Column      | Description                       |
| ----------- | --------------------------------- |
| event\_id   | Unique ID for the event           |
| event\_name | Type of event (view, order, etc.) |
| product\_id | Unique ID of the product          |
| user\_id    | Unique ID of the user             |
| order\_id   | Unique ID of the order            |
| price       | Price associated with the event   |
| date        | Date of the event                 |

### Product Table

| Column        | Description              |
| ------------- | ------------------------ |
| product\_id   | Unique ID of the product |
| product\_name | Name of the product      |
| category      | Category of the product  |
| price         | Price of the product     |
| date          | Date of the record       |

### User Table

| Column     | Description           |
| ---------- | --------------------- |
| user\_id   | Unique ID of the user |
| user\_name | Name of the user      |
| date       | Date of the record    |

### Order Table

| Column      | Description              |
| ----------- | ------------------------ |
| order\_id   | Unique ID of the order   |
| product\_id | Unique ID of the product |
| user\_id    | Unique ID of the user    |
| date        | Date of the order        |

---

## Streaming Data

A script will be developed to publish streaming event data to Pub/Sub or Kafka. The script will generate simulated user behaviour events for testing and benchmarking purposes.

---

## Analytics and Metrics

### Key Metrics to Monitor

1. **Top Products**:
   - Most sold, wishlisted, and returned products.
2. **Average Spending**:
   - Average amount spent per user per session.
3. **Unique Visitors**:
   - Total number of unique visitors.
4. **Orders by Date**:
   - Distribution of orders across dates.
5. **Daily Traffic**:
   - Number of events and their types per day.

---
## Summary
This project outlines the collection, processing, and analysis of e-commerce data. It leverages modern data engineering tools (PySpark, Airflow, Kafka, Dataproc, and BigQuery) to create a robust and scalable pipeline supporting business intelligence and analytics workflows.



https://www.kaggle.com/datasets/PromptCloudHQ/flipkart-products