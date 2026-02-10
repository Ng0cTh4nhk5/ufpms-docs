# Module 5: Reporting & Analytics - Medium-Level Use Cases

> **Module**: 5 - Reporting & Analytics  
> **High-Level UC**: [UC-HL-005](../High_Level/uc_hl_05_reporting_analytics.md)

---

## UC-M5-001: Generate Faculty Report
**ID**: UC-M5-001 | **Priority**: 🟡 P1 | **Actor**: Faculty Reviewer  
**Related**: US-FCR-008, FR-REP-002

**Goal**: Generate faculty-level publication report  
**Preconditions**: User is Faculty Reviewer  
**Main Flow**:
1. Reviewer selects parameters:
   - Year range (from-to)
   - Group by: Researcher, Quartile, Type
2. Reviewer clicks "Generate Report"
3. System queriesPublications WHERE faculty = reviewer's faculty AND status = PUBLISHED
4. System generates report:
   - Summary: Total, by quartile, by type
   - Researcher breakdown
   - Detailed publication list
5. System displays preview

**Business Rules**: BR-REP-001 (only own faculty), BR-REP-002 (PUBLISHED only)

---

## UC-M5-002: Generate University Report
**ID**: UC-M5-002 | **Priority**: 🟡 P1 | **Actor**: University Reviewer  
**Related**: US-UNR-008, FR-REP-002, FR-REP-005

**Goal**: Generate university-wide report  
**Preconditions**: User is University Reviewer or SuperAdmin  
**Main Flow**:
1. Reviewer selects parameters:
   - Year range
   - Faculty filter (all or specific)
   - Grouping options
2. Reviewer clicks "Generate Report"
3. System queries all faculties
4. System generates comprehensive report:
   - University summary
   - By faculty comparison
   - By researcher (top researchers)
   - Detailed lists
5. System shows progress bar (may take 30s-5min)

**Postconditions**: Report ready for export  
**Business Rules**: BR-REP-001 (university-wide access), BR-REP-004 (< 5min)

---

## UC-M5-003: Export to Excel
**ID**: UC-M5-003 | **Priority**: 🟡 P1 | **Actor**: Faculty/University Reviewer  
**Related**: FR-REP-006

**Goal**: Export report to Excel format  
**Main Flow**:
1. User has generated report
2. User clicks "Export to Excel"
3. System creates .xlsx file with multiple sheets:
   - Summary
   - By Faculty
   - By Researcher
   - Detail (all publications)
4. System downloads file: `report_YYYY-MM-DD.xlsx`

**Business Rules**: BR-REP-005 (30-day retention)

---

## UC-M5-004: Export to PDF
**ID**: UC-M5-004 | **Priority**: 🟡 P1 | **Actor**: Faculty/University Reviewer  
**Related**: FR-REP-006

**Goal**: Export formatted report to PDF  
**Main Flow**:
1. User has generated report
2. User clicks "Export to PDF"
3. System generates formatted PDF with:
   - Cover page (university logo, date)
   - Summary page with charts
   - Detailed tables
4. System downloads file

---

## UC-M5-005: View Dashboard Statistics
**ID**: UC-M5-005 | **Priority**: 🟡 P1 | **Actor**: Faculty/University Reviewer  
**Related**: US-UNR-007, FR-REP-001

**Goal**: View real-time dashboardstatistics  
**Main Flow**:
1. Reviewer accesses dashboard
2. System displays key metrics:
   - Total publications (this year, all time)
   - Distribution by quartile (pie chart)
   - Distribution by faculty (bar chart)
   - Trend line (last 5 years)
   - Top researchers
3. Charts are interactive
4. Data updates on page load

**Business Rules**: BR-REP-003 (cache 1 hour)

---

## UC-M5-006: Track Productivity Trends
**ID**: UC-M5-006 | **Priority**: 🟢 P2 | **Actor**: University Reviewer  
**Related**: US-UNR-010, FR-REP-004

**Goal**: Analyze productivity trends  
**Main Flow**:
1. Reviewer accesses Trend Analysis
2. System calculates:
   - Year-over-year growth rate
   - Top growing faculties
   - Emerging research fields (keyword frequency)
   - Most productive researchers this year
3. System visualizes with charts

---

## UC-M5-007: Benchmark Faculties
**ID**: UC-M5-007 | **Priority**: 🟢 P2 | **Actor**: University Reviewer  
**Related**: FR-REP-007

**Goal**: Compare faculties side-by-side  
**Main Flow**:
1. Reviewer selects 2+ faculties
2. Reviewer selects year range
3. System shows comparison table:
   - Total publications
   - By quartile
   - Top researchers
4. System highlights best performers

---

**Tài liệu liên quan**:
- [High-Level UC-HL-005](../High_Level/uc_hl_05_reporting_analytics.md)
- [User Stories - Reviewers](../../04_User_Stories/By_Role/)
- [Requirements - Reporting](../../03_Requirements/Functional/module_reporting.md)
