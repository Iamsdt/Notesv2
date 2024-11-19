---
Created by: Shudipto Trafder
Created time: 2024-11-12T17:50:00
Last edited by: Shudipto Trafder
Last edited time: 2024-11-12T17:54:00
tags:
  - mongo
  - database
---
#### **1. Connecting to MongoDB**

**1.1 Local Connection**  
```bash
mongosh --version
```

**1.2 Remote Connection with Authentication**  
```bash
mongosh --host <host> --port <port> --authenticationDatabase admin -u <user> -p <pwd>
```

**1.3 MongoDB Atlas Connection**  
```bash
mongosh "mongodb+srv://cluster-name.abcde.mongodb.net/<dbname>" --apiVersion 1 --username <username>
```

---

#### **2. Database Operations**

**2.1 General Commands**  
```javascript
show dbs                // List databases
use <database_name>     // Switch to a database
db                      // Show current database
```

**2.2 Collection Commands**  
```javascript
show collections        // List collections in the database
db.coll.stats()         // Get collection statistics
```

**2.3 Script Execution**  
```javascript
load("myScript.js")     // Load and execute a script
```

---

#### **3. CRUD Operations**

**3.1 Create**  
```javascript
db.coll.insertOne({ name: "Alice" }) 
db.coll.insertMany([{ name: "Bob" }, { name: "Charlie" }]) 
```

**3.2 Read**  
```javascript
db.coll.findOne()                           // Retrieve the first document
db.coll.find({ name: "Alice" })             // Find by filter
db.coll.find().pretty()                     // Pretty print the result
```

**3.3 Update**  
```javascript
db.coll.updateOne({ name: "Bob" }, { $set: { age: 25 } }) 
db.coll.updateMany({}, { $inc: { age: 1 } }) // Increment age for all
```

**3.4 Delete**  
```javascript
db.coll.deleteOne({ name: "Charlie" }) 
db.coll.deleteMany({ age: { $lt: 20 } })
```

---

#### **4. Aggregations**

**4.1 Group and Sort**  
```javascript
db.comments.aggregate([
   { $group: { _id: "$movie_id", totalComments: { $count: {} } } },
   { $sort: { totalComments: -1 } }, 
   { $limit: 10 } // Top 10 movies by comments
]);
```

**4.2 Group with Average**  
```javascript
db.movies.aggregate([
   { $match: { "imdb.rating": { $exists: true } } },
   { $group: { 
      _id: "$year", 
      averageRating: { $avg: "$imdb.rating" },
      totalMovies: { $count: {} }
   }},
   { $sort: { averageRating: -1 } }
]);
```

**4.3 Lookup**  
```javascript
db.movies.aggregate([
   { $lookup: {
      from: "comments",
      localField: "_id",
      foreignField: "movie_id",
      as: "movieComments"
   }},
   { $project: { title: 1, movieComments: 1 } }
]);
```

---

#### **5. Indexing**

**5.1 Create Index**  
```javascript
db.coll.createIndex({ name: 1 })                 // Ascending index
db.coll.createIndex({ age: -1 }, { unique: true }) // Descending and unique
```

**5.2 Manage Indexes**  
```javascript
db.coll.getIndexes()                             // List indexes
db.coll.dropIndex("name_1")                      // Drop index
```

---

#### **6. Handy Commands**

```javascript
db.coll.countDocuments()                         // Count documents
db.currentOp()                                   // View ongoing operations
db.killOp(<opid>)                                // Terminate an operation
db.serverStatus()                                // Check server health and metrics
```

---

#### **7. Change Streams**

```javascript
watchCursor = db.coll.watch(); 
while (!watchCursor.isExhausted()) {
   if (watchCursor.hasNext()) {
      printjson(watchCursor.next());
   }
}
```

---

#### **8. Replica Sets**

```javascript
rs.status()                                       // Check replica set status
rs.initiate()                                     // Initiate replica set
rs.add("mongodb2.example.net:27017")             // Add a node to the replica set
rs.stepDown()                                     // Step down primary
```

---

#### **9. Sharded Clusters**

```javascript
sh.status()                                       // Check sharding status
sh.addShard("rs1/mongodb1.example.net:27017")     // Add a shard
sh.shardCollection("mydb.orders", { orderId: 1 })// Shard a collection
sh.moveChunk("mydb.orders", { orderId: 123 }, "shard002") // Move chunk
```

---

#### **10. Advanced Queries**

**10.1 Basic Field Search**  
```javascript
db.movies.find({ "imdb.rating": { $gt: 8 } });    // Find movies with IMDb > 8
db.users.find({ email: "example@email.com" });    // Find users by email
```

**10.2 Logical Operators**  
```javascript
db.sessions.find({
   $or: [
      { day: { $in: ["Saturday", "Sunday"] } },
      { availableSeats: { $gt: 50 } }
   ]
});
```

**10.3 Nested Field Search**  
```javascript
db.embedded_movies.find({ "director.name": "Christopher Nolan" }); 
```

**10.4 Regex Search**  
```javascript
db.movies.find({ title: { $regex: "star", $options: "i" } });
```

**10.5 Array Search**  
```javascript
db.movies.find({ genres: "Action" });
```

**10.6 Range Search**  
```javascript
db.movies.find({ year: { $gte: 2010, $lte: 2020 } });
```

**10.7 Projection**  
```javascript
db.movies.find(
   { "imdb.rating": { $gte: 8 } },
   { title: 1, "imdb.rating": 1, _id: 0 }
);
```

**10.8 Sorting and Pagination**  
```javascript
db.movies.find().sort({ "imdb.rating": -1 });     // Sort by rating (desc)
db.movies.find().skip((pageNumber - 1) * pageSize).limit(pageSize); // Pagination
```

**10.9 Text Search**  
```javascript
db.movies.createIndex({ title: "text", plot: "text" });
db.movies.find({ $text: { $search: "adventure thriller" } });
```

**10.10 Geospatial Search**  
```javascript
db.theaters.find({
   location: {
      $near: {
         $geometry: { type: "Point", coordinates: [-73.935242, 40.73061] },
         $maxDistance: 10000
      }
   }
});
```
Unit: Meter
Coordinates: Long, latiude

---

#### **11. Creating and Dropping**

**11.1 Create**  
```javascript
db.createCollection("products");
```

**11.2 Drop**  
```javascript
db.coll.drop(); 
db.dropDatabase(); // CAUTION! Irreversible
```

**11.3 Rename Collection**  
```javascript
db.coll.renameCollection("new_coll");
```

---

#### **12. Explain Plan & Query Optimization**

**Purpose of `explain()`:**  
The `explain()` function is a debugging and optimization tool that shows how MongoDB plans to execute a query. It provides insights into query performance and whether indexes are being utilized effectively.

#### **Syntax**
```javascript
db.collection.find(query).explain("executionStats")
```

#### **Key Output Fields**
- **queryPlanner:** Information about how MongoDB plans to execute the query.
  - `winningPlan`: The strategy chosen by MongoDB to execute the query.
  - `rejectedPlans`: Alternative plans that were considered but not chosen.
- **executionStats:**
  - `totalKeysExamined`: Number of index keys scanned.
  - `totalDocsExamined`: Number of documents scanned.
  - `executionTimeMillis`: Total time (in ms) to execute the query.

#### **Examples**
1. **Basic Query:**
```javascript
   db.movies.find({ "imdb.rating": { $gte: 8 } }).explain("executionStats");
```

2. **Query Without Index:**
   ```javascript
   db.movies.find({ title: "Inception" }).explain("executionStats");
   ```

3. **Query with Index:**
   ```javascript
   db.movies.createIndex({ title: 1 });
   db.movies.find({ title: "Inception" }).explain("executionStats");
   ```

**Optimization Tips:**
1. Create indexes for fields used in filters (`$match`, `find`) and sorts (`$sort`).
2. Use compound indexes for queries with multiple fields.
3. Avoid using `$regex` and `$where` in queries as they are slow and unindexed.
4. Use projection to limit the data returned and reduce the query load.

#### **13. Schema Design Tips**

MongoDB’s flexible schema design offers two main patterns:
- **Embedding** (store related data in the same document).
- **Referencing** (store references to related data in separate collections).

#### **When to Use Embedding**
1. Data is frequently accessed together.
2. One-to-few or one-to-one relationships.
3. The document size remains under MongoDB's 16MB limit.

#### **When to Use Referencing**
1. One-to-many relationships with frequent updates.
2. Data that is shared across multiple documents.
3. Large datasets that exceed document size limits.

#### **Best Practices**
1. **Design for the application’s query patterns**: Optimize schema to minimize joins and reduce query complexity.
2. **Avoid deeply nested documents**: Limit nesting to a reasonable depth (e.g., 3 levels).
3. **Pre-aggregate data for frequent queries**: Store computed fields in the document if recalculating is costly.
4. **Consider shard keys**: Ensure they provide even distribution for writes in a sharded cluster.
5. **Use meaningful field names**: Short but descriptive (e.g., `username`, not `usrnm`).
6. **Avoid large arrays**: Break down large arrays into subdocuments or use `$unwind` for querying.

#### **14. Advanced Aggregation**

Aggregation pipelines in MongoDB allow complex data processing in stages. Below are advanced techniques:  

##### **14.1. `$unwind`**  
Deconstructs an array into separate documents.
```javascript
db.movies.aggregate([
   { $unwind: "$genres" },
   { $group: { _id: "$genres", count: { $sum: 1 } } },
   { $sort: { count: -1 } }
]);
```

##### **14.2. `$facet`**  
Runs multiple pipelines in parallel and returns combined results.
```javascript
db.movies.aggregate([
   { $facet: {
       topRated: [{ $match: { "imdb.rating": { $gte: 9 } } }],
       byYear: [{ $group: { _id: "$year", count: { $sum: 1 } } }]
   }}
]);
```

##### **14.3. `$merge`**  
Writes the output of an aggregation back to a collection.
```javascript
db.movies.aggregate([
   { $group: { _id: "$year", totalMovies: { $sum: 1 } } },
   { $merge: "yearlyStats" } // Save results to "yearlyStats" collection
]);
```

#### **15. Joins (Using `$lookup`)**
MongoDB does not support traditional joins but provides `$lookup` for joining collections. Below are practical examples using the **movies database** from Atlas:

##### **15.1. Join Movies with Comments**
```javascript
db.movies.aggregate([
   { $lookup: {
       from: "comments",
       localField: "_id",
       foreignField: "movie_id",
       as: "movieComments"
   }},
   { $project: { title: 1, movieComments: 1 } }
]);
```

##### **15.2. Join Movies with Theaters Showing Them**
```javascript
db.movies.aggregate([
   { $lookup: {
       from: "theaters",
       localField: "_id",
       foreignField: "movie_id",
       as: "showingIn"
   }},
   { $project: { title: 1, showingIn: 1 } }
]);
```

##### **15.3. Join Movies with Users Who Rated Them**
```javascript
db.movies.aggregate([
   { $lookup: {
       from: "users",
       localField: "_id",
       foreignField: "ratedMovies.movieId",
       as: "userRatings"
   }},
   { $project: { title: 1, userRatings: 1 } }
]);
```

##### **15.4. Nested Joins**
Join multiple collections in a pipeline:
```javascript
db.movies.aggregate([
   { $lookup: {
       from: "comments",
       localField: "_id",
       foreignField: "movie_id",
       as: "movieComments"
   }},
   { $lookup: {
       from: "users",
       localField: "movieComments.user_id",
       foreignField: "_id",
       as: "commentUsers"
   }},
   { $project: { title: 1, commentUsers: 1, movieComments:1 } }
]);
```

---


#### **Reference**  
For more details, visit the [MongoDB Documentation](https://www.mongodb.com/docs/)