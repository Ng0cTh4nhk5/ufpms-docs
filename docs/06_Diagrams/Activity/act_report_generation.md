# Report Generation Workflow - Activity Diagram

> 📊 **Diagram**: Report Generation  
> 🎯 **Scope**: Generate faculty/university reports  
> 👤 **Actors**: Faculty Reviewer, University Reviewer, SuperAdmin

---

## 📊 Activity Diagram

```mermaid
flowchart TD
    Start([User clicks<br/>"Generate Report"]) --> SelectType{Report type?}
    
    SelectType -->|Faculty Report| SetScopeFac[Scope:<br/>Current faculty only]
    SetScopeFac --> SelectPeriod
    
    SelectType -->|University Report| CheckRole{User role?}
    CheckRole -->|Not Uni Reviewer/Admin| ShowError[Show: Access Denied]
    ShowError --> End1([End])
    
    CheckRole -->|Authorized| SetScopeUni[Scope:<br/>All faculties]
    SetScopeUni --> SelectPeriod
    
    SelectPeriod[Select time period] --> PeriodOptions{Period type?}
    
    PeriodOptions -->|By Year| SelectYear[Select year:<br/>2020-current]
    SelectYear --> SelectMetrics
    
    PeriodOptions -->|By Date Range| SelectStart[Select start date]
    SelectStart --> SelectEnd[Select end date]
    SelectEnd --> ValidateRange{Valid range?}
    
    ValidateRange -->|End < Start| ShowError2[Show: Invalid range]
    ShowError2 --> SelectStart
    
    ValidateRange -->|> 5 years| ShowWarning[Show: Large range,<br/>may be slow]
    ShowWarning --> SelectMetrics
    
    ValidateRange -->|Valid| SelectMetrics
    
    SelectMetrics[Select metrics] --> MetricOptions{Include?}
    
    MetricOptions --> CheckTotal[☑ Total publications]
    CheckTotal --> CheckByType[☑ By type breakdown]
    CheckByType --> CheckByFaculty[☑ By faculty P1]
    CheckByFaculty --> CheckTopAuthors[☑ Top authors]
    CheckTopAuthors --> SelectFormat
    
    SelectFormat{Output format?}
    
    SelectFormat -->|View on screen| ClickGenerate[Click "Generate"]
    SelectFormat -->|Export| SelectExport{Export format?}
    
    SelectExport -->|PDF| SetFormatPDF[Format: PDF]
    SelectExport -->|Excel| SetFormatExcel[Format: Excel]
    SetFormatPDF --> ClickGenerate
    SetFormatExcel --> ClickGenerate
    
    ClickGenerate --> ShowLoading[Show loading spinner]
    
    ShowLoading --> QueryDB[Query database]
    QueryDB --> FilterData[Filter by:<br/>- Scope<br/>- Period<br/>- Status = PUBLISHED]
    
    FilterData --> AggregateData[Aggregate data:<br/>- Count by type<br/>- Count by year<br/>- Top authors]
    
    AggregateData --> CheckData{Data found?}
    
    CheckData -->|No data| ShowEmpty[Show:<br/>"No publications<br/>in this period"]
    ShowEmpty --> End2([End])
    
    CheckData -->|Has data| GenerateCharts[Generate charts:<br/>- Bar chart by type<br/>- Line chart by year<br/>- Pie chart by faculty]
    
    GenerateCharts --> FormatOutput{Output type?}
    
    FormatOutput -->|Screen| RenderHTML[Render HTML report]
    RenderHTML --> DisplayReport[Display on page]
    DisplayReport --> UserAction{User action?}
    
    UserAction -->|Save| SaveReport[Save report config<br/>for future P1]
    SaveReport --> End3([End])
    
    UserAction -->|Export now| SelectExport
    UserAction -->|Close| End3
    
    FormatOutput -->|PDF| GeneratePDF[Generate PDF<br/>with charts + tables]
    GeneratePDF --> DownloadPDF[Trigger download]
    DownloadPDF --> End4([Downloaded])
    
    FormatOutput -->|Excel| GenerateExcel[Generate Excel<br/>with data + pivot]
    GenerateExcel --> DownloadExcel[Trigger download]
    DownloadExcel --> End5([Downloaded])
    
    style Start fill:#e3f2fd
    style End1 fill:#ffcdd2
    style End2 fill:#fff9c4
    style End3 fill:#c8e6c9
    style End4 fill:#c8e6c9
    style End5 fill:#c8e6c9
    style DisplayReport fill:#fff9c4
```

---

## 📋 Report Types

### 1. Faculty Report
**Scope**: Publications from one faculty only

**Access**:
- Faculty Reviewer (own faculty)
- University Reviewer (all faculties)
- SuperAdmin (all faculties)

**Default period**: Current year

---

### 2. University Report
**Scope**: All faculties combined

**Access**:
- University Reviewer only
- SuperAdmin only

**Default period**: Current year

---

## 📊 Metrics Included

### Basic Metrics
1. **Total publications** (PUBLISHED only)
2. **By publication type**:
   - Journal articles
   - Conference papers
   - Book chapters
   - Others

3. **By year** (trend line chart)

### Advanced Metrics (P1)
4. **By faculty** (for university reports)
5. **Top authors** (top 10 by publication count)
6. **Average publications per researcher**
7. **Quartile distribution** (Q1, Q2, Q3, Q4 - P2)

---

## 📥 Export Formats

### PDF Format
**Content**:
- Cover page (logo, title, date)
- Summary statistics (numbers)
- Charts (PNG embedded)
- Tables (detailed breakdown)
- Footer (page numbers)

**Library**: jsPDF + Chart.js

---

### Excel Format
**Sheets**:
1. **Summary** - Key metrics
2. **By Type** - Breakdown table
3. **By Year** - Trend data
4. **By Faculty** - Faculty comparison (if applicable)
5. **Raw Data** - Full publication list

**Library**: SheetJS (xlsx)

---

## 🔒 Access Control

| Role | Faculty Report | University Report |
|------|----------------|-------------------|
| Researcher | ❌ | ❌ |
| Faculty Reviewer | ✅ (own faculty) | ❌ |
| University Reviewer | ✅ (all faculties) | ✅ |
| SuperAdmin | ✅ (all faculties) | ✅ |

---

## ⏱️ Performance

**Target**: 
- On-screen: < 3 seconds
- PDF export: < 10 seconds
- Excel export: < 5 seconds

**Optimizations**:
- Database aggregation queries (GROUP BY)
- Caching for current year reports (P1)
- Background job for large reports (>1000 publications) (P2)

---

## 📊 Sample SQL Query

```sql
-- Faculty report, year 2024
SELECT 
    publication_type,
    COUNT(*) as count
FROM publications p
JOIN publication_authors pa ON p.id = pa.publication_id
JOIN users u ON pa.user_id = u.id
WHERE u.faculty_id = ?
  AND YEAR(p.published_at) = 2024
  AND p.status = 'PUBLISHED'
GROUP BY publication_type
ORDER BY count DESC;
```

---

**Related**: UC-M5-001 to UC-M5-007, FR-REP-001 to FR-REP-010  
**Created**: 11/02/2026
