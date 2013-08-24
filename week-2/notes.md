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
## Node JS Driver
``` javascript
	
	-ex.
	var MongoClient = require('mongodb').MongoClient;
	MongoClient.connect('mongodb://localhost:27017/course', function(err, db) 
	{
	     if(err) throw err;

	     var query = { 'grade' : 100};

	     function callback(err, doc) {
	          if(err) throw err;

	          console.dir(doc);

	          db.close();
	     } 
		db.collection('grades').findOne(query,callback);
	});	
```
### Projections
``` javascript
	-ex.
	...
		var query = { 'title' : { '$regex' : 'NSA' } };
		var projection = { 'title': 1, "_id" : 0 };

		db.collection('reddit').find(query, projection).each( function(err, doc) {
			if(err) throw err;

			if(doc == null) {
				return db.close();
			}

			console.dir(doc.title);

		});
	...
```
### Dot Notation w/ Node JS Driver
``` javascript
	-ex.
	...
		var query = { 'media.oembed.type' : 'video' };
		var projection = { 'media.oembed.url': 1, "_id" : 0 };


		db.colletion('reddit').find(query,projection).each(function(err,doc) {
			if(err) throw err;

			if (doc == null) {
				return db.close();
			}

			console.dir(doc)
		});
	...
```

### Insert
``` javascript

	...
		var doc = { 'student' : 'Calvin', 'age' : 6 };

		db.collection('students').insert(doc, function(err, inserted) {
			if(err) throw err;

			console.dir("Successfully Inserted:" + JSON.stringify(inserted));

			return db.close();
		});
	...

	...
		// You can also insert Multiple Documents with array Syntax

		var docs = [
			 	{ '_id' : 'George', 'age' : 6 },
            	{ '_id' : 'george', 'age' : 7 } 
             ];
	...

```
### Update

* Replacement

``` javascript
	...
		var query = { 'assignment' : 'hw1' };

		db.collection('grades').findOne(query, function(err,doc) {
			if(err) throw err;
			if (!doc) {
				console.log('No document for assignment' + query.assignment + 'found!');
				return db.close();
			}

			// Ensure's our query is only replacing ID

			query[ '_id' ] = doc[ '_id' ];
			doc[ 'date_returned' ] = new Date();

			db.collection('grades').update(query, doc, function(err,updated) {
				if(err) throw err;

				console.dir("Successfully updated " + updated + "document!");

				return db.close();

			});
		});
	...

```
* In Place
``` javascript
	...
	var query = { 'assignment' : 'hw1' };
	var operator = { '$set' : { 'date_returned' : new Date() } };

	db.collection('grades').update(query, operator, function(err,updated) {
		if(err) throw err;

		console.dir("Successfully updated " + updated + "document!");

		return db.close(); 
	
	});
	...

```

* Multi
``` javascript
	...
	var query = {};
	var operator = { '$unset' : { 'date_returned': '' } };
	var options = { 'multi' : true };

	db.collection('grades').update(query, operator, options, function(err, updated) {
		if(err) throw err;

		console.dir("Successfully updated " + updated + "documents!");

		return db.close();
	});


```










