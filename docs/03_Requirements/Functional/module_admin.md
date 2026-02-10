# Module 6: Admin & User Management - Yêu Cầu Chức Năng

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Module**: Quản trị Hệ thống  
> 👥 **Users**: SuperAdmin

---

## 1. Functional Requirements

### FR-ADM-001: User Management (CRUD)
**Priority**: 🔴 P0 - Must Have

**Actions**:
- Create user (manual hoặc import từ Excel)
- Edit user (name, email, faculty, role)
- Delete user (soft delete)
- Lock/Unlock account
- Reset password

---

### FR-ADM-002: Role Assignment
**Priority**: 🔴 P0 - Must Have

**Roles**:
- SuperAdmin
- Researcher
- Faculty Reviewer
- University Reviewer
- Viewer (default)

**Business Rules**:
- 1 user có thể có nhiều roles
- Researcher + Faculty Reviewer (common)

---

### FR-ADM-003: Faculty/Department Management
**Priority**: 🔴 P0 - Must Have

**CRUD**:
- Add/Edit/Delete Faculty
- Assign Faculty Reviewer
- List researchers by faculty

---

### FR-ADM-004: LDAP/AD Configuration
**Priority**: 🔴 P0 - Must Have

**Settings**:
- LDAP server URL
- Base DN
- Bind DN, password
- Test connection

---

### FR-ADM-005: Email Configuration
**Priority**: 🔴 P0 - Must Have

**SMTP Settings**:
- Host, Port
- Username, Password
- From address
- Test email

---

### FR-ADM-006: Audit Logs
**Priority**: 🔴 P0 - Must Have

**Log events**:
- User login/logout
- Publication state changes
- User role changes
- System config changes

**View**:
- Filter by user, action type, date range
- Export to CSV

---

### FR-ADM-007: Backup & Restore
**Priority**: 🔴 P0 - Must Have

**Backup**:
- Manual trigger
- Scheduled (daily)
- Database + Files

**Restore**:
- Select backup file
- Restore with confirmation

---

### FR-ADM-008: System Dashboard
**Priority**: 🟡 P1 - Should Have

**Metrics**:
- Users online
- Total users by role
- Total publications by status
- System health (CPU, Memory, Disk)

---

### FR-ADM-009: Import Users từ Excel
**Priority**: 🟡 P1 - Should Have

**Format**: Name, Email, Faculty, Role

**Validation**:
- Email format
- Faculty exists
- Role valid

---

### FR-ADM-010: Bulk Operations
**Priority**: 🟡 P1 - Should Have

**Actions**:
- Assign role to multiple users
- Move users to different faculty
- Lock/Unlock multiple accounts

---

## 2. Permissions

| Action | SuperAdmin | Others |
|--------|-----------|--------|
| All admin functions | ✅ | ❌ |

---

**Tài liệu liên quan**:
- [User Needs - SuperAdmin](../../02_System_Clarification/User_Analysis/user_needs.md#5-superadmin)
