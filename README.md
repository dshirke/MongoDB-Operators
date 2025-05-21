
# MongoDB Operators

Crud Operations

## 1. Create

#### InsertOne()
Inserts single document into a collection

#### eg:

db.collection_Name.insertOne({height:"20kg",.....})

#### InsertMany()
Inserts many documents into a collection by accepting array as a parameter.

#### eg:

db.collection_Name.insertOne([{height:"20kg",.....},{height:"30kg",.....}])

#### Commonly Associated Operators:

#### $currentDate

Can be used in upsert operations to set current date/time
	{ $currentDate: { createdAt: true } }

#### $setOnInsert	

Sets fields only during insert via upsert	
{ $setOnInsert: { createdAt: new Date() } }

## 2. Read/Query
These use query operators to filter and match documents.

### Comparison Operators

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

### Logical Operators

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
### Element Operators

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
