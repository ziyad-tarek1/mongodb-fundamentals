Here's a well-organized and clean version of your MongoDB self-study document, formatted for clarity and easy learning:

---

# 📘 MongoDB Fundamentals – Self-Study Guide

---

## 1. 🆚 Difference Between MySQL and MongoDB (NoSQL) Terminology

| MySQL Terminology | MongoDB Terminology          |
|-------------------|------------------------------|
| database          | database                     |
| table             | collection                   |
| row               | document                     |
| column            | field                        |
| index             | index                        |
| transaction       | transaction                  |
| primary key       | primary key (default is `_id`) |

---

## 2. 🗃️ Database Operations

Basic database-level commands in MongoDB:

| Operation               | Command Example                      |
|-------------------------|--------------------------------------|
| Show all databases      | `show dbs`                           |
| Show current database   | `db`                                 |
| Create/Switch database  | `use <DB_name>`                     |
| Delete current database | `db.dropDatabase()`                 |

> ⚠️ **Note:** You must be in the database you want to drop.

---

## 3. 📁 Collections

| Operation                        | Command Example                            |
|----------------------------------|--------------------------------------------|
| Show all collections             | `show collections`                         |
| Create a new collection          | `db.createCollection("collection_name")`   |
| Auto-create collection on insert | Insert directly into a non-existent collection |

---

## 4. 🔁 CRUD Operations

### 🟢 Create

| Method        | Description                             |
|---------------|-----------------------------------------|
| `insert()`    | Insert one or more documents            |
| `insertOne()` | Insert a single document                |
| `insertMany()`| Insert multiple documents               |

#### Example:
```js
db.students.insertMany([
  {
    _id: 1,
    name: "ziad",
    grades: { arabic: 30, english: 40 },
    address: ["cairo", "fayiom"]
  },
  {}
])
```

📝 **Explanation**:
- `_id`: Document identifier (auto-generated if not specified).
- `grades`: A nested (embedded) document.
- `address`: An array of strings.

---

### 🔍 Read

#### SQL vs MongoDB Queries

| SQL                                     | MongoDB                                           |
|----------------------------------------|--------------------------------------------------|
| `SELECT * FROM people`                 | `db.people.find()`                              |
| `SELECT id, user_id, status FROM people` | `db.people.find({}, { user_id: 1, status: 1 })` |
| `SELECT user_id, status FROM people`   | `db.people.find({}, { user_id: 1, status: 1, _id: 0 })` |
| `SELECT * FROM people WHERE status = "A"` | `db.people.find({ status: "A" })`               |
| `SELECT * FROM people WHERE status != "A"` | `db.people.find({ status: { $ne: "A" } })`     |

#### Example 1:
```js
db.people.find({}, { user_id: 1, status: 1, _id: 0 })
```

🔍 **Explanation**:
- Empty `{}` filter = return all documents.
- Projection: `1` = include field, `0` = exclude field.
- `_id: 0` hides the auto-generated MongoDB ID.

#### Example 2:
```js
db.people.find({ status: "A" }, { user_id: 1, status: 1, _id: 0 })
```

#### Other Read Commands:

| Purpose                     | Command Example                                 |
|-----------------------------|-------------------------------------------------|
| Find one document           | `db.collection_name.findOne({ })`              |
| Find multiple documents     | `db.collection_name.find({ })`                 |
| Find with condition (JSON)  | `db.collection_name.find({ "field": "value" })`|
| Pretty print output         | `db.collection_name.find().pretty()`           |

---

### 🟡 Update

_(This section can be expanded when you provide update examples.)_

---

### 🔴 Delete

| Operation               | Command                              |
|-------------------------|--------------------------------------|
| Delete a collection     | `db.collection_name.drop()`          |
| Delete a database       | `db.dropDatabase()`                  |

> ⚠️ **Reminder:** You must be in the database you want to delete.

---

Let me know when you're ready to send the next section and I’ll continue organizing it the same way!