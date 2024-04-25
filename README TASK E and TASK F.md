
## TASK E

/ Get the nearest 10 zips from one of Chicago's landmarks, the Willis Tower situated at coordinates 41.878876, -87.635918. / 

The first step was to convert the existing coordinates to an array of coordinates. So, MongoDB Atlas was used to check the existing coordinates:

![image](https://github.com/MirceaBnd/PROIECT_ABD/blob/main/TASK%20E/Fig1%20extras%20of%20lat%20long%20current%20values%20from%20Atlas.jpg)

and also one random example of such a check:

![image](https://github.com/MirceaBnd/PROIECT_ABD/blob/main/TASK%20E/Fig2%20extras%20of%20lat%20long%20current%20values.jpg)

The next step was to use a code to convert the coordinates in array:

db.proiect.updateMany({}, [ { $set: { location: { type: "Point", coordinates: ["$lng", "$lat" ] } } } ])

Short description of code: 
The above code updates each document in the "proiect" collection by adding a "location" field with a GeoJSON Point object, where the coordinates are taken from the "lng" and "lat" fields of each document.

![image](https://github.com/MirceaBnd/PROIECT_ABD/blob/main/TASK%20E/Fig3%20task%20e%20replace%20lat%20long%20with%20array%20of%20coord.jpg)

and after a new check of an object, it can be seen the array (ref coordinates):

![image](https://github.com/MirceaBnd/PROIECT_ABD/blob/main/TASK%20E/Fig4%20task%20e%20confirmation%20existance%20array%20of%20coord%20in%20Atlas.jpg)

The next step was to use a code containing $near, but an error appeared (extras):

![image](https://github.com/MirceaBnd/PROIECT_ABD/blob/main/TASK%20E/Fig5%20task%20e%20error%20when%20using%20near.jpg)

So, to solve the issue, I created an index called '2dsphere' and used the code:

db.proiect.createIndex({ location: "2dsphere" })

![image](https://github.com/MirceaBnd/PROIECT_ABD/blob/main/TASK%20E/Fig6%20task%20e%20creation%20of%20index%202dsphere.jpg)

The final code used to solve the task is:

db.proiect.find({ location: { $near: { type: "Point", coordinates: [-87.635918, 41.878876] } } }).limit(10)

Short description of the final code:
The above retrieves up to 10 ZIPS/ locations from the "proiect" collection that are nearest to the specified geographic 
point (-87.635918 longitude, 41.878876 latitude).

![image](https://github.com/MirceaBnd/PROIECT_ABD/blob/main/TASK%20E/Fig7%20task%20e%20nearest%2010%20zips.jpg)


## TASK F

/ Get the total population situated between 50 and 200 kms around New York's landmark, the Statue of Liberty at coordinates 40.689247, -74.044502. / 

For this task, I have a final code proposal:

db.proiect.aggregate([{$geoNear: { near: { type: "Point", coordinates : [-74.044502, 40.689247] }, distanceField: "distance", minDistance: 50000, maxDistance: 200000}}, { $group: { _id: 0, Population: {$sum: "$population"}}}]).toArray()[0].Population

![image](https://github.com/MirceaBnd/PROIECT_ABD/blob/main/TASK%20F/Fig1%20task%20F%20total%20population%20betw%2050%20and%20200%20kms.jpg)

Short description of the above code: 
The above calculates the total population of documents in the "proiect" collection that are within a certain distance range from a specified geographic point.

For additional details, please consult also /Useful MongoDB documentation.md/
