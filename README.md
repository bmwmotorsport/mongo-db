# 📘 MongoDB Shell Commands

[![MongoDB](https://img.shields.io/badge/MongoDB-%5E6.0-green?logo=mongodb)](https://www.mongodb.com/)
[![Shell](https://img.shields.io/badge/Shell-mongosh-blue?logo=gnubash)](https://www.mongodb.com/docs/mongodb-shell/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> MongoDB Shell commands with short notes for database, collection, document operations and queries.

---

## 🧾 Commands with Notes

```shell
mongosh // Start MongoDB shell
show dbs // List all databases
use domain // Switch to or create 'domain' database
db.createCollection("Student1") // Create collection named 'Student1'
db.renameCollection("Student1","Student3") // Rename 'Student1' to 'Student3'
db.Student1.insertOne({name:"Romil",age:19}) // Insert one document into 'Student1' (will fail if renamed)

test> db.Student1.insertMany({name:"ABC",age:10},{name:"XYZ",age:20},{name:"PQR",age:30})
// ❌ Invalid: insertMany expects an array of documents

test> db.Student1.insertMany([{name:"ABC",age:10},{name:"XYZ",age:20},{name:"PQR",age:30}])
// ✅ Correct way to insert multiple documents

{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId("682e59ef2910b6a324511a98"),
    '1': ObjectId("682e59ef2910b6a324511a99"),
    '2': ObjectId("682e59ef2910b6a324511a9a")
  }
}

test> db.Student1.updateOne({name:"Romil",Age:19},{$set:{name:"Romil",Age:20}})
// Update first match where name = Romil and Age = 19

test> db.Student1.updateMany({name:"Romil",Age:19},{$set:{Age:20}})
// Update all matching documents

test> db.Student1.updateMany({},{$set:{age:21}})
// Set age = 21 for all documents

test> db.Student1.updateOne({Age:99},{$set:{name:"PQR"}},{upsert:true})
// Upsert: insert if not found (Age = 99)

test> db.Student1.find({name:"Romil"})
// Find all with name = Romil

test> db.Student1.findOne({name:"Romil"},{Age:1})
// Find one and show only Age field
-> Only One Obj will print

test> db.Student1.find({name:"Romil"},{Age:1}).limit(1)
// Limit result to 1 document

test> db.Student1.find({name:"Romil"},{Age:1})
// Show only Age field (default _id shown)

test> db.Student1.find({name:"Romil"},{_id:0})
// Exclude _id field from result

test> db.Student1.find({},{age:19}).count()
// Count with incorrect projection (should be a filter)

test> db.Student1.count({name:"Romil"})
// Count documents with name = Romil

test> db.Student1.find({},{age:1}).sort()
// Sort query without direction (undefined behavior)

-> Descending
test> db.Student1.find().sort({age:-1})
// Sort by age in descending order

-> Ascending
test> db.Student1.find().sort({age:1})
// Sort by age in ascending order
