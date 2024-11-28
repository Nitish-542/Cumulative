
# Teacher App API

This project provides an API for managing teacher and course data from a school database. It allows retrieving information about teachers, their courses, and filtering teachers by their hire date range. The data is returned in JSON format and is used to display teacher and course details on the front-end.

## Features

- **Get Teacher Info**: Retrieve all teachers' information.
- **Get Teacher by Hire Date Range**: Filter teachers by hire date.
- **Get Specific Teacher Info**: Retrieve information about a specific teacher by their ID.
- **Get Course Info**: Retrieve all course-related data for teachers.
- **Filter Teachers by Attributes**: Find teachers matching specific criteria.

## Code Overview

### File Structure

- **TeacherAPIController.cs**: Handles API requests related to teacher data.
- **CourseAPIController.cs**: Handles API requests for course data.
- **SchoolDbContext.cs**: Manages database interactions with the school database.
- **Models**: Contains data models for `Teacher` and `Course`.

### `TeacherAPIController.cs`

This is the primary controller responsible for managing teacher-related API endpoints. It retrieves data from the database and interacts with models to provide teacher information.

#### Constructor (`TeacherAPIController(SchoolDbContext db)`)

- Initializes with the database context to access teacher and course data.
- Populates teacher lists with relevant course associations based on `teacherId`.

#### Key Methods

1. **GetTeacherInfo (GET `/api/teachers`)**
   - Retrieves a list of all teachers and their details in JSON format.
   - Provides full teacher profiles, including associated courses.

2. **GetTeacherByHireDate (POST `/api/teachers/hiredate`)**
   - Filters and retrieves teachers based on hire date range.
   - Returns teachers hired between the provided dates or an error message if no match is found.

3. **GetSpecificTeacher (GET `/api/teachers/{id}`)**
   - Fetches information for a specific teacher by their ID.
   - Returns detailed information, including associated courses.

4. **GetAllCourses (GET `/api/courses`)**
   - Retrieves all courses and their details from the database.

### Data Flow and Database Interaction

1. **Database Queries**
   - Queries the database for teacher and course information using raw SQL or LINQ.
   - Ensures proper relationships between teachers and their courses are maintained.

2. **JSON Serialization**
   - Data is serialized into JSON format for efficient front-end consumption.

### Models

1. **Teacher**
   - Fields: `Id`, `FirstName`, `LastName`, `EmployeeNumber`, `HireDate`, `Salary`.
   - Relationships: Holds a list of `Courses`.

2. **Course**
   - Fields: `CourseId`, `CourseCode`, `CourseName`, `StartDate`, `EndDate`, `TeacherId`.

## Example Requests

### 1. Retrieve All Teachers

**GET** `/api/teachers`

**Response:**
```json
[
  {
    "Id": 1,
    "FirstName": "John",
    "LastName": "Doe",
    "EmployeeNumber": "T12345",
    "HireDate": "2015-06-15T00:00:00",
    "Salary": 50000,
    "Courses": [
      {
        "CourseId": 101,
        "CourseCode": "CS101",
        "CourseName": "Intro to Computer Science",
        "StartDate": "2022-09-01",
        "EndDate": "2022-12-15"
      }
    ]
  }
]
```

### 2. Filter Teachers by Hire Date

**POST** `/api/teachers/hiredate`

**Request Body:**
```json
{
  "startRange": "2010-01-01",
  "endRange": "2020-12-31"
}
```

**Response:**
```json
[
  {
    "Id": 2,
    "FirstName": "Jane",
    "LastName": "Smith",
    "EmployeeNumber": "T67890",
    "HireDate": "2018-08-01T00:00:00",
    "Salary": 55000,
    "Courses": []
  }
]
```

## How to Run

1. **Set Up the Database**:
   - Ensure the database is configured in `appsettings.json`.
   - Run migrations if required.

2. **Run the Application**:
   - Use Visual Studio or CLI to run the application.
   - Access API endpoints via Postman or browser.

3. **Test the API**:
   - Use the provided example requests to test endpoints.
