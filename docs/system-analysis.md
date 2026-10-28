System Analysis — Student Management System

1. Existing System

Currently, the college manages student information using paper registers, spreadsheets, and separate records maintained by different departments.

Existing Workflow

1. The admission office collects student details.
2. Administrative staff enter student information into registers or spreadsheets.
3. Faculty members maintain attendance records separately.
4. Examination staff record examination marks.
5. Administrative staff collect information from different sources.
6. The college prepares student reports manually.

2. Problems in the Existing System

- Duplicate student records may be created.
- Incorrect or inconsistent information may be recorded.
- Finding student information takes time.
- Attendance and marks are stored separately.
- Preparing reports requires manual effort.
- Confidential records may not have proper access controls.
- Records may be lost or damaged.

3. Proposed System

The proposed Student Management System is a web application built using React, Node.js, Express.js, and MongoDB.

It provides a centralized platform for managing student profiles, courses, enrollments, attendance, and examination marks.

Proposed Workflow

1. An authorized user logs in.
2. The system verifies the user's credentials and role.
3. The user accesses the permitted dashboard and features.
4. The user enters or requests information.
5. The backend validates the request and checks permissions.
6. Valid information is stored in or retrieved from MongoDB.
7. The system displays the result or an appropriate error message.

4. System Boundary

Included

- User authentication and role-based access.
- Student record management.
- Course and enrollment management.
- Attendance recording and viewing.
- Examination marks entry and viewing.
- Dashboard and basic reports.
- Input validation and error handling.

Excluded

- Biometric attendance devices.
- Online payment gateway integration.
- A separate mobile application.
- Integration with external university systems.

5. Inputs, Processes, and Outputs

Input| Process| Output
Student details| Validate and save student record| Student profile
Login credentials| Verify credentials and role| Authorized dashboard or error
Course details| Validate and save course| Course record
Enrollment details| Check student and course, then save enrollment| Enrollment confirmation
Attendance data| Validate and record attendance| Attendance records and summary
Examination marks| Validate and save marks| Marks report
Search criteria| Search matching records| Filtered results

6. Stored Data

The system is expected to store:

- User accounts and roles.
- Student profiles.
- Faculty profiles, where implemented.
- Courses and enrollments.
- Attendance records.
- Examinations and marks.

Passwords must be stored as secure hashes, not plain text.

7. Assumptions and Limitations

Assumptions

- Users have access to a device and a web browser.
- Authorized users have valid accounts.
- The college provides accurate student and academic information.
- The server and database are available when the system is used.

Limitations

- The system depends on network and server availability.
- Incorrect information entered by authorized users can still affect records.
- Advanced integrations are outside the initial project scope.
- Reports depend on the completeness and accuracy of stored data.

8. Expected Improvements

The following are proposed targets to verify during testing, not proven results:

1. Reduce the time required to find a student record by at least 50% compared with the manual process.
2. Display a basic student report within 5 seconds under the project's test conditions.
3. Ensure that all tested unauthorized access attempts to restricted features are rejected.

9. Technology Stack

- Frontend: React with Vite.
- Backend: Node.js and Express.js.
- Database: MongoDB.
- API style: REST.
- Authentication and authorization: secure login and role-based access control.