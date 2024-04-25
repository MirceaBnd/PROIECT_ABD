
## TASK E

/ Get the nearest 10 zips from one of Chicago's landmarks, the Willis Tower situated at coordinates 41.878876, -87.635918. / 



## TASK F

/ Get the total population situated between 50 and 200 kms around New York's landmark, the Statue of Liberty at coordinates 40.689247, -74.044502. / 

For this task, I have a final code proposal:

db.proiect.aggregate([{$geoNear: { near: { type: "Point", coordinates : [-74.044502, 40.689247] }, distanceField: "distance", minDistance: 50000, maxDistance: 200000}}, { $group: { _id: 0, Population: {$sum: "$population"}}}]).toArray()[0].Population

![image](https://github.com/MirceaBnd/PROIECT_ABD/blob/main/TASK%20F/Fig1%20task%20F%20total%20population%20betw%2050%20and%20200%20kms.jpg)

Short description of the above code: 
The above calculates the total population of documents in the "proiect" collection that are within a certain distance range from a specified geographic point.

For more details, please consult also /Useful MongoDB documentation.md/
