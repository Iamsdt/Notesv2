---
Author: Hans-Jürgen Schönig
Status: In progress
Type: Book
tag: pgsql
---
  

# CH1: PostgreSQL 15 Overview

### Removing support for old pg_dump

One of the first things that is worth noting is that support for ancient databases has been removed  
from pg_dump. PostgreSQL databases that are older than PostgreSQL 9.2 are not supported anymore  

  

### Fixing the public schema

Up to PostgreSQL 14, the public schema that exists in every database has been available to every  
user. This has caused various security concerns among the user base. Basically, it is easy to just use  
the following:  

```Shell
REVOKE ALL ON SCHEMA public FROM public;
```

This was rarely done but caused security leaks that people were generally not aware of. With the introduction  
of PostgreSQL, the situation has changed. The public schema is, from now on, not available to the  
general public and you have to be granted permission to use it like before. The new behaviour will make  
applications safer and ensure that permissions are not there accidentally.  

  

### Tip

```Shell
Tip
Keep in mind that the now() function will return the transaction time. The SELECT statement
will, therefore, always return two identical timestamps. If you want the real time, consider using
clock_timestamp() instead of now().
```

# CH2: Understanding Transactionsand Locking

## Postgres locking

As you can see, PostgreSQL offers eight types of locks to lock an entire table. In PostgreSQL, a lock can  
be as light as an ACCESS SHARE lock or as heavy as an ACCESS EXCLUSIVE lock. The following  
list shows what these locks do:  

- **ACCESS SHARE**: This type of lock is taken by reads and conflicts only with ACCESS EXCLUSIVE, which is set by DROP TABLE and so on. Practically, this means that SELECT cannot start if a table is about to be dropped. This also implies that DROP TABLE has to wait until a reading transaction is complete.
- **ROW SHARE**: PostgreSQL takes this kind of lock in the case of SELECT FOR UPDATE/ SELECT FOR SHARE. It conflicts with EXCLUSIVE and ACCESS EXCLUSIVE.
- **ROW EXCLUSIVE**: This lock is taken by INSERT, UPDATE, and DELETE. It conflicts with SHARE, SHARE ROW EXCLUSIVE, EXCLUSIVE, and ACCESS EXCLUSIVE.
- **SHARE UPDATE EXCLUSIVE**: This kind of lock is taken by CREATE INDEX CONCURRENTLY,  
    ANALYZE, ALTER TABLE, VALIDATE, and some other flavours of ALTER TABLE, as well  
    as by VACUUM (not VACUUM FULL). It conflicts with the SHARE UPDATE EXCLUSIVE,  
    SHARE, SHARE ROW EXCLUSIVE, EXCLUSIVE, and ACCESS EXCLUSIVE lock modes.  
    
- **SHARE**: When an index is created, SHARE locks will be set. It conflicts with ROW EXCLUSIVE, SHARE UPDATE EXCLUSIVE, SHARE ROW EXCLUSIVE, EXCLUSIVE, and ACCESS EXCLUSIVE.
- **SHARE ROW EXCLUSIVE**: This one is set by CREATE TRIGGER and some forms of ALTER TABLE and conflicts with everything except ACCESS SHARE.
- **EXCLUSIVE**: This type of lock is by far the most restrictive one. It protects against reads and writes alike. If this lock is taken by a transaction, nobody else can read or write to the table  
    that’s been affected.  
    
- **ACCESS EXCLUSIVE**: This lock prevents concurrent transactions from reading and writing

  

# CH3: Making Use of Indexes

```Shell
CREATE TABLE t_test (id serial, name text);
INSERT INTO t_test (name) SELECT 'hans' FROM generate_series(1, 2000000);
```

In PostgreSQL, a SQL statement will be executed  
in four stages. The following components are at work:  
• The  
**parser** will check for syntax errors and obvious problems  
• The  
**rewrite** system takes care of rules (views and other things)  
• The  
**optimizer** will figure out how to execute a query most efficiently and work out a plan  
• The  
**plan** provided by the optimizer will be used by the executor to finally create the result

  

PostgreSQL uses **Lehman-Yao’s** high-concurrency B-tree for standard indexes ([https://www](https://www/).[csd.uoc.gr/~hy460/pdf/p650-lehman.pdf](http://csd.uoc.gr/~hy460/pdf/p650-lehman.pdf)). Along with some PostgreSQL-specific  
optimizations, these trees provide end users with excellent performance. The most important thing  
is that Lehman-Yao allows you to run many operations (reading and writing) on the very same index  
at the same time, which helps to improve throughput dramatically  

  

However, indexes are not free:

```Shell

test=# \x
Expanded display is on.
test=# \di+ idx_id
```

In other words, if you use INSERT on a table that has 20 indexes, you also have to keep in mind that you have to write to all those indexes on INSERT, which seriously slows down the process.  
With the introduction of version 11, PostgreSQL now supports parallel index creation. It is possible to utilize more than one CPU core to build an index, thereby speeding up the process considerably.  
For now, this is only possible if you want to build a normal B-tree—there is no support for other index types yet. However, this will most likely change in the future. The parameter to control the level of parallelism is max_parallel_maintenance_workers. This tells PostgreSQL how many  
processes it can use as an upper limit.  

### **Making use of sorted output**

**B-tree** indexes are not just used to find rows; they are also used to feed sorted data to the next stage in a process

  

### Using more than one index at a time

```Shell
explain SELECT * FROM t_test WHERE id = 30 OR id = 50;

A bitmap scan is not the same as a bitmap index, which people who have a good Oracle
background might know. They are two distinct things and have nothing in common. Bitmap
indexes are an index type in Oracle while bitmap scans are a scan method.
```

The idea behind a bitmap scan is that PostgreSQL will scan the first index, collecting a list of blocks (pages of a table) containing the data. Then, the next index will be scanned to—again—compile a list of blocks. This is done for as many indexes as desired. In the case of OR, these lists will then be unified,  
leaving us with a long list of blocks containing the data. Using this list, the table will be scanned to retrieve these blocks.  

In general, OR can be a pretty expensive operation. If you have the feeling that a query containing OR is too expensive, consider trying out UNION to see whether it runs faster. In many cases, this can produce a relevant performance boost.

### Clustering tables

In PostgreSQL, a command called CLUSTER allows us to rewrite a table in the desired order. It is possible to point to an index and store data in the same order as the index:

```Shell
CLUSTER t_random USING idx_random;
```

### Adding data while indexing

Creating an index is easy. However, keep in mind that you cannot modify a table while an index is being built. The CREATE INDEX command will lock the table using a SHARE lock to ensure that no changes happen. While this is clearly no problem for small tables, it will cause issues for large ones in  
production systems. Indexing 1 TB of data or so will take some time, and therefore blocking a table for too long can become an issue. The solution to this problem is the CREATE INDEX CONCURRENTLY command. Building the index will take a lot longer (usually, at least twice as long), but you can use the table normally during index creation. Here’s how it works:  

```Shell
CREATE INDEX CONCURRENTLY idx_name2 ON t_test (name);
```

Note that PostgreSQL doesn’t guarantee success if you are using the CREATE INDEX CONCURRENTLY command. An index can end up being marked as invalid if the operations running on your system somehow conflict with the creation of the index. If you want to figure out whether your indexes are invalid, use \d on the relation.

### Understanding PostgreSQL index types

B-trees are basically based on sorting. The <, <=, =, >=, and > operators can be handled using B-trees. The trouble is that not every data type can be sorted in a useful way. Just imagine a polygon. How would you sort these objects in a useful way? Sure, you can sort by the area covered, its length, and so on, but doing this won’t allow you to find them using a geometric search.

```Shell
SELECT * FROM pg_am;
```

### Hash indexes

Hash indexes have been around for many years. While B-trees are basically sorted lists, hash indexes store the hash of the value we want to index. A hash index is basically a large hash map stored on disk. The idea is to hash the input value and store it for later lookups. Having hash indexes makes sense. However, before PostgreSQL 10.0, it was not advisable to use hash indexes because PostgreSQL had no WAL support for them. In PostgreSQL 10.0, this has changed. Hash indexes are now fully logged and are therefore ready for replication and considered to be 100% crash-safe. Hash indexes are generally a bit larger than B-tree indexes. Suppose you want to index 4 million integer values. A B-tree will need around 90 MB of storage to do this. A hash index will need around 125 MB on disk. The assumption that’s made by many people is that a hash is super small on disk and in many cases, that assumption is wrong.

### GiST indexes

Generalized Search Tree (GiST) indexes are a highly important index type because they are used for a variety of different things. GiST indexes can be used to implement R-tree behavior, and it is even possible for them to act as B-trees. However, abusing GiST for B-tree indexes is not recommended.  
Typical use cases for GiST are as follows:  
• Range types  
• Geometric indexes (for example, ones that are used by the highly popular PostGIS extension)  
• Fuzzy searching  

  

### Speeding up LIKE queries

LIKE queries definitely cause some of the worst performance problems faced by users around the globe these days. In most database systems, LIKE is pretty slow and requires a sequential scan. In addition to this, end users quickly figure out that a fuzzy search will, in many cases, return better results than precise queries. A single type of a LIKE query on a large table can, therefore, often diminish the performance of an entire database server if it is called often enough. Fortunately, PostgreSQL offers a solution to this problem, and the solution happens to be installed already:

```Shell
explain SELECT * FROM t_location WHERE name LIKE
'%neusi%';
```