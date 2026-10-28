Entity Analysis — Student Management System

1. Purpose

This document identifies the main entities, their attributes, and relationships required for the Student Management System.

2. Main Entities

1. User

Stores account and login information.

- userId
- name
- email
- passwordHash
- role
- status
- createdAt

2. Student

Stores student profile information.

- studentId
- userId (optional, if a student login account is created)
- fullName
- dateOfBirth
- phone
- email
- department
- admissionDate
- status

3. Faculty

Stores faculty profile information.

- facultyId
- userId
- fullName
- email
- department
- status

4. Course

Stores course information.

- courseId
- courseName
- courseCode
- department
- description
- status

5. Enrollment

Connects students with courses.

- enrollmentId
- studentId
- courseId
- enrollmentDate
- status

6. Attendance

Stores attendance records.

- attendanceId
- studentId
- courseId
- recordedBy
- date
- status

7. Examination

Stores examination information.

- examinationId
- courseId
- examinationName
- examinationDate
- maximumMarks

8. Mark

Stores marks obtained by students.

- markId
- examinationId
- studentId
- marksObtained
- enteredBy
- updatedAt

3. Entity Relationships

- A User account has one role: Administrator, Faculty, or Student.
- A Student may be linked to a User account if student self-service is implemented.
- A Faculty profile is linked to a User account.
- A Student can have many Enrollments.
- A Course can have many Enrollments.
- A Course can have many Attendance records.
- A Student can have many Attendance records.
- A Course can have many Examinations.
- An Examination can have many student Marks records.
- A Faculty member may record many Attendance and Mark records, subject to permissions.

4. Relationship Summary

Entity A| Relationship| Entity B
User| One-to-one, when linked| Student
User| One-to-one| Faculty
Student| One-to-many| Enrollment
Course| One-to-many| Enrollment
Student| One-to-many| Attendance
Course| One-to-many| Attendance
Course| One-to-many| Examination
Examination| One-to-many| Mark
Student| One-to-many| Mark

5. Data Integrity Rules

- Each student must have a unique student identifier.
- Each course must have a unique course code.
- Each enrollment must reference an existing student and course.
- Attendance must reference a valid student and course.
- Marks must reference an existing student and examination.
- Marks obtained must be between zero and the examination's maximum marks.
- Duplicate attendance entries for the same student, course, and date must be prevented according to the attendance policy.
- Passwords must never be stored in plain text.

6. MongoDB Design Notes

MongoDB stores data in collections containing documents.

The proposed collections are:

- users
- students
- faculty
- courses
- enrollments
- attendance
- examinations
- marks

Relationships can be represented using document references. The final collection structure and indexes will be confirmed during database design.

7. Items to Confirm

- Whether student login will be included in the initial release.
- Whether each course has one or multiple faculty members.
- Whether attendance is recorded once per course per day or per class session.
- Whether students can enroll in multiple courses.
- Whether marks can be edited after submission, and who is authorized to edit them.