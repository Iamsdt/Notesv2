---
Created by: Shudipto Trafder
Created time: 2024-11-12T17:50:00
Last edited by: Shudipto Trafder
Last edited time: 2024-11-12T17:54:00
tags:
  - mongo
  - database
---
**1. Connect via MongoDB Shell**

```bash
# Local
mongosh

# Remote with Authentication
mongosh --host <host> --port <port> --authenticationDatabase admin -u <user> -p <pwd>

# MongoDB Atlas
mongosh "mongodb+srv://cluster-name.abcde.mongodb.net/<dbname>" --apiVersion 1 --username <username> 
```

**2. Helpers**

```javascript
// Database Operations
show dbs
use <database_name>
db // current database

// Collection Operations
show collections
db.coll.stats() // collection stats

// Script Execution
load("myScript.js")
```

**3. CRUD Operations**

```javascript
// Create
db.coll.insertOne({name: "Alice"}) 
db.coll.insertMany([{name: "Bob"}, {name:"Charlie"}]) 

// Read
db.coll.findOne() // first document
db.coll.find({name: "Alice"}) 
db.coll.find().pretty() // formatted output

// Update
db.coll.updateOne({name: "Bob"}, {$set: {age: 25}}) 
db.coll.updateMany({}, {$inc: {age: 1}}) // increment age

// Delete
db.coll.deleteOne({name: "Charlie"}) 
db.coll.deleteMany({age: {$lt: 20}})
```


Aggregation

```
db.comments.aggregate([
   { $group: { _id: "$movie_id", totalComments: { $count: {} } } },
   { $sort: { totalComments: -1 } }, // Sort by the number of comments
   { $limit: 10 } // Top 10 movies by comments
]);
```

```
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


Lookup
```
db.movies.aggregate([
   { $lookup: {
      from: "comments",
      localField: "_id",
      foreignField: "movie_id",
      as: "movieComments"
   }},
   { $project: { title: 1, movieComments: 1 } } // Display title and comments
]);

```


**4. Databases & Collections**

```javascript
// Create
db.createCollection("products")

// Drop
db.coll.drop()
db.dropDatabase() // CAUTION! Irreversible

// Other
db.coll.renameCollection("new_coll") 
```

**5. Indexes**

```javascript
// Create
db.coll.createIndex({name: 1}) // ascending
db.coll.createIndex({age: -1}, {unique: true}) // descending & unique

// List & Drop
db.coll.getIndexes()
db.coll.dropIndex("name_1")
```

**6. Handy Commands**

```javascript
db.coll.countDocuments()
db.currentOp() // view ongoing operations
db.killOp(<opid>) // terminate operation
db.serverStatus() // server health & metrics
```

**7. Change Streams**

```javascript
watchCursor = db.coll.watch() // track changes
while (!watchCursor.isExhausted()) {
   if (watchCursor.hasNext()) {
      printjson(watchCursor.next()) 
   }
}
```

**8. Replica Set**

```javascript
rs.status()
rs.initiate() // initiate replica set
rs.add("mongodb2.example.net:27017") 
rs.stepDown() // force primary step down
```

**9. Sharded Cluster**

```javascript
sh.status()
sh.addShard("rs1/mongodb1.example.net:27017")
sh.shardCollection("mydb.orders", {orderId: 1})
sh.moveChunk("mydb.orders", {orderId: 123}, "shard002")
```


Text Search
```
db.movies.createIndex({ title: "text", plot: "text" });
db.movies.find({ $text: { $search: "adventure thriller" } });
```

**Wrap Up**

This cheat sheet offers a quick reference for common MongoDB operations. Refer to the official documentation for in-depth knowledge and advanced features: [https://www.mongodb.com/docs/](https://www.mongodb.com/docs/) 
