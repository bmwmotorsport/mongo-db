# 📘 MongoDB Shell Example

[![MongoDB Version](https://img.shields.io/badge/MongoDB-%5E6.0-green?logo=mongodb)](https://www.mongodb.com/)
[![Shell](https://img.shields.io/badge/Shell-mongosh-blue?logo=terminal)](https://www.mongodb.com/docs/mongodb-shell/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> A simple walkthrough of MongoDB shell (`mongosh`) commands to manage databases, collections, and documents.

---

## 🛠️ Prerequisites

- [MongoDB](https://www.mongodb.com/try/download/community) installed and running
- Access to `mongosh` (MongoDB Shell)

---

## 📂 Commands Overview

```js
// 🔍 List all databases
show dbs

// 🚀 Switch to (or create) a database named "domain"
use domain

// 🏗️ Create a new collection called "Student1"
db.createCollection("Student1")

// ✏️ Rename "Student1" to "Student3"
db.renameCollection("Student1", "Student3")

// ⚠️ This will fail (Student1 no longer exists after renaming)
db.Student1.insertOne({ name: "Romil", age: 19 })

// ❌ Incorrect: insertMany expects an array, not multiple objects
db.Student1.insertMany(
  { name: "ABC", age: 10 },
  { name: "XYZ", age: 20 },
  { name: "PQR", age: 30 }
)

// ✅ Correct: insert multiple documents into "Student1" (after recreating if needed)
db.createCollection("Student1") // Recreate if deleted
db.Student1.insertMany([
  { name: "ABC", age: 10 },
  { name: "XYZ", age: 20 },
  { name: "PQR", age: 30 }
])
