# User Stories - SuperAdmin

> 👤 **Role**: SuperAdmin  
> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục tiêu**: Quản trị hệ thống, người dùng, và cấu hình

---

## Tổng Quan

**Total Stories**: 10  
**P0 (Must Have)**: 8  
**P1 (Should Have)**: 2  
**P2 (Nice to Have)**: 0

---

## Module 6: Admin & User Management

### US-ADM-001: Quản Lý Người Dùng (CRUD)
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-ADM-001

**User Story**:
```
As a SuperAdmin,
I want to create, edit, and delete user accounts,
So that I can manage who has access to the system.
```

**Acceptance Criteria**:
```
GIVEN I am logged in as SuperAdmin
WHEN I access the User Management page
THEN I can:
- Create new users manually or import from Excel
- Edit user details (name, email, faculty, role)
- Delete users (soft delete)
- Lock/Unlock accounts
- Reset passwords
```

---

### US-ADM-002: Gán Vai Trò Người Dùng
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-ADM-002

**User Story**:
```
As a SuperAdmin,
I want to assign and manage user roles,
So that users have appropriate permissions for their responsibilities.
```

**Acceptance Criteria**:
```
GIVEN I am editing a user
WHEN I access the roles section
THEN I can assign multiple roles:
- SuperAdmin
- Researcher (default)
- Faculty Reviewer
- University Reviewer
- Viewer
AND a user can have multiple roles simultaneously
```

---

### US-ADM-003: Quản Lý Khoa/Đơn Vị
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-ADM-003

**User Story**:
```
As a SuperAdmin,
I want to manage faculty/department information,
So that the organizational structure is up to date.
```

**Acceptance Criteria**:
```
GIVEN I am in Faculty Management
WHEN I perform CRUD operations
THEN I can:
- Add/Edit/Delete faculties
- Assign Faculty Reviewers to each faculty
- View list of researchers by faculty
```

---

### US-ADM-004: Cấu Hình LDAP/AD
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-ADM-004

**User Story**:
```
As a SuperAdmin,
I want to configure LDAP/AD authentication settings,
So that users can log in with university credentials.
```

**Acceptance Criteria**:
```
GIVEN I am in System Configuration
WHEN I access LDAP settings
THEN I can configure:
- LDAP server URL
- Base DN
- Bind DN and password
AND I can test the connection before saving
```

---

### US-ADM-005: Cấu Hình Email
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-ADM-005

**User Story**:
```
As a SuperAdmin,
I want to configure email server settings,
So that the system can send notifications to users.
```

**Acceptance Criteria**:
```
GIVEN I am in System Configuration
WHEN I access Email settings
THEN I can configure:
- SMTP Host and Port
- Username and Password
- From address
AND I can send a test email to verify settings
```

---

### US-ADM-006: Xem Audit Logs
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-ADM-006

**User Story**:
```
As a SuperAdmin,
I want to view system audit logs,
So that I can monitor user activities and system changes.
```

**Acceptance Criteria**:
```
GIVEN I am on the Audit Logs page
WHEN I view the logs
THEN I see all events:
- User login/logout
- Publication state changes
- User role changes
- System configuration changes
AND I can filter by: User, Action Type, Date Range
AND I can export logs to CSV
```

---

### US-ADM-007: Backup và Restore
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-ADM-007

**User Story**:
```
As a SuperAdmin,
I want to backup and restore the system,
So that data is protected and can be recovered if needed.
```

**Acceptance Criteria**:
```
GIVEN I am on the Backup page
WHEN I trigger a backup
THEN the system:
- Backs up the database
- Backs up uploaded files
- Can be scheduled (daily automatic backup)
AND I can select a backup file to restore
WITH confirmation before restoring
```

---

### US-ADM-008: Xem System Dashboard
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-ADM-008

**User Story**:
```
As a SuperAdmin,
I want to see system health and usage statistics,
So that I can monitor system performance.
```

**Acceptance Criteria**:
```
GIVEN I am on the Admin Dashboard
WHEN the page loads
THEN I see:
- Users currently online
- Total users by role
- Total publications by status
- System health metrics (CPU, Memory, Disk usage)
```

---

### US-ADM-009: Import Người Dùng từ Excel
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-ADM-009

**User Story**:
```
As a SuperAdmin,
I want to bulk import users from an Excel file,
So that I can efficiently onboard many users at once.
```

**Acceptance Criteria**:
```
GIVEN I have an Excel file with format: Name, Email, Faculty, Role
WHEN I upload and process the file
THEN the system:
- Validates email format
- Validates faculty exists
- Validates role is valid
- Creates users
- Shows a summary report (success/failed)
```

---

### US-ADM-010: Thao Tác Hàng Loạt
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-ADM-010

**User Story**:
```
As a SuperAdmin,
I want to perform bulk operations on multiple users,
So that I can manage users efficiently.
```

**Acceptance Criteria**:
```
GIVEN I have selected multiple users (checkboxes)
WHEN I choose a bulk action
THEN I can:
- Assign roles to all selected users
- Move users to a different faculty
- Lock/Unlock multiple accounts
- Delete multiple users
WITH a confirmation dialog before executing
```

---

## Traceability Matrix

| Story ID | Title | Priority | FR ID | Module |
|----------|-------|----------|-------|--------|
| US-ADM-001 | Quản Lý Người Dùng (CRUD) | P0 | FR-ADM-001 | 6 |
| US-ADM-002 | Gán Vai Trò Người Dùng | P0 | FR-ADM-002 | 6 |
| US-ADM-003 | Quản Lý Khoa/Đơn Vị | P0 | FR-ADM-003 | 6 |
| US-ADM-004 | Cấu Hình LDAP/AD | P0 | FR-ADM-004 | 6 |
| US-ADM-005 | Cấu Hình Email | P0 | FR-ADM-005 | 6 |
| US-ADM-006 | Xem Audit Logs | P0 | FR-ADM-006 | 6 |
| US-ADM-007 | Backup và Restore | P0 | FR-ADM-007 | 6 |
| US-ADM-008 | Xem System Dashboard | P1 | FR-ADM-008 | 6 |
| US-ADM-009 | Import Người Dùng từ Excel | P1 | FR-ADM-009 | 6 |
| US-ADM-010 | Thao Tác Hàng Loạt | P0 | FR-ADM-010 | 6 |

---

**Tài liệu liên quan**:
- [Requirements - Admin & User Management](../../03_Requirements/Functional/module_admin.md)
