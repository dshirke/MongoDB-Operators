
# MongoDB Operators

Crud Operations

### 1. Create

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
