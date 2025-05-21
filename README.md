
# 🧩 MongoDB Operators

Crud Operations

## ✅ Create

#### InsertOne()
Inserts single document into a collection

#### eg:
```diff 
db.collection_Name.insertOne({height:"20kg",.....})
```
#### InsertMany()
Inserts many documents into a collection by accepting array as a parameter.

#### eg:
```diff 
db.collection_Name.insertOne([{height:"20kg",.....},{height:"30kg",.....}])
```
#### Commonly Associated Operators:

#### $currentDate

Can be used in upsert operations to set current date/time
	{ $currentDate: { createdAt: true } }

#### $setOnInsert	

Sets fields only during insert via upsert	
{ $setOnInsert: { createdAt: new Date() } }

## ✅ Read/Query
These use query operators to filter and match documents.

### 🔹Comparison Operators

#### $eq - Equal to
```diff 
db.users.find({ age: { $eq: 25 } })
```
#### $ne - Not Equal to
```diff 
db.users.find({ age: { $ne: 25 } })
```
#### $gt - Grater than
```diff 
db.users.find({ age: { $gt: 25 } })
```
#### $gte - Greater Than equal to
```diff 
db.users.find({ age: { $gte: 25 } })
```
#### $lt - Less than
```diff 
db.users.find({ age: { $lt: 25 } })
```
#### $lte - Less Than equal to
```diff 
db.users.find({ age: { $lte: 25 } })
```
#### $in - Matches any value in Array
```diff 
db.users.find({ age: { $in: [25, 30, 35] } })
```
#### $nin - Not in Array
```diff 
db.users.find({ age: { $nin: [25, 30, 35] } })
```

### 🔹Logical Operators

#### $and – All Conditions Must Be True
```diff 
db.users.find({
  $and: [
    { age: { $gte: 25 } },
    { city: "New York" }
  ]
})
```
#### $or – At Least One Condition Must Be True
```diff 
{ $or: [ { field1: condition1 }, { field2: condition2 } ] }

db.users.find({
  $or: [
    { age: { $lt: 20 } },
    { city: "Los Angeles" }
  ]
})
```
#### $not – Inverts the Condition
```diff 
{ field: { $not: { condition } } }

db.users.find({
  age: { $not: { $gte: 30 } }
})
```
#### $nor – None of the Conditions Must Be True
```diff 
{ $nor: [ { condition1 }, { condition2 } ] }

db.users.find({
  $nor: [
    { age: { $lt: 18 } },
    { city: "Chicago" }
  ]
})
```
### 🔹Element Operators

#### $exists – Checks if a Field Exists

```diff 
{ field: { $exists: <true|false> } }

db.users.find({ email: { $exists: true } })
```
Finds all documents where the email field is present, regardless of its value.

#### $type – Checks the BSON Data Type of a Field
```diff 
{ field: { $type: <BSON type> } }

db.users.find({ age: { $type: "string" } })

db.users.find({ age: { $type: ["int", "double"] } })

```

### 🔹Evaluation Operators

#### $regex – Regular Expression Pattern Match
```diff 
db.users.find({ name: { $regex: /^A/ } })

db.users.find({ name: { $regex: /john/i } })

```

#### $expr – Use Aggregation Expressions in Queries

Allows use of aggregation expressions inside the find() query.



```diff 
 //Example: Compare Two Fields

db.sales.find({
  $expr: { $gt: ["$amount", "$target"] }
})
//Finds documents where amount is greater than target.

 //Example: Add Fields Together

db.orders.find({
  $expr: { $eq: [{ $add: ["$price", "$tax"] }, "$total"] }
})

Finds orders where price + tax equals total.

```

#### $mod – Modulo (Remainder)

Checks if a field value divided by a number has a specific remainder.


```diff 
db.users.find({ age: { $mod: [2, 0] } })

```
#### $text – Text Search (requires a text index)

Performs full-text search on string content.



```diff 
// Step 1 - Create Index
db.articles.createIndex({ title: "text", content: "text" })

// Step 2 - Search using $text
db.articles.find({ $text: { $search: "mongodb indexing" } })

```
#### $where – JavaScript Expression (⚠️ Use with caution)

Allows JavaScript-based condition; slower and not secure for user input.



```diff 
db.users.find({
  $where: "this.age < 30 && this.city == 'New York'"
})

```

### 🔹Array Operators

#### $elemMatch – Match Based on Multiple Conditions for Array Elements

Matches at least one element in the array that satisfies multiple conditions.
```diff 
db.users.find({
  scores: { $elemMatch: { subject: "Math", score: { $gt: 90 } } }
})
//Finds users with at least one score in Math greater than 90.

```

#### $size – Match Array by Length

Matches at least one element in the array that satisfies multiple conditions.
```diff 
db.comments.find({ tags: { $size: 3 } })

//Finds documents where tags array has exactly 3 elements.


```

#### Direct Index Match – Match Array Element by Position

You can also match array elements at a specific index using the dot notation.


```diff 
db.users.find({ "scores.0": 100 })

//Finds users whose first score in the scores array is 100.

```
