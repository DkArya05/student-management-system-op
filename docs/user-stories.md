User Stories

Project Title

Student Management System — Full Stack Web Application

1. Purpose

User stories describe the main tasks that different users should be able to perform in the Student Management System. They will help the team understand user needs and prioritize features.

2. User Roles

- Administrator: Manages student and academic records and controls authorized access.
- Faculty/Teacher: Views assigned academic information and manages attendance and marks where permitted.
- Student: Views their own academic information where student access is enabled.

3. User Stories

Authentication

- As an authorized user, I want to log in securely so that I can access permitted features.
- As an authorized user, I want to log out so that my account is not left open on a shared computer.

Student Management

- As an administrator, I want to add student records so that student information is maintained centrally.
- As an administrator, I want to view, edit, search, and update student records so that information remains accurate.
- As an administrator, I want to view a student's details so that I can retrieve information when required.

Department and Course Management

- As an administrator, I want to create and update department records so that academic departments are organized.
- As an administrator, I want to manage course information so that courses can be maintained centrally.
- As an administrator, I want to enroll students in courses so that their academic registrations can be tracked.

Attendance Management

- As an authorized faculty member, I want to record attendance so that student attendance is maintained.
- As an authorized user, I want to view attendance records so that attendance information can be checked when required.

Assessments and Marks

- As an authorized faculty member, I want to record assessment marks so that student performance is documented.
- As an authorized user, I want to view marks so that academic results can be reviewed according to permissions.

Security and Access Control

- As an administrator, I want users to have role-based permissions so that they can access only the features they are authorized to use.
- As a student, if student login is implemented, I want to view only my own permitted academic records so that my information remains private.

4. Priority

High priority

- Login and logout
- Student record management
- Department and course management
- Enrollment management

Medium priority

- Attendance management
- Assessment and marks management
- Role-based permissions

Optional, depending on time

- Student self-service dashboard
- Additional reports and advanced search filters

5. Acceptance Criteria

- Required fields must be validated before records are saved.
- Authorized users must be able to perform only permitted actions.
- Search should return matching records when available.
- Invalid requests should display understandable error messages.
- Saved records should persist in the database.
- The team must test each implemented feature before the final demonstration.

6. Scope Note

These user stories describe proposed requirements. The team must confirm them in the Software Requirements Specification (SRS) before implementation. Optional features will be included only if time and project scope permit
