• Created a database named “todo”  
        use todo  

• Inserted one record to a table named tasks_table  
Table contains task_name, time(start,end), status of the task  
```js
db.tasks_table.insertOne({
  task_name:"Attend Class",
  time:{start: new Date("2025-05-28T10:00:00Z"), end: new Date("2025-05-28T18:00:00Z")},
  status:"pending"
})
```

• To see the contents of the table  
```js
db.tasks_table.find()
```

• Inserting records one by one  
```js
db.tasks_table.insertOne({
  task_name:"Submit Assignment",
  time:{start:new Date("2025-05-28T11:30:00"), end:new Date("2025-05-28T12:00:00")},
  status:"done"
})
db.tasks.insertOne({
  task_name: "Study MongoDB",
  time: {start: new Date("2025-05-28T14:00:00Z"), end: new Date("2025-05-28T15:00:00Z")},
  acknowledge: "pending"
})
db.tasks_table.insertOne({
  task_name: "Study MongoDB",
  time: {start: new Date("2025-05-28T14:00:00Z"), end: new Date("2025-05-28T15:00:00Z")},
  acknowledge: "pending"
})
db.tasks_table.insertOne({
  task_name: "Check Results",
  time: {start: new Date("2025-05-28T15:15:00Z"), end: new Date("2025-05-28T15:30:00Z")},
  acknowledge: "done"
})
db.tasks_table.insertOne({
  task_name: "Join Teams call",
  time: {start: new Date("2025-05-28T13:50:00Z"), end: new Date("2025-05-28T17:30:00Z")},
  acknowledge: "pending"
})
```

• Inserting multiple records at a time  
```js
db.tasks_table.insertMany([
  {
    task_name: "Assignment",
    time: {start: new Date("2025-05-28T18:00:00Z"), end: new Date("2025-05-28T19:00:00Z")},
    acknowledge: "pending"
  },
  {
    task_name: "Lunch break",
    time: {start: new Date("2025-05-28T13:00:00Z"), end: new Date("2025-05-28T13:30:00Z")},
    acknowledge: "pending"
  }
])
```

• Changing some acknowledge fields of records to “status”  
```js
db.tasks_table.updateMany({ acknowledge: "done" }, { $set: { acknowledge: true } })
db.tasks_table.updateMany({ acknowledge: "pending" }, { $set: { acknowledge: false } })
db.tasks_table.updateMany({ acknowledge: { $exists: true } }, { $rename: { "acknowledge": "status" } })
db.tasks.updateMany({ status: "done" }, { $set: { status: true } })
db.tasks_table.updateMany({ status: "done" }, { $set: { status: true } })
db.tasks_table.updateMany({ status: "pending" }, { $set: { status: false } })
```

• Displaying records  
```js
db.tasks_table.find().pretty()
```

• Setting default status to false  
```js
db.tasks_table.insertOne({task_name: "Example Task", status: false})
db.tasks_table.insertOne({task_name: "Example Task1"})
```

• Adding “createdAt” and “updatedAt” field to records  
```js
db.tasks_table.updateMany({}, {$set: {createdAt: new Date(), updatedAt: new Date()}})
```

• Altering the status of a record and changing the updatedAt field  
```js
db.tasks_table.updateOne({ task_name:"Lunch Break" }, {$set: {status: true, updatedAt: new Date()}})
db.tasks_table.updateOne({ task_name:"Lunch break" }, {$set: {status: true, updatedAt: new Date()}})
```

• To get the records which are created in the last 20 minutes  
```js
db.tasks_table.find({
  createdAt: {
    $gte: new Date(Date.now() - 20 * 60 * 1000)
  }
})
```

> `Date.now()` gives the current time in milliseconds, so we subtract 20 minutes by converting it to milliseconds to get records that are created within the last 20 minutes.
