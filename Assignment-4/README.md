# Assignment-4: MongoDB Tasks

### Database:

```js
use codinggitastudents2
```

```js
db.createCollection("students");
db.createCollection("courses");
```

```js
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

```js
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

#### **Task 1: Add more students to the `students` collection**

- Add at least 5 new students to the `students` collection with unique names, roll numbers, and course enrollments.

```js
db.students.insertMany([
  {
    name: "Ishita",
    rollNumber: "CS1005",
    department: "CSE",
    year: 1,
    coursesEnrolled: ["CS101", "PHY101", "CHEM101"],
  },
  {
    name: "Veer",
    rollNumber: "CS1006",
    department: "IT",
    year: 2,
    coursesEnrolled: ["CS201", "MATH202", "DSA201"],
  },
  {
    name: "Shubham",
    rollNumber: "CS1007",
    department: "ME",
    year: 3,
    coursesEnrolled: ["ME301", "MATH303", "THERMO101"],
  },
  {
    name: "Kalpan",
    rollNumber: "CS1008",
    department: "ECE",
    year: 1,
    coursesEnrolled: ["ECE101", "MATH101", "PHY101"],
  },
  {
    name: "Garvit",
    rollNumber: "CS1009",
    department: "CSE",
    year: 4,
    coursesEnrolled: ["CS401", "AI402", "MATH402"],
  },
]);
```

#### **Task 2: Insert a new course into the `courses` collection**

- Add a new course with the following details:

  - Course Code: `CS202`
  - Name: `Data Structures`
  - Credits: 3
  - Instructor: `Prof. Krishna`

  ```js
  db.courses.insertOne({
    courseCode: "CS102",
    name: "Data Structures",
    credits: 3,
    instructor: "Prof. Krishna",
  });
  ```

#### **Task 3: Fetch a specific student's record by roll number**

- Use `find()` to fetch a student's information using their roll number (`CS1002`).

```js
db.students.find({ rollNumber: "CS1002" });

{
  _id: ObjectId('677cccf74f57c817046e50e9'),
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

#### **Task 4: Query all students who are enrolled in a particular course**

- Retrieve all students who are enrolled in "MATH101".

```js
db.students.find({ coursesEnrolled: "MATH101" });

{
  _id: ObjectId('677cccf74f57c817046e50e9'),
  name: 'Mahir',
  rollNumber: 'CS1002',
  department: 'IT',
  year: 1,
  coursesEnrolled: [
    'CS101',
    'MATH101'
  ]
}
{
  _id: ObjectId('677cccf74f57c817046e50e9'),
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

#### **Task 5: Update a student's courses**

- Update the student with roll number `CS1001` to enroll in an additional course "CS202".

```js
db.students.updateOne({ rollNumber: "CS1001" }, { $push: { coursesEnrolled: "CS202"} });

{
  _id: ObjectId('677cccf74f57c817046e50e8'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  coursesEnrolled: [
    'CS101',
    'MATH202',
    'PHY101',
    'CS202'
  ]
}
```

#### **Task 6: Remove a course from a student's courses list**

- Remove the course `MATH101` from the student `Mahir`'s list of enrolled courses.

```js
db.students.updateOne(
  { name: "Mahir" },
  { $pull: { coursesEnrolled: "MATH101" } }
);

{
  _id: ObjectId('677cccf74f57c817046e50e9'),
  name: 'Mahir',
  rollNumber: 'CS1002',
  department: 'IT',
  year: 1,
  coursesEnrolled: [
    'CS101'
  ]
}
```

#### **Task 7: Find all courses with 3 credits**

- Query the `courses` collection to find all courses where the `credits` field equals 3.

```js
db.courses.find({ credits: 3 });

{
  _id: ObjectId('677cccfe4f57c817046e50ec'),
  courseCode: 'CS101',
  name: 'Introduction to Programming',
  credits: 3,
  instructor: 'Prof. Krishna'
}
{
  _id: ObjectId('677cccfe4f57c817046e50ef'),
  courseCode: 'ECE201',
  name: 'Digital Electronics',
  credits: 3,
  instructor: 'Prof. Mahir'
}
{
  _id: ObjectId('677cdc104f57c817046e50f5'),
  courseCode: 'CS102',
  name: 'Data Structures',
  credits: 3,
  instructor: 'Prof. Krishna'
}
```

#### **Task 8: Find students who have enrolled in more than 2 courses**

- Use `$size` operator to query students who are enrolled in more than 2 courses.

```js
db.students.find({
  $expr: { $gt: [ { $size: "$coursesEnrolled" }, 2 ] }
});

{
  _id: ObjectId('677cccf74f57c817046e50e8'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  coursesEnrolled: [
    'CS101',
    'MATH202',
    'PHY101',
    'CS202'
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f0'),
  name: 'Ishita',
  rollNumber: 'CS1005',
  department: 'CSE',
  year: 1,
  coursesEnrolled: [
    'CS101',
    'PHY101',
    'CHEM101'
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f1'),
  name: 'Veer',
  rollNumber: 'CS1006',
  department: 'IT',
  year: 2,
  coursesEnrolled: [
    'CS201',
    'MATH202',
    'DSA201'
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f2'),
  name: 'Shubham',
  rollNumber: 'CS1007',
  department: 'ME',
  year: 3,
  coursesEnrolled: [
    'ME301',
    'MATH303',
    'THERMO101'
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f3'),
  name: 'Kalpan',
  rollNumber: 'CS1008',
  department: 'ECE',
  year: 1,
  coursesEnrolled: [
    'ECE101',
    'MATH101',
    'PHY101'
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f4'),
  name: 'Garvit',
  rollNumber: 'CS1009',
  department: 'CSE',
  year: 4,
  coursesEnrolled: [
    'CS401',
    'AI402',
    'MATH402'
  ]
}
```

#### **Task 9: Use the `$in` operator to find students enrolled in multiple courses**

- Use the `$in` operator to find students who are enrolled in either `CS101` or `MATH202`.

```js
db.students.find({
  coursesEnrolled: { $in: ["CS101", "MATH202"] },
});

{
  _id: ObjectId('677cccf74f57c817046e50e8'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  coursesEnrolled: [
    'CS101',
    'MATH202',
    'PHY101',
    'CS202'
  ]
}
{
  _id: ObjectId('677cccf74f57c817046e50e9'),
  name: 'Mahir',
  rollNumber: 'CS1002',
  department: 'IT',
  year: 1,
  coursesEnrolled: [
    'CS101'
  ]
}
{
  _id: ObjectId('677cccf74f57c817046e50eb'),
  name: 'Yashvi',
  rollNumber: 'CS1004',
  department: 'ECE',
  year: 2,
  coursesEnrolled: [
    'ECE201',
    'MATH202'
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f0'),
  name: 'Ishita',
  rollNumber: 'CS1005',
  department: 'CSE',
  year: 1,
  coursesEnrolled: [
    'CS101',
    'PHY101',
    'CHEM101'
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f1'),
  name: 'Veer',
  rollNumber: 'CS1006',
  department: 'IT',
  year: 2,
  coursesEnrolled: [
    'CS201',
    'MATH202',
    'DSA201'
  ]
}
```

#### **Task 10: Fetch all students from a specific department (e.g., CSE)**

- Use a query to find all students in the `CSE` department.

```js
db.students.find({ department: "CSE" });

{
  _id: ObjectId('677cccf74f57c817046e50e8'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  coursesEnrolled: [
    'CS101',
    'MATH202',
    'PHY101',
    'CS202'
  ]
}
{
  _id: ObjectId('677cccf74f57c817046e50ea'),
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
  _id: ObjectId('677cdb1a4f57c817046e50f0'),
  name: 'Ishita',
  rollNumber: 'CS1005',
  department: 'CSE',
  year: 1,
  coursesEnrolled: [
    'CS101',
    'PHY101',
    'CHEM101'
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f4'),
  name: 'Garvit',
  rollNumber: 'CS1009',
  department: 'CSE',
  year: 4,
  coursesEnrolled: [
    'CS401',
    'AI402',
    'MATH402'
  ]
}
```

#### **Task 11: Query students who are in their 3rd year**

- Retrieve students who are in the `3rd` year using the `year` field.

```js
db.students.find({ year: 3 });

{
  _id: ObjectId('677cccf74f57c817046e50ea'),
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
  _id: ObjectId('677cdb1a4f57c817046e50f2'),
  name: 'Shubham',
  rollNumber: 'CS1007',
  department: 'ME',
  year: 3,
  coursesEnrolled: [
    'ME301',
    'MATH303',
    'THERMO101'
  ]
}
```

#### **Task 12: Query students using a range for their year**

- Find all students who are in `2nd` or `3rd` year by using the `$gte` operator.

```js
db.students.find({ year: { $gte: 2 } });

{
  _id: ObjectId('677cccf74f57c817046e50e8'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  coursesEnrolled: [
    'CS101',
    'MATH202',
    'PHY101',
    'CS202'
  ]
}
{
  _id: ObjectId('677cccf74f57c817046e50ea'),
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
  _id: ObjectId('677cccf74f57c817046e50eb'),
  name: 'Yashvi',
  rollNumber: 'CS1004',
  department: 'ECE',
  year: 2,
  coursesEnrolled: [
    'ECE201',
    'MATH202'
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f1'),
  name: 'Veer',
  rollNumber: 'CS1006',
  department: 'IT',
  year: 2,
  coursesEnrolled: [
    'CS201',
    'MATH202',
    'DSA201'
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f2'),
  name: 'Shubham',
  rollNumber: 'CS1007',
  department: 'ME',
  year: 3,
  coursesEnrolled: [
    'ME301',
    'MATH303',
    'THERMO101'
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f4'),
  name: 'Garvit',
  rollNumber: 'CS1009',
  department: 'CSE',
  year: 4,
  coursesEnrolled: [
    'CS401',
    'AI402',
    'MATH402'
  ]
}
```

#### **Task 13: Count the total number of students in each department**

- Use the `$group` stage of aggregation to group students by department and count them.

```js
db.students.aggregate([
  {
    $group: {
      _id: "$department",
      studentCount: { $sum: 1 },
    },
  },
]);

{
  _id: 'ECE',
  studentCount: 2
}
{
  _id: 'CSE',
  studentCount: 4
}
{
  _id: 'ME',
  studentCount: 1
}
{
  _id: 'ME',
  studentCount: 1
}
```

#### **Task 14: Group courses by credits**

-

```js
db.courses.aggregate([
  {
    $group: {
      _id: "$credits",
      courseCount: { $sum: 1 },
    },
  },
]);

{
  _id: 3,
  courseCount: 3
}
{
  _id: 4,
  courseCount: 2
}
```

#### **Task 15: Find the highest credit course**

- Query for the course with the highest number of credits using the `$sort` operator.

```js
db.courses.find().sort({ credits: -1 }).limit(1);

{
  _id: ObjectId('677cccfe4f57c817046e50ed'),
  courseCode: 'MATH101',
  name: 'Mathematics I',
  credits: 4,
  instructor: 'Prof. Priyesha'
}
```

#### **Task 16: Use the `$and` operator for filtering students**

- Find all students who belong to the `CSE` department and are enrolled in more than 2 courses.

```js
db.students.find({
  $and: [
    { department: "CSE" },
    { $expr: { $gt: [{ $size: "$coursesEnrolled" }, 2] } },
  ],
});

{
  _id: ObjectId('677cccf74f57c817046e50e8'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  coursesEnrolled: [
    'CS101',
    'MATH202',
    'PHY101',
    'CS202'
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f0'),
  name: 'Ishita',
  rollNumber: 'CS1005',
  department: 'CSE',
  year: 1,
  coursesEnrolled: [
    'CS101',
    'PHY101',
    'CHEM101'
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f4'),
  name: 'Garvit',
  rollNumber: 'CS1009',
  department: 'CSE',
  year: 4,
  coursesEnrolled: [
    'CS401',
    'AI402',
    'MATH402'
  ]
}
```

#### **Task 17: Add a new field to all documents in the `students` collection**

- Add a new field `activeStatus` and set it to `true` for all students.

```js
db.students.updateMany(
  {},
  {
    $set: { activeStatus: true },
  }
);

{
  _id: ObjectId('677cccf74f57c817046e50e8'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  coursesEnrolled: [
    'CS101',
    'MATH202',
    'PHY101',
    'CS202'
  ],
  activeStatus: true
}
{
  _id: ObjectId('677cccf74f57c817046e50e9'),
  name: 'Mahir',
  rollNumber: 'CS1002',
  department: 'IT',
  year: 1,
  coursesEnrolled: [
    'CS101'
  ],
  activeStatus: true
},
....
```

#### **Task 18: Use `$rename` to rename a field**

- Rename the `coursesEnrolled` field in the `students` collection to `enrolledCourses`.

```js
db.students.updateMany(
  {},
  {
    $rename: { coursesEnrolled: "enrolledCourses" },
  }
);

{
  _id: ObjectId('677cccf74f57c817046e50e8'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  enrolledCourses: [
    'CS101',
    'MATH202',
    'PHY101',
    'CS202'
  ],
  activeStatus: true
}
{
  _id: ObjectId('677cccf74f57c817046e50e9'),
  name: 'Mahir',
  rollNumber: 'CS1002',
  department: 'IT',
  year: 1,
  enrolledCourses: [
    'CS101'
  ],
  activeStatus: true
},
....
```

#### **Task 19: Set default values for new fields in all student documents**

- Add a field `graduationYear` with a default value for all students.

```js
db.students.updateMany(
  {},
  {
    $set: {
      graduationYear: 2025,
    },
  }
);

{
  _id: ObjectId('677cccf74f57c817046e50e8'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  activeStatus: true,
  enrolledCourses: [
    'CS101',
    'MATH202',
    'PHY101',
    'CS202'
  ],
  graduationYear: 2025
}
{
  _id: ObjectId('677cccf74f57c817046e50e9'),
  name: 'Mahir',
  rollNumber: 'CS1002',
  department: 'IT',
  year: 1,
  activeStatus: true,
  enrolledCourses: [
    'CS101'
  ],
  graduationYear: 2025
}
....
```

#### **Task 20: Use the `$push` operator to add a new course to a student’s course list**

- Add the course "CS303" to `Mahir`’s `coursesEnrolled` list.

```js
db.students.updateOne(
  { name: "Mahir" },
  { $push: { enrolledCourses: "CS303" } }
);

{
  _id: ObjectId('677cccf74f57c817046e50e9'),
  name: 'Mahir',
  rollNumber: 'CS1002',
  department: 'IT',
  year: 1,
  activeStatus: true,
  enrolledCourses: [
    'CS101',
    'CS303'
  ],
  graduationYear: 2025
}
```

#### **Task 21: Use `$pull` to remove a course from a student's courses list**

- Remove the course `CS101` from `Jenil`’s list.

```js
db.students.updateOne(
  { name: "Jenil" },
  { $pull: { enrolledCourses: "CS101" } }
);

{
  _id: ObjectId('677cccf74f57c817046e50e8'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  activeStatus: true,
  enrolledCourses: [
    'MATH202',
    'PHY101',
    'CS202'
  ],
  graduationYear: 2025
}
```

#### **Task 22: Remove a student from the `students` collection**

- Delete the student record with roll number `CS1004`.

```js
db.students.deleteOne({ rollNumber: "CS1004" });
```

#### **Task 23: Find students who are enrolled in both `CS101` and `MATH202`**

- Use `$all` operator to find students who are enrolled in both courses.

```js
db.students.find({ enrolledCourses: { $all: ["CS101", "MATH202"] } });
```

#### **Task 24: Use `$regex` to search for students whose name starts with "A"**

- Use regular expressions to search for students whose names begin with the letter "A".

```js
db.students.find({ name: { $regex: "^A" } });

{
  _id: ObjectId('677cccf74f57c817046e50ea'),
  name: 'Arjun',
  rollNumber: 'CS1003',
  department: 'CSE',
  year: 3,
  activeStatus: true,
  enrolledCourses: [
    'CS301',
    'MATH303'
  ],
  graduationYear: 2025
}
```

#### **Task 25: Use `$exists` to find students with enrolled courses**

- Query students who have an entry in the `coursesEnrolled` array.

```js
db.students.find({ enrolledCourses: { $exists: true } });

{
  _id: ObjectId('677cccf74f57c817046e50e8'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  activeStatus: true,
  enrolledCourses: [
    'MATH202',
    'PHY101',
    'CS202'
  ],
  graduationYear: 2025
}
{
  _id: ObjectId('677cccf74f57c817046e50e9'),
  name: 'Mahir',
  rollNumber: 'CS1002',
  department: 'IT',
  year: 1,
  activeStatus: true,
  enrolledCourses: [
    'CS101',
    'CS303'
  ],
  graduationYear: 2025
}
....
```

#### **Task 26: Add a field to store students' grades for each course**

- Add a new field `grades` to the `students` collection and store an array of grades for each course.

```js
db.students.updateMany(
  {},
  {
    $set: {
      grades: [85, 90, 78],
    },
  }
);

{
  _id: ObjectId('677cccf74f57c817046e50e8'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  activeStatus: true,
  enrolledCourses: [
    'MATH202',
    'PHY101',
    'CS202'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cccf74f57c817046e50e9'),
  name: 'Mahir',
  rollNumber: 'CS1002',
  department: 'IT',
  year: 1,
  activeStatus: true,
  enrolledCourses: [
    'CS101',
    'CS303'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cccf74f57c817046e50ea'),
  name: 'Arjun',
  rollNumber: 'CS1003',
  department: 'CSE',
  year: 3,
  activeStatus: true,
  enrolledCourses: [
    'CS301',
    'MATH303'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
....
```

#### **Task 27: Use `$elemMatch` to query students enrolled in specific courses**

- Find students enrolled in `CS101` and have the grade `A`.

```js
db.students.find({
  enrolledCourses: { $elemMatch: { $eq: "CS101" } },
  grades: { $elemMatch: { $eq: 90 } },
});

{
  _id: ObjectId('677cccf74f57c817046e50e9'),
  name: 'Mahir',
  rollNumber: 'CS1002',
  department: 'IT',
  year: 1,
  activeStatus: true,
  enrolledCourses: [
    'CS101',
    'CS303'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f0'),
  name: 'Ishita',
  rollNumber: 'CS1005',
  department: 'CSE',
  year: 1,
  activeStatus: true,
  enrolledCourses: [
    'CS101',
    'PHY101',
    'CHEM101'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
```

#### **Task 28: Use `$size` operator to query students with exactly 2 courses enrolled**

- Query students who have enrolled in exactly two courses.

```js
db.students.find({
  enrolledCourses: { $size: 2 },
});

{
  _id: ObjectId('677cccf74f57c817046e50e9'),
  name: 'Mahir',
  rollNumber: 'CS1002',
  department: 'IT',
  year: 1,
  activeStatus: true,
  enrolledCourses: [
    'CS101',
    'CS303'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cccf74f57c817046e50e9'),
  name: 'Mahir',
  rollNumber: 'CS1002',
  department: 'IT',
  year: 1,
  activeStatus: true,
  enrolledCourses: [
    'CS101',
    'CS303'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
```

#### **Task 29: Perform a text search for a course title**

- Use text indexing to search for the course `Digital Electronics` in the `courses` collection.

```js
db.courses.createIndex({ name: "text" });

name_text

db.courses.find({ $text: { $search: "Digital Electronics" } });

{
  _id: ObjectId('677cccfe4f57c817046e50ef'),
  courseCode: 'ECE201',
  name: 'Digital Electronics',
  credits: 3,
  instructor: 'Prof. Mahir'
}
```

#### **Task 30: Create a compound index on department and year**

- Create a compound index on the fields `department` and `year` for better querying performance.

```js
db.students.createIndex({ department: 1, year: 1 });

department_1_year_1;
```

#### **Task 31: Use `$sort` to order students by their roll number**

- Sort the students in ascending order of their roll number.

```js
db.students.find().sort({ rollNumber: 1 });

{
  _id: ObjectId('677cccf74f57c817046e50e8'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  activeStatus: true,
  enrolledCourses: [
    'MATH202',
    'PHY101',
    'CS202'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cccf74f57c817046e50e9'),
  name: 'Mahir',
  rollNumber: 'CS1002',
  department: 'IT',
  year: 1,
  activeStatus: true,
  enrolledCourses: [
    'CS101',
    'CS303'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cccf74f57c817046e50ea'),
  name: 'Arjun',
  rollNumber: 'CS1003',
  department: 'CSE',
  year: 3,
  activeStatus: true,
  enrolledCourses: [
    'CS301',
    'MATH303'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f0'),
  name: 'Ishita',
  rollNumber: 'CS1005',
  department: 'CSE',
  year: 1,
  activeStatus: true,
  enrolledCourses: [
    'CS101',
    'PHY101',
    'CHEM101'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f1'),
  name: 'Veer',
  rollNumber: 'CS1006',
  department: 'IT',
  year: 2,
  activeStatus: true,
  enrolledCourses: [
    'CS201',
    'MATH202',
    'DSA201'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f2'),
  name: 'Shubham',
  rollNumber: 'CS1007',
  department: 'ME',
  year: 3,
  activeStatus: true,
  enrolledCourses: [
    'ME301',
    'MATH303',
    'THERMO101'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f3'),
  name: 'Kalpan',
  rollNumber: 'CS1008',
  department: 'ECE',
  year: 1,
  activeStatus: true,
  enrolledCourses: [
    'ECE101',
    'MATH101',
    'PHY101'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f4'),
  name: 'Garvit',
  rollNumber: 'CS1009',
  department: 'CSE',
  year: 4,
  activeStatus: true,
  enrolledCourses: [
    'CS401',
    'AI402',
    'MATH402'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
```

#### **Task 32: Create a unique index on the roll number**

- Create a unique index to ensure that the roll numbers in the `students` collection are unique.

```js
db.students.createIndex({ rollNumber: 1 }, { unique: true });

rollNumber_1;
```

#### **Task 33: Update the course name in the `courses` collection**

- Update the name of the course `CS101` to `Intro to Programming`.

```js
db.courses.updateOne(
  { name: "CS101" },
  { $set: { name: "Intro to Programming" } }
);

{
  _id: ObjectId('677cccfe4f57c817046e50ec'),
  courseCode: 'CS101',
  name: 'Intro to Programming',
  credits: 3,
  instructor: 'Prof. Krishna'
}
```

#### **Task 34: Create a backup of the `CodingGitaStudents` database**

- Use `mongodump` to back up the entire `CodingGitaStudents` database.

```js

```

#### **Task 35: Restore the `CodingGitaStudents` database from the backup**

- Use `mongorestore` to restore the database after a backup.

```js

```

#### **Task 36: Use `$project` to reshape data in aggregation**

- Project only the `name` and `department` of students using an aggregation query.

```js
db.students.aggregate([
  {
    $project: {
      name: 1,
      department: 1,
    },
  },
]);

{
  _id: ObjectId('677cccf74f57c817046e50e8'),
  name: 'Jenil',
  department: 'CSE'
}
{
  _id: ObjectId('677cccf74f57c817046e50e9'),
  name: 'Mahir',
  department: 'IT'
}
{
  _id: ObjectId('677cccf74f57c817046e50ea'),
  name: 'Arjun',
  department: 'CSE'
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f0'),
  name: 'Ishita',
  department: 'CSE'
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f1'),
  name: 'Veer',
  department: 'IT'
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f2'),
  name: 'Shubham',
  department: 'ME'
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f3'),
  name: 'Kalpan',
  department: 'ECE'
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f4'),
  name: 'Garvit',
  department: 'CSE'
}
```

#### **Task 37: Use `$unwind` to deconstruct the courses array**

- Use `$unwind` to split the `coursesEnrolled` array into individual documents.

```js
db.students.aggregate([
  {
    $unwind: "$coursesEnrolled",
  },
]);

{
  _id: ObjectId('677cccf74f57c817046e50e8'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  activeStatus: true,
  enrolledCourses: 'MATH202',
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cccf74f57c817046e50e8'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  activeStatus: true,
  enrolledCourses: 'PHY101',
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cccf74f57c817046e50e8'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  activeStatus: true,
  enrolledCourses: 'CS202',
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cccf74f57c817046e50e9'),
  name: 'Mahir',
  rollNumber: 'CS1002',
  department: 'IT',
  year: 1,
  activeStatus: true,
  enrolledCourses: 'CS101',
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cccf74f57c817046e50e9'),
  name: 'Mahir',
  rollNumber: 'CS1002',
  department: 'IT',
  year: 1,
  activeStatus: true,
  enrolledCourses: 'CS303',
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
....
```

#### **Task 38: Use `$limit` to retrieve only the first 3 students**

- Use `$limit` to limit the result to the first 3 students in the `students` collection.

```js
db.students.aggregate([
  {
    $limit: 3,
  },
]);

{
  _id: ObjectId('677cccf74f57c817046e50e8'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  activeStatus: true,
  enrolledCourses: [
    'MATH202',
    'PHY101',
    'CS202'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cccf74f57c817046e50e9'),
  name: 'Mahir',
  rollNumber: 'CS1002',
  department: 'IT',
  year: 1,
  activeStatus: true,
  enrolledCourses: [
    'CS101',
    'CS303'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cccf74f57c817046e50ea'),
  name: 'Arjun',
  rollNumber: 'CS1003',
  department: 'CSE',
  year: 3,
  activeStatus: true,
  enrolledCourses: [
    'CS301',
    'MATH303'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
```

#### **Task 39: Use `$skip` to skip the first 2 students and get the rest**

- Use `$skip` to fetch all students except the first two.

```js
db.students.aggregate([
  {
    $skip: 2,
  },
]);

{
  _id: ObjectId('677cccf74f57c817046e50ea'),
  name: 'Arjun',
  rollNumber: 'CS1003',
  department: 'CSE',
  year: 3,
  activeStatus: true,
  enrolledCourses: [
    'CS301',
    'MATH303'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f0'),
  name: 'Ishita',
  rollNumber: 'CS1005',
  department: 'CSE',
  year: 1,
  activeStatus: true,
  enrolledCourses: [
    'CS101',
    'PHY101',
    'CHEM101'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f1'),
  name: 'Veer',
  rollNumber: 'CS1006',
  department: 'IT',
  year: 2,
  activeStatus: true,
  enrolledCourses: [
    'CS201',
    'MATH202',
    'DSA201'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f2'),
  name: 'Shubham',
  rollNumber: 'CS1007',
  department: 'ME',
  year: 3,
  activeStatus: true,
  enrolledCourses: [
    'ME301',
    'MATH303',
    'THERMO101'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f3'),
  name: 'Kalpan',
  rollNumber: 'CS1008',
  department: 'ECE',
  year: 1,
  activeStatus: true,
  enrolledCourses: [
    'ECE101',
    'MATH101',
    'PHY101'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f4'),
  name: 'Garvit',
  rollNumber: 'CS1009',
  department: 'CSE',
  year: 4,
  activeStatus: true,
  enrolledCourses: [
    'CS401',
    'AI402',
    'MATH402'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
```

#### **Task 40: Use `$lookup` to join student data with courses**

- Use `$lookup` to fetch the course information for students.

```js
db.students.aggregate([
  {
    $lookup: {
      from: "courses",
      localField: "enrolledCourses",
      foreignField: "courseCode",
      as: "courseDetails",
    },
  },
]);

{
  _id: ObjectId('677cccf74f57c817046e50e8'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  activeStatus: true,
  enrolledCourses: [
    'MATH202',
    'PHY101',
    'CS202'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ],
  courseDetails: [
    {
      _id: ObjectId('677cccfe4f57c817046e50ee'),
      courseCode: 'PHY101',
      name: 'Physics I',
      credits: 4,
      instructor: 'Prof. Arjun'
    }
  ]
}
{
  _id: ObjectId('677cccf74f57c817046e50e9'),
  name: 'Mahir',
  rollNumber: 'CS1002',
  department: 'IT',
  year: 1,
  activeStatus: true,
  enrolledCourses: [
    'CS101',
    'CS303'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ],
  courseDetails: [
    {
      _id: ObjectId('677cccfe4f57c817046e50ec'),
      courseCode: 'CS101',
      name: 'Intro to Programming',
      credits: 3,
      instructor: 'Prof. Krishna'
    }
  ]
}
{
  _id: ObjectId('677cccf74f57c817046e50ea'),
  name: 'Arjun',
  rollNumber: 'CS1003',
  department: 'CSE',
  year: 3,
  activeStatus: true,
  enrolledCourses: [
    'CS301',
    'MATH303'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ],
  courseDetails: []
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f0'),
  name: 'Ishita',
  rollNumber: 'CS1005',
  department: 'CSE',
  year: 1,
  activeStatus: true,
  enrolledCourses: [
    'CS101',
    'PHY101',
    'CHEM101'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ],
  courseDetails: [
    {
      _id: ObjectId('677cccfe4f57c817046e50ec'),
      courseCode: 'CS101',
      name: 'Intro to Programming',
      credits: 3,
      instructor: 'Prof. Krishna'
    },
    {
      _id: ObjectId('677cccfe4f57c817046e50ee'),
      courseCode: 'PHY101',
      name: 'Physics I',
      credits: 4,
      instructor: 'Prof. Arjun'
    }
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f1'),
  name: 'Veer',
  rollNumber: 'CS1006',
  department: 'IT',
  year: 2,
  activeStatus: true,
  enrolledCourses: [
    'CS201',
    'MATH202',
    'DSA201'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ],
  courseDetails: []
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f2'),
  name: 'Shubham',
  rollNumber: 'CS1007',
  department: 'ME',
  year: 3,
  activeStatus: true,
  enrolledCourses: [
    'ME301',
    'MATH303',
    'THERMO101'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ],
  courseDetails: []
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f3'),
  name: 'Kalpan',
  rollNumber: 'CS1008',
  department: 'ECE',
  year: 1,
  activeStatus: true,
  enrolledCourses: [
    'ECE101',
    'MATH101',
    'PHY101'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ],
  courseDetails: [
    {
      _id: ObjectId('677cccfe4f57c817046e50ed'),
      courseCode: 'MATH101',
      name: 'Mathematics I',
      credits: 4,
      instructor: 'Prof. Priyesha'
    },
    {
      _id: ObjectId('677cccfe4f57c817046e50ee'),
      courseCode: 'PHY101',
      name: 'Physics I',
      credits: 4,
      instructor: 'Prof. Arjun'
    }
  ]
}
.....
```

#### **Task 41: Create a new collection for storing `studentFeedback`**

- Create a collection `studentFeedback` with fields: `studentRollNumber`, `feedbackText`, `date`.

```js
db.createCollection("studentFeedback");
```

```js
db.studentFeedback.insertMany([
  {
    studentRollNumber: "CS1001",
    feedbackText: "The course material is very helpful.",
    date: new Date("2025-01-01"),
  },
  {
    studentRollNumber: "CS1002",
    feedbackText: "The instructor was very engaging.",
    date: new Date("2025-01-03"),
  },
  {
    studentRollNumber: "CS1003",
    feedbackText: "More practical sessions would be great.",
    date: new Date("2025-01-05"),
  },
  {
    studentRollNumber: "CS1004",
    feedbackText: "The course pace was perfect.",
    date: new Date("2025-01-07"),
  },
  {
    studentRollNumber: "CS1005",
    feedbackText: "The assignments were challenging but fun.",
    date: new Date("2025-01-09"),
  },
]);
```

#### **Task 42: Query the `studentFeedback` collection to find feedback from a specific student**

- Use `find()` to retrieve feedback from `Jenil`.

```js
db.students.find({ name: "Jenil" }, { rollNumber: 1, _id: 0 });

{
  rollNumber: 'CS1001'
}

db.studentFeedback.find({ studentRollNumber: "CS1001" }).pretty();

{
  _id: ObjectId('677d1ddd55ea85235e7e7572'),
  studentRollNumber: 'CS1001',
  feedbackText: 'The course material is very helpful.',
  date: 2025-01-01T00:00:00.000Z
}
```

#### **Task 43: Use `$set` to update multiple fields at once**

- Use the `$set` operator to update the `department` and `coursesEnrolled` fields for `Arjun`.

```js
db.students.updateOne(
  { name: "Arjun" },
  {
    $set: {
      department: "Computer Science",
      enrolledCourses: ["Data Structures", "Algorithms", "Web Development"],
    },
  }
);

{
  _id: ObjectId('677cccf74f57c817046e50ea'),
  name: 'Arjun',
  rollNumber: 'CS1003',
  department: 'Computer Science',
  year: 3,
  activeStatus: true,
  enrolledCourses: [
    'Data Structures',
    'Algorithms',
    'Web Development'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
```

#### **Task 44: Create a custom index on the `coursesEnrolled` field**

- Create an index on the `coursesEnrolled` array for faster querying.

```js
db.students.createIndex({ enrolledCourses: 1 });

enrolledCourses_1;
```

#### **Task 45: Perform a query on nested documents in `students` collection**

- Query for students who have grades `A` in their courses.

```js
db.students
  .find({
    grades: 90,
  })
  .pretty();

  {
  _id: ObjectId('677cccf74f57c817046e50e8'),
  name: 'Jenil',
  rollNumber: 'CS1001',
  department: 'CSE',
  year: 2,
  activeStatus: true,
  enrolledCourses: [
    'MATH202',
    'PHY101',
    'CS202'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cccf74f57c817046e50e9'),
  name: 'Mahir',
  rollNumber: 'CS1002',
  department: 'IT',
  year: 1,
  activeStatus: true,
  enrolledCourses: [
    'CS101',
    'CS303'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cccf74f57c817046e50ea'),
  name: 'Arjun',
  rollNumber: 'CS1003',
  department: 'Computer Science',
  year: 3,
  activeStatus: true,
  enrolledCourses: [
    'Data Structures',
    'Algorithms',
    'Web Development'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f0'),
  name: 'Ishita',
  rollNumber: 'CS1005',
  department: 'CSE',
  year: 1,
  activeStatus: true,
  enrolledCourses: [
    'CS101',
    'PHY101',
    'CHEM101'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
{
  _id: ObjectId('677cdb1a4f57c817046e50f1'),
  name: 'Veer',
  rollNumber: 'CS1006',
  department: 'IT',
  year: 2,
  activeStatus: true,
  enrolledCourses: [
    'CS201',
    'MATH202',
    'DSA201'
  ],
  graduationYear: 2025,
  grades: [
    85,
    90,
    78
  ]
}
....
```
