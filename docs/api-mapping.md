API Mapping — Student Management System

1. Purpose

This document maps the frontend pages of the Student Management System to the proposed backend REST API endpoints. It explains how the React frontend will communicate with the Node.js, Express.js, and MongoDB backend.

Note: These endpoints are proposed designs. They must be implemented and tested before being considered functional.

2. Technology Stack

- Frontend: React.js with Vite
- Backend: Node.js and Express.js
- Database: MongoDB with Mongoose
- Authentication: JWT
- API communication: Axios
- Data format: JSON

3. Frontend-to-API Mapping

Frontend Page / Module| HTTP Method| API Endpoint| Purpose
Login| POST| "/api/auth/login"| Authenticate a user
User Session| GET| "/api/auth/me"| Retrieve the logged-in user's details
Logout| POST| "/api/auth/logout"| End the user session according to the chosen authentication strategy
Admin Dashboard| GET| "/api/dashboard/stats"| Retrieve dashboard statistics
Student List| GET| "/api/students"| Retrieve and filter students
Student Registration| POST| "/api/students"| Create a student record
Student Details| GET| "/api/students/:id"| Retrieve one student's details
Edit Student| PATCH| "/api/students/:id"| Update permitted student fields
Student Management| DELETE| "/api/students/:id"| Deactivate a student, subject to authorization
Department Management| GET| "/api/departments"| Retrieve departments
Department Management| POST| "/api/departments"| Create a department
Department Management| PATCH| "/api/departments/:id"| Update a department
Department Management| DELETE| "/api/departments/:id"| Delete a department when permitted and safe
Course Management| GET| "/api/courses"| Retrieve courses
Course Management| POST| "/api/courses"| Create a course
Course Management| PATCH| "/api/courses/:id"| Update a course
Course Management| DELETE| "/api/courses/:id"| Delete a course when permitted and safe
Enrollments| GET| "/api/enrollments"| View enrollments the user is authorized to access
Enrollments| POST| "/api/enrollments"| Enroll a student in a course
Enrollments| PATCH| "/api/enrollments/:id"| Update enrollment details or status
Enrollments| DELETE| "/api/enrollments/:id"| Remove an enrollment when permitted
Faculty Assignments| GET| "/api/faculty-assignments"| View authorized faculty-course assignments
Faculty Assignments| POST| "/api/faculty-assignments"| Assign faculty to a course
Faculty Assignments| PATCH| "/api/faculty-assignments/:id"| Update an assignment
Class Sessions| GET| "/api/class-sessions"| Retrieve authorized class sessions
Class Sessions| POST| "/api/class-sessions"| Create a class session
Class Sessions| PATCH| "/api/class-sessions/:id"| Update a class session
Attendance| GET| "/api/attendance"| View authorized attendance records
Attendance| POST| "/api/attendance"| Record attendance
Attendance| PATCH| "/api/attendance/:id"| Correct an attendance record when permitted
Assessments| GET| "/api/assessments"| Retrieve assessments
Assessments| POST| "/api/assessments"| Create an assessment
Assessments| PATCH| "/api/assessments/:id"| Update an assessment
Marks| GET| "/api/marks"| View authorized marks
Marks| POST| "/api/marks"| Record marks
Marks| PATCH| "/api/marks/:id"| Update marks when permitted

4. Role-Based API Access

Administrator

- Manage student records, departments, and courses.
- Create authorized staff accounts and faculty assignments.
- View overall dashboard statistics and authorized academic reports.
- Manage academic records according to system permissions.

Faculty

- View students assigned to their courses.
- Record or update attendance for authorized classes.
- Enter or update marks for assigned assessments.
- Access only relevant academic reports.

Student

- View permitted profile information.
- View enrolled courses, personal attendance, and marks.
- Access only their own academic records.

Security rule: The backend must authenticate requests and enforce role-based and record-level authorization. Hiding a button in React is not sufficient security.

5. Request and Response Format

The API will use JSON for request and response bodies.

Example student creation request:

{
  "fullName": "Sample Student",
  "email": "student@example.com",
  "departmentId": "DEPARTMENT_ID",
  "courseId": "COURSE_ID"
}

The backend must validate the request and return the created student record with an appropriate HTTP status. The exact fields must match the final Mongoose schema.

Example success response:

{
  "success": true,
  "message": "Student created successfully",
  "data": {
    "id": "STUDENT_ID",
    "fullName": "Sample Student",
    "email": "student@example.com"
  }
}

Example error response:

{
  "success": false,
  "message": "Validation failed",
  "errors": [
    {
      "field": "email",
      "message": "A valid email address is required"
    }
  ]
}

6. Authentication

- Protected endpoints require a valid authentication token or session.
- If JWT is stored in an HTTP-only cookie, configure Axios and the backend for credentialed requests.
- If bearer-token authentication is selected, send the token using the "Authorization: Bearer <token>" header.
- Passwords must never be returned in API responses.
- Authentication and authorization must be checked on the backend.

The final authentication strategy must be consistent across the frontend, backend, and security configuration.

7. Query Parameters and Filtering

The following query parameters may be supported where applicable:

- "search" — search by permitted student or course fields.
- "page" — page number for pagination.
- "limit" — number of records per page.
- "departmentId" — filter by department.
- "courseId" — filter by course.
- "status" — filter by an allowed status.
- "date" — filter attendance or class sessions by date.

The backend must validate query parameters and apply authorization before returning results.

8. HTTP Status Codes

Status Code| Meaning
200| Request successful
201| Resource created successfully
400| Invalid request or validation error
401| Authentication required or invalid
403| User lacks permission
404| Resource not found
409| Conflict, such as a duplicate unique value
500| Unexpected server error

9. Error Handling

- Validate incoming data on the backend.
- Return consistent JSON error responses.
- Use centralized Express error-handling middleware.
- Do not expose stack traces, passwords, tokens, or sensitive information.
- Show clear, user-friendly error messages in the React interface.
- Provide loading, success, empty, and failure states on relevant pages.
- Handle network failures and expired authentication sessions.

10. API Testing

The proposed endpoints will be tested using Postman or an equivalent API testing tool.

Testing should cover:

- Successful requests.
- Missing or invalid input.
- Duplicate records.
- Unauthenticated requests.
- Unauthorized role access.
- Invalid resource IDs and missing records.
- Database or server errors.

