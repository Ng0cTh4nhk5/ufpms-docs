# Module 5: Reporting & Analytics - Yêu Cầu Chức Năng

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Module**: Báo cáo và Thống kê  
> 👥 **Users**: University Reviewer, Faculty Reviewer, SuperAdmin

---

## 1. Functional Requirements

### FR-REP-001: Dashboard Analytics
**Priority**: 🟡 P1 - Should Have

**Metrics**:
- Total publications (all time)
- Publications this year
- By quartile (Q1/Q2/Q3/Q4)
- By faculty
- Top researchers

**Visualization**:
- Line chart: Trend by year
- Pie chart: Distribution by quartile
- Bar chart: By faculty

---

### FR-REP-002: Report by Faculty
**Priority**: 🟡 P1 - Should Have

**Acceptance Criteria**:
```
GIVEN chọn Faculty và Year range
WHEN generate report
THEN export:
  - List of publications
  - Grouped by researcher
  - Summary statistics
  - Excel/PDF format
```

---

### FR-REP-003: Report by Quartile
**Priority**: 🟡 P1 - Should Have

**Breakdown**:
- Q1 publications
- Q2 publications
- Q3/Q4 publications
- Conference papers

---

### FR-REP-004: Trend Analysis
**Priority**: 🟢 P2 - Nice to Have

**Show**:
- Year-over-year growth
- Top growing faculties
- Emerging research fields (từ keywords)

---

### FR-REP-005: Export Report
**Priority**: 🔴 P0 - Must Have

**Formats**:
- Excel (.xlsx)
- PDF
- CSV

**Speed**: < 5 phút (vs 2-3 ngày hiện tại)

---

### FR-REP-006: Scheduled Reports
**Priority**: 🟢 P2 - Nice to Have

**Auto-generate monthly/quarterly reports**:
- Email to university leaders
- Save to archive

---

### FR-REP-007: Top Researchers
**Priority**: 🟡 P1 - Should Have

**Ranking by**:
- Total publications
- Q1 publications
- Most productive this year

---

## 2. Permissions

| Report Type | Faculty Reviewer | University Reviewer | SuperAdmin |
|-------------|------------------|---------------------|------------|
| Faculty report (own) | ✅ | ✅ | ✅ |
| Faculty report (all) | ❌ | ✅ | ✅ |
| University-wide | ❌ | ✅ | ✅ |
| Trend analysis | ❌ | ✅ | ✅ |

---

**Tài liệu liên quan**:
- [User Needs - University Reviewer](../../02_System_Clarification/User_Analysis/user_needs.md#3-university-reviewer)
