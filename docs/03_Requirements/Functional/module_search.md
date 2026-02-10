# Module 3: Search & Browse - Yêu Cầu Chức Năng

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Module**: Tìm kiếm và Tra cứu Bài báo  
> 👥 **Users**: Tất cả (Public Access)

---

## 1. Functional Requirements

### FR-SEA-001: Full-Text Search
**Priority**: 🟡 P1 - Should Have

**Acceptance Criteria**:
```
GIVEN user truy cập trang tìm kiếm
WHEN nhập từ khóa và search
THEN hiển thị kết quả chỉ công trình PUBLISHED:
  - Tìm trong: Title, Abstract, Keywords, Author names
  - Highlight từ khóa trong kết quả
  - Sắp xếp theo relevance
```

---

### FR-SEA-002: Advanced Filters
**Priority**: 🟡 P1 - Should Have

**Filters**:
- Year (range: từ năm - đến năm)  
- Faculty/Department  
- Journal Type (Q1/Q2/Q3/Q4 hoặc Conference)  
- Publication Type (Journal/Conference)  
- Research Field

---

### FR-SEA-003: Browse by Category
**Priority**: 🟡 P1 - Should Have

**Acceptance Criteria**:
```
WHEN chọn "Browse"
THEN hiển thị các danh mục:
  - By Faculty
  - By Year
  - By Research Field
  - By Journal Quartile
```

---

### FR-SEA-004: Export Search Results
**Priority**: 🟢 P2 - Nice to Have

**Export formats**:
- BibTeX
- RIS (for reference managers)
- CSV  
- JSON

---

### FR-SEA-005: Pagination
**Priority**: 🔴 P0 - Must Have

**Acceptance Criteria**:
- Default: 20 results/page
- Options: 10, 20, 50, 100
- Infinite scroll (optional)

---

### FR-SEA-006: View Publication Details (Public)
**Priority**: 🔴 P0 - Must Have

**Acceptance Criteria**:
```
WHEN click vào bài báo
THEN hiển thị:
  - Full metadata
  - DOI link
  - Download PDF (nếu cho phép)
  - Author profiles (link đến profile)
```

---

### FR-SEA-007: Sort Options
**Priority**: 🟡 P1 - Should Have

**Sort by**:
- Newest first (default)
- Oldest first  
- Most cited  
- Impact Factor (high to low)

---

## 2. Non-Functional Requirements

**Performance**:
- Search response time < 1 second (10,000 publications)
- Support fuzzy search
- Index với Elasticsearch (optional)

**SEO**:
- Meta tags cho từng publication page
- Sitemap.xml
- Robots.txt

---

**Tài liệu liên quan**:
- [Module 4: Researcher Profile](./module_profile.md)
