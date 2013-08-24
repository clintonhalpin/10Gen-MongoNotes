# Notes From Week 2

## BSON 

http://www.bsonspec.org = Binary JSON that MongoDB uses

	> NumberInt(1)
	1
	> NumberLong(1) + NumberLong(3)
	4
	> new Date()
	ISODate("2013-08-24T14:26:02.209Z")

## Inserting Objects

	> doc = { ... }
	> db.{ collection name }.insert( doc )
	> db.{ collection name }.find()

	{ ... }

	-ex.
	db.fruit.insert({name:"apple", color:"red", shape:"round"})


## Querying

	db.{ collection name }.find()
	db.{ collection name }.find( { arg1 }, { arg2 } )

		// arg1 = Criteria
		// arg2 = Fields to be returned, this is boolean and defaults as true

	-ex.
	db.scores.find({ "type": "essay", "score": 50}, { "_id": false, "student": true })

### Operators in Queries

	db.{ collection name }.find( {  key : { $gt: value, $lte:value} } ) 

	This works with Numbers and Strings

	-ex. 
	db.users.find( { name : { $gt : "F" , $lte : "Q" } } );

	$gt, $lte, $exists, $type, $regex

	-ex. 
	db.users.find( { name: { $regex : "q"}, email : { $exists:true } } )














