# Module 3: Search & Browse - Medium-Level Use Cases

> **Module**: 3 - Search & Browse  
> **High-Level UC**: [UC-HL-003](../High_Level/uc_hl_03_search_browse.md)

---

## UC-M3-001: Basic Search
**ID**: UC-M3-001 | **Priority**: 🟡 P1 | **Actor**: Public Visitor, All Users  
**Related**: US-VIW-001, FR-SEA-001

**Goal**: Search for publications using keywords  
**Preconditions**: None (public access)  
**Main Flow**:
1. User enters keywords in search box
2. User clicks "Search"
3. System searches in: Title, Abstract, Keywords, Author names
4. System returns ONLY PUBLISHED publications
5. System highlights matching keywords
6. System sorts by relevance
7. System paginates (20 per page default)

**Postconditions**: Results displayed  
**Business Rules**: BR-SEA-001 (PUBLISHED only), BR-SEA-005 (performance < 1s)

---

## UC-M3-002: Advanced Search
**ID**: UC-M3-002 | **Priority**: 🟡 P1 | **Actor**: Public Visitor, All Users  
**Related**: FR-SEA-002

**Goal**: Multi-criteria search  
**Main Flow**:
1. User clicks "Advanced Search"
2. System shows form with fields:
   - Keywords, Author name, Title
   - Year range, Faculty, Quartile
3. User fills criteria
4. System combines with AND logic
5. System returns matching publications

**Business Rules**: All filters combine with AND

---

## UC-M3-003: Filter Results
**ID**: UC-M3-003 | **Priority**: 🟡 P1 | **Actor**: Public Visitor  
**Related**: US-VIW-002, FR-SEA-002

**Goal**: Filter search results by multiple criteria  
**Main Flow**:
1. User has search results
2. User applies filters (sidebar):
   - Year range (slider or from-to)
   - Faculty (multi-select)
   - Quartile (Q1/Q2/Q3/Q4/Conference)
   - Publication Type (Journal/Conference)
3. System updates results dynamically (AJAX)
4. System shows result count
5. User can clear individual filters or all

**Business Rules**: Filters are cumulative (AND logic)

---

## UC-M3-004: Sort Results
**ID**: UC-M3-004 | **Priority**: 🟡 P1 | **Actor**: Public Visitor  
**Related**: US-VIW-004, FR-SEA-007

**Goal**: Sort search results  
**Main Flow**:
1. User has search results
2. User selects sort option:
   - Newest first (default)
   - Oldest first
   - Most cited (if available)
   - Impact Factor (high to low)
3. System re-sorts results
4. Pagination resets to page 1

---

## UC-M3-005: View Publication Details (Public)
**ID**: UC-M3-005 | **Priority**: 🔴 P0 | **Actor**: Public Visitor  
**Related**: US-VIW-006, FR-SEA-006

**Goal**: View complete publication information  
**Preconditions**: Publication status = PUBLISHED  
**Main Flow**:
1. User clicks publication from search results
2. System displays detail page:
   - Full metadata
   - Abstract
   - DOI link (clickable)
   - Author profile links
   - Download PDF button (if allowed)
   - Citation information
3. Page is SEO-optimized (meta tags)

**Business Rules**: BR-SEA-006 (SEO tags), unique URL per publication

---

## UC-M3-006: Browse by Faculty
**ID**: UC-M3-006 | **Priority**: 🟡 P1 | **Actor**: Public Visitor  
**Related**: US-VIW-003, FR-SEA-003

**Goal**: Browse publications by faculty/department  
**Main Flow**:
1. User clicks "Browse by Faculty"
2. System shows list of faculties
3. User selects a faculty
4. System shows all PUBLISHED publications from that faculty
5. User can drill down by year or researcher

---

## UC-M3-007: Browse by Year/Quartile
**ID**: UC-M3-007 | **Priority**: 🟡 P1 | **Actor**: Public Visitor  
**Related**: US-VIW-003, FR-SEA-003

**Goal**: Browse by year or journal quartile  
**Main Flow**:
1. User clicks "Browse by Year" or "Browse by Quartile"
2. System shows options (years or Q1/Q2/Q3/Q4)
3. User selects
4. System displays matching publications

---

**Tài liệu liên quan**:
- [High-Level UC-HL-003](../High_Level/uc_hl_03_search_browse.md)
- [User Stories - Public Visitor](../../04_User_Stories/By_Role/public_visitor_stories.md)
- [Requirements - Search](../../03_Requirements/Functional/module_search.md)
