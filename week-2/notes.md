# Notes From Week 2

## BSON 
http://www.bsonspec.org = Binary JSON that MongoDB uses
``` shell    
	> NumberInt(1)
	1
	> NumberLong(1) + NumberLong(3)
	4
	> new Date()
	ISODate("2013-08-24T14:26:02.209Z")
```
## Inserting Objects
``` shell 
	> doc = { ... }
	> db.{ collection name }.insert( doc )
	> db.{ collection name }.find()

	{ ... }

	-ex.
	db.fruit.insert({name:"apple", color:"red", shape:"round"})
```
## Querying
``` shell
	db.{ collection name }.find()
	db.{ collection name }.find( { arg1 }, { arg2 } )

		// arg1 = Criteria
		// arg2 = Fields to be returned, this is boolean and defaults as true

	-ex.
	db.scores.find({ "type": "essay", "score": 50}, { "_id": false, "student": true })
```
### Inequalitys
``` shell
	db.{ collection name }.find( {  key : { $gt: value, $lte:value} } ) 

	This works with Numbers and Strings

	-ex. 
	db.users.find( { name : { $gt : "F" , $lte : "Q" } } )

	$gt, $lte, $exists, $type, $regex

	-ex. 
	db.users.find( { name: { $regex : "q"}, email : { $exists:true } } )
```
### Connecting Inequalitys
``` shell
	db.{ collection name }.find( { $or : [ ... ] )
	// Both must be true

	-ex. 
	db.scores.find({ $or :[{ score : { $lt : 50 } }, { score : { $gt : 90 }}]});

	db.{ collection name }.find( { $and : [ ... ] )

	// $and operator can generally not ideal and can be optimized

	db.{ collection name }.find( { $all : [ ... ] )
	// Must Match
	
	db.{ collection name }.find( { $in : [ ... ] )
	// At least 1
```
### Removing Documents
``` shell
	db.{ collection name }.remove( ... )
	// Same args as find

	db.{ collection name }.drop()
	// All


	-ex.
	db.scores.remove({ score: { $lt : 60}})
```
### Shell Erros
``` shell
	db.runCommand({ getLastError: 1 });
	//Way to check if write operation suceeded or failed.
```




