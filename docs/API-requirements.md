API Requirements and Validation Rules

1. Purpose

This document defines the initial REST API requirements for the Student Management System. The APIs will allow the React frontend to communicate with the Node.js and Express.js backend.

2. API Conventions

- Base URL during local development: "/api"
- Data format: JSON
- Authentication: secure session or token-based authentication, to be finalized during design
- Protected endpoints must enforce authorization on the backend.
- HTTP status codes must communicate success or failure.
- Input validation must be performed on the server.

3. Initial API Endpoints

Method| Endpoint| Purpose| Access
POST| "/api/auth/login"| Authenticate a user| Public
POST| "/api/auth/logout"| Log out the current user| Authenticated
GET| "/api/auth/me"| Get current user's profile and role| Authenticated
GET| "/api/students"| List and search students| Administrator; authorized faculty access as defined
POST| "/api/students"| Register a student| Administrator
GET| "/api/students/:id"| Get a student record| Administrator; authorized faculty; own record for students
PUT| "/api/students/:id"| Update a student record| Administrator
GET| "/api/courses"| List courses available to the user| Based on role
POST| "/api/courses"| Create a course| Administrator
PUT| "/api/courses/:id"| Update a course| Administrator
POST| "/api/enrollments"| Enroll a student in a course| Administrator
GET| "/api/enrollments"| List permitted enrollments| Based on role
POST| "/api/attendance"| Record attendance| Administrator or authorized faculty
GET| "/api/attendance"| Retrieve permitted attendance records| Based on role
POST| "/api/examinations"| Create an examination| Administrator or explicitly authorized role
POST| "/api/marks"| Enter examination marks| Administrator or authorized faculty
GET| "/api/marks"| Retrieve permitted marks records| Based on role
GET| "/api/reports/summary"| Retrieve dashboard summary| Administrator; limited data for other roles

These endpoints are an initial proposal. Final permissions and endpoint details must match the approved SRS and RBAC matrix.

4. Validation Rules

Authentication

- Email or username and password are required.
- Invalid credentials must produce a generic error message.
- Passwords must never be returned in API responses.

Student Records

- Student identifier must be unique.
- Required fields must not be empty.
- Email must follow a valid format when provided.
- Phone number must follow the chosen validation rules.
- Unknown or unsupported fields should be rejected or safely ignored according to the API design.

Courses and Enrollments

- Course code must be unique.
- Referenced student and course records must exist.
- Duplicate active enrollments must be prevented.

Attendance

- Student, course, date, and attendance status are required.
- The student must be enrolled in the relevant course, according to the college's rules.
- Only authorized users may record or modify attendance.
- Duplicate attendance entries must be prevented according to the approved attendance policy.

Examinations and Marks

- The examination must exist.
- The student must be eligible for the examination.
- Marks must be numeric and within the permitted range.
- Marks must not exceed the examination's maximum marks.
- Only authorized users may enter or modify marks.

General Security

- Validate all requests on the backend.
- Reject unauthorized operations.
- Do not trust role values submitted by the frontend.
- Protect against invalid identifiers and malformed requests.
- Avoid returning confidential information unnecessarily.

5. Expected HTTP Status Codes

Status| Meaning
200| Request successful
201| Resource created
400| Invalid request or validation failure
401| Authentication required or invalid
403| Authenticated user lacks permission
404| Resource not found
409| Conflict, such as a duplicate identifier
500| Unexpected server error

6. Example Error Response

{
  "success": false,
  "message": "Validation failed",
  "errors": [
    {
      "field": "studentId",
      "message": "Student ID is required"
    }
  ]
}

7. Decisions Required Before Coding

- Final authentication mechanism.
- Exact required student fields.
- Pagination and search parameters.
- Attendance recording policy.
- Marks editing permissions.
- Whether student self-service is included in the initial release.
- Whether faculty profile management is required.

8. Implementation Principle

Build and test the APIs incrementally. Do not implement all endpoints at once. Each endpoint must be checked against the SRS, RBAC matrix, validation rules, and expected responses.