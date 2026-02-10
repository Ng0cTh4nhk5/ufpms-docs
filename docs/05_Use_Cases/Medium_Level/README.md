# Medium-Level Use Cases - README

> 📁 **Level**: Medium-Level Use Cases  
> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục đích**: Chi tiết 54 use cases theo chức năng của từng module

---

## 📊 Tổng Quan

Medium-level use cases chia nhỏ các high-level use cases thành các chức năng cụ thể, mỗi chức năng là 1 use case độc lập với preconditions, main flow, và postconditions rõ ràng.

### 54 Medium-Level Use Cases

| Module | File | SL Use Cases | P0 | P1 | P2 |
|--------|------|---------|----|----|---- |
| 1. Publication Management | [module_01_publication_management.md](./module_01_publication_management.md) | 9 | 7 | 2 | 0 |
| 2. Approval Workflow | [module_02_approval_workflow.md](./module_02_approval_workflow.md) | 15 | 10 | 3 | 2 |
| 3. Search & Browse | [module_03_search_browse.md](./module_03_search_browse.md) | 7 | 2 | 4 | 1 |
| 4. Researcher Profile | [module_04_researcher_profile.md](./module_04_researcher_profile.md) | 6 | 0 | 3 | 3 |
| 5. Reporting & Analytics | [module_05_reporting_analytics.md](./module_05_reporting_analytics.md) | 7 | 0 | 5 | 2 |
| 6. Admin & User Management | [module_06_admin_management.md](./module_06_admin_management.md) | 10 | 8 | 2 | 0 |
| **TỔNG** | | **54** | **27** | **19** | **8** |

---

## 📋 Use Case Format

Mỗi medium-level use case bao gồm:

```markdown
## UC-MX-XXX: [Use Case Name]

**ID**: UC-MX-XXX
**Priority**: P0/P1/P2
**Actor(s)**: [Actor names]
**Related User Stories**: US-XXX-XXX, ...
**Related FR**: FR-XXX-XXX

### Goal
Brief description

### Preconditions
- Required system/user states

### Main Flow
1. Step 1
2. Step 2
...

### Postconditions
**Success**: What happens on success
**Failure**: What happens on failure

### Business Rules
- BR-XXX-001: Rule description
```

---

## 📖 Modules

### [Module 1: Publication Management](./module_01_publication_management.md)
9 use cases cho CRUD operations, file upload, và validation.

- UC-M1-001: Create Publication
- UC-M1-002: Edit Publication  
- UC-M1-003: Delete Publication
- UC-M1-004: View Publication List
- UC-M1-005: View Publication Details
- UC-M1-006: Upload PDF File
- UC-M1-007: Download PDF File
- UC-M1-008: Add Co-Authors
- UC-M1-009: Validate DOI/ISSN

---

### [Module 2: Approval Workflow](./module_02_approval_workflow.md)
15 use cases cho 2-tier approval process.

**Researcher Actions** (4):
- UC-M2-001: Submit for Review
- UC-M2-002: Track Review Status
- UC-M2-003: Revise Publication
- UC-M2-004: Withdraw Submission

**Faculty Reviewer Actions** (4):
- UC-M2-005: Faculty Review - Approve
- UC-M2-006: Faculty Review - Request Revision
- UC-M2-007: Faculty Review - Reject
- UC-M2-012: Bulk Approve (Faculty)

**University Reviewer Actions** (4):
- UC-M2-008: University Review - Approve & Publish
- UC-M2-009: University Review - Reject
- UC-M2-013: Bulk Approve (University)
- UC-M2-014: Reassign Reviewer

**System Actions** (3):
- UC-M2-010: View Review History
- UC-M2-011: Send Email Notifications
- UC-M2-015: SLA Monitoring

---

### [Module 3: Search & Browse](./module_03_search_browse.md)
7 use cases tìm kiếm và duyệt công khai.

- UC-M3-001: Basic Search
- UC-M3-002: Advanced Search
- UC-M3-003: Filter Results
- UC-M3-004: Sort Results
- UC-M3-005: View Publication Details (Public)
- UC-M3-006: Browse by Faculty
- UC-M3-007: Browse by Year/Quartile

---

### [Module 4: Researcher Profile](./module_04_researcher_profile.md)
6 use cases quản lý profile công khai.

- UC-M4-001: View Public Profile
- UC-M4-002: Edit Profile
- UC-M4-003: Update Profile Photo
- UC-M4-004: Link ORCID
- UC-M4-005: View Publication Analytics
- UC-M4-006: Generate Word Cloud

---

### [Module 5: Reporting & Analytics](./module_05_reporting_analytics.md)
7 use cases báo cáo và phân tích.

- UC-M5-001: Generate Faculty Report
- UC-M5-002: Generate University Report
- UC-M5-003: Export to Excel
- UC-M5-004: Export to PDF
- UC-M5-005: View Dashboard Statistics
- UC-M5-006: Track Productivity Trends
- UC-M5-007: Benchmark Faculties

---

### [Module 6: Admin & User Management](./module_06_admin_management.md)
10 use cases quản trị hệ thống.

- UC-M6-001: Create User
- UC-M6-002: Edit User
- UC-M6-003: Delete User
- UC-M6-004: Assign Roles
- UC-M6-005: Manage Faculties
- UC-M6-006: Configure LDAP
- UC-M6-007: Configure Email
- UC-M6-008: View Audit Logs
- UC-M6-009: Backup System
- UC-M6-010: Import Users from Excel

---

**Tài liệu liên quan**:
- [High-Level Use Cases](../High_Level/)
- [Detailed-Level Use Cases](../Detailed_Level/)
- [Main README](../README.md)
