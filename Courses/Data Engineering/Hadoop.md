The Hadoop Distributed File System (HDFS) is a distributed file system designed for storing and processing large datasets on commodity hardware.  Unlike traditional file systems, HDFS prioritizes throughput over low-latency access and assumes hardware failure as the norm.  This design allows for cost-effective scaling and robust operation.

HDFS operates on two key server types:

* **NameNode:** A single master node managing the file system metadata (directory structure, file locations, etc.).  It acts as a central point of coordination, instructing clients where to find data blocks. While a single NameNode simplifies architecture, it presents a single point of failure, mitigated in later Hadoop versions (2.0 and beyond) through active/passive high-availability configurations using shared storage.
* **DataNodes:** Multiple worker nodes storing the actual data blocks.  They report their stored blocks to the NameNode and serve data directly to clients.

Key features and characteristics of HDFS include:

* **Focus on Large Files and Streaming Access:** Optimized for batch processing of large datasets, HDFS prioritizes high throughput streaming access over random access.
* **Write-Once-Read-Many (WORM):** Assumes data is written once and read multiple times, simplifying data consistency and optimizing for read performance.
* **Data Replication:**  Ensures fault tolerance by replicating data blocks across multiple DataNodes.  The default replication policy prioritizes placing replicas within the same rack for performance while ensuring redundancy across different racks for resilience.
* **Hierarchical File System:**  Uses a familiar directory structure, but currently lacks support for hard or soft links.
* **Metadata Management:** The NameNode stores metadata in memory and persists changes to a transaction log (EditLog).  Periodically, this log is merged with the file system image (FsImage) to create a checkpoint, ensuring recoverability in case of failure.
* **Data Integrity:**  Checksums are calculated for data blocks and stored separately to ensure data integrity during reads.
* **Robustness:** Designed to handle various failure scenarios, including DataNode failures, network partitions, and NameNode failures. DataNode failures are handled through replication and heartbeat mechanisms.  NameNode failure is mitigated through redundant storage of EditLog and FsImage files.

While the single NameNode architecture presents a potential bottleneck and single point of failure, later Hadoop versions address this through high-availability configurations.  HDFS’s focus on fault tolerance, high throughput, and simplified data model makes it well-suited for large-scale data processing applications.
