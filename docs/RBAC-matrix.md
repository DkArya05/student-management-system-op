Role-Based Access Control (RBAC) Matrix

1. Purpose

Role-Based Access Control (RBAC) ensures that users can access only the features and information permitted for their roles.

2. User Roles

- Administrator: Manages student records, courses, enrollments, and reports.
- Faculty: Accesses assigned academic records, records attendance, and enters marks.
- Student: Views their own permitted academic information, if student self-service is implemented.

3. Permission Matrix

Feature| Administrator| Faculty| Student
Login and logout| Yes| Yes| Yes, if enabled
View dashboard| Yes| Yes, role-specific| Yes, if enabled
Register student| Yes| No| No
View all student records| Yes| Assigned students only| No
Update student records| Yes| No, unless explicitly authorized| No
Manage courses| Yes| No| No
Manage enrollments| Yes| No| No
View assigned students| Yes| Yes| No
Record attendance| Yes, for administration| Assigned courses only| No
View attendance| All permitted records| Assigned courses| Own records only
Enter examination marks| Yes, if authorized| Assigned examinations/courses| No
View marks| All permitted records| Assigned courses| Own records only
View reports| Yes| Limited to assigned academic data| Own permitted information
Manage user roles| Yes| No| No

4. Security Rules

- Every user must authenticate before accessing protected features.
- The backend must verify permissions for every protected API request.
- The frontend must not be treated as the only security layer.
- Students must not access another student's private records.
- Faculty must not modify records outside their assigned permissions.
- Passwords must be stored as secure hashes.
- Sensitive configuration values must be kept in environment variables.
- Unauthorized requests must be rejected with an appropriate HTTP status.
- Administrative actions should be logged where practical.

5. Implementation Notes

- Use a role field associated with each user account.
- Apply authentication middleware to protected routes.
- Apply authorization checks based on the user's role and, where necessary, their assigned courses.
- Return only the data required by the authorized user.
- Do not expose password hashes in API responses.

6. Decisions to Confirm

- Whether students will have login accounts in the first release.
- Whether administrators can edit attendance and marks.
- Whether faculty can edit previously submitted attendance or marks.
- Whether audit logs will be included in the initial version.

These permissions must remain consistent with the approved SRS and be enforced by the backend.