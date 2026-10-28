Software Requirements Specification (SRS)

1. Introduction

1.1 Purpose

This document defines the functional and non-functional requirements of the Student Management System. It will guide the analysis, design, development, and testing of the application.

1.2 Project Scope

The Student Management System is a full-stack web application intended to organize student information and academic records in a centralized database.

The application will use React with Vite for the frontend, Node.js and Express.js for the backend, and MongoDB for data storage.

1.3 Intended Users

- Administrator
- Faculty/Teacher
- Student, if student self-service access is implemented within the available time

2. Overall Description

2.1 Product Perspective

The system will provide a web-based interface connected to a backend API and a MongoDB database. The frontend will send requests to the backend, which will validate requests, apply business rules, and access stored records.

2.2 User Classes

Administrator: Manages student records, departments, courses, enrollments, and authorized user access.

Faculty/Teacher: Performs permitted academic tasks, such as recording attendance and marks.

Student: May view permitted personal and academic records if this feature is included in the implemented scope.

2.3 Operating Environment

- Operating system: Windows or another supported operating system
- Frontend: React and Vite
- Backend: Node.js and Express.js
- Database: MongoDB
- Development tool: Visual Studio Code
- Version control: Git and GitHub
- Browser: A modern web browser

3. Functional Requirements

FR-01: Authentication

The system shall allow authorized users to log in and log out securely.

FR-02: Student Management

The system shall allow authorized administrators to add, view, edit, search, and manage student records.

FR-03: Department Management

The system shall allow authorized administrators to create, view, and update department records.

FR-04: Course Management

The system shall allow authorized administrators to create, view, and update course records.

FR-05: Enrollment Management

The system shall allow authorized administrators to associate students with appropriate courses and view enrollment records.

FR-06: Attendance Management

The system shall allow authorized faculty members to record and view attendance for permitted students and courses.

FR-07: Assessment and Marks

The system shall allow authorized faculty members to record and update assessment marks and allow permitted users to view them.

FR-08: Role-Based Access Control

The system shall restrict features and data according to each user's assigned role and permissions.

FR-09: Data Validation

The system shall validate required fields and reject invalid input before saving records.

FR-10: Error Handling

The system shall display understandable error messages when an operation fails.

FR-11: Dashboard

The system should provide a dashboard showing relevant summary information for the implemented modules.

4. Non-Functional Requirements

NFR-01: Usability

The interface should be understandable and easy to navigate.

NFR-02: Responsiveness

The application should work on common desktop, tablet, and mobile screen sizes.

NFR-03: Security

Passwords must be securely hashed. Protected backend routes must enforce authentication and authorization. Sensitive configuration values must not be committed to GitHub.

NFR-04: Reliability

The system should handle invalid requests and database errors without crashing during normal use.

NFR-05: Maintainability

The frontend and backend should be organized into understandable modules so that features can be maintained and tested.

NFR-06: Data Integrity

The system should validate data and prevent invalid or unauthorized modifications to records.

5. Data Requirements

The database is expected to contain records for:

- Users and roles
- Students
- Departments
- Courses
- Enrollments
- Attendance
- Assessments
- Marks

The final database structure will be confirmed during system analysis and database design.

6. External Interface Requirements

6.1 User Interface

The application shall provide forms, tables, navigation, and feedback messages suitable for the implemented modules.

6.2 Software Interface

The React frontend shall communicate with the Express backend through HTTP API endpoints. The backend shall interact with MongoDB to store and retrieve records.

7. Scope Exclusions

The initial version will not include biometric attendance, a mobile application, an online payment gateway, or advanced third-party integrations.

8. Assumptions and Constraints

- The application is being developed as a BCA academic project.
- The target development period is ten days.
- The project will prioritize essential features that can be implemented and tested within the available time.
- Users must have appropriate accounts and permissions to access protected features.
- Student self-service features will be included only if time permits.

9. Acceptance Criteria

The project will be considered ready for demonstration when:

- Authorized users can log in and log out.
- Student records can be created, viewed, updated, and searched.
- Implemented academic modules can save and retrieve records from MongoDB.
- Role-based access restrictions are tested.
- Invalid inputs produce appropriate validation errors.
- Core workflows are tested successfully.
- The application can be demonstrated using documented setup instructions.

10. Requirements Review

This SRS will serve as the baseline for detailed system analysis, design, implementation, and testing. Any changes to the agreed scope must be reviewed and documented before implementation.