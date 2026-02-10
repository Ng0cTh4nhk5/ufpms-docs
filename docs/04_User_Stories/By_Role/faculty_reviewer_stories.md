# User Stories - Faculty Reviewer

> 👤 **Role**: Faculty Reviewer (Cán bộ Khoa)  
> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục tiêu**: Xét duyệt bài báo cấp Khoa và quản lý báo cáo

---

## Tổng Quan

**Total Stories**: 9  
**P0 (Must Have)**: 6  
**P1 (Should Have)**: 2  
**P2 (Nice to Have)**: 1

---

## Module 2: Approval Workflow - Faculty Review

### US-FCR-001: Xem Dashboard Chờ Duyệt Khoa
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-005

**User Story**:
```
As a Faculty Reviewer,
I want to see all publications pending my review from my faculty,
So that I can manage my review workload effectively.
```

**Acceptance Criteria**:
```
GIVEN I am logged in as a Faculty Reviewer
WHEN I access "Faculty Review Dashboard"
THEN I see ONLY publications from my faculty
AND with status: SUBMITTED or FACULTY_REVIEWING
AND I can filter by: All / New / In Review
AND results are sorted: Oldest first
AND publications over 7 days old are highlighted
```

---

### US-FCR-002: Phê Duyệt Bài Báo
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-006

**User Story**:
```
As a Faculty Reviewer,
I want to approve publications that meet our faculty standards,
So that they can proceed to university-level review.
```

**Acceptance Criteria**:
```
GIVEN a publication is in FACULTY_REVIEWING status
WHEN I click "Approve" and optionally add a comment
THEN the status changes to FACULTY_APPROVED
AND an email is sent to the researcher: "Approved by Faculty"
AND an email is sent to University Reviewer: "New publication pending review"
AND an audit log is created (reviewer, timestamp, comment)
```

---

### US-FCR-003: Yêu Cầu Bổ Sung
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-007

**User Story**:
```
As a Faculty Reviewer,
I want to request revisions on publications that need improvement,
So that researchers can address issues before full approval.
```

**Acceptance Criteria**:
```
GIVEN a publication is in FACULTY_REVIEWING status
WHEN I click "Request Revision" and enter a comment (required, min 10 chars)
THEN the status changes to REVISION_REQUIRED
AND an email is sent to the researcher with my comment
AND an audit log is created
```

---

### US-FCR-004: Từ Chối Bài Báo
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-008

**User Story**:
```
As a Faculty Reviewer,
I want to reject publications that don't meet standards,
So that only quality work proceeds to the next level.
```

**Acceptance Criteria**:
```
GIVEN a publication is in FACULTY_REVIEWING status
WHEN I click "Reject" and enter a reason (required)
THEN the status changes to FACULTY_REJECTED
AND an email is sent to the researcher with the reason
AND an audit log is created
AND this decision cannot be reverted
```

---

### US-FCR-005: Xem Lịch Sử Xét Duyệt
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-015

**User Story**:
```
As a Faculty Reviewer,
I want to see the complete review history of a publication,
So that I can understand previous decisions and revisions.
```

**Acceptance Criteria**:
```
GIVEN I am viewing a publication's details
WHEN I check the audit trail section
THEN I see all status transitions with:
- From/To status
- Reviewer name and role
- Comments
- Timestamp
```

---

### US-FCR-006: Nhận Thông Báo Email
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-016

**User Story**:
```
As a Faculty Reviewer,
I want to receive email notifications when new publications need review,
So that I don't miss submissions requiring my attention.
```

**Acceptance Criteria**:
```
GIVEN a researcher has submitted a publication from my faculty
WHEN the status changes to SUBMITTED
THEN I receive an email with:
- Subject: "[UFPMS] New publication pending review"
- Author name and publication title
- Direct link to review the publication
```

---

### US-FCR-007: Duyệt Nhiều Bài Cùng Lúc
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-APR-009

**User Story**:
```
As a Faculty Reviewer,
I want to approve multiple publications at once,
So that I can process routine approvals more efficiently.
```

**Acceptance Criteria**:
```
GIVEN I have selected multiple publications (checkboxes)
WHEN I click "Approve Selected"
THEN all selected publications change to FACULTY_APPROVED
AND individual emails are sent to each researcher
AND one summary email is sent to the University Reviewer
```

---

## Module 5: Reporting & Analytics

### US-FCR-008: Xem Báo Cáo Khoa
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-REP-002

**User Story**:
```
As a Faculty Reviewer,
I want to generate reports for my faculty's publications,
So that I can track our research productivity.
```

**Acceptance Criteria**:
```
GIVEN I select my faculty and a year range
WHEN I click "Generate Report"
THEN I see a report with:
- List of all publications
- Grouped by researcher
- Summary statistics (total, by quartile)
AND I can export to Excel/PDF format
```

---

### US-FCR-009: Theo Dõi SLA Xét Duyệt
**Priority**: 🟢 P2 - Nice to Have  
**Related FR**: FR-APR-020

**User Story**:
```
As a Faculty Reviewer,
I want to see which publications are approaching or past the review deadline,
So that I can prioritize my review work.
```

**Acceptance Criteria**:
```
GIVEN I am on my review dashboard
WHEN I view the pending list
THEN publications over 7 days old are highlighted in yellow/red
AND I can see average review time metrics:
- Average time: SUBMITTED → FACULTY_APPROVED
- % reviewed within 7 days
```

---

## Traceability Matrix

| Story ID | Title | Priority | FR ID | Module |
|----------|-------|----------|-------|--------|
| US-FCR-001 | Xem Dashboard Chờ Duyệt Khoa | P0 | FR-APR-005 | 2 |
| US-FCR-002 | Phê Duyệt Bài Báo | P0 | FR-APR-006 | 2 |
| US-FCR-003 | Yêu Cầu Bổ Sung | P0 | FR-APR-007 | 2 |
| US-FCR-004 | Từ Chối Bài Báo | P0 | FR-APR-008 | 2 |
| US-FCR-005 | Xem Lịch Sử Xét Duyệt | P0 | FR-APR-015 | 2 |
| US-FCR-006 | Nhận Thông Báo Email | P0 | FR-APR-016 | 2 |
| US-FCR-007 | Duyệt Nhiều Bài Cùng Lúc | P1 | FR-APR-009 | 2 |
| US-FCR-008 | Xem Báo Cáo Khoa | P1 | FR-REP-002 | 5 |
| US-FCR-009 | Theo Dõi SLA Xét Duyệt | P2 | FR-APR-020 | 2 |

---

**Tài liệu liên quan**:
- [Requirements - Approval Workflow](../../03_Requirements/Functional/module_approval_workflow.md)
- [Requirements - Reporting](../../03_Requirements/Functional/module_reporting.md)
- [To-Be Process](../../02_System_Clarification/Business_Context/to_be_process.md)
