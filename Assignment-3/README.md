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

