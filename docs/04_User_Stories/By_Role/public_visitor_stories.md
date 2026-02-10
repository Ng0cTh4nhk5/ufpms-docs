# User Stories - Public Visitor

> 👤 **Role**: Public Visitor (Khách truy cập)  
> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục tiêu**: Tìm kiếm và xem thông tin công trình công bố, profile giảng viên

---

## Tổng Quan

**Total Stories**: 8  
**P0 (Must Have)**: 2  
**P1 (Should Have)**: 4  
**P2 (Nice to Have)**: 2

---

## Module 3: Search & Browse

### US-VIW-001: Tìm Kiếm Full-Text
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-SEA-001

**User Story**:
```
As a public visitor,
I want to search for publications using keywords,
So that I can find research relevant to my interests.
```

**Acceptance Criteria**:
```
GIVEN I am on the search page (no login required)
WHEN I enter keywords and click search
THEN I see results showing ONLY PUBLISHED publications
WHERE the search matches: Title, Abstract, Keywords, Author names
AND matching keywords are highlighted
AND results are sorted by relevance
```

---

### US-VIW-002: Lọc Kết Quả Nâng Cao
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-SEA-002

**User Story**:
```
As a public visitor,
I want to filter search results by various criteria,
So that I can narrow down to specific types of publications.
```

**Acceptance Criteria**:
```
GIVEN I have search results
WHEN I apply filters
THEN I can filter by:
- Year range (from year - to year)
- Faculty/Department
- Journal Type (Q1/Q2/Q3/Q4/Conference)
- Publication Type (Journal/Conference)
- Research Field
AND results update dynamically
```

---

### US-VIW-003: Duyệt Theo Danh Mục
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-SEA-003

**User Story**:
```
As a public visitor,
I want to browse publications by category,
So that I can explore research without needing specific keywords.
```

**Acceptance Criteria**:
```
GIVEN I click "Browse"
WHEN the page loads
THEN I see category options:
- By Faculty
- By Year
- By Research Field
- By Journal Quartile (Q1/Q2/Q3/Q4)
AND clicking a category shows publications in that category
```

---

### US-VIW-004: Sắp Xếp Kết Quả
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-SEA-007

**User Story**:
```
As a public visitor,
I want to sort search results by different criteria,
So that I can find the most relevant or recent publications first.
```

**Acceptance Criteria**:
```
GIVEN I have search results
WHEN I select a sort option
THEN results can be sorted by:
- Newest first (default)
- Oldest first
- Most cited
- Impact Factor (high to low)
```

---

### US-VIW-005: Phân Trang Kết Quả
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-SEA-005

**User Story**:
```
As a public visitor,
I want search results to be paginated,
So that the page loads quickly and I can navigate through results.
```

**Acceptance Criteria**:
```
GIVEN I have search results
WHEN viewing the results
THEN I see:
- Default: 20 results per page
- Pagination controls (1, 2, 3... Next)
- Options to show: 10, 20, 50, or 100 results per page
- Optional: Infinite scroll
```

---

### US-VIW-006: Xem Chi Tiết Công Trình
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-SEA-006

**User Story**:
```
As a public visitor,
I want to view detailed information about a publication,
So that I can read the full metadata and access the paper.
```

**Acceptance Criteria**:
```
GIVEN I click on a publication from search results
WHEN the detail page loads
THEN I see:
- Full metadata (title, authors, journal, year, abstract, etc.)
- DOI link (clickable to external source)
- Download PDF button (if allowed)
- Links to author profiles
```

---

### US-VIW-007: Export Kết Quả Tìm Kiếm
**Priority**: 🟢 P2 - Nice to Have  
**Related FR**: FR-SEA-004

**User Story**:
```
As a public visitor,
I want to export search results in various formats,
So that I can use them in reference managers or spreadsheets.
```

**Acceptance Criteria**:
```
GIVEN I have search results
WHEN I click "Export"
THEN I can choose format:
- BibTeX (for LaTeX)
- RIS (for EndNote, Mendeley, Zotero)
- CSV (for Excel)
- JSON (for developers)
AND the file is downloaded with the selected results
```

---

## Module 4: Researcher Profile (View Only)

### US-VIW-008: Xem Profile Giảng Viên
**Priority**: 🟢 P2 - Nice to Have  
**Related FR**: FR-PRO-001, FR-PRO-006

**User Story**:
```
As a public visitor,
I want to view a researcher's public profile,
So that I can learn about their research and publications.
```

**Acceptance Criteria**:
```
GIVEN I access a researcher's profile URL (/profile/[username])
WHEN the page loads
THEN I see:
- Profile photo, name, title, faculty
- Contact information (email, ORCID)
- Bio and research interests
- List of PUBLISHED publications only
- Publications per year chart
- Research field word cloud
AND I can click on publications to view details
AND the page is SEO-optimized with proper meta tags
```

---

## Traceability Matrix

| Story ID | Title | Priority | FR ID | Module |
|----------|-------|----------|-------|--------|
| US-VIW-001 | Tìm Kiếm Full-Text | P1 | FR-SEA-001 | 3 |
| US-VIW-002 | Lọc Kết Quả Nâng Cao | P1 | FR-SEA-002 | 3 |
| US-VIW-003 | Duyệt Theo Danh Mục | P1 | FR-SEA-003 | 3 |
| US-VIW-004 | Sắp Xếp Kết Quả | P1 | FR-SEA-007 | 3 |
| US-VIW-005 | Phân Trang Kết Quả | P0 | FR-SEA-005 | 3 |
| US-VIW-006 | Xem Chi Tiết Công Trình | P0 | FR-SEA-006 | 3 |
| US-VIW-007 | Export Kết Quả Tìm Kiếm | P2 | FR-SEA-004 | 3 |
| US-VIW-008 | Xem Profile Giảng Viên | P2 | FR-PRO-001, FR-PRO-006 | 4 |

---

**Tài liệu liên quan**:
- [Requirements - Search & Browse](../../03_Requirements/Functional/module_search.md)
- [Requirements - Researcher Profile](../../03_Requirements/Functional/module_profile.md)
