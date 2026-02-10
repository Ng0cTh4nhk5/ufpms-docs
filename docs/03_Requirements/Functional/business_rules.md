# Quy Tắc Nghiệp Vụ - UFPMS

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục đích**: Định nghĩa quy tắc nghiệp vụ cốt lõi

---

## 1. State Transition Rules

### BR-001: Quyền Chuyển Trạng Thái

| From State | To State | Who Can | Condition |
|-----------|----------|---------|-----------|
| DRAFT | SUBMITTED | Researcher (owner) | Đủ required fields |
| SUBMITTED | FACULTY_REVIEWING | Faculty Reviewer | Auto hoặc manual |
| FACULTY_REVIEWING | FACULTY_APPROVED | Faculty Reviewer | - |
| FACULTY_REVIEWING | REVISION_REQUIRED | Faculty Reviewer | Phải có comment |
| FACULTY_REVIEWING | FACULTY_REJECTED | Faculty Reviewer | Phải có lý do |
| REVISION_REQUIRED | DRAFT | Researcher (owner) | - |
| FACULTY_APPROVED | UNIVERSITY_REVIEWING | University Reviewer | Auto hoặc manual |
| UNIVERSITY_REVIEWING | PUBLISHED | University Reviewer | - |
| UNIVERSITY_REVIEWING | UNIVERSITY_REJECTED | University Reviewer | Phải có lý do |

---

## 2. Visibility Rules

### BR-010: Quy Tắc Hiển Thị Công Trình

```
DRAFT:
  - Visible to: Owner + SuperAdmin
  - NOT visible: Reviewers, Public

SUBMITTED, FACULTY_REVIEWING, REVISION_REQUIRED, FACULTY_REJECTED:
  - Visible to: Owner + Faculty Reviewer (same faculty) + SuperAdmin
  - NOT visible: Public

FACULTY_APPROVED, UNIVERSITY_REVIEWING, UNIVERSITY_REJECTED:
  - Visible to: Owner + Faculty Reviewer + University Reviewer + SuperAdmin
  - NOT visible: Public

PUBLISHED:
  - Visible to: EVERYONE (Public)
  - Xuất hiện trong: Search, Profile, Reports
```

---

## 3. Data Validation Rules

### BR-020: DOI Format
```
Pattern: 10.xxxx/xxxxx
Regex: ^10\.\d{4,9}/[-._;()/:A-Z0-9]+$
Example: 10.1000/xyz123
```

### BR-021: ISSN Format
```
Pattern: xxxx-xxxx
Regex: ^\d{4}-\d{3}[0-9X]$
Example: 1234-567X
```

### BR-022: ORCID Format
```
Pattern: 0000-0002-xxxx-xxxx
Regex: ^\d{4}-\d{4}-\d{4}-\d{3}[0-9X]$
Example: 0000-0002-1825-0097
```

###BR-023: File Upload Rules
- File type: PDF only (`.pdf`)
- Max size: 10MB
- Sanitize filename (remove special chars)

---

## 4. Co-author Rules

### BR-030: Ownership và Permissions

```
Corresponding Author (Owner):
  - Có thể: Edit, Delete (if DRAFT), Submit, Withdraw
  - Là người đầu tiên tạo bài báo

Co-author:
  - Có thể: View only
  - KHÔNG thể: Edit, Delete, Submit
  - Xuất hiện trong profile của họ (khi PUBLISHED)
```

### BR-031: Duplicate Detection
```
IF publication có DOI
AND DOI đã tồn tại trong hệ thống
THEN
  - Hiển thị warning: "Bài này đã được [Researcher Name] khai báo"
  - Gợi ý: "Thêm làm đồng tác giả?"
  - Allow continue (có thể cùng DOI nhưng khác owner)
```

---

## 5. Review Assignment Rules

### BR-040: Faculty Review Assignment

```
Faculty Reviewer CHỈ xem được:
  - Publications từ Faculty của mình
  - Status: SUBMITTED hoặc FACULTY_REVIEWING
```

### BR-041: University Review Assignment

```
University Reviewer xem được:
  - Publications từ TẤT CẢ faculties
  - Status: FACULTY_APPROVED hoặc UNIVERSITY_REVIEWING
```

---

## 6. Audit Trail Rules

### BR-050: Logging Requirements

**Mọi state transition phải log**:
- Publication ID
- From Status → To Status
- Reviewer User ID, Name, Role
- Timestamp
- Comment/Reason (if any)

**Không được xóa audit logs** (immutable)

---

## 7. Email Notification Rules

### BR-060: Trigger Events

| Event | Recipients | Template |
|-------|-----------|----------|
| Publication submitted | Faculty Reviewer | "New publication pending" |
| Faculty approved | Researcher + University Reviewer | "Approved by faculty" |
| Revision required | Researcher | "Revision needed" |
| Faculty rejected | Researcher | "Rejected by faculty" |
| University approved (Published) | Researcher | "Congratulations! Published" |
| University rejected | Researcher + Faculty Reviewer | "Rejected by university" |

---

## 8. Performance Rules

### BR-070: SLA Targets

```
Target review time:
  - Faculty review: 3-7 days
  - University review: 3-7 days
  - Total: 6-14 days (from submit to publish)

Highlight công trình:
  - > 7 days trong FACULTY_REVIEWING: Yellow
  - > 14 days trong FACULTY_REVIEWING: Red
```

---

## 9. Data Retention Rules

### BR-080: Soft Delete
```
Khi delete publication (chỉ DRAFT):
  - Set deleted_at timestamp
  - KHÔNG xóa vật lý khỏi database
  - PDF file: Move to trash folder (xóa sau 30 ngày)
```

---

## 10. Security Rules

### BR-090: Authentication
```
Internal users (Researcher, Reviewer, Admin):
  - PHẢI đăng nhập qua LDAP/AD
  - Session timeout: 8 giờ
  - JWT token expiry: 24 giờ

Public users (Viewer):
  - KHÔNG cần đăng nhập
  - CHỈ access PUBLISHED content
```

### BR-091: Authorization
```
RBAC (Role-Based Access Control):
  - Check role trước mọi operation
  - Private endpoints: Require authentication
  - Public endpoints: No auth required

PDF Download:
  - DRAFT/REVIEWING: CHỈ owner + reviewers + admin
  - PUBLISHED: Everyone (if allowed by owner)
```

---

**Tài liệu liên quan**:
- [To-Be Process](../../02_System_Clarification/Business_Context/to_be_process.md)
- [Module 2: Approval Workflow](./module_approval_workflow.md)
