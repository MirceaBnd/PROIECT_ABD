# PROIECT_ABD

## TASK A
<Get the states with a total population of over 10 million.>

I used the following:
db.proiect.aggregate([{$group: {_id: {state_name: "$state_name"}, state_population: {$sum: "$population"}}}, {$match: {state_population: {$gt: 10000000}}}, {$sort: {state_population: 1}}])

![image](https://github.com/MirceaBnd/PROIECT_ABD/blob/main/TASK%20A/Fig%20Task%20a%20ref%20pr%20MongoDB.jpg)

### TASK B



