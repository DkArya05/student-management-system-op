Use-Case Analysis — Student Management System

1. Purpose

This document describes how the Administrator, Faculty, and Student interact with the Student Management System.

2. Actors

Administrator

Manages student records, faculty records, courses, enrollments, and reports.

Faculty

Views assigned students, records attendance, and enters examination marks according to assigned permissions.

Student

Views their own profile, courses, attendance, and marks, if student self-service is implemented.

3. Main Use Cases

ID| Use Case| Actor
UC-01| Login| Administrator, Faculty, Student
UC-02| Logout| Administrator, Faculty, Student
UC-03| Register a student| Administrator
UC-04| View, update, and search student records| Administrator
UC-05| Manage courses| Administrator
UC-06| Manage enrollments| Administrator
UC-07| View assigned students| Faculty
UC-08| Record attendance| Faculty
UC-09| Enter examination marks| Faculty
UC-10| View attendance and marks| Student
UC-11| View dashboard and reports| Administrator
UC-12| Enforce role permissions| System

4. Use-Case Diagram

flowchart LR
    Admin[Administrator]
    Faculty[Faculty]
    Student[Student]

    subgraph SMS[Student Management System]
        Login([Login / Logout])
        Students([Manage Student Records])
        Courses([Manage Courses])
        Enroll([Manage Enrollments])
        Attendance([Record Attendance])
        Marks([Enter Examination Marks])
        Reports([View Reports])
        OwnData([View Own Profile, Attendance and Marks])
    end

    Admin --> Login
    Faculty --> Login
    Student --> Login

    Admin --> Students
    Admin --> Courses
    Admin --> Enroll
    Admin --> Reports

    Faculty --> Attendance
    Faculty --> Marks
    Faculty --> OwnData

    Student --> OwnData

Note: This is a simplified interaction diagram using Mermaid flowchart notation. It illustrates the actors, system boundary, and main use cases. A formal UML use-case diagram can be prepared later if required.

5. Detailed Use Cases

UC-01: Login

Primary actors: Administrator, Faculty, Student

Preconditions:

- The user has an account.
- The system is available.

Main flow:

1. The user opens the login page.
2. The user enters their credentials.
3. The backend verifies the credentials.
4. The system identifies the user's role.
5. The system displays the appropriate dashboard.

Alternative flow:

- If the credentials are invalid, the system displays a generic error.
- If required fields are missing, the system asks the user to complete them.

Postcondition: The authenticated user can access only permitted features.

UC-02: Register a Student

Primary actor: Administrator

Precondition: The administrator is authenticated and authorized.

Main flow:

1. The administrator opens the student registration form.
2. The administrator enters the student's details.
3. The system validates required fields and formats.
4. The system checks for duplicate student identifiers.
5. The backend saves the valid record.
6. The system displays a confirmation.

Alternative flow:

- Missing or invalid fields produce validation messages.
- A duplicate student identifier prevents the record from being saved.

Postcondition: A valid student record exists in the database.

UC-03: Record Attendance

Primary actor: Faculty

Preconditions:

- Faculty is authenticated.
- The faculty member is authorized for the relevant course or class.

Main flow:

1. Faculty selects an assigned course and date.
2. The system displays the relevant student list.
3. Faculty records attendance statuses.
4. The backend validates the submitted data and permissions.
5. The system saves the attendance records.
6. The system confirms the result.

Alternative flow:

- Invalid dates, student identifiers, or statuses are rejected.
- Unauthorized course access is denied.

Postcondition: Valid attendance records are stored.

UC-04: Enter Examination Marks

Primary actor: Faculty

Preconditions:

- Faculty is authenticated and authorized for the relevant course or examination.

Main flow:

1. Faculty selects an examination and course.
2. Faculty enters marks for students.
3. The system checks required fields and allowed mark ranges.
4. The backend verifies permissions and validates the request.
5. Valid marks are saved.
6. The system displays confirmation.

Alternative flow:

- Missing values, invalid marks, or marks above the maximum are rejected.
- Unauthorized changes are denied.

Postcondition: Valid examination marks are stored.

6. Authorization Rules

- Administrators can manage records according to the approved SRS.
- Faculty can access only assigned academic records and permitted functions.
- Students, if self-service is implemented, can view only their own permitted information.
- All protected backend endpoints must enforce authorization; hiding a button in the frontend is not sufficient.

7. Requirements to Confirm

- Whether student self-service will be implemented in the initial version.
- Whether faculty accounts and faculty profile management are included in the initial scope.
- Whether reports include only basic student and academic summaries.