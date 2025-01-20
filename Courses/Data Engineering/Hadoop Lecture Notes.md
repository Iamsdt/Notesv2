
## What is Hadoop?

Hadoop is an open-source framework designed for storing and processing vast amounts of data across a distributed cluster of commodity hardware. Inspired by Google's MapReduce and Google File System (GFS) papers, Hadoop offers a powerful and cost-effective solution for handling Big Data challenges.  It's particularly well-suited for batch processing large datasets where parallel processing is feasible. It is written in Java and Shell Scripts.

## Key Components of Hadoop
![[Pasted image 20241223182129.png]]

* **Hadoop Distributed File System (HDFS):**  A distributed file system that provides high-throughput access to application data and is designed to store very large files across multiple machines. HDFS is fault-tolerant and optimized for streaming data access, making it ideal for write-once, read-many scenarios.
* **MapReduce:** A programming model for processing large datasets in parallel. It divides the processing into two phases: *Map* and *Reduce*. The *Map* phase transforms the input data into intermediate key-value pairs, while the *Reduce* phase aggregates these pairs based on the keys to produce the final output.
* **YARN (Yet Another Resource Negotiator):** A cluster resource management system that manages cluster resources and schedules applications.  It allows for running various distributed applications beyond MapReduce, providing flexibility and scalability.

## When to Use Hadoop

Hadoop excels in situations where:

* You need to process massive volumes of unstructured or semi-structured data.
* Your processing tasks can be easily parallelized.
* Batch processing is acceptable (interactive, real-time processing is not a requirement).
* You have access to a cluster of affordable commodity hardware.
* Fault tolerance is important
* You need high throughput for large files

Examples of Hadoop Use Cases:

* **Image processing:** Analyzing large image datasets (like those used in medical imaging or satellite imagery) can be efficiently handled by Hadoop.  Special frameworks and techniques address the challenges of handling numerous small image files within HDFS.
* **Log processing:** Analyzing website logs, application logs, or security logs to identify trends, anomalies, or performance bottlenecks.
* **Text analysis:** Processing large text corpora for sentiment analysis, natural language processing, or information retrieval.
* **Recommendation systems:** Building recommendation engines based on vast amounts of user data.


## When to Avoid Hadoop

Hadoop may not be the best choice if:

* Your computations are intensive but involve minimal data.
* Your processing tasks cannot be easily parallelized.
* Your data is not self-contained or requires complex joins.
* You need interactive, real-time results.
* Low latency is required



## HDFS Architecture

* **NameNode:**  Manages the file system metadata, including the location of data blocks. It's a single point of failure in Hadoop 1.x but has been addressed with high-availability solutions in later versions.
* **DataNodes:** Store the actual data blocks. They are designed to be commodity hardware and are responsible for serving read/write requests from clients.
* **Secondary NameNode:**  Periodically merges the file system metadata from the NameNode's memory to disk, aiding in recovery and reducing the NameNode's workload.  It is *not* a backup NameNode.

## Hadoop Ecosystem

Hadoop's capabilities are extended by a rich ecosystem of related projects, including:

* **Pig:** A high-level data flow language and execution framework for simplifying MapReduce development.
* **Hive:** A data warehouse system built on top of Hadoop for providing SQL-like querying capabilities.
* **HBase:** A NoSQL database built on top of HDFS for providing random, real-time read/write access to data.


## Hadoop Versions

Hadoop has evolved over time, with major improvements in its architecture and functionality.  Hadoop 2.x introduced YARN, which significantly improved resource management and allowed for running various types of applications beyond MapReduce.


## Hadoop and Google Cloud

Google Cloud Platform (GCP) offers managed Hadoop services like Dataproc, which simplifies the deployment, management, and scaling of Hadoop clusters.  This allows users to leverage the power and flexibility of Hadoop without the complexities of managing the infrastructure.  Dataproc integrates with other GCP services, providing a comprehensive platform for Big Data processing.

## Hadoop vs Other File System
HDFS is markedly different from traditional file systems like Ext4, NTFS, or even distributed file systems like GlusterFS and Ceph. Here's a comparison across several key aspects:

**1. Data Storage and Processing:**

* **HDFS:** Designed for storing and processing *large* files (gigabytes to terabytes). Data is broken into blocks and distributed across multiple DataNodes, enabling parallel processing using frameworks like MapReduce and Spark. Optimized for write-once, read-many workloads.  Not ideal for storing numerous small files.
* **Traditional File Systems (e.g., Ext4, NTFS):** Optimized for storing and accessing a mix of small and large files on a single machine. Not designed for distributed data storage or processing.
* **Other Distributed File Systems (e.g., GlusterFS, Ceph):** Can handle both small and large files distributed across multiple servers. Offer various data access protocols and can be used for different workloads, including high-performance computing, cloud storage, and content delivery. Can support random read/write access more efficiently than HDFS.

**2. Scalability:**

* **HDFS:** Highly scalable. Can be easily expanded by adding more DataNodes to the cluster. Designed to handle petabytes of data.
* **Traditional File Systems:** Limited scalability, constrained by the capacity of a single machine.
* **Other Distributed File Systems:** Scalable but may have different scaling characteristics depending on the specific file system's architecture.

**3. Fault Tolerance:**

* **HDFS:** Highly fault-tolerant. Data is replicated across multiple DataNodes. The NameNode manages the metadata and handles DataNode failures automatically.
* **Traditional File Systems:** Limited fault tolerance. Data loss is possible if the hard drive fails.
* **Other Distributed File Systems:** Fault-tolerant through data replication and other mechanisms, but their approaches may vary.

**4. Data Locality:**

* **HDFS:** Emphasizes data locality. Computation is moved to the data, minimizing network transfer overhead.
* **Traditional File Systems:** Data locality is not a primary concern.
* **Other Distributed File Systems:** May consider data locality but not to the same extent as HDFS.

**5. Data Access:**

* **HDFS:** Optimized for sequential read access of large files.  Random read/write or accessing small files is less efficient.
* **Traditional File Systems:** Efficient random and sequential access to both small and large files.
* **Other Distributed File Systems:**  Generally provide faster random read/write access capabilities compared to HDFS. Can offer different consistency guarantees and data access protocols (e.g., POSIX compliance).


**6. Cost:**

* **HDFS:** Cost-effective due to its ability to run on commodity hardware.
* **Traditional File Systems:** Can be cost-effective depending on the storage solution and hardware used.
* **Other Distributed File Systems:** Cost can vary depending on the specific file system, hardware requirements, and licensing (if applicable).


**7. Use Cases:**

* **HDFS:** Batch processing, data warehousing, log analysis, machine learning on large datasets.
* **Traditional File Systems:** General-purpose file storage on a single machine.
* **Other Distributed File Systems:**  A wider range of use cases, including high-performance computing, cloud storage, content delivery, and shared file storage.


**8. Complexity:**

* **HDFS:** Managing a Hadoop cluster can be complex, requiring specialized expertise. However, cloud-managed services simplify this significantly.
* **Traditional File Systems:** Relatively simple to manage.
* **Other Distributed File Systems:** Complexity varies depending on the specific system.



**Summary Table:**

| Feature                 | HDFS                                          | Traditional File Systems     | Other Distributed File Systems |
| ----------------------- | --------------------------------------------- | ---------------------------- | ------------------------------ |
| Data Storage/Processing | Large files, distributed, parallel processing | Mix of files, single machine | Mix of files, distributed      |
| Scalability             | Very High                                     | Limited                      | High (varies)                  |
| Fault Tolerance         | High                                          | Limited                      | High (varies)                  |
| Data Locality           | High                                          | Not a primary concern        | Moderate                       |
| Data Access             | Sequential read optimized                     | Random/Sequential            | Random/Sequential              |
| Cost                    | Low                                           | Moderate                     | Varies                         |
| Use Cases               | Batch processing, Big Data                    | General purpose              | Varies (HPC, cloud, etc.)      |
| Complexity              | High (managed services simplify)              | Low                          | Varies                         |


## Additional Notes
https://eecs.csuohio.edu/~sschung/cis612/CIS612_LectureNotes_Intro_HDFS.pdf


## Hadoop Commands
**Hadoop Distributed File System (HDFS) Commands**

HDFS commands are used to interact with the Hadoop Distributed File System.  They generally follow the pattern: `hadoop fs -command [options] /path`.

**1. File and Directory Management:**
* **`ls -ls /path/to/directory`**: Lists the contents of a directory, including detailed information like permissions, size, and modification time.  `ls /path/to/directory` provides a simpler listing.
* **`mkdir -p /path/to/new_directory`**: Creates a new directory.  The `-p` option creates parent directories as needed.
* **`rm -r /path/to/directory`**: Removes a file or directory. The `-r` option is crucial for deleting directories recursively.  Use `-f` (force) to skip confirmation prompts, especially when using wildcards. Be extremely cautious with `rm -rf`, as it deletes recursively and forcefully.
* **`rmdir /path/to/empty_directory`**: Removes an *empty* directory.
* **`mv /source/path /destination/path`**: Moves or renames files and directories.
* **`cp /source/path /destination/path`**: Copies files within HDFS.

**2. Data Transfer between Local and HDFS:**
* **`put /local/path /hdfs/path`**: Uploads files from the local filesystem to HDFS.  Can accept multiple local paths.
* **`get /hdfs/path /local/path`**: Downloads files from HDFS to the local filesystem.  Can download multiple files and merge them into a local directory.
* **`copyFromLocal /local/path /hdfs/path`**: Similar to `put`.
* **`copyToLocal /hdfs/path /local/path`**: Similar to `get`.

**3. Viewing File Contents:**
* **`cat /hdfs/path/to/file`**: Displays the entire file contents.
* **`tail [-f] /hdfs/path/to/file`**: Displays the last part of a file.  The `-f` option allows following the file as it grows (similar to `tail -f` on Linux).
* **`head /hdfs/path/to/file`**: Displays the first part of a file (default is 10 lines).

**4. File System Checks and Disk Usage:**
* **`fsck /path`**: Checks the consistency of the HDFS filesystem.  Useful for identifying and resolving issues.
* **`du -h /hdfs/path`**: Displays disk usage statistics.  The `-h` option provides human-readable sizes (e.g., KB, MB, GB).  `-s` gives a summary for the specified path.

**5. Permissions and Ownership:**
* **`chown user:group /hdfs/path`**: Changes ownership.
* **`chmod permissions /hdfs/path`**: Changes permissions (e.g., `755`).  Use octal representation.
* **`chgrp group /hdfs/path`**: Changes group association.

**6. Other Important Commands:**
* **`hdfs dfs -help [command]`**: Displays help for HDFS commands.  Providing a specific command shows detailed usage information for that command.
* **`stat /hdfs/path`**: Displays status information (permissions, size, modification time, etc.).
* **`test -e /hdfs/path`**:  Checks if a file or directory exists. Returns 0 for true, 1 for false.
* **`touchz /hdfs/path/to/file`**: Creates an empty file.

**Key Considerations:**
* **`hdfs dfs` vs. `hadoop fs`**: While both prefixes often work interchangeably, `hdfs dfs` is more specific to HDFS operations and is recommended for clarity.
* **Wildcards**:  HDFS commands support wildcards like `*` and `?`.
* **Paths**:  Paths can be absolute (starting with `/`) or relative to the current HDFS directory.



## HDFS commands

**Basic File Operations:**

* **`hdfs dfs -ls <path>`:** Lists the contents of a directory.  Add `-R` for recursive listing.
* **`hdfs dfs -cat <file>`:** Displays the contents of a file.
* **`hdfs dfs -get <hdfs_path> <local_path>`:** Copies a file or directory from HDFS to the local filesystem.  `-crc` verifies checksum.
* **`hdfs dfs -put <local_path> <hdfs_path>`:** Copies a file or directory from the local filesystem to HDFS.
* **`hdfs dfs -cp <hdfs_src_path> <hdfs_dest_path>`:** Copies files within HDFS.
* **`hdfs dfs -mv <hdfs_src_path> <hdfs_dest_path>`:** Moves files within HDFS.  Can also be used to rename files.
* **`hdfs dfs -rm <path>`:** Deletes a file.  `-r` for recursive deletion of directories.  `-f` to force deletion without confirmation. `-skipTrash` bypasses trash.  Use with extreme caution!
* **`hdfs dfs -mkdir <path>`:** Creates a directory.  `-p` creates parent directories as needed.
* **`hdfs dfs -touchz <file>`:** Creates an empty file.
* **`hdfs dfs -stat <path>`:** Displays various file statistics (size, modification time, etc.).
* **`hdfs dfs -test -[ezd] <path>`:** Checks file existence (-e), if empty (-z), or if a directory (-d).
* **`hdfs dfs -du [-s] [-h] <path>`:** Displays disk usage.  `-s` summarizes recursively, `-h` shows human-readable sizes.
* **`hdfs dfs -count [-q] <path>`:** Counts files, directories, and bytes.  `-q` only outputs counts.
* **`hdfs dfs -chmod [-R] <MODE> <path>`:** Changes file permissions.  `-R` for recursive change.
* **`hdfs dfs -chown [-R] <OWNER>:<GROUP> <path>`:** Changes file ownership.  `-R` for recursive change.
* **`hdfs dfs -chgrp [-R] <GROUP> <path>`:** Changes file group.  `-R` for recursive change.


**Advanced File Operations:**

* **`hdfs dfs -setrep [-R] [-w] <replication_factor> <path>`:** Sets the replication factor for a file or directory.  `-R` for recursive change.  `-w` waits for the replication to complete.
* **`hdfs dfs -appendToFile <local_src> <hdfs_dest>`:** Appends the contents of local files to an existing HDFS file.
* **`hdfs dfs -truncate <length> <path>`:** Truncates a file to the specified length.
* **`hdfs dfs -tail [-f] <file>`:** Displays the last kilobyte of the file (like the Unix `tail` command).  `-f` follows file growth.
* **`hdfs dfs -getmerge <hdfs_src> <local_dest>`:** Merges multiple HDFS files into a single local file.


**Filesystem Administration (requires appropriate permissions):**

* **`hdfs dfsadmin -report`:** Displays overall cluster health and statistics.
* **`hdfs dfsadmin -safemode [enter | leave | get | wait]`:** Manages Safe Mode.
* **`hdfs dfsadmin -refreshNodes`:** Refreshes the Namenode's view of the DataNodes.
* **`hdfs dfsadmin -setQuota <quota> <path>`:** Sets a storage quota on a directory.
* **`hdfs dfsadmin -clrQuota <path>`:** Clears the storage quota on a directory.
* **`hdfs dfsadmin -setSpaceQuota <quota> <path>`:** Sets a storage space quota on a directory (including replications).
* **`hdfs dfsadmin -clrSpaceQuota <path>`:** Clears the storage space quota on a directory.
* **`hdfs haadmin -getServiceState <service_id>`:** Checks the status of HDFS High Availability.  (If HA is configured)
* **`hdfs fsck <path> [-delete | -move | -openforwrite]`:** Checks for and potentially repairs inconsistencies in the filesystem.  Use with caution!

**Snapshotting:**

* **`hdfs dfs -createSnapshot <directory> <snapshotName>`:** Creates a snapshot of a directory.
* **`hdfs dfs -deleteSnapshot <directory> <snapshotName>`:** Deletes a snapshot.
* **`hdfs dfs -renameSnapshot <directory> <oldName> <newName>`:** Renames a snapshot.

## Hive: A Deep Dive into Hadoop's Data Warehouse

Apache Hive is a data warehouse system built on top of Apache Hadoop for querying and managing large datasets stored in HDFS (Hadoop Distributed File System) or other compatible storage systems. It provides an SQL-like interface (HiveQL) that allows users familiar with SQL to interact with data stored in Hadoop without needing to write complex MapReduce jobs.  Hive translates HiveQL queries into MapReduce, Tez, or Spark jobs, enabling parallel processing and efficient analysis of massive datasets.

**Key Features and Components:**
* **HiveQL:**  The SQL-like query language used to query, manipulate, and manage data. It supports many SQL features, including DDL (Data Definition Language) for creating tables, DML (Data Manipulation Language) for inserting and querying data, and UDFs (User-Defined Functions) for extending functionality.
* **Hive Metastore:** Stores metadata about Hive tables, such as schema, location, and partitioning information. This metadata is crucial for Hive's operation and can be stored in various databases (e.g., Derby, MySQL).
* **Driver:**  Receives HiveQL queries from the client, parses them, and creates execution plans.
* **Compiler:** Translates HiveQL queries into MapReduce, Tez, or Spark jobs.
* **Optimizer:** Optimizes the execution plan to improve query performance.
* **Executor:** Executes the generated MapReduce, Tez, or Spark jobs.
* **CLI, JDBC/ODBC, Web UI:** Different interfaces for interacting with Hive.


**How Hive Works:**
1. **Query Submission:** A user submits a HiveQL query through one of the available interfaces (CLI, JDBC/ODBC, Web UI).
2. **Query Parsing and Compilation:** The Hive driver receives the query, parses it, and creates an execution plan. The compiler then translates the query into a series of MapReduce, Tez, or Spark jobs.
3. **Job Execution:** The generated jobs are submitted to the underlying processing framework (MapReduce, Tez, or Spark) for execution on the Hadoop cluster.
4. **Result Retrieval:** The results of the query are retrieved and presented to the user.


**Use Cases:**
* **Data Warehousing and ETL:** Hive excels at ETL (Extract, Transform, Load) processes, allowing users to transform and load large volumes of data into a structured format for analysis.
* **Ad-hoc Querying:**  Hive enables users to perform ad-hoc queries on large datasets to gain insights.
* **Batch Processing:** Hive is well-suited for batch processing large datasets, where real-time performance is not critical.
* **Data Analysis and Reporting:** Hive can be used to generate reports and analyze large datasets for business intelligence.
* **Data Preparation for Machine Learning:** Hive can be used to preprocess and prepare large datasets for use in machine learning algorithms.


**Advantages of Hive:**
* **SQL-like Interface:**  Makes it easy for users familiar with SQL to interact with Hadoop.
* **Scalability and Fault Tolerance:**  Leverages the scalability and fault tolerance of Hadoop.
* **Extensibility:** Supports UDFs for custom functionality.
* **Integration with Hadoop Ecosystem:**  Seamlessly integrates with other Hadoop components like HDFS, MapReduce, YARN, HBase.


**Limitations of Hive:**
* **Not Suitable for OLTP:**  Hive is not designed for online transaction processing (OLTP) workloads.
* **High Latency:**  Hive queries can have high latency, especially for complex queries. Not suitable for low-latency, interactive querying.
* **Limited Subquery Support:**  Hive has limited support for subqueries compared to traditional SQL databases.
* **No Real-time Querying:** Hive is designed for batch processing and does not support real-time queries.


**Hive Optimization Techniques:**
* **Partitioning:** Dividing tables into smaller partitions based on values in specific columns.
* **Bucketing:**  Further dividing partitions into buckets based on hash values of specified columns.
* **File Formats:** Using optimized file formats like ORC and Parquet for efficient storage and retrieval.
* **Compression:** Compressing data to reduce storage space and improve query performance.
* **Join Optimization:** Using appropriate join strategies to improve join performance.
* **Predicate Pushdown:** Pushing predicates down to the data source to reduce the amount of data processed.


**Hive vs. Other SQL-on-Hadoop Systems:**
Hive is often compared to other SQL-on-Hadoop systems like Presto, Impala, and Drill. Presto and Drill excel at low-latency, interactive queries and querying data from diverse sources. Impala provides faster query performance than Hive for some workloads but is more tightly coupled with HDFS.  Choosing the right tool depends on the specific requirements of the application.


**Hive and Cloud Environments:**
Cloud platforms like AWS (Amazon Web Services), Azure, and GCP (Google Cloud Platform) offer managed Hadoop and Hive services, simplifying deployment and management.  These services often integrate with other cloud offerings, providing a comprehensive Big Data platform.


## HBase: A Deep Dive into Hadoop's NoSQL Database

Apache HBase is a distributed, scalable, NoSQL database built on top of the Hadoop Distributed File System (HDFS). Inspired by Google's Bigtable, HBase provides random, real-time read/write access to data stored in HDFS. It's designed to handle large amounts of sparse data, making it an excellent choice for applications requiring low-latency access to individual rows within massive datasets.

**Key Features and Architecture:**

* **Data Model:** HBase uses a column-oriented data model. Data is stored in tables composed of rows and columns, where each column belongs to a column family.  Rows are identified by a unique row key, and columns within a family are grouped together. This model allows for efficient retrieval of specific data subsets and is especially suited for sparse datasets where not all columns have values for every row.
* **Scalability:** HBase is highly scalable. It can handle billions of rows and millions of columns by distributing data and processing across a cluster of machines.  New machines can be added to the cluster seamlessly to accommodate growing data volumes.
* **Fault Tolerance:**  HBase relies on HDFS for fault tolerance. Data is replicated across multiple DataNodes, ensuring data availability even if some nodes fail.
* **Consistency:**  HBase offers strong consistency guarantees within a row. All changes to a single row are atomic and immediately visible.
* **Random Read/Write Access:** HBase supports random read and write access to data using the row key. This makes it suitable for applications requiring low-latency data retrieval.
* **Integration with Hadoop Ecosystem:** HBase integrates seamlessly with other Hadoop ecosystem components, including HDFS, MapReduce, and YARN.
* **Regions:** Tables in HBase are split into regions, which are distributed and managed by RegionServers. The region boundaries are determined by row key ranges.


**HBase Architecture:**

* **Client:** The client communicates with the HBase cluster to read and write data.
* **ZooKeeper:** Coordinates and manages the HBase cluster, including RegionServer assignments and master election.
* **HMaster:** Manages the metadata about tables and regions. Assigns regions to RegionServers and monitors their health.
* **RegionServers:**  Store and manage regions of data. Handle read and write requests from clients.
* **HDFS:** The underlying distributed file system used to store HBase data.


**HBase vs. RDBMS:**

HBase differs significantly from traditional relational database management systems (RDBMS) like MySQL, PostgreSQL, and Oracle.

| Feature       | HBase                                | RDBMS                                    |
| ------------- | ------------------------------------ | ---------------------------------------- |
| Data Model    | Column-oriented                      | Row-oriented                             |
| Schema        | Flexible                             | Fixed                                    |
| Scalability   | High                                 | Limited                                  |
| Consistency   | Strong within a row                  | ACID properties                          |
| Relationships | No joins                             | Joins supported                          |
| Use Cases     | Large, sparse data, real-time access | Structured data, transactional workloads |


**Use Cases:**

* **Real-time analytics:** HBase's low-latency access makes it ideal for real-time dashboards and analytics.
* **Time series data:** Storing and analyzing time series data, such as sensor readings, stock prices, or web traffic.
* **Content stores:** Storing large amounts of unstructured data, such as web pages, documents, or images.
* **Recommendation engines:**  Storing user preferences and recommendations.
* **Internet of Things (IoT):**  Ingesting and processing large volumes of data from IoT devices.


**HBase Shell:**

HBase provides a command-line interface (shell) for interacting with the database.  It allows users to create tables, insert data, perform queries, and manage the HBase cluster.


**HBase API:**

HBase offers Java, REST, and Thrift APIs for application development. These APIs allow developers to interact with HBase programmatically.


**HBase Data Modeling:**

Effective data modeling is essential for optimal HBase performance. Key considerations include:

* **Row Key Design:**  Choosing an appropriate row key is critical for performance. Row keys should be unique, short, and sorted in a way that supports efficient data access.
* **Column Family Design:**  Column families should be designed to group related columns together.  The number of column families should be kept relatively small.
* **Data Types:**  HBase supports various data types, including strings, integers, booleans, and timestamps.


**HBase Performance Tuning:**
Several techniques can be used to optimize HBase performance:
* **Region Splitting and Compaction:**  Managing region sizes and compacting HFiles to improve read performance.
* **Caching:**  Caching frequently accessed data in memory.
* **Bloom Filters:**  Using Bloom filters to quickly check if a row exists, reducing read latency.
