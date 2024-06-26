# PROIECT_ABD

## TASK A
/ Get the states with a total population of over 10 million. /

I used the following:

db.proiect.aggregate([{$group: {_id: {state_name: "$state_name"}, state_population: {$sum: "$population"}}}, {$match: {state_population: {$gt: 10000000}}}, {$sort: {state_population: 1}}])

![image](https://github.com/MirceaBnd/PROIECT_ABD/blob/main/TASK%20A/Fig%20Task%20a%20ref%20pr%20MongoDB.jpg)

Short explanation of used final code:
The above first groups documents by the "state_name" field, calculates the total population for each state, filters out states with a total population greater than 10 000 000, and at the end sorts the resulting states based on their populations - in ascending order.

## TASK B
/ Get the average city population by state. /

I made a first evaluation of how many cities are in a state (chosen randomly), as a number:

db.proiect.find({ state_name: "Michigan" }, { "city": 1, "_id": 0, population: 1}).count()

![image](https://github.com/MirceaBnd/PROIECT_ABD/blob/main/TASK%20B/Fig1%20Task%20b%20ref%20state%20pr%20MongoDB.jpg)

and finally I made the following:

db.proiect.aggregate([ { $group: { _id: {state_name: "$state_name"}, total_population: { $sum: "$population" }, All_cities: { $sum: 1 } } }, { $addFields: { Average_city_population_by_state: { $divide: ["$total_population", "$All_cities"] } } } ] )

![image](https://github.com/MirceaBnd/PROIECT_ABD/blob/main/TASK%20B/Fig2%20Task%20b%20ref%20average1%20pr%20MongoDB.jpg)

Short explanation of used final code:
The above groups documents by the "state_name" field, calculates the total population and counts the number of cities for each state, then adds a new field (with the calculated average) that represents the average population within each state.


