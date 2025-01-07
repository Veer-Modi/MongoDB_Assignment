# Assignment-2

```javascript
use codinggita2
```

```javascript
db.createCollection("students");
db.createCollection("subjects");
```

```javascript
db.students.insertMany([
  {
    name: "Jenil",
    rollNumber: 101,
    department: "Computer Science",
    year: 2,
    subjectsEnrolled: ["React", "NodeJS", "MongoDB"],
  },
  {
    name: "Mahir",
    rollNumber: 102,
    department: "Computer Science",
    year: 2,
    subjectsEnrolled: ["React", "NodeJS"],
  },
  {
    name: "Arjun",
    rollNumber: 103,
    department: "Electrical Engineering",
    year: 3,
    subjectsEnrolled: ["Circuit Theory", "Electrical Machines"],
  },
]);
```

```javascript
db.subjects.insertMany([
  {
    subjectName: "React",
    topics: ["JSX", "Components", "State", "Props", "Hooks"],
  },
  {
    subjectName: "NodeJS",
    topics: ["Modules", "Express", "File System", "Asynchronous Programming"],
  },
  {
    subjectName: "MongoDB",
    topics: ["Database Design", "CRUD Operations", "Aggregation", "Indexes"],
  },
]);
```

## Task-1:

```javascript
db.students.insertMany([
  {
    name: "Garvit",
    rollNumber: 104,
    department: "Computer Science",
    year: 1,
    subjectsEnrolled: ["Python", "Data Structures"],
  },
  {
    name: "Yashvi",
    rollNumber: 105,
    department: "Mechanical Engineering",
    year: 3,
    subjectsEnrolled: ["Thermodynamics", "Fluid Mechanics", "Material Science"],
  },
  {
    name: "Ishita",
    rollNumber: 106,
    department: "Computer Science",
    year: 4,
    subjectsEnrolled: ["AI", "Machine Learning", "Data Science"],
  },
  {
    name: "Shubham",
    rollNumber: 107,
    department: "Civil Engineering",
    year: 2,
    subjectsEnrolled: ["Structural Analysis", "Concrete Technology"],
  },
  {
    name: "Veer",
    rollNumber: 108,
    department: "Electronics Engineering",
    year: 3,
    subjectsEnrolled: ["Microprocessors", "Embedded Systems"],
  },
]);
```

## Task-2:

```Javascript
db.subjects.insertMany([
  {
    "subjectName": "C++",
    "topics": [
      "Syntax and Basics",
      "OOP Concepts",
      "STL (Standard Template Library)",
      "Pointers and Memory Management",
      "File Handling"
    ]
  },
  {
    "subjectName": "JavaScript",
    "topics": [
      "Variables and Data Types",
      "Functions and Scope",
      "DOM Manipulation",
      "ES6 Features",
      "Asynchronous Programming"
    ]
  },
  {
    "subjectName": "HTML",
    "topics": [
      "Elements and Attributes",
      "Forms and Inputs",
      "Semantic HTML",
      "Tables",
      "Multimedia Elements"
    ]
  },
  {
    "subjectName": "CSS",
    "topics": [
      "Selectors and Properties",
      "Flexbox and Grid",
      "Responsive Design",
      "Animations",
      "Media Queries"
    ]
  }
])
```

## Task-3:

```javascript
db.students.find({subjectsEnrolled:"NodeJS"})

{
  _id: ObjectId('677c00ba7dc818802c3bec95'),
  name: 'Jenil',
  rollNumber: 101,
  department: 'Computer Science',
  year: 2,
  subjectsEnrolled: [
    'React',
    'NodeJS',
    'MongoDB'
  ]
}
{
  _id: ObjectId('677c00ba7dc818802c3bec95'),
  name: 'Jenil',
  rollNumber: 101,
  department: 'Computer Science',
  year: 2,
  subjectsEnrolled: [
    'React',
    'NodeJS',
    'MongoDB'
  ]
}
```

## Task-4:

```javascript
db.subjects.updateOne(
  { subjectName: "NodeJS" },
  { $push: { topics: "Event Loop" } }
)

{
  _id: ObjectId('677c00d37dc818802c3bec99'),
  subjectName: 'NodeJS',
  topics: [
    'Modules',
    'Express',
    'File System',
    'Asynchronous Programming',
    'Event Loop'
  ]
}
```

## Task-5:

```javascript
db.subjects.find({
  topics: { $size: 4 },
})

{
  _id: ObjectId('677c00d37dc818802c3bec9a'),
  subjectName: 'MongoDB',
  topics: [
    'Database Design',
    'CRUD Operations',
    'Aggregation',
    'Indexes'
  ]
}
```

## Task-6:

```javascript
db.students.updateOne(
  { name: "Jenil" },
  { $set: { subjectsEnrolled: ["React","NodeJS","MongoDB","React Native"]} }

  {
  _id: ObjectId('677c00ba7dc818802c3bec95'),
  name: 'Jenil',
  rollNumber: 101,
  department: 'Computer Science',
  year: 2,
  subjectsEnrolled: [
    'React',
    'NodeJS',
    'MongoDB',
    'React Native'
  ]
}
)
```

## Task-7:

```javascript
db.students.find({}, { name: 1, subjectcEnrolled: 1 })
???
```

## Task-8:

```javascript
db.students.updateMany(
  { department:"Computer Science" },
  { $set: { year:3 }}
)

{
  _id: ObjectId('677c00077dc818802c3bec90'),
  name: 'Garvit',
  rollNumber: 104,
  department: 'Computer Science',
  year: 3,
  subjectsEnrolled: [
    'Python',
    'Data Structures'
  ]
}
{
  _id: ObjectId('677c00077dc818802c3bec92'),
  name: 'Ishita',
  rollNumber: 106,
  department: 'Computer Science',
  year: 3,
  subjectsEnrolled: [
    'AI',
    'Machine Learning',
    'Data Science'
  ]
}
{
  _id: ObjectId('677c00ba7dc818802c3bec95'),
  name: 'Jenil',
  rollNumber: 101,
  department: 'Computer Science',
  year: 3,
  subjectsEnrolled: [
    'React',
    'NodeJS',
    'MongoDB',
    'React Native'
  ]
}
{
  _id: ObjectId('677c00ba7dc818802c3bec96'),
  name: 'Mahir',
  rollNumber: 102,
  department: 'Computer Science',
  year: 3,
  subjectsEnrolled: [
    'React',
    'NodeJS'
  ]
}
```

## Task-9:

```javascript
db.subjects.updateOne(
  { subjectName: "React" },
  { $push: { topics: "Context API" } }
)

db.subjects.updateOne(
  { subjectName: "NodeJS" },
  { $push: { topics: "Streams" } }
)

db.subjects.updateOne(
  { subjectName: "NodeJS" },
  { $push: { topics: "Streams" } }
)

{
  _id: ObjectId('677c00d37dc818802c3bec98'),
  subjectName: 'React',
  topics: [
    'JSX',
    'Components',
    'State',
    'Props',
    'Hooks',
    'Context API'
  ]
}
{
  _id: ObjectId('677c00d37dc818802c3bec99'),
  subjectName: 'NodeJS',
  topics: [
    'Modules',
    'Express',
    'File System',
    'Asynchronous Programming',
    'Event Loop',
    'Streams'
  ]
}
{
  _id: ObjectId('677c00d37dc818802c3bec9a'),
  subjectName: 'MongoDB',
  topics: [
    'Database Design',
    'CRUD Operations',
    'Aggregation',
    'Indexes',
    'Sharding'
  ]
}
```

## Task-10:

```javascript
db.subjects.updateOne(
  { subjectName: "NodeJS" },
  { $pull: { topics: "Express" } }
)

{
  _id: ObjectId('677c00d37dc818802c3bec99'),
  subjectName: 'NodeJS',
  topics: [
    'Modules',
    'File System',
    'Asynchronous Programming',
    'Event Loop',
    'Streams'
  ]
}
```

## Task-11:

```javascript
db.students.find(
  { year:{$gte:2}}
)

{
  _id: ObjectId('677c00077dc818802c3bec90'),
  name: 'Garvit',
  rollNumber: 104,
  department: 'Computer Science',
  year: 3,
  subjectsEnrolled: [
    'Python',
    'Data Structures'
  ]
}
{
  _id: ObjectId('677c00077dc818802c3bec91'),
  name: 'Yashvi',
  rollNumber: 105,
  department: 'Mechanical Engineering',
  year: 3,
  subjectsEnrolled: [
    'Thermodynamics',
    'Fluid Mechanics',
    'Material Science'
  ]
}
{
  _id: ObjectId('677c00077dc818802c3bec92'),
  name: 'Ishita',
  rollNumber: 106,
  department: 'Computer Science',
  year: 3,
  subjectsEnrolled: [
    'AI',
    'Machine Learning',
    'Data Science'
  ]
}
{
  _id: ObjectId('677c00077dc818802c3bec93'),
  name: 'Shubham',
  rollNumber: 107,
  department: 'Civil Engineering',
  year: 2,
  subjectsEnrolled: [
    'Structural Analysis',
    'Concrete Technology'
  ]
}
{
  _id: ObjectId('677c00077dc818802c3bec94'),
  name: 'Veer',
  rollNumber: 108,
  department: 'Electronics Engineering',
  year: 3,
  subjectsEnrolled: [
    'Microprocessors',
    'Embedded Systems'
  ]
}
{
  _id: ObjectId('677c00ba7dc818802c3bec95'),
  name: 'Jenil',
  rollNumber: 101,
  department: 'Computer Science',
  year: 3,
  subjectsEnrolled: [
    'React',
    'NodeJS',
    'MongoDB',
    'React Native'
  ]
}
{
  _id: ObjectId('677c00ba7dc818802c3bec96'),
  name: 'Mahir',
  rollNumber: 102,
  department: 'Computer Science',
  year: 3,
  subjectsEnrolled: [
    'React',
    'NodeJS'
  ]
}
{
  _id: ObjectId('677c00ba7dc818802c3bec97'),
  name: 'Arjun',
  rollNumber: 103,
  department: 'Electrical Engineering',
  year: 3,
  subjectsEnrolled: [
    'Circuit Theory',
    'Electrical Machines'
  ]
}
```

## Task-12:

```javascript
db.students.deleteOne({
  rollNumber: 101,
});
```

## Task-13:

```javascript
db.students.deleteMany({
  department: "Electrical Engineering",
});
```

## Task-14:

```javascript
db.subjects.find();
```

## Task-15:

```javascript
db.students.aggregate([
  {
    $project: {
      name: 1,
      subjectsCount: { $size: "$subjectsEnrolled" },
    },
  },
])

{
  _id: ObjectId('677c00077dc818802c3bec90'),
  name: 'Garvit',
  subjectsCount: 2
}
{
  _id: ObjectId('677c00077dc818802c3bec91'),
  name: 'Yashvi',
  subjectsCount: 3
}
{
  _id: ObjectId('677c00077dc818802c3bec92'),
  name: 'Ishita',
  subjectsCount: 3
}
{
  _id: ObjectId('677c00077dc818802c3bec93'),
  name: 'Shubham',
  subjectsCount: 2
}
{
  _id: ObjectId('677c00077dc818802c3bec94'),
  name: 'Veer',
  subjectsCount: 2
}
{
  _id: ObjectId('677c00ba7dc818802c3bec96'),
  name: 'Mahir',
  subjectsCount: 2
}
{
  _id: ObjectId('677c00ba7dc818802c3bec97'),
  name: 'Arjun',
  subjectsCount: 2
}
```
