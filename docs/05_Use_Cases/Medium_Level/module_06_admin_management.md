# Module 6: Admin & User Management - Medium-Level Use Cases

> **Module**: 6 - Admin & User Management  
> **High-Level UC**: [UC-HL-006](../High_Level/uc_hl_06_admin_management.md)

---

## UC-M6-001: Create User
**ID**: UC-M6-001 | **Priority**: 🔴 P0 | **Actor**: SuperAdmin  
**Related**: US-ADM-001, FR-ADM-001

**Goal**: Create new user account  
**Preconditions**: User is SuperAdmin  
**Main Flow**:
1. Admin clicks "Add User"
2. System displays form: Name, Email, Faculty, Role
3. Admin enters information
4. System validates:
   - Email format and uniqueness
   - Faculty exists
   - Role is valid
5. System creates user with default password
6. System sends welcome email (optional)
7. System shows "User created successfully"

**Postconditions**: User account created  
**Business Rules**: BR-ADM-006 (email unique), default role = Researcher

---

## UC-M6-002: Edit User
**ID**: UC-M6-002 | **Priority**: 🔴 P0 | **Actor**: SuperAdmin  
**Related**: US-ADM-001, FR-ADM-001

**Goal**: Edit existing user  
**Main Flow**:
1. Admin selects user from list
2. Admin clicks "Edit"
3. System shows editable form
4. Admin modifies: Name, Email, Faculty, Role
5. Admin saves
6. System validates and updates
7. System logs change in audit trail

**Business Rules**: BR-ADM-002 (cannot edit self to remove SuperAdmin)

---

##UC-M6-003: Delete User
**ID**: UC-M6-003 | **Priority**: 🔴 P0 | **Actor**: SuperAdmin  
**Related**: US-ADM-001, FR-ADM-001

**Goal**: Delete user account  
**Main Flow**:
1. Admin selects user
2. Admin clicks "Delete"
3. System confirms: "Are you sure? This cannot be undone."
4. Admin confirms
5. System soft deletes (sets deleted_at)
6. User locked out immediately

**Business Rules**: BR-ADM-002 (cannot delete self), BR-ADM-002 (at least 1 SuperAdmin)

---

## UC-M6-004: Assign Roles
**ID**: UC-M6-004 | **Priority**: 🔴 P0 | **Actor**: SuperAdmin  
**Related**: US-ADM-002, FR-ADM-002

**Goal**: Assign or remove user roles  
**Main Flow**:
1. Admin views user details
2. Admin sees current roles
3. Admin selects/deselects roles:
   - SuperAdmin
   - Researcher
   - Faculty Reviewer
   - University Reviewer
4. User can have MULTIPLE roles
5. System updates permissions immediately
6. System logs role changes

**Business Rules**: BR-ADM-001 (only SuperAdmin can assign), BR-ADM-003 (role hierarchy)

---

## UC-M6-005: Manage Faculties
**ID**: UC-M6-005 | **Priority**: 🔴 P0 | **Actor**: SuperAdmin  
**Related**: US-ADM-003, FR-ADM-003

**Goal**: CRUD faculties/departments  
**Main Flow**:
1. Admin clicks "Manage Faculties"
2. Admin can:
   - Add new faculty (name, code)
   - Edit faculty info
   - Delete faculty (only if no users assigned)
   - Assign Faculty Reviewer to each faculty
3. Changes saved to database

**Business Rules**: Cannot delete faculty with assigned users

---

## UC-M6-006: Configure LDAP
**ID**: UC-M6-006 | **Priority**: 🔴 P0 | **Actor**: SuperAdmin  
**Related**: US-ADM-004, FR-ADM-004

**Goal**: Configure LDAP/AD authentication  
**Main Flow**:
1. Admin clicks "System Config" → "LDAP"
2. Admin enters:
   - LDAP Server URL
   - Base DN
   - Bind DN and Password
   - Search filter
3. Admin clicks "Test Connection"
4. System attempts LDAP bind
5. If success: "Connection successful ✓"
6. Admin saves configuration

**Postconditions**: Users can login with university credentials  
**Business Rules**: Must test before saving

---

## UC-M6-007: Configure Email
**ID**: UC-M6-007 | **Priority**: 🔴 P0 | **Actor**: SuperAdmin  
**Related**: US-ADM-005, FR-ADM-005

**Goal**: Configure SMTP email settings  
**Main Flow**:
1. Admin clicks "System Config" → "Email"
2. Admin enters:
   - SMTP Host, Port
   - Username, Password
   - From Address
   - Use TLS: Yes/No
3. Admin clicks "Send Test Email"
4. System sends test email
5. Admin confirms receipt
6. Admin saves configuration

**Postconditions**: Notifications can be sent

---

## UC-M6-008: View Audit Logs
**ID**: UC-M6-008 | **Priority**: 🔴 P0 | **Actor**: SuperAdmin  
**Related**: US-ADM-006, FR-ADM-006

**Goal**: View system audit logs  
**Main Flow**:
1. Admin clicks "Audit Logs"
2. System displays filterable log:
   - User login/logout
   - Publication state changes
   - User role changes
   - Config changes
3. Admin filters by: Date range, User, Action type
4. Admin can export to CSV

**Business Rules**: BR-ADM-004 (all logged, immutable, 2-year retention)

---

## UC-M6-009: Backup System
**ID**: UC-M6-009 | **Priority**: 🔴 P0 | **Actor**: SuperAdmin  
**Related**: US-ADM-007, FR-ADM-007

**Goal**: Create system backup  
**Main Flow**:
1. Admin clicks "Backup"
2. System warns: "May take several minutes"
3. System backs up:
   - Database (SQL dump)
   - Uploaded files
4. System creates .zip file
5. System provides download link
6. Admin can schedule daily backups

**Business Rules**: BR-ADM-005 (daily auto-backup, keep 30 days)

---

## UC-M6-010: Import Users from Excel
**ID**: UC-M6-010 | **Priority**: 🟡 P1 | **Actor**: SuperAdmin  
**Related**: US-ADM-009, FR-ADM-009

**Goal**: Bulk import users  
**Main Flow**:
1. Admin downloads template Excel
2. Admin fills: Name, Email, Faculty, Role
3. Admin uploads file
4. System validates each row
5. System shows preview with errors (if any)
6. Admin confirms import
7. System creates users
8. System shows summary: "50 created, 3 failed"

**Business Rules**: Validate all rows before import

---

**Tài liệu liên quan**:
- [High-Level UC-HL-006](../High_Level/uc_hl_06_admin_management.md)
- [User Stories - SuperAdmin](../../04_User_Stories/By_Role/admin_stories.md)
- [Requirements - Admin](../../03_Requirements/Functional/module_admin.md)
