# Notes From Week 1
======

## Basics of Mongo Shell

// See what Databases are hosted
> show dbs

// Name DB
> use nameofDB

// Insert Whatever!
> db.things.insert({ "d" : 4})

// Find Stuff
> db.things.find()

// Collection with formating.
> db.things.find().pretty()

## Json Basic Structures

The only thing that is in a "JSON" file is {Dictionarys} and [Arrays] You can nest each of these how ever you like, to be as complex as needed.

### ex.1

{
        "fruit": [
                "apple",
                "pear",
                "peach"
        ]
}

### ex.2

{
    'address':
        {
            'street_address': "23 Elm Drive",
            'city' : "Palo Alto",
            'state': "California",
            'zipcode': "94305"
        }
}

### ex.3

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
