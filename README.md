# School Management and Timetable Program

## Summary
This program is designed to streamline the management of staff and pupils in a school setting. 
It offers a comprehensive approach to handling various administrative tasks, primarily focusing on the timetable generating.

## Description of usage
Students, teachers and subjects must be added to the program. 
Then assign teachers to subjects(one teacher can teach many subjects), students to classes, 
subjects to classes and teachers to classes(there can be several teachers of one subject). Classes can be created automatically using a chosen strategy(alphabetically or by age). 
The allocation of teachers can also be done automatically. If all parameters are set, the application can create a timetable.



### Student
###### StudentRequest

```json
{
    "firstName":"Jan",
    "lastName":"Kowalski",
    "pesel":"12313153",
    "birthday":"21-03-2008",
    "phone":"231 312 231",
    "email":"jankowalski",
    "city":"Warszawa",
    "street":"Dzierżynskiego",
    "houseNumber":1,
    "flatNumber":7,
    "gradeToBirthdayDeflection":1
}
```

###### StudentDto
```json
{
  "id": 1,
  "firstName": "Jan",
  "lastName": "Kowalski",
  "className": "Not assigned"
}
```

#### Endpoints





##### Add students



###### Single Student

- **Endpoint:** `POST api/students`
- **Request Body:**
    - `StudentRequest` object representing a single student.
- **Response:**
    - Returns the saved student as `StudentDto` if successful.
    - `400 Bad Request` if a student with the same ID already exists.
    - `500 Internal Server Error` for other errors.

###### Multiple Students
- **Endpoint:** `POST api/students/list`
- **Request Body:**
    - List of `StudentRequest` objects representing multiple students.
- **Response:**
    - Returns a list of saved students as `List<StudentDto>` if successful.
    - `400 Bad Request` if there is an error in the input data.
    - `500 Internal Server Error` for other errors.



##### Read Students

###### Single Student
- **Endpoint:** `GET api/students/{id}`
- **Path Variable:**
    - `id` - ID of the student to retrieve.
- **Response:**
    - Returns the student as `StudentDto` if found.
    - `404 Not Found` if the student with the specified ID does not exist.
    - `500 Internal Server Error` for other errors.

###### All Students
- **Endpoint:** `GET api/students`
- **Response:**
    - Returns a list of all students as `List<StudentDto>` if successful.
    - `500 Internal Server Error` for other errors.

##### Update a Student

- **Endpoint:** `PUT api/students/{id}`
- **Path Variable:**
    - `id` - ID of the student to update.
- **Request Body:**
    - `StudentRequest` object representing the updated student information.
- **Response:**
    - Returns the updated student as `StudentDto` if successful.
    - `400 Bad Request` if the student with the specified ID does not exist.
    - `500 Internal Server Error` for other errors.

##### Delete a Student

- **Endpoint:** `DELETE api/students/{id}`
- **Path Variable:**
    - `id` - ID of the student to delete.
- **Response:**
    - Returns "Student deleted." if successful.
    - `404 Not Found` if the student with the specified ID does not exist.
    - `500 Internal Server Error` for other errors.


### Teacher

This Spring Boot application provides RESTful endpoints for managing teacher information. It follows CRUD operations (Create, Read, Update, Delete) for a `Teacher` entity.

###### TeacherRequest

```json
{
  "firstName":"Jan",
  "lastName":"Kowalski",
  "pesel":"123123123",
  "birthday":"21-03-1923",
  "phone":"231 312 231",
  "email":"jankowalski@gmail.com",
  "city":"Warszawa",
  "street":"Dzierżynskiego",
  "houseNumber":13,
  "flatNumber":7,
  "salary": 5000,
  "hoursPerWeek":40
}
```

###### TeacherDto

```json
{
  "id": 1,
  "firstName": "Jan",
  "lastName": "Kowalski",
  "teachingSubjects": [],
  "teachingClasses": []
}
```

#### Endpoints

##### Add a Teacher

###### Single Teacher
- **Endpoint:** `POST api/teachers`
- **Request Body:**
    - `TeacherRequest` object representing a single teacher.
- **Response:**
    - Returns the saved teacher as `TeacherDto` if successful.
    - `400 Bad Request` if a teacher with the same ID already exists.
    - `500 Internal Server Error` for other errors.

###### Multiple Teachers
- **Endpoint:** `POST api/teachers/list`
- **Request Body:**
    - List of `TeacherRequest` objects representing multiple teachers.
- **Response:**
    - Returns a list of saved teachers as `List<TeacherDto>` if successful.
    - `400 Bad Request` if there is an error in the input data.
    - `500 Internal Server Error` for other errors.

##### Retrieve Teachers

###### Single Teacher
- **Endpoint:** `GET api/teachers/{id}`
- **Path Variable:**
    - `id` - ID of the teacher to retrieve.
- **Response:**
    - Returns the teacher as `TeacherDto` if found.
    - `404 Not Found` if the teacher with the specified ID does not exist.
    - `500 Internal Server Error` for other errors.

###### Multiple Teachers
- **Endpoint:** `GET api/teachers/all`
- **Response:**
    - Returns a list of all teachers as `List<TeacherDto>` if successful.
    - `500 Internal Server Error` for other errors.

##### Update a Teacher

- **Endpoint:** `PUT api/teachers/{id}`
- **Path Variable:**
    - `id` - ID of the teacher to update.
- **Request Body:**
    - `TeacherRequest` object representing the updated teacher information.
- **Response:**
    - Returns the updated teacher as `TeacherDto` if successful.
    - `500 Internal Server Error` for other errors.

##### Delete a Teacher

- **Endpoint:** `DELETE api/teachers/{id}`
- **Path Variable:**
    - `id` - ID of the teacher to delete.
- **Response:**
    - Returns the deleted teacher as `TeacherDto` if successful.
    - `404 Not Found` if the teacher with the specified ID does not exist.
    - `500 Internal Server Error` for other errors.

#### Exception Handling

- The API handles specific exceptions like `EntityExistsException`, `EntityNotFoundException`, and `DataIntegrityViolationException`.
- Provides meaningful error messages and appropriate HTTP status codes for better understanding.

#### Usage

- Use tools like cURL or Postman for testing the API.

### School Subject

This Spring Boot application provides RESTful endpoints for managing school subjects. 
It supports basic CRUD operations (Create, Read, Update, Delete) for a `SchoolSubject` entity.

##### SchoolSubjectRequest

```json
{
  "name": "History",
  "hoursPerWeekPerGrade": {
    "1":"2",
    "2":"2",
    "3":"2",
    "4":"2",
    "5":"2",
    "6":"2",
    "7":"2",
    "8":"2"
  }
}
```

###### SchoolSubjectDto

```json
{
  "id": 1,
  "name": "History",
  "hoursPerWeek": {
    "II": 2,
    "VI": 2,
    "V": 2,
    "VII": 2,
    "III": 2,
    "I": 2,
    "VIII": 2,
    "IV": 2
  }
}
```

#### Endpoints

##### Add a School Subject

###### Single School Subject
- **Endpoint:** `POST api/school-subjects`
- **Request Body:**
  - `SchoolSubjectRequest` object representing a single school subject.
- **Response:**
  - Returns the saved school subject as `SchoolSubjectDto` if successful.
  - `400 Bad Request` if a school subject with the same ID already exists.
  - `500 Internal Server Error` for other errors.

###### Multiple School Subjects
- **Endpoint:** `POST api/school-subjects/list`
- **Request Body:**
  - List of `SchoolSubjectRequest` objects representing multiple school subjects.
- **Response:**
  - Returns a list of saved school subjects as `List<SchoolSubjectDto>` if successful.
  - `500 Internal Server Error` for other errors.

##### Retrieve School Subjects

###### Single School Subject
- **Endpoint:** `GET api/school-subjects/{id}`
- **Path Variable:**
  - `id` - ID of the school subject to retrieve.
- **Response:**
  - Returns the school subject as `SchoolSubjectDto` if found.
  - `404 Not Found` if the school subject with the specified ID does not exist.
  - `500 Internal Server Error` for other errors.

###### Multiple School Subjects
- **Endpoint:** `GET api/school-subjects`
- **Response:**
  - Returns a list of all school subjects as `List<SchoolSubjectDto>` if successful.
  - `500 Internal Server Error` for other errors.

##### Update a School Subject

- **Endpoint:** `PUT api/school-subjects/{id}`
- **Request Parameter:**
  - `id` - ID of the school subject to update.
- **Request Body:**
  - `SchoolSubjectRequest` object representing the updated school subject information.
- **Response:**
  - Returns the updated school subject as `SchoolSubjectDto` if successful.
  - `404 Not Found` if the school subject with the specified ID does not exist.
  - `500 Internal Server Error` for other errors.

##### Delete a School Subject

- **Endpoint:** `DELETE api/school-subjects/{id}`
- **Path Variable:**
  - `id` - ID of the school subject to delete.
- **Response:**
  - Returns "Subject deleted." if successful.
  - `404 Not Found` if the school subject with the specified ID does not exist.
  - `500 Internal Server Error` for other errors.

#### Exception Handling

- The API handles specific exceptions like `EntityExistsException`, `EntityNotFoundException`, and `EmptyResultDataAccessException`.
- Provides meaningful error messages and appropriate HTTP status codes for better understanding.

#### Usage

- Use tools like cURL or Postman for testing the API.


### Assignments



#### Assignment Controller API

This Spring Boot `AssignmentController` provides RESTful endpoints for assigning students, subjects, teachers, and automating teacher-to-class assignments.

#### Endpoints

##### Assign Students to School Classes

```json
{
    "studentId": 1,
    "schoolClassId": 2
}
```

- **Endpoint:** `POST /api/assignment/students/to/classes`
- **Request Body:**
  - List of `StudentToSchoolClassAssignmentRequest` objects representing student-to-school-class assignments.
- **Response:**
  - Returns the assignment result as a map if successful.
  - `404 Not Found` if entities are not found.
  - `400 Bad Request` if the request is invalid.
  - `500 Internal Server Error` for other errors.

##### Assign Subjects to Grades



```json
[
  {
    "grade":1,
    "subjects":[
      "Math",
      "Polish",
      "Chemistry",
      "English",
      "PE",
      "Physics",
      "Religion",
      "Music"
    ]
  },
  {
    "grade":2,
    "subjects":[
      "Math",
      "Polish",
      "Chemistry",
      "English",
      "PE",
      "Physics",
      "Religion",
      "Music"
    ]
  },
  {
    "grade":3,
    "subjects":[
      "Math",
      "Polish",
      "Chemistry",
      "English",
      "PE",
      "Physics",
      "Religion",
      "Music"
    ]
  },
  {
    "grade":4,
    "subjects":[
      "Math",
      "Polish",
      "Chemistry",
      "English",
      "PE",
      "Physics",
      "Religion",
      "Music"
    ]
  },
  {
    "grade":5,
    "subjects":[
      "Math",
      "Polish",
      "Chemistry",
      "English",
      "PE",
      "Physics",
      "Religion",
      "Music"
    ]
  },
  {
    "grade":6,
    "subjects":[
      "Math",
      "Polish",
      "Chemistry",
      "English",
      "PE",
      "Physics",
      "Religion",
      "Music"
    ]
  },
  {
    "grade":7,
    "subjects":[
      "Math",
      "Polish",
      "Chemistry",
      "English",
      "PE",
      "Physics",
      "Religion",
      "Music"
    ]
  },
  {
    "grade":8,
    "subjects":[
      "Math",
      "Polish",
      "Chemistry",
      "English",
      "PE",
      "Physics",
      "Religion",
      "Music"
    ]
  }
]
```

- **Endpoint:** `POST /api/assignment/subjects/to/grades`
- **Request Body:**
  - List of `SubjectsToGradesAssignmentRequest` objects representing subject-to-grade assignments.
- **Response:**
  - Returns the assignment result as a map if successful.
  - `404 Not Found` if entities are not found.
  - `400 Bad Request` if the request is invalid.
  - `500 Internal Server Error` for other errors.


##### Assign Teachers to Subjects

```json
[
  {"teacherId": 1, "subjectId": 1},
  {"teacherId": 2, "subjectId": 1},
  {"teacherId": 3, "subjectId": 1},
  {"teacherId": 4, "subjectId": 1},
  {"teacherId": 5, "subjectId": 1},
  {"teacherId": 6, "subjectId": 1},

  {"teacherId": 7, "subjectId": 2},
  {"teacherId": 8, "subjectId": 2},
  {"teacherId": 9, "subjectId": 2},
  {"teacherId": 10, "subjectId": 2},

  {"teacherId": 11, "subjectId": 3},
  {"teacherId": 12, "subjectId": 3},
  {"teacherId": 13, "subjectId": 3},

  {"teacherId": 14, "subjectId": 4},
  {"teacherId": 15, "subjectId": 4},
  {"teacherId": 16, "subjectId": 4},

  {"teacherId": 17, "subjectId": 5},
  {"teacherId": 18, "subjectId": 5},

  {"teacherId": 19, "subjectId": 6},
  {"teacherId": 20, "subjectId": 7},

  {"teacherId": 21, "subjectId": 8},
  {"teacherId": 22, "subjectId": 8}
]
```

- **Endpoint:** `POST /api/assignment/teachers/to/subjects`
- **Request Body:**
  - List of `TeachersToSubjectsAssignmentRequest` objects representing teacher-to-subject assignments.
- **Response:**
  - Returns the assignment result as a map if successful.
  - `404 Not Found` if entities are not found.
  - `400 Bad Request` if the request is invalid.
  - `500 Internal Server Error` for other errors.


##### Assign Teachers to School Classes
```json
{
    "teacherId": 1,
    "schoolClassId": 2,
    "schoolSubjectId": 3
}
```


- **Endpoint:** `POST /api/assignment/teachers/to/classes`
- **Request Body:**
  - List of `TeacherToSchoolClassAssignmentRequest` objects representing teacher-to-school-class assignments.
- **Response:**
  - Returns the assignment result as a map if successful.
  - `404 Not Found` if entities are not found.
  - `400 Bad Request` if the request is invalid.
  - `500 Internal Server Error` for other errors.

##### Automatically Assign Teachers to Classes

- **Endpoint:** `POST /api/assignment/teachers/to/classes/auto`
- **Response:**
  - Returns "ok" if successful.
  - `500 Internal Server Error` with hire recommendations if not enough teachers are available.
  - `500 Internal Server Error` for other errors.

#### Exception Handling

- Handles specific exceptions like `EntityNotFoundException`, `IllegalArgumentException`, and `NotEnoughTeachersException`.
- Provides meaningful error messages and appropriate HTTP status codes for better understanding.

#### Usage

- Use tools like cURL or Postman for testing the API.


### Timetable

This Spring Boot `TimetableController` provides RESTful endpoints for managing timetables.

#### Endpoints

##### Create Timetable

- **Endpoint:** `POST /api/timetables/create`
- **Response:**
  - Returns the created timetable as a `TimetableDto` if successful.
  - `409 Conflict` with hire recommendations if not enough teachers are available.
  - `409 Conflict` for other errors.

##### Generate Excel File

- **Endpoint:** `POST /api/timetables/excel`
- **Request Parameter:**
  - `timetableId` - ID of the timetable to generate an Excel file.
- **Response:**
  - Returns the generated timetable as a `TimetableDto` in Excel format if successful.
  - `500 Internal Server Error` if there is an issue generating the Excel file.

##### Get Timetable by ID

- **Endpoint:** `GET /api/timetables/{id}`
- **Path Variable:**
  - `id` - ID of the timetable to retrieve.
- **Response:**
  - Returns the timetable as a `TimetableDto` if found.
  - `404 Not Found` if the timetable with the specified ID does not exist.
  - `500 Internal Server Error` for other errors.

##### Exception Handling

- Handles specific exceptions like `NotEnoughTeachersException` and `IOException`.
- Provides meaningful error messages and appropriate HTTP status codes for better understanding.

##### Usage

- Use tools like cURL or Postman for testing the API.



