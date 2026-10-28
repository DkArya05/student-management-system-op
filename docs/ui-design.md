UI Wireframes and Navigation Specification

Student Management System — Full Stack Web Application

Document: "docs/ui-wireframes.md"
Status: UI design specification
Frontend: React, Vite, JavaScript, Bootstrap
Backend: Node.js, Express.js, REST API
Database: MongoDB with Mongoose

1. Purpose

This document specifies the wireframes, page layouts, form fields, navigation, validation messages, loading states, empty states, and error states for the Student Management System.

The interface follows the approved Software Requirements Specification (SRS). It supports three roles: Administrator, Faculty, and Student.

The wireframes describe the proposed interface and do not represent completed application functionality.

2. Common Design System

2.1 Visual Style

- Theme: Clean, professional academic dashboard.
- Primary color: Indigo/purple.
- Background: Light grey or off-white.
- Cards: White backgrounds with subtle borders and rounded corners.
- Typography: Clear, readable sans-serif font.
- Framework: Bootstrap grid, forms, tables, buttons, alerts, modals, and responsive utilities.
- Navigation: Sidebar on larger screens and collapsible navigation on smaller screens.

2.2 Common Layout

+------------------------------------------------------+
| College Logo       Page Title       Profile / Logout |
+---------------+--------------------------------------+
|               |                                      |
|   Sidebar     |          Main Content                |
|               |                                      |
|   Dashboard   |   Page Heading       Primary Action  |
|   Students    |                                      |
|   Courses     |   Search / Filters                   |
|   Attendance  |                                      |
|   Marks       |   Cards / Forms / Data Table          |
|               |                                      |
+---------------+--------------------------------------+

The sidebar displays only the navigation items permitted for the authenticated role. Backend authorization remains mandatory.

3. Page 1 — Login

Layout

+--------------------------------------+
|          COLLEGE LOGO                |
|                                      |
|       Student Management System      |
|                                      |
|       Sign in to your account        |
|                                      |
|       Email / Username               |
|       [________________________]     |
|                                      |
|       Password                       |
|       [________________________]     |
|                                      |
|       [ ] Show password              |
|                                      |
|       [         Sign In         ]    |
|                                      |
|       Authentication error area      |
+--------------------------------------+

Components and fields

- College logo and application name.
- Email or username field, according to the authentication API.
- Password field with an optional visibility toggle.
- Sign In button.
- Loading indicator during authentication.
- Accessible validation and error-message area.

Navigation

- Successful login → role-appropriate dashboard.
- Invalid credentials → remain on Login.
- Expired or invalid session → return to Login.
- Logout → clear the authenticated session and return to Login.

Validation messages

- “Please enter your email or username.”
- “Please enter your password.”
- “Invalid credentials. Please try again.”
- “Unable to sign in. Please try again later.”

States

- Loading: Disable the submit button and show “Signing in…”.
- Empty: Show the login form with no previous values.
- Error: Display a generic authentication error without revealing whether an account exists.

Security: Public self-registration is not included. Accounts are created through authorized administrative workflows.

4. Page 2 — Administrator Dashboard

Layout

+------------------------------------------------------+
| Logo       Administrator Dashboard      Profile     |
+---------------+--------------------------------------+
| Dashboard     | Welcome, Administrator               |
| Students      |                                      |
| Departments   | +----------+ +----------+ +--------+ |
| Courses       | | Students | | Courses  | | Depts  | |
| Enrollments   | +----------+ +----------+ +--------+ |
| Faculty       |                                      |
| Attendance    | +----------------------------------+ |
| Marks         | | Attendance Summary               | |
| Reports       | +----------------------------------+ |
| Logout        |                                      |
|               | +----------------------------------+ |
|               | | Recent Student Registrations     | |
|               | +----------------------------------+ |
+---------------+--------------------------------------+

Components

- Welcome message and page heading.
- Total students, active students, courses, and departments cards.
- Attendance summary.
- Recent student registrations table.
- Quick actions such as Add Student and Manage Courses.
- Profile and logout controls.

Navigation

- Students → Student List.
- Add Student → Student Registration.
- Courses → Course Management.
- Attendance → Attendance Management.
- Marks → Marks Management.
- Departments → Department Management.
- Reports → approved academic reports.

Validation and messages

- “Dashboard data could not be loaded.”
- “No recent student registrations found.”
- “No attendance data is available for this period.”

States

- Loading: Display skeleton cards and table placeholders.
- Empty: Show zero or unavailable statistics with an explanatory message.
- Error: Display an error alert and a Retry action.

Statistics must come from actual backend records, not permanent hardcoded sample values.

5. Page 3 — Student List

Layout

+------------------------------------------------------+
| Students                            [+ Add Student]  |
+------------------------------------------------------+
| Search by name or student ID                         |
| [____________________] [Search]                      |
| Department [All v] Course [All v] Status [All v]     |
+------------------------------------------------------+
| Student ID | Name | Course | Department | Status     |
|------------|------|--------|------------|------------|
| STU001     | ...  | ...    | ...        | Active     |
| STU002     | ...  | ...    | ...        | Active     |
+------------------------------------------------------+
| Previous       Page 1 of N          Next             |
+------------------------------------------------------+

Components and fields

- Page title and Add Student button.
- Search by student name or student ID.
- Department filter.
- Course filter.
- Student status filter.
- Responsive student table.
- View and Edit actions.
- Deactivate action with confirmation.
- Pagination controls.

Table columns

- Student ID.
- Student name.
- Email.
- Department.
- Course or enrollment summary.
- Status.
- Actions.

Navigation

- Add Student → Registration form.
- Edit → Student Editing form.
- View → Student details.
- Deactivate → Confirmation dialog.

Validation messages

- “No matching students found.”
- “Please enter a valid search term.”
- “Unable to load student records.”
- “You do not have permission to perform this action.”

States

- Loading: Show table skeleton rows.
- Empty: “No students have been registered yet.”
- Filtered empty: “No students match your search or filters.”
- Error: Show an error alert with Retry.

Deactivation should not permanently delete academic history.

6. Page 4 — Student Registration and Editing

Layout

+------------------------------------------------------+
| Add Student / Edit Student                           |
+------------------------------------------------------+
| PERSONAL INFORMATION                                 |
| Student ID       [____________________]              |
| Full Name        [____________________]              |
| Email            [____________________]              |
| Phone            [____________________]              |
|                                                      |
| ACADEMIC INFORMATION                                 |
| Department       [Select Department v]               |
| Course           [Select Course v]                   |
| Enrollment Date  [Select Date]                       |
| Status           [Active v]                          |
|                                                      |
| [Cancel]                    [Save Student]            |
+------------------------------------------------------+

Fields

- Student ID — required, unique.
- Full name — required.
- Email — required if specified by the approved SRS.
- Phone — optional unless required by the final SRS.
- Department — required selection.
- Course — required selection where applicable.
- Enrollment date — required according to the approved rules.
- Status — controlled by authorized users.

Additional profile fields may be added only when approved by the SRS and database design.

Navigation

- Student List → Add Student.
- Student row → Edit Student.
- Cancel → return to Student List.
- Successful save → show confirmation and return to the list or student details.

Validation messages

- “Student ID is required.”
- “This student ID already exists.”
- “Full name is required.”
- “Please enter a valid email address.”
- “Please select a valid department.”
- “Please select a valid course.”
- “Please correct the highlighted fields.”

States

- Loading: Load department/course options and existing student data.
- Empty: In registration mode, show a blank form; if no courses exist, explain that course setup is required first.
- Error: Preserve entered values when safe and display the relevant server or validation message.
- Saving: Disable repeated submission and show “Saving…”.

The backend must validate uniqueness and referenced records. Editing must not create a duplicate student record.

7. Page 5 — Course Management

Layout

+------------------------------------------------------+
| Course Management                    [+ Add Course]  |
+------------------------------------------------------+
| Search courses [________________] [Search]            |
| Department [All v]                                   |
+------------------------------------------------------+
| Course Code | Course Name | Department | Status      |
|-------------|-------------|------------|-------------|
| BCA         | Bachelor... | Computer...| Active      |
| ...         | ...         | ...        | ...         |
+------------------------------------------------------+
| [View] [Edit] [Deactivate, if permitted]              |
+------------------------------------------------------+

Course form fields

- Course code — required and unique.
- Course name — required.
- Department — required reference.
- Description — optional.
- Duration or academic details — only if included in the approved SRS.
- Status — active or inactive, according to the approved data model.

Navigation

- Add Course → course form.
- Edit Course → edit form.
- Department selector → uses existing department records.
- Course list → search, filter, and pagination.

Validation messages

- “Course code is required.”
- “This course code already exists.”
- “Course name is required.”
- “Please select a valid department.”
- “Unable to save course details.”

States

- Loading: Show course table placeholders.
- Empty: “No courses found. Add a course to get started.”
- Error: Show the server error and Retry action.
- Saving: Disable duplicate form submission.

Course deletion or deactivation must respect existing enrollment and academic-record relationships.

8. Page 6 — Attendance Entry

Layout

+------------------------------------------------------+
| Attendance Management                                |
+------------------------------------------------------+
| Course [Select v]    Class [Select v]                |
| Date   [YYYY-MM-DD]  Session [Select v]              |
|                                                      |
| Student ID | Student Name | Attendance Status        |
|------------|--------------|--------------------------|
| STU001     | Student A    | [Present v]              |
| STU002     | Student B    | [Absent v]               |
| STU003     | Student C    | [Late v, if supported]   |
|                                                      |
| [Cancel]                      [Save Attendance]       |
+------------------------------------------------------+

Components and fields

- Course selector.
- Authorized class/session selector.
- Attendance date.
- Student list for the selected class.
- Attendance status for each student.
- Save Attendance button.
- Optional summary of present and absent counts.

The final attendance statuses must match the approved data model. Do not include “Late” unless it is supported by the SRS.

Navigation

- Faculty → Attendance.
- Select an assigned class/session → load eligible students.
- Save Attendance → display confirmation.
- Attendance reports → approved report view.

Validation messages

- “Please select a course.”
- “Please select a valid class session.”
- “Please select an attendance date.”
- “Attendance status is required for each student.”
- “Attendance has already been recorded for this class and date.”
- “You are not authorized to record attendance for this class.”

States

- Loading: Show a loading indicator while class and student records are fetched.
- Empty: “No eligible students found for this class.”
- Error: Display a useful error and preserve unsaved entries where safe.
- Saving: Disable repeated submission and display “Saving attendance…”.

The backend must prevent duplicate attendance records for the same student, class session, and date according to the approved data model.

9. Page 7 — Marks Entry

Layout

+------------------------------------------------------+
| Marks Management                                     |
+------------------------------------------------------+
| Course [Select v]     Assessment [Select v]          |
| Subject [Select v]    Maximum Marks [Read-only]      |
|                                                      |
| Student ID | Student Name | Maximum | Obtained       |
|------------|--------------|---------|----------------|
| STU001     | Student A    | 100      | [____]        |
| STU002     | Student B    | 100      | [____]        |
| STU003     | Student C    | 100      | [____]        |
|                                                      |
| [Cancel]                          [Save Marks]       |
+------------------------------------------------------+

Components and fields

- Course selector.
- Assessment selector.
- Subject or academic context, as defined in the approved model.
- Maximum marks, retrieved from the assessment record.
- Student list.
- Obtained marks input.
- Save Marks button.
- Optional calculated total or percentage where applicable.

Navigation

- Faculty → Marks Management.
- Select an authorized assessment → load eligible students.
- Enter marks → validate and save.
- Student academic dashboard → view personal results.

Validation messages

- “Please select an assessment.”
- “Maximum marks must be greater than zero.”
- “Obtained marks cannot be negative.”
- “Obtained marks cannot exceed maximum marks.”
- “Please enter valid marks for each student.”
- “You are not authorized to enter marks for this assessment.”

States

- Loading: Load assessment details and eligible students.
- Empty: “No eligible students are available for this assessment.”
- Error: Show the relevant validation or server error.
- Saving: Display “Saving marks…” and prevent duplicate submission.

The backend must validate marks independently of the frontend. Calculated percentages should use the approved grading rules.

10. Page 8 — Student Academic Dashboard

Layout

+------------------------------------------------------+
| Student Dashboard                      Profile       |
+------------------------------------------------------+
| Welcome, Student                                     |
|                                                      |
| +----------------+ +----------------+                |
| | Enrolled       | | Attendance     |                |
| | Courses        | | Summary        |                |
| +----------------+ +----------------+                |
|                                                      |
| +--------------------------------------------------+ |
| | My Enrolled Courses                              | |
| +--------------------------------------------------+ |
|                                                      |
| +--------------------------------------------------+ |
| | My Attendance                                    | |
| +--------------------------------------------------+ |
|                                                      |
| +--------------------------------------------------+ |
| | My Assessment Marks and Results                  | |
| +--------------------------------------------------+ |
+------------------------------------------------------+

Components and fields

- Welcome message.
- Permitted personal profile details.
- Enrolled courses.
- Attendance percentage and summary.
- Assessment marks and results.
- Relevant academic notices only if approved by the SRS.
- Profile and logout controls.

Navigation

- Login → Student Dashboard.
- Enrolled Courses → course details.
- Attendance Summary → personal attendance details.
- Marks and Results → personal assessment records.
- Profile → permitted profile fields.

Validation and messages

- “Your enrolled courses could not be loaded.”
- “No attendance records are available.”
- “No marks have been published yet.”
- “Unable to load your academic information.”

States

- Loading: Display summary-card and table skeletons.
- Empty: Explain which records are not yet available.
- Error: Show a retry option without exposing private server details.

Students must only access their own academic records. The backend must enforce this restriction for every request.

11. Role-Based Navigation Matrix

Legend: Full = authorized management access; Assigned = only assigned academic records; Own = only personal records; — = no access by default.

Page / Feature| Administrator| Faculty| Student
Login / Logout| Full| Full| Full
Administrator Dashboard| Full| —| —
Student List| Full| Assigned| —
Student Registration / Editing| Full| —| —
Departments| Full| View if authorized| —
Course Management| Full| Assigned courses| Own enrolled courses
Enrollments| Full| View if authorized| Own enrollments
Faculty Assignments| Full| Own assignments| —
Class Sessions| Full| Assigned sessions| View if permitted
Attendance Entry| View reports| Assigned classes| —
Personal Attendance| View reports| Assigned classes| Own
Marks Entry| View reports| Assigned assessments| —
Academic Results| Full report access| Assigned assessments| Own
Reports| Full| Authorized academic reports| Own academic information
User Administration| Authorized accounts| —| —

This matrix is the proposed UI navigation specification. Exact permissions must match the approved SRS and RBAC matrix. All restrictions must also be implemented and tested on the backend.

12. Responsive Design Guidelines

Desktop — 992 px and above

- Use a fixed or collapsible sidebar.
- Display dashboard summary cards in multiple columns.
- Show full data tables with search, filters, and pagination.
- Use Bootstrap grid and spacing utilities.
- Keep primary actions visible near the page heading.

Tablet — 768 px to 991 px

- Allow the sidebar to collapse into a drawer.
- Display two dashboard cards per row where space permits.
- Reduce table columns or allow horizontal scrolling.
- Stack filters into two-column layouts.
- Ensure forms remain readable and touch-friendly.

Mobile — below 768 px

- Use a collapsible navigation menu.
- Display summary cards in one column or a compact two-column layout when readable.
- Stack form fields vertically.
- Make primary buttons wide enough for comfortable touch interaction.
- Use responsive tables or card-based record layouts.
- Keep validation messages close to their fields.
- Avoid horizontal page overflow.
- Support keyboard navigation and visible focus indicators.

Use Bootstrap responsive breakpoints and utilities rather than creating separate applications for each screen size.

13. Accessibility and Usability

- Associate every form field with a visible label.
- Use meaningful button labels instead of icon-only actions where possible.
- Provide sufficient color contrast.
- Do not communicate status through color alone.
- Make validation errors understandable to users and screen readers.
- Maintain visible keyboard focus.
- Ask for confirmation before deactivation or other destructive actions.
- Keep page titles and navigation consistent.

14. Wireframe Acceptance Criteria

The wireframes will be considered complete when:

- All eight requested pages are documented.
- Each page defines its layout, fields/components, navigation, validation, loading, empty, and error states.
- Role-based navigation reflects the approved SRS.
- Administrator, Faculty, and Student permissions are clearly distinguished.
- Desktop, tablet, and mobile behavior is specified.
- Bootstrap is identified as the UI framework.
- No unapproved feature is treated as a mandatory requirement.
- The frontend specification remains consistent with the API requirements, database design, and RBAC matrix.

