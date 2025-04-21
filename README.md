# MongoDB Fundamentals

## 1. Difference Between MySQL and NoSQL Terminology

| MySQL Terminology  | MongoDB Terminology         |
|--------------------|-----------------------------|
| database           | database                    |
| column             | field                       |
| row                | document                    |
| table              | collection                  |
| index              | index                       |
| transaction        | transaction                 |
| primary key        | primary key (default is _id)|

---

## 2. Database Operations

The basic operations to perform on a database in MongoDB:

- **Show All Databases**
  ```bash
  show dbs
  ```

- **Show Current Database**
  ```bash
  db
  ```

- **Create / Switch to New Database**
  ```bash
  use `<DB_name>`
  ```

- **Delete Database**
  ```bash
  db.dropDatabase()
  ```
  **Note**: To drop a database, you need to be in that database.

---

## 3. Collections

- **Show All Collections of Current Database**
  ```bash
  show collections
  ```

- **Create New Collection**
  ```bash
  db.createCollection("collection_name")
  ```

  **Note**: You can insert directly into a non-existing collection, and it will be automatically created.

---

## 4. CRUD Operations

`CRUD` operations refer to the basic functions of persistent storage. In MongoDB, these operations are as follows:

- **Create**
  - **Insert**: Insert a single or multiple documents in the collection.
    ```bash
    db.collection_name.insert( { } )  // For a single document
    db.collection_name.insert([ {}, {} ])  // For multiple documents
    ```

  - **InsertOne**: Insert a single document in the collection.
    ```bash
    db.collection_name.insertOne( { } )
    ```

  - **InsertMany**: Insert multiple documents in the collection.
    ```bash
    db.collection_name.insertMany( [ {}, {} ] )
    ```

### Example & Explanation:

```bash
db.collection_name.insertMany( [ 
    { 
        _id: 1, 
        name: 'ziad', 
        grades: { arabic: 30, english: 40 }, 
        address: [ "cairo", "fayiom" ] 
    }, 
    {} 
] )
```

- **db.collection_name**: This specifies the collection where the documents will be inserted. Replace `collection_name` with the actual name of your collection.

- **insertMany()**: This method is used to insert multiple documents into the specified collection. It takes an array of documents as an argument.

- **Array of Documents**: The array contains two elements:
  1. **First Document**:
     - **_id**: This is a unique identifier for the document. In this case, it is set to `1`. If you do not specify an `_id`, MongoDB will automatically generate one.
     - **name**: This field holds the value `'ziad'`, representing the name of the individual.
     - **grades**: This is an embedded document (sub-document) that contains two fields:
       - **arabic**: Set to `30`.
       - **english**: Set to `40`.
     - **address**: This is an array that contains two strings: `"cairo"` and `"fayiom"`, representing the locations associated with the individual.

  2. **Second Document**: The second document in the array is an empty object `{}`. This means that a document with no fields will be inserted into the collection. MongoDB will automatically generate an `_id` for this document.

### Summary:
This query inserts two documents into the specified collection. The first document contains detailed information about an individual named "ziad," including their grades and addresses, while the second document is empty and will have a generated `_id`.

- **Read**

#### To understand it better, let's compare between MySQL and NoSQL:

| SQL Schema Statements                | MongoDB Schema Statements        |
|--------------------------------------|----------------------------------|
| SELECT * FROM people                 | db.people.find()                 |
| SELECT id, user_id, status FROM people | db.people.find({}, {user_id: 1, status: 1}) |
| SELECT user_id, status FROM people   | db.people.find({}, {user_id: 1, status: 1, _id: 0}) |
SELECT WHERE - "!=" & FIND()- $NE

SQL Schema Statements

MongoDB Schema Statements

SELECT * FROM people WHERE status = "A"

db.people.find({status: "A"})

SELECT user_id, status FROM people WHERE status = "A"

db.people.find({ status: "A" }, { user_id: 1, status: 1, _id: 0})

SELECT * FROM people WHERE status != "A"

db.people.find({status: {$ne: "A"}})
### Example & Explanation:
- Example 1:
```bash
db.people.find({}, {user_id: 1, status: 1, _id: 0})
```

#### Explanation:

- **db.people**: This specifies the `people` collection from which we want to retrieve documents. Replace `people` with the actual name of your collection if different.

- **find()**: This method is used to query documents in the collection. It takes two parameters:
  1. **Query Filter**: The first parameter `{}` is an empty filter, which means we want to retrieve all documents in the collection. If you wanted to filter results based on specific criteria, you would place those criteria inside the curly braces.
  
  2. **Projection**: The second parameter `{user_id: 1, status: 1, _id: 0}` specifies which fields to include or exclude in the returned documents:
     - **user_id: 1**: This means that the `user_id` field will be included in the results.
     - **status: 1**: This means that the `status` field will also be included in the results.
     - **_id: 0**: This means that the default `_id` field will be excluded from the results. By default, MongoDB includes the `_id` field in every document, but setting it to `0` will prevent it from being returned.

#### Summary:
This query retrieves all documents from the `people` collection but only returns the `user_id` and `status` fields for each document, while excluding the `_id` field. This is useful for reducing the amount of data transferred over the network and focusing on only the relevant fields needed for your application.

- Example 2:

```bash
db.people.find({ status: "A" }, { user_id: 1, status: 1, _id: 0})
```

---

  - **Find One Document**: Retrieve a single document from the collection.
    ```bash
    db.collection_name.findOne( { } )
    ```

  - **Find Multiple Documents**: Retrieve multiple documents from the collection.
    ```bash
    db.collection_name.find( { } )
    ```

  - **Find Multiple Documents with JSON**: Retrieve documents that match specific criteria in JSON format.
    ```bash
    db.collection_name.find( { "field_name": "value" } )
    ```

  - **Pretty Print Documents**: Retrieve and format documents for better readability.
    ```bash
    db.collection_name.find().pretty()
    ```

- **Update**
- **Delete**
  - **Delete a Collection**
    ```bash
    db.collection_name.drop()
    ```

  - **Delete Database**
    ```bash
    db.dropDatabase()
    ```
  **Note**: To drop a database, you need to be in that database.
---