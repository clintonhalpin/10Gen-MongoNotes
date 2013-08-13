# Basics of Mongo Shell

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

