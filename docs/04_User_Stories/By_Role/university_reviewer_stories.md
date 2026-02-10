# User Stories - University Reviewer

> 👤 **Role**: University Reviewer (Cán bộ Trường)  
> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục tiêu**: Phê duyệt cuối cùng và công bố, quản lý báo cáo toàn trường

---

## Tổng Quan

**Total Stories**: 10  
**P0 (Must Have)**: 6  
**P1 (Should Have)**: 3  
**P2 (Nice to Have)**: 1

---

## Module 2: Approval Workflow - University Review

### US-UNR-001: Xem Dashboard Chờ Duyệt Trường
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-010

**User Story**:
```
As a University Reviewer,
I want to see all university-wide publications pending final approval,
So that I can manage the final review process.
```

**Acceptance Criteria**:
```
GIVEN I am logged in as a University Reviewer
WHEN I access "University Review Dashboard"
THEN I see ONLY publications with status FACULTY_APPROVED
AND I can filter by: Faculty, Journal Type, Year
AND results are sorted: Oldest first
AND columns show: Title, Author, Faculty, Faculty Review Date
```

---

### US-UNR-002: Xem Ý Kiến Cấp Khoa
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-011

**User Story**:
```
As a University Reviewer,
I want to see the faculty reviewer's comments and decision,
So that I can make an informed final approval decision.
```

**Acceptance Criteria**:
```
GIVEN a publication is in FACULTY_APPROVED status
WHEN I view its details
THEN I see:
- Faculty reviewer's name
- Faculty approval date  
- Faculty reviewer's comments (if any)
- Revision history (if there were revisions)
```

---

### US-UNR-003: Phê Duyệt và Công Bố
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-012

**User Story**:
```
As a University Reviewer,
I want to give final approval and publish publications,
So that they become publicly visible on the platform.
```

**Acceptance Criteria**:
```
GIVEN a publication is in UNIVERSITY_REVIEWING status
WHEN I click "Approve & Publish"
THEN the status changes to PUBLISHED
AND an email is sent to the researcher: "Your publication is now published!"
AND the publication appears publicly in Search and on the researcher's profile
AND an audit log is created
```

---

### US-UNR-004: Từ Chối Cấp Trường
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-013

**User Story**:
```
As a University Reviewer,
I want to reject publications at the university level if needed,
So that publications not meeting university standards aren't published.
```

**Acceptance Criteria**:
```
GIVEN a publication is in UNIVERSITY_REVIEWING status
WHEN I click "Reject" and enter a reason (required)
THEN the status changes to UNIVERSITY_REJECTED
AND an email is sent to both the researcher and Faculty Reviewer
AND an audit log is created
```

---

### US-UNR-005: Xem Audit Trail
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-015

**User Story**:
```
As a University Reviewer,
I want to see the complete audit trail of all publications,
So that I can track the entire approval process.
```

**Acceptance Criteria**:
```
GIVEN I am viewing any publication
WHEN I access the audit trail
THEN I see all status transitions from all levels (Faculty and University)
WITH reviewer names, roles, comments, and timestamps
```

---

### US-UNR-006: Nhận Thông Báo Email
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-016

**User Story**:
```
As a University Reviewer,
I want to receive notifications when publications are approved at faculty level,
So that I know when new publications need my final review.
```

**Acceptance Criteria**:
```
GIVEN a publication has been approved at faculty level
WHEN the status changes to FACULTY_APPROVED
THEN I receive an email with:
- Subject: "[UFPMS] Publication awaiting university review"
- Author name, faculty, and publication title
- Faculty reviewer's name and approval date
- Direct link to review
```

---

## Module 5: Reporting & Analytics

### US-UNR-007: Xem Dashboard Analytics Toàn Trường
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-REP-001

**User Story**:
```
As a University Reviewer,
I want to see university-wide publication analytics,
So that I can monitor overall research productivity.
```

**Acceptance Criteria**:
```
GIVEN I am on the analytics dashboard
WHEN the page loads
THEN I see:
- Total publications (all time and this year)
- Distribution by quartile (Q1/Q2/Q3/Q4)
- Distribution by faculty
- Top researchers
WITH visualizations:
- Line chart: Trend by year
- Pie chart: Distribution by quartile
- Bar chart: By faculty
```

---

### US-UNR-008: Tạo Báo Cáo Toàn Trường
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-REP-002, FR-REP-005

**User Story**:
```
As a University Reviewer,
I want to generate comprehensive university-wide reports,
So that I can provide leadership with research output data.
```

**Acceptance Criteria**:
```
GIVEN I select parameters (year range, faculty filter, etc.)
WHEN I click "Generate Report"
THEN the system generates a report with:
- All published publications
- Grouped by faculty and researcher
- Summary statistics
AND I can export in Excel/PDF/CSV format
AND generation completes in < 5 minutes
```

---

### US-UNR-009: Xem Báo Cáo Theo Quartile
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-REP-003

**User Story**:
```
As a University Reviewer,
I want to see publication breakdown by journal quartile,
So that I can assess research quality metrics.
```

**Acceptance Criteria**:
```
GIVEN I access the quartile report
WHEN I select a year range
THEN I see breakdown:
- Q1 publications (count and list)
- Q2 publications (count and list)
- Q3/Q4 publications (count and list)
- Conference papers (count and list)
WITH comparisons to previous years
```

---

### US-UNR-010: Xem Xu Hướng Phát Triển
**Priority**: 🟢 P2 - Nice to Have  
**Related FR**: FR-REP-004

**User Story**:
```
As a University Reviewer,
I want to see trend analysis and emerging research areas,
So that I can identify growth opportunities.
```

**Acceptance Criteria**:
```
GIVEN I access trend analysis
WHEN the report loads
THEN I see:
- Year-over-year growth rate
- Top growing faculties
- Emerging research fields (from keywords)
- Most productive researchers this year
```

---

## Traceability Matrix

| Story ID | Title | Priority | FR ID | Module |
|----------|-------|----------|-------|--------|
| US-UNR-001 | Xem Dashboard Chờ Duyệt Trường | P0 | FR-APR-010 | 2 |
| US-UNR-002 | Xem Ý Kiến Cấp Khoa | P0 | FR-APR-011 | 2 |
| US-UNR-003 | Phê Duyệt và Công Bố | P0 | FR-APR-012 | 2 |
| US-UNR-004 | Từ Chối Cấp Trường | P0 | FR-APR-013 | 2 |
| US-UNR-005 | Xem Audit Trail | P0 | FR-APR-015 | 2 |
| US-UNR-006 | Nhận Thông Báo Email | P0 | FR-APR-016 | 2 |
| US-UNR-007 | Xem Dashboard Analytics Toàn Trường | P1 | FR-REP-001 | 5 |
| US-UNR-008 | Tạo Báo Cáo Toàn Trường | P1 | FR-REP-002, FR-REP-005 | 5 |
| US-UNR-009 | Xem Báo Cáo Theo Quartile | P1 | FR-REP-003 | 5 |
| US-UNR-010 | Xem Xu Hướng Phát Triển | P2 | FR-REP-004 | 5 |

---

**Tài liệu liên quan**:
- [Requirements - Approval Workflow](../../03_Requirements/Functional/module_approval_workflow.md)
- [Requirements - Reporting](../../03_Requirements/Functional/module_reporting.md)
- [To-Be Process](../../02_System_Clarification/Business_Context/to_be_process.md)
