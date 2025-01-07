# Assginment-3

## Task-1:

```javsacript
use codinggitastudents
```

```javascript
db.createCollection("students");
db.createCollection("courses");
```

## Task-2:

```javascript
db.students.insertMany([
  {
    name: "Jenil",
    rollNumber: "CS1001",
    department: "CSE",
    year: 2,
    coursesEnrolled: ["CS101", "MATH202", "PHY101"],
  },
  {
    name: "Mahir",
    rollNumber: "CS1002",
    department: "IT",
    year: 1,
    coursesEnrolled: ["CS101", "MATH101"],
  },
  {
    name: "Arjun",
    rollNumber: "CS1003",
    department: "CSE",
    year: 3,
    coursesEnrolled: ["CS301", "MATH303"],
  },
  {
    name: "Yashvi",
    rollNumber: "CS1004",
    department: "ECE",
    year: 2,
    coursesEnrolled: ["ECE201", "MATH202"],
  },
]);
```

```javascript
db.courses.insertMany([
  {
    courseCode: "CS101",
    name: "Introduction to Programming",
    credits: 3,
    instructor: "Prof. Krishna",
  },
  {
    courseCode: "MATH101",
    name: "Mathematics I",
    credits: 4,
    instructor: "Prof. Priyesha",
  },
  {
    courseCode: "PHY101",
    name: "Physics I",
    credits: 4,
    instructor: "Prof. Arjun",
  },
  {
    courseCode: "ECE201",
    name: "Digital Electronics",
    credits: 3,
    instructor: "Prof. Mahir",
  },
]);
```

## Task-3:

```javascript
db.students.find()

{
    name: "Jenil",
    rollNumber: "CS1001",
    department: "CSE",
    year: 2,
    coursesEnrolled: ["CS101", "MATH202", "PHY101"],
}
{
    name: "Mahir",
    rollNumber: "CS1002",
    department: "IT",
    year: 1,
    coursesEnrolled: ["CS101", "MATH101"],
}
{
    name: "Arjun",
    rollNumber: "CS1003",
    department: "CSE",
    year: 3,
    coursesEnrolled: ["CS301", "MATH303"],
}
{
    name: "Yashvi",
    rollNumber: "CS1004",
    department: "ECE",
    year: 2,
    coursesEnrolled: ["ECE201", "MATH202"],
}
```

```javascript
db.students.find({ coursesEnrolled: "CS101" })

{
  _id: ObjectId('677cc5bc4f57c817046e50e0'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  coursesEnrolled: [
    'CS101',
    'MATH202',
    'PHY101'
  ]
}
{
  _id: ObjectId('677cc5bc4f57c817046e50e1'),
  name: 'Mahir',
  rollNumber: 'CS1002',
  department: 'IT',
  year: 1,
  coursesEnrolled: [
    'CS101',
    'MATH101'
  ]
}
```

```javascript
db.students.find({ department: "CSE" });

{
  _id: ObjectId('677cc5bc4f57c817046e50e0'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  coursesEnrolled: [
    'CS101',
    'MATH202',
    'PHY101'
  ]
}
{
  _id: ObjectId('677cc5bc4f57c817046e50e2'),
  name: 'Arjun',
  rollNumber: 'CS1003',
  department: 'CSE',
  year: 3,
  coursesEnrolled: [
    'CS301',
    'MATH303'
  ]
}
```

```javascript
db.students.find({}, { name: 1, department: 1 })

{
  _id: ObjectId('677cc5bc4f57c817046e50e0'),
  name: 'Jenil',
  department: 'CSE'
}
{
  _id: ObjectId('677cc5bc4f57c817046e50e1'),
  name: 'Mahir',
  department: 'IT'
}
{
  _id: ObjectId('677cc5bc4f57c817046e50e2'),
  name: 'Arjun',
  department: 'CSE'
}
{
  _id: ObjectId('677cc5bc4f57c817046e50e3'),
  name: 'Yashvi',
  department: 'ECE'
}
```

```javascript
db.students.find({ year: { $eq: 2 } });

{
  _id: ObjectId('677cc5bc4f57c817046e50e0'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  coursesEnrolled: [
    'CS101',
    'MATH202',
    'PHY101'
  ]
}
{
  _id: ObjectId('677cc5bc4f57c817046e50e3'),
  name: 'Yashvi',
  rollNumber: 'CS1004',
  department: 'ECE',
  year: 2,
  coursesEnrolled: [
    'ECE201',
    'MATH202'
  ]
}
```

```javascript
db.students.find({ "coursesEnrolled.3": { $exists: true } });
```

```javascript
db.students.find({ $or: [{ department: "CSE" }, { department: "ECE" }] })

{
  _id: ObjectId('677cc5bc4f57c817046e50e0'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  coursesEnrolled: [
    'CS101',
    'MATH202',
    'PHY101'
  ]
}
{
  _id: ObjectId('677cc5bc4f57c817046e50e2'),
  name: 'Arjun',
  rollNumber: 'CS1003',
  department: 'CSE',
  year: 3,
  coursesEnrolled: [
    'CS301',
    'MATH303'
  ]
}
{
  _id: ObjectId('677cc5bc4f57c817046e50e3'),
  name: 'Yashvi',
  rollNumber: 'CS1004',
  department: 'ECE',
  year: 2,
  coursesEnrolled: [
    'ECE201',
    'MATH202'
  ]
}
```

## Task-4:

```javascript
db.students.updateOne({ name: "Yashvi" }, { $set: { department: "CS" } })

{
  _id: ObjectId('677cc5bc4f57c817046e50e3'),
  name: 'Yashvi',
  rollNumber: 'CS1004',
  department: 'CS',
  year: 2,
  coursesEnrolled: [
    'ECE201',
    'MATH202'
  ]
}
```

```javascript
db.students.updateMany(
  { coursesEnrolled: "MATH101" },
  { $push: { coursesEnrolled: "CS102" } }
)

{
  _id: ObjectId('677cc5bc4f57c817046e50e1'),
  name: 'Mahir',
  rollNumber: 'CS1002',
  department: 'IT',
  year: 1,
  coursesEnrolled: [
    'CS101',
    'MATH101',
    'CS102'
  ]
}
```

```javascript
db.courses.updateOne(
  { courseCode: "CS101" },
  { $set: { instructor: "Prof. Krishna Kumar" } }
)

{
  _id: ObjectId('677cc5c54f57c817046e50e4'),
  courseCode: 'CS101',
  name: 'Introduction to Programming',
  credits: 3,
  instructor: 'Prof. Krishna Kumar'
}
```

## Task-5:

```javascript
db.students.deleteOne({ rollNumber: "CS1004" });

db.students.deleteMany({ year: 1 });

{
  _id: ObjectId('677cc5bc4f57c817046e50e0'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  coursesEnrolled: [
    'CS101',
    'MATH202',
    'PHY101'
  ]
}
{
  _id: ObjectId('677cc5bc4f57c817046e50e1'),
  name: 'Mahir',
  rollNumber: 'CS1002',
  department: 'IT',
  year: 1,
  coursesEnrolled: [
    'CS101',
    'MATH101',
    'CS102'
  ]
}
{
  _id: ObjectId('677cc5bc4f57c817046e50e1'),
  name: 'Mahir',
  rollNumber: 'CS1002',
  department: 'IT',
  year: 1,
  coursesEnrolled: [
    'CS101',
    'MATH101',
    'CS102'
  ]
}
```

## Task-6:

```javascript
db.students.aggregate([
  { $group: { _id: "$department", totalStudents: { $sum: 1 } } },
])

{
  _id: 'IT',
  totalStudents: 1
}
{
  _id: 'CSE',
  totalStudents: 2
}
```

```javascript
db.students.aggregate([
  { $project: { numCourses: { $size: "$coursesEnrolled" } } },
  { $group: { _id: null, avgCourses: { $avg: "$numCourses" } } },
])

{
  _id: null,
  avgCourses: 2.6666666666666665
}
```

## Task-7:

```javascript
db.students.createIndex({ rollNumber: 1 })

db.students.find({ name: { $regex: "^A" } })

{
  _id: ObjectId('677cc5bc4f57c817046e50e2'),
  name: 'Arjun',
  rollNumber: 'CS1003',
  department: 'CSE',
  year: 3,
  coursesEnrolled: [
    'CS301',
    'MATH303'
  ]
}
```
