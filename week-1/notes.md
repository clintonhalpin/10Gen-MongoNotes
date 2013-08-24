# Notes From Week 1


## Basics of Mongo Shell
```shell    
        // Show the databases in the current Mongo Instance
                        
        > show dbs
                
        // Switch to use a Mongo Database
                        
        > use nameofDB
                
        // Insert 
                        
        > db.things.insert({ "d" : 4})
                
        // Find
                        
        > db.things.find()
                
        // Print out response, with formating.
                        
        > db.things.find().pretty()
```        
## Json Basic Structures

The only data types in Json - {Dictionarys} and [Arrays]. You can nest these two types to be as deep and complex as needed.

### ex.1
```javascript
        {
                "fruit": [
                        "apple",
                        "pear",
                        "peach"
                ]
        }
```
### ex.2
```javascript
        {
            'address':
                {
                    'street_address': "23 Elm Drive",
                    'city' : "Palo Alto",
                    'state': "California",
                    'zipcode': "94305"
                }
        }
```
### ex.3
```javascript
        {
            'address':
                {
                    'street_address': "23 Elm Drive",
                    'cities' : [{
                        'summer':'Palo Alto',
                        'winter':'New York'
                     }],
                    'state': "California",
                    'zipcode': "94305"
            	}
        }
```
