---
Created by: Shudipto Trafder
Created time: 2023-10-18T21:53
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:11
tags:
  - Graph
---
# Neo4j Database Backup and Restoration Guide

## Introduction

This guide provides detailed instructions on how to back up and restore a Neo4j database using Docker containers. Neo4j database backups are crucial for data integrity and disaster recovery. By following these steps, you can create backups of your Neo4j database and restore them in case of data loss or system failures.

## Neo4j Database Backup

To back up a Neo4j database, follow these steps:

### Step 1: Stop Neo4j Database Server

Before taking any backup, stop the Neo4j database server. If you are using the Neo4j community version, use the following command:

```Shell
docker stop neo4j-container-name
```

Replace `neo4j-container-name` with the actual name of your Neo4j Docker container.

### Step 2: Create a Database Backup

Use the following command to create a backup of the Neo4j database:

```Shell
docker run --interactive --tty --rm \\
   --volume=$HOME/django-backend/recruit/neo4j/data:/data \\
   --volume=$HOME/django-backend/recruit/neo4j/backups:/backups \\
   neo4j/neo4j-admin:5.11.0 \\
   neo4j-admin database dump neo4j --to-path=/backups
```

This command exports the Neo4j database to the specified backup directory.

## Neo4j Database Restoration

To restore a Neo4j database from a backup, follow these steps:

### Step 1: Stop Neo4j Database Server

Stop the Neo4j database server on the target system using the same command as in Step 1 of the backup process.

### Step 2: Restore the Database

Copy the backup files to the target system, then use the following command to restore the Neo4j database:

```Shell
docker run --interactive --tty --rm \\
   --volume=/var/lib/docker/volumes/database_neo4j_data/_data:/data \\
   --volume=$HOME/backups:/backups \\
   neo4j/neo4j-admin:5.8.0 \\
   neo4j-admin database load neo4j --from-path=/backups --overwrite-destination=true
```

This command loads the Neo4j database from the specified backup directory. Ensure that you have copied the backup files to the correct location (`/backups` in this case).

### Step 3: Start Neo4j Database Server

After the restoration is complete, start the Neo4j database server on the target system:

```Shell
docker start neo4j-container-name
```

Replace `neo4j-container-name` with the actual name of your Neo4j Docker container.

## Conclusion

Regularly back up your Neo4j databases to ensure data integrity and facilitate seamless disaster recovery. By following this guide, you can create backups of your Neo4j database and restore them whenever needed. Always stop the Neo4j database server before performing backup or restoration operations to prevent data inconsistencies.