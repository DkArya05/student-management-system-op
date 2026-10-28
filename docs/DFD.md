Data Flow Diagrams (DFD) — Student Management System

1. Purpose

A Data Flow Diagram (DFD) shows how information moves between users, system processes, and data stores.

2. Context-Level DFD

The entire Student Management System is represented as one process.

flowchart TD
    Admin[Administrator]
    Faculty[Faculty]
    Student[Student]

    SMS((Student Management System))

    Admin -->|Login, student details, courses, reports requests| SMS
    SMS -->|Dashboard, confirmations, reports| Admin

    Faculty -->|Login, attendance, examination marks| SMS
    SMS -->|Assigned student lists, confirmations| Faculty

    Student -->|Login, profile and academic data requests| SMS
    SMS -->|Permitted profile, attendance and marks| Student

3. Level 1 DFD

The main system is divided into functional processes.

flowchart TD
    Admin[Administrator]
    Faculty[Faculty]
    Student[Student]

    P1((1.0 Authentication))
    P2((2.0 Manage Students))
    P3((3.0 Manage Courses and Enrollments))
    P4((4.0 Manage Attendance))
    P5((5.0 Manage Examination Marks))
    P6((6.0 View Reports and Academic Data))

    D1[(D1 User Accounts)]
    D2[(D2 Student Records)]
    D3[(D3 Courses and Enrollments)]
    D4[(D4 Attendance Records)]
    D5[(D5 Examination and Marks Records)]

    Admin -->|Credentials| P1
    Faculty -->|Credentials| P1
    Student -->|Credentials| P1
    P1 <--> D1

    Admin -->|Student details and updates| P2
    P2 <--> D2

    Admin -->|Course and enrollment details| P3
    P3 <--> D2
    P3 <--> D3

    Faculty -->|Attendance entries| P4
    P4 -->|Read student and enrollment data| D2
    P4 -->|Read course and enrollment data| D3
    P4 <--> D4

    Faculty -->|Examination marks| P5
    P5 -->|Read student and enrollment data| D2
    P5 -->|Read course and enrollment data| D3
    P5 <--> D5

    Admin -->|Report request| P6
    Student -->|Own academic data request| P6
    P6 -->|Read student data| D2
    P6 -->|Read enrollment data| D3
    P6 -->|Read attendance data| D4
    P6 -->|Read marks data| D5
    P6 -->|Reports and permitted academic data| Admin
    P6 -->|Permitted personal academic data| Student

4. Data Stores

- D1 — User Accounts: User identifiers, password hashes, and roles.
- D2 — Student Records: Student identifiers and profile information.
- D3 — Courses and Enrollments: Course details and student-course relationships.
- D4 — Attendance Records: Student, course, date, and attendance status.
- D5 — Examination and Marks Records: Examination details and student marks.

These are conceptual data stores; the actual collections will be finalized during database design.

5. Important Notes

- The diagrams show logical data movement, not program execution.
- Authentication and role authorization must protect restricted operations.
- Students can access only their own permitted academic information, if student self-service is implemented.
- The diagrams must remain consistent with the approved SRS.
- Error responses and detailed validation flows can be added during API design.