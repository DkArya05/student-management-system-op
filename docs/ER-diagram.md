ER Diagram — Student Management System

1. Introduction

An Entity-Relationship Diagram (ERD) shows the main entities of a database and how they are connected.

Our Student Management System uses MongoDB. Each entity represents a collection, and each document has a unique "_id" field.

2. Main Entities and Their Purpose

Entity| Purpose
USERS| Stores login details and user roles, such as Administrator, Faculty, and Student.
STUDENTS| Stores student profile information.
DEPARTMENTS| Stores department names and details.
COURSES| Stores course information.
ENROLLMENTS| Connects students with the courses they join.
FACULTY_ASSIGNMENTS| Connects faculty members with their assigned courses.
CLASS_SESSIONS| Stores individual class sessions.
ATTENDANCE| Records whether a student attended a class.
ASSESSMENTS| Stores tests, examinations, and other assessments.
MARKS| Stores marks obtained by students.

3. Relationship Explanation

- One department can have many students.
- One department can offer many courses.
- One student can have multiple enrollments.
- One course can have multiple enrollments.
- One faculty member can teach multiple assigned courses.
- One course can have multiple faculty assignments.
- One course can have multiple class sessions.
- One class session can have multiple attendance records.
- One student can have multiple attendance records.
- One course can have multiple assessments.
- One assessment can have multiple marks records.
- One student can have multiple marks records.

Important: Students and courses have a many-to-many relationship. The ENROLLMENTS collection connects them.

4. ER Diagram

The following Mermaid code shows the main entities and their relationships.

erDiagram
    USERS ||--o| STUDENTS : "has profile"
    DEPARTMENTS ||--o{ STUDENTS : "contains"
    DEPARTMENTS ||--o{ COURSES : "offers"

    STUDENTS ||--o{ ENROLLMENTS : "has"
    COURSES ||--o{ ENROLLMENTS : "includes"

    USERS ||--o{ FACULTY_ASSIGNMENTS : "assigned through"
    COURSES ||--o{ FACULTY_ASSIGNMENTS : "has faculty"

    COURSES ||--o{ CLASS_SESSIONS : "schedules"
    CLASS_SESSIONS ||--o{ ATTENDANCE : "records"
    STUDENTS ||--o{ ATTENDANCE : "has"

    COURSES ||--o{ ASSESSMENTS : "has"
    ASSESSMENTS ||--o{ MARKS : "contains"
    STUDENTS ||--o{ MARKS : "receives"

5. Important Identifiers and References

Entity| Main Identifier| Important References
USERS| "_id"| User role
STUDENTS| "_id"| "userId", "departmentId"
DEPARTMENTS| "_id"| —
COURSES| "_id"| "departmentId"
ENROLLMENTS| "_id"| "studentId", "courseId"
FACULTY_ASSIGNMENTS| "_id"| "facultyUserId", "courseId"
CLASS_SESSIONS| "_id"| "courseId"
ATTENDANCE| "_id"| "studentId", "classSessionId"
ASSESSMENTS| "_id"| "courseId"
MARKS| "_id"| "studentId", "assessmentId"

These references represent links between MongoDB documents. The final Mongoose schemas must define and validate them consistently.


For example, "DEPARTMENTS ||--o{ COURSES" means one department can have zero or many courses, while each course belongs to one department under this design.

6. Design Assumptions

- Every document has a MongoDB "_id".
- USERS stores account information and role-based access details.
- STUDENTS stores student-specific information linked to a user account.
- Faculty accounts are stored in USERS and assigned to courses through FACULTY_ASSIGNMENTS.
- ENROLLMENTS connects students and courses.
- Attendance is recorded for a student and a particular class session.
- Marks connect a student to an assessment.
- Unique constraints should prevent duplicate enrollment, duplicate attendance for the same student and session, and duplicate marks for the same student and assessment.
- Fees, separate TEACHERS, and SUBJECTS collections are excluded from this version to keep it consistent with the current 10-collection design.

