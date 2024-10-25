
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

**Wrap Up**

This cheat sheet offers a quick reference for common MongoDB operations. Refer to the official documentation for in-depth knowledge and advanced features: [https://www.mongodb.com/docs/](https://www.mongodb.com/docs/) 
