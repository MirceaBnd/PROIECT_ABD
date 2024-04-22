### TASK C

/ Get the largest and the smallest city in each state. /

To solve the task, I made a first test, to see all cities with 0 population that are in all states. See following:

db.proiect.aggregate([{$match: { "population": 0 } }, { $group: { _id: {state_name: "$state_name"}, cities: { $addToSet: { city: "$city", population: "$population" } } } }, {$sort: {"_id": 1 } }, { $project: { _id: 1, state_name: 1,  cities: 1} }] )

Short explanation of the code: 
The above aggregates documents from the "proiect" collection, first filtering for documents where the population is 0, then grouping them by state name, creating an array of unique cities within each state along with their populations, sorting the results alphabetically by state name, and finally projecting the "_id", "state_name", and "cities" fields into the output.

![image](https://github.com/MirceaBnd/PROIECT_ABD/blob/main/TASK%20C/Fig1%20Task%20c%20ref%20cities%20with%20population%200%20in%20state%20pr%20MongoDB.jpg)

After this, I made a second test, to see how the smallest city does not necesarrily have to have 0 population:

db.proiect.aggregate([ { $match: { state_name: "Idaho" } }, { $group: { _id: "$city", Population: { $sum: "$population" }} }, { $sort: { Population: 1 } }] )

Short explanation of the code: 
The above code aggregates documents from the "proiect" collection, first filtering for documents where the state (randomly chosen) is "Idaho", then grouping them by city and calculating the total population for each city. At the end, it sorts the result by population in ascending order.

![image](https://github.com/MirceaBnd/PROIECT_ABD/blob/main/TASK%20C/Fig2%20Task%20c%20ref%20small%20city%20not%20necess%20with%200%20population%20pr%20MongoDB.jpg)



### TASK D

/ Get the largest and the smallest counties in each state. /


