---
Created by: Shudipto Trafder
Created time: 2024-11-29T22:20:00
tags:
  - pyspark
  - de
---
Google Cloud Dataproc is a fully managed service designed to run Apache Spark, Apache Hadoop, and other Big Data tools and frameworks on Google Cloud. Dataproc simplifies data processing by automating cluster management, making it easy to run large-scale data processing jobs, whether they are batch, streaming, or interactive workloads. 

Dataproc offers two primary deployment models:

1. **Server-based**: Traditional clusters that are explicitly created and managed, ideal for consistent, long-running workloads.
2. **Serverless**: On-demand batch jobs that require no cluster management, ideal for sporadic, ad-hoc jobs where cost efficiency is essential.

---

## Server vs. Serverless in Dataproc

| Feature               | Server (Managed Clusters)                                  | Serverless (Batch Jobs)                            |
|-----------------------|------------------------------------------------------------|----------------------------------------------------|
| **Cluster Creation**  | Explicit cluster setup required                            | No cluster setup; managed dynamically              |
| **Configuration**     | Full control over cluster configuration                    | Limited to job-specific configurations             |
| **Resource Allocation** | Customizable nodes with master and worker roles          | Automatically scales based on workload             |
| **Cost Efficiency**   | Suitable for long-running tasks                            | Cost-effective for on-demand, short-term jobs      |
| **Setup Complexity**  | Higher initial setup; useful for persistent infrastructure | Simple setup for quick, short-lived jobs           |

---

## Server-Based: Creating a Cluster

### Step 1: Cluster Creation on Google Compute Engine

1. **Service Options**: You can create a Dataproc cluster on either Google Compute Engine or Google Kubernetes Engine (GKE). For this example, we’ll use Google Compute Engine.

2. **Cluster Configuration**:
   - **Name**: Assign a descriptive name to your cluster.
   - **Location**: Specify the Google Cloud region and zone for cluster deployment.
   - **Cluster Type**:
     - **Standard**: One master node and multiple worker nodes.
     - **Single Node**: A single master node with no workers, suitable for testing.
     - **High Availability**: Three master nodes to improve resilience, along with multiple worker nodes.

3. **Versioning**: Choose the appropriate image version for the Dataproc service to ensure compatibility with your Spark version and other Big Data tools.

4. **Performance Enhancements**:
   - **Enable Advanced Optimizations**: Turn on advanced optimization features for improved Spark performance.
   - **Enable Advanced Execution Layer**: Improve execution efficiency using Dataproc's latest enhancements.
   - **Enable Google Cloud Storage Caching**: Enhance data processing speed by caching data from Google Cloud Storage.

### Step 2: Node Configuration

#### Master Node
   - **Machine Type**: `N2-standard-4` (4 vCPUs, 2 cores, 16 GB RAM)
   - **Primary Disk**: 100 GB, **Balanced Persistent Disk**
   - **Local SSDs**: 1 SSD, NVMe interface for high-speed storage access

#### Worker Node
   - **Machine Type**: `N2-standard-4` (4 vCPUs, 2 cores, 16 GB RAM)
   - **Primary Disk**: 100 GB, **Balanced Persistent Disk**
   - **Local SSDs**: 1 SSD, NVMe interface
   - **Number of Worker Nodes**: Define the number of worker nodes required (e.g., 2).

#### Secondary Worker Nodes (Optional)
   - **Preemptibility**: Spot (cost-effective option for non-critical tasks)
   - **Primary Disk Size**: Set to 0 for ephemeral storage
   - **Local SSDs**: Optional; if needed, specify NVMe interface

After finalizing all configurations, click **Create** to set up your Dataproc cluster.

---
### Server-Based: Creating a Cluster with Job Submission

After setting up the Dataproc cluster, you can submit jobs in two ways: using the Google Cloud Console UI or via the `gcloud` command-line tool.

---

### Submitting a Job on a Server-Based Cluster

#### 1. **Using the Google Cloud Console UI**

1. Go to the **Google Cloud Console** and navigate to **Dataproc**.
2. Select your Dataproc cluster from the list.
3. Click on **Submit Job**.
4. In the **Job Type** dropdown, select **PySpark**.
5. Under **Main Python File**, enter the path to your script (e.g., `gs://bucketname/nyc_jobs.py`).
6. Set any required **Properties** for your Spark job:
    - For example: `spark.dynamicAllocation.enabled=true` and `spark.shuffle.service.enabled=true`
7. Specify other job parameters, such as region, arguments, and JAR files, if needed.
8. Click **Submit** to start the job.

#### 2. **Using the `gcloud` Command-Line Tool**

Alternatively, you can submit the job directly from the command line:

```bash
gcloud dataproc jobs submit pyspark gs://bucketname/nyc_jobs.py \     --cluster=cluster-name \     --region=us-central1 \     --properties="spark.dynamicAllocation.enabled=true,spark.shuffle.service.enabled=true"

```

In this command:
- Replace `cluster-name` with the name of your Dataproc cluster.
- Use `gs://bucketname/nyc_jobs.py` to specify the Python script stored in Google Cloud Storage.

This command will submit a PySpark job to your specified cluster, enabling Spark dynamic allocation and shuffle service properties for efficient resource management.


## Serverless: Running Batch Jobs

For serverless jobs, Dataproc enables quick, ad-hoc batch processing without requiring persistent cluster management. Serverless is ideal for use cases like ETL processing, ML model training, and other on-demand computations.

### Submitting a Serverless Batch Job

1. **Setup Parameters**:
   - **Batch ID**: A unique identifier for your job.
   - **Region**: Specify the region where the job will be executed.
   - **Batch Type**: Select from supported types, such as Spark or PySpark.
   - **Runtime Version**: Choose the Dataproc runtime version that supports your workload.
   - **Main Python File**: Provide the path to the Python script or main Spark application.

2. **Submit the Job**:
   Use the `gcloud` command-line tool to submit your batch job. This command submits a PySpark job to Dataproc, specifying parameters such as project ID, region, and source file location in Google Cloud Storage.

   ```bash
   gcloud dataproc batches submit pyspark \
       --project=gpuworks \
       --region=us-central1 \
       --batch=batch-b977 \
       gs://bucketname/nyc_jobs.py \
       --version=2.2 \
       --subnet=default \
       --properties=spark.dataproc.appContext.enabled=true
   ```

3. **Monitor and Review**:
   After submission, Dataproc provides real-time log monitoring and error reporting, allowing you to track the job’s progress and review any issues.

---

### Conclusion

Google Cloud Dataproc provides flexible, scalable solutions for running Apache Spark and other Big Data frameworks. Whether you opt for traditional server-based clusters or the newer serverless batch processing, Dataproc adapts to a variety of data processing needs. For long-term or frequent jobs, server-based clusters offer enhanced configuration control, while serverless batch jobs are ideal for fast, cost-effective data processing with minimal setup.

