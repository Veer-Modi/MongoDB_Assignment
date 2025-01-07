# Assignment-1

## Task-1:

```javascript
use codinggita
```

```javascript
db.createCollection("students");
db.createCollection("courses");
```

```javascript
db.students.insertMany([
  {
    name: "Jenil",
    rollNumber: 101,
    department: "Computer Science",
    year: 2,
    coursesEnrolled: ["CS101", "CS102"],
  },
  {
    name: "Mahir",
    rollNumber: 102,
    department: "Computer Science",
    year: 2,
    coursesEnrolled: ["CS101", "CS103"],
  },
  {
    name: "Arjun",
    rollNumber: 103,
    department: "Electrical Engineering",
    year: 3,
    coursesEnrolled: ["EE101", "EE102"],
  },
]);
```

```javascript
db.courses.insertMany([
  {
    courseCode: "CS101",
    courseName: "Introduction to Programming",
    credits: 3,
    instructor: "Prof. Sharma",
  },
  {
    courseCode: "CS102",
    courseName: "Data Structures",
    credits: 3,
    instructor: "Prof. Gupta",
  },
  {
    courseCode: "CS103",
    courseName: "Algorithms",
    credits: 3,
    instructor: "Prof. Kapoor",
  },
  {
    courseCode: "EE101",
    courseName: "Basic Electrical Engineering",
    credits: 4,
    instructor: "Prof. Verma",
  },
  {
    courseCode: "EE102",
    courseName: "Circuit Theory",
    credits: 4,
    instructor: "Prof. Yadav",
  },
]);
```

## Task-2:

```javascript
db.students.find({department:"Computer Science"})

 {
  _id: ObjectId('677beab07dc818802c3bec88'),
  name: 'Jenil',
  rollNumber: 101,
  department: 'Computer Science',
  year: 2,
  coursesEnrolled: [
    'CS101',
    'CS102'
  ]
}
{
  _id: ObjectId('677beab07dc818802c3bec89'),
  name: 'Mahir',
  rollNumber: 102,
  department: 'Computer Science',
  year: 2,
  coursesEnrolled: [
    'CS101',
    'CS103'
  ]
}
```

```javascript
db.students.find({year: 2})

{
  _id: ObjectId('677beab07dc818802c3bec88'),
  name: 'Jenil',
  rollNumber: 101,
  department: 'Computer Science',
  year: 2,
  coursesEnrolled: [
    'CS101',
    'CS102'
  ]
}
{
  _id: ObjectId('677beab07dc818802c3bec89'),
  name: 'Mahir',
  rollNumber: 102,
  department: 'Computer Science',
  year: 2,
  coursesEnrolled: [
    'CS101',
    'CS103'
  ]
}
```

```javascript
db.students.find({coursesEnrolled: "CS101"})

{
  _id: ObjectId('677beab07dc818802c3bec88'),
  name: 'Jenil',
  rollNumber: 101,
  department: 'Computer Science',
  year: 2,
  coursesEnrolled: [
    'CS101',
    'CS102'
  ]
}
{
  _id: ObjectId('677beab07dc818802c3bec89'),
  name: 'Mahir',
  rollNumber: 102,
  department: 'Computer Science',
  year: 2,
  coursesEnrolled: [
    'CS101',
    'CS103'
  ]
}
```

```javascript
db.students.updateOne(
{ name: "Mahir" },
{ $set: { coursesEnrolled:["CS101","CS102","CS103"]}}
)

{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}

db.students.find({name:"Mahir"})

{
  _id: ObjectId('677beab07dc818802c3bec89'),
  name: 'Mahir',
  rollNumber: 102,
  department: 'Computer Science',
  year: 2,
  coursesEnrolled: [
    'CS101',
    'CS102',
    'CS103'
  ]
}
```

```javascript

db.students.deleteOne({name:"Jenil"})

{
  acknowledged: true,
  deletedCount: 1
}

db.students.find()

{
  _id: ObjectId('677beab07dc818802c3bec89'),
  name: 'Mahir',
  rollNumber: 102,
  department: 'Computer Science',
  year: 2,
  coursesEnrolled: [
    'CS101',
    'CS102',
    'CS103'
  ]
}
{
  _id: ObjectId('677beab07dc818802c3bec8a'),
  name: 'Arjun',
  rollNumber: 103,
  department: 'Electrical Engineering',
  year: 3,
  coursesEnrolled: [
    'EE101',
    'EE102'
  ]
}
```
