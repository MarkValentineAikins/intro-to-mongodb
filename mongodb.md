# MongoDb CheatSheet
Using Markdown to create user guide for MongoDb

## MongoDb common commands
Show the version of database server
```
db.version()
```
Return statistics about the server 
```
db.stats()
```
List all the database in the MongoDB server

```
show dbs
```
Switch to use the database specified
```
use <dbName>
```
Creates new collection in the database
```
db.createCollection(“name”)
```
List all collections under the specified database
```
use <db name>
show collections
```
## inserting Document
Inserts one document into the collection
```
insertOne({…})
```

Syntax
```
db.<collectionName>.insertOne({})
```
Inserts many documents into the collection.
```
insertMany([{}, {} … {}])
```
Syntax
```
db.<collectionName>.insertMany([ {}, {} … {}])
```
## Finding document in collection
Returns all the documents in the collection that matches the query. It will return an empty array if there is no document in the collection. If empty object ({}) is passed as query it will return all the documents in the collection.
```
find({ query })
```
Returns a single document that matches the query
```
findOne({ query })
```
### NB: 
Query is just JavaScript object with key-value pairs.
Use dot (.) notation to query for nested (embedded) documents

## Query methods
Are methods helper methods of the find method. It needs to be chained after the find() method

Sorts documents in either ascending or descending order

```
sort()
```
Limits the returning documents to the number specified
```
limit()
```
Skips the first number of items specified
```
skip()
```
Counts the number of documents returned from a find result
```
count()
```
## Equality query
Match by field name and it’s exact value

Syntax
```
{<fieldName1> :  <value1>, <fieldName1> :  <value1>}
```
Example
```
{“name”:  “John Doe” }
{“age”:  30}
{“gender”: “male”,  “maritalStatus” :  “single”}
```

### NB
comma (,) represents AND	

## Query Operators	

```
$or				$eq				$lt
$and			$ne				$gt
$gte			$lte			$in
$nin			$regex
```
# Comparison operators
Operators add conditions that compares two or more values

Syntax
```
{<fieldName1>: {<operator1>: <value1>}, …}
```

Examples
```
{“age”: {$gt : 25}}
{“age”: {$lt : 25}}
{“favouriteFruit”: {“$in”: [“apple”, “orange”]}}
```
# Comparison operators con’t
This comparison operators require an ARRAY

Syntax
```
{<fieldName1>: { <operator1>:  [ <value1>,  <value2>] }, …}
```

Examples
```
{“eyeColor”: {“$in”: [“blue”, “brown”]}}
{“favouriteFruit”: {“$nin”: [“apple”, “orange”]}}
```
# “and” operator
Logically combines multiple conditions. Resulting documents must much ALL conditions

Syntax
```
{ $and: [ { <condition1> }, { <condition2> } … ] }
```

Example
```
{ $and: [ {“gender” : “male”} , “age” : 25 } ] }
```

### NB
Explicit $and MUST be used if conditions contains same field or operator


# Sample code and data
```
show databases

use admin

use local

use config

db.version()

use posts

use school
db.createCollection("Students")
db.createCollection("Teachers")

show collections

db.Students.insertMany(
[{"firstName":"Pippy","lastName":"Fronsek","gender":"Female","age":12,"class":4},
{"firstName":"Antonie","lastName":"McTeer","gender":"Female","age":12,"class":1},
{"firstName":"Ellery","lastName":"Drexel","gender":"Male","age":6,"class":1},
{"firstName":"Maible","lastName":"Brozek","gender":"Female","age":13,"class":6},
{"firstName":"Rudyard","lastName":"Mothersdale","gender":"Male","age":7,"class":2},
{"firstName":"Adiana","lastName":"Raffin","gender":"Female","age":7,"class":4},
{"firstName":"Free","lastName":"Sheehy","gender":"Genderqueer","age":11,"class":3},
{"firstName":"Roger","lastName":"Jachimczak","gender":"Male","age":13,"class":6},
{"firstName":"Isidor","lastName":"Fronsek","gender":"Male","age":6,"class":5},
{"firstName":"Stu","lastName":"Iredell","gender":"Male","age":7,"class":4},
{"firstName":"Jed","lastName":"Swinley","gender":"Male","age":9,"class":3},
{"firstName":"Terencio","lastName":"Sarre","gender":"Male","age":13,"class":1},
{"firstName":"Fidole","lastName":"Harrold","gender":"Male","age":12,"class":5},
{"firstName":"Michaella","lastName":"Willcox","gender":"Female","age":8,"class":1},
{"firstName":"Aura","lastName":"Keech","gender":"Female","age":11,"class":1},
{"firstName":"Antonia","lastName":"Anchor","gender":"Female","age":9,"class":4},
{"firstName":"Martainn","lastName":"Taylo","gender":"Male","age":6,"class":1},
{"firstName":"Tatum","lastName":"Ratlee","gender":"Female","age":7,"class":6},
{"firstName":"Manda","lastName":"Hampshaw","gender":"Female","age":10,"class":6},
{"firstName":"Maurene","lastName":"Stait","gender":"Genderqueer","age":10,"class":3},
{"firstName":"Josy","lastName":"MacIlwrick","gender":"Female","age":12,"class":3},
{"firstName":"Courtenay","lastName":"Coldbathe","gender":"Female","age":6,"class":2},
{"firstName":"Skyler","lastName":"Pringell","gender":"Male","age":9,"class":3},
{"firstName":"Rozele","lastName":"Fulham","gender":"Polygender","age":13,"class":5},
{"firstName":"Binny","lastName":"Kerswell","gender":"Female","age":9,"class":3},
{"firstName":"Robinet","lastName":"Bayldon","gender":"Female","age":9,"class":6},
{"firstName":"Jenny","lastName":"Powys","gender":"Female","age":7,"class":2},
{"firstName":"Wally","lastName":"Ambrogioni","gender":"Male","age":8,"class":5},
{"firstName":"Marrilee","lastName":"Pohls","gender":"Female","age":9,"class":4},
{"firstName":"Skippie","lastName":"Othick","gender":"Male","age":12,"class":4},
{"firstName":"Mara","lastName":"Partener","gender":"Female","age":13,"class":5},
{"firstName":"Jdavie","lastName":"Gunderson","gender":"Male","age":12,"class":3},
{"firstName":"Armin","lastName":"Jirieck","gender":"Male","age":9,"class":4},
{"firstName":"Ruthy","lastName":"Chiplen","gender":"Bigender","age":9,"class":2},
{"firstName":"Babb","lastName":"Butler-Bowdon","gender":"Female","age":11,"class":3},
{"firstName":"Dru","lastName":"Chipps","gender":"Female","age":6,"class":6},
{"firstName":"Otes","lastName":"Meates","gender":"Male","age":9,"class":1},
{"firstName":"Doug","lastName":"Covill","gender":"Male","age":12,"class":6},
{"firstName":"Reinhold","lastName":"Ebbins","gender":"Male","age":8,"class":5},
{"firstName":"Guenna","lastName":"Handslip","gender":"Bigender","age":6,"class":1},
{"firstName":"Granville","lastName":"Riddington","gender":"Male","age":10,"class":3},
{"firstName":"Northrup","lastName":"Roft","gender":"Male","age":10,"class":3},
{"firstName":"Sapphira","lastName":"Baradel","gender":"Female","age":9,"class":5},
{"firstName":"Suzanna","lastName":"Abramino","gender":"Female","age":9,"class":3},
{"firstName":"Ebba","lastName":"Trebble","gender":"Female","age":7,"class":2},
{"firstName":"Rhoda","lastName":"Yardley","gender":"Female","age":6,"class":2},
{"firstName":"Decca","lastName":"Karslake","gender":"Male","age":7,"class":5},
{"firstName":"Nancey","lastName":"Dreini","gender":"Female","age":10,"class":2},
{"firstName":"Morie","lastName":"Bachmann","gender":"Male","age":13,"class":3},
{"firstName":"Slade","lastName":"Keats","gender":"Male","age":6,"class":5}]
)

show collections

db.Teachers.insertMany(
[{"firstName":"Tallia","lastName":"Joice","gender":"Female","email":"tjoice0@plala.or.jp","class":1},
{"firstName":"Curr","lastName":"Brauner","gender":"Male","email":"cbrauner1@photobucket.com","class":2},
{"firstName":"Marcel","lastName":"Cranney","gender":"Male","email":"mcranney2@deliciousdays.com","class":3},
{"firstName":"Loren","lastName":"Rubinsaft","gender":"Female","email":"lrubinsaft3@kickstarter.com","class":4},
{"firstName":"Pearce","lastName":"Goodrum","gender":"Male","email":"pgoodrum4@paypal.com","class":5},
{"firstName":"Daryl","lastName":"O'Doogan","gender":"Male","email":"dodoogan5@simplemachines.org","class":6}]
)

db.Students.find({gender:"Female"})

db.Students.find({class:4})

db.Students.find({class:4, gender:"Female"})

db.Students.findOne({_id:ObjectId("631890440f2c3e3d845c435c")})

db.Students.find({}).sort({class:1})

db.Students.find({}).sort({class:-1})

db.Students.find({class:4, gender:"Male"}).count()

db.Students.find({class:4}).count()

db.Students.find({}).skip(5)

db.Students.find({
 age:{$gt:10}
})

db.Students.find({
 age:{$gte:10}
})

db.Students.find({
 $or: [{gender:"Female"}, {class:3}]
}).count()

db.Students.find({
 class:{$in:[1,2,3]}
}).sort({class:-1})

db.Students.find({
 $and: [{gender:"Male"}, {class:6}]
})
```





