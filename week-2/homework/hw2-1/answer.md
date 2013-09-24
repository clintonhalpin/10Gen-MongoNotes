db.weather.find({ "Wind Direction" : { "$gt": 180, "$lt": 360 } }).sort( { "Temperature": 1 } )


// Prints out New Mexico