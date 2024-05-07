---
Created by: Shudipto Trafder
Created time: 2023-10-18T21:54
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:13
tags:
  - pgsql
  - Docker
---
# PostgreSQL Database Backup, Restoration, and Transfer Guide

## Introduction

This comprehensive guide provides detailed instructions on how to back up, restore, and transfer a PostgreSQL database between Docker containers and different virtual machines. Proper database backups are essential for data integrity, disaster recovery, and seamless migration between environments.

## Database Backup

To back up a PostgreSQL database, follow these steps:

### Step 1: Connect to the Database Container

First, connect to the PostgreSQL database container using the following command:

```Shell
docker exec -it database /bin/bash
```

### Step 2: Create a Backup File

Inside the database container, use the `pg_dump` command to create a backup of the PostgreSQL database. For example, to back up a database named `hire10xdb` with the `postgres` user:

```Shell
/usr/bin/pg_dump -U postgres hire10xdb > data25.sql
```

This command exports the database to a file named `data25.sql` in the current directory inside the container.

### Step 3: Copy the Backup File to Host Machine

Exit the container and copy the backup file from the container to your host machine:

```Shell
docker cp database:/path/to/data25.sql /path/on/host/machine/
```

The backup file is now available on your host machine for safekeeping.

## Database Restoration

To restore a PostgreSQL database from a backup, follow these steps:

### Step 1: Copy the Backup File to the Database Container

Copy the backup file from your host machine to the PostgreSQL database container:

```Shell
docker cp /path/to/data25.sql database:/path/in/container/
```

### Step 2: Restore the Database

Connect to the database container:

```Shell
docker exec -it database /bin/bash
```

Inside the container, use the `psql` command to restore the database from the backup file:

```Shell
psql -U postgres -d hire10xdb < /path/in/container/data25.sql
```

This command restores the `hire10xdb` database using the `data25.sql` backup file.

### Step 3: Verify the Restoration

Exit the container and verify that the database has been successfully restored by connecting to the database and querying data:

```Shell
docker exec -it database /bin/bash
psql -U postgres -d hire10xdb
```

## Database Transfer between VMs using SCP

To transfer the PostgreSQL database from one virtual machine to another using Secure Copy Protocol (SCP), follow these steps:

### Step 1: Move Database Backup to New VM

Move the `data25.sql` backup file from the source VM to the destination VM using SCP:

```Shell
scp /path/to/data25.sql shudipto@34.122.236.253:~/data25.sql
```

Replace `/path/to/data25.sql` with the actual path of the backup file on your source VM.

### Step 2: Restore Database on Destination VM

Connect to the destination VM using SSH and copy the backup file to the PostgreSQL database container:

```Shell
scp shudipto@34.122.236.253:~/data25.sql ~/
docker cp ~/data25.sql database:/path/in/container/
```

Connect to the PostgreSQL database container on the destination VM:

```Shell
docker exec -it database /bin/bash
```

Inside the container, restore the database from the backup file:

```Shell
psql -U postgres -d hire10xdb < /path/in/container/data25.sql
```

Verify the restoration by connecting to the database and querying data.

## Conclusion

This guide provides a comprehensive approach to PostgreSQL database backup, restoration, and transfer. Regularly back up your databases, securely store backup files, and test the restoration process to ensure data integrity. Additionally, use SCP for secure database transfers between virtual machines, making sure to maintain the security and confidentiality of your data during the migration process.