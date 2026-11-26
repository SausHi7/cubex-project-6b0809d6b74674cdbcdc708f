# SQL hands-on submission

## q1

```sql
{"collection":"classes","filter":{"instructor.name":"Ayesha Khan"},"projection":{"name":1,"capacity":1}}
```

## q4

```sql
{"collection":"classes","pipeline":[{"$lookup":{"from":"bookings","localField":"id","foreignField":"classId","as":"allB"}},{"$addFields":{"confirmedCount":{"$size":{"$filter":{"input":"$allB","cond":{"$eq":["$$this.status","confirmed"]}}}}}},{"$match":{"confirmedCount":{"$gte":1}}},{"$project":{"name":1,"confirmedCount":1}},{"$sort":{"confirmedCount":-1,"name":1}}]}
```

## q2

```sql
{"collection":"classes","filter":{"schedule":{"$elemMatch":{"day":"Tue"}}},"projection":{"name":1}}
```

## q3

```sql
{"collection":"bookings","pipeline":[{"$match":{"status":"confirmed"}},{"$group":{"_id":"$classId","confirmedCount":{"$sum":1}}},{"$sort":{"confirmedCount":-1}},{"$limit":1},{"$project":{"classId":"$_id","confirmedCount":1,"_id":0}}]}
```

## q5

```sql
{"collection":"classes","pipeline":[{"$lookup":{"from":"bookings","localField":"id","foreignField":"classId","as":"allB"}},{"$match":{"allB":{"$size":0}}},{"$project":{"name":1}},{"$sort":{"name":1}}]}
```

## q6

```sql
{"collection":"bookings","pipeline":[{"$match":{"status":"cancelled"}},{"$group":{"_id":"$member"}},{"$project":{"member":"$_id","_id":0}},{"$sort":{"member":1}}]}
```
