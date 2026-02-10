# Search and Filter Workflow - Activity Diagram

> 📊 **Diagram**: Search & Filter Publications  
> 🎯 **Scope**: Public search với multiple filters  
> 👤 **Actor**: Public Visitor / Researcher

---

## 📊 Activity Diagram

```mermaid
flowchart TD
    Start([User opens<br/>Search Page]) --> LoadPage[Load search page]
    
    LoadPage --> FetchFilters[Fetch filter options<br/>from database]
    FetchFilters --> DisplaySearch[Display search form<br/>+ empty results]
    
    DisplaySearch --> UserAction{User action?}
    
    UserAction -->|Enter keywords| EnterQuery[Type search keywords]
    EnterQuery --> CheckQuery{Query length?}
    CheckQuery -->|< 3 chars| ShowHint[Show: "Min 3 characters"]
    ShowHint --> EnterQuery
    CheckQuery -->|>= 3 chars| ApplyFilters
    
    UserAction -->|Select filters| SelectYear[Select year range]
    SelectYear --> SelectType[Select publication type]
    SelectType --> SelectFaculty[Select faculty optional]
    SelectFaculty --> ApplyFilters{Apply search?}
    
    ApplyFilters -->|Click Search| BuildQuery[Build search query]
    
    BuildQuery --> CheckAuth{User<br/>authenticated?}
    
    CheckAuth -->|No: Public| AddPublicFilter[Add filter:<br/>status = PUBLISHED]
    AddPublicFilter --> ExecuteSearch
    
    CheckAuth -->|Yes: Researcher| AddResearcherFilter[Add filter:<br/>PUBLISHED OR<br/>owner = userId]
    AddResearcherFilter --> ExecuteSearch
    
    ExecuteSearch[Execute<br/>full-text search] --> GetResults[Fetch from database]
    
    GetResults --> CheckResults{Results found?}
    
    CheckResults -->|No results| ShowEmpty[Show:<br/>"No publications found"<br/>+ suggestions]
    ShowEmpty --> UserAction
    
    CheckResults -->|Has results| SortResults[Sort by relevance<br/>then year DESC]
    
    SortResults --> Paginate[Apply pagination<br/>20 per page]
    
    Paginate --> DisplayResults[Display results list]
    
    DisplayResults --> UserNext{User action?}
    
    UserNext -->|Click publication| ViewDetail[Redirect to<br/>publication detail page]
    ViewDetail --> End1([End])
    
    UserNext -->|Change page| ChangePage[Go to page N]
    ChangePage --> Paginate
    
    UserNext -->|Modify filters| UserAction
    
    UserNext -->|Export results| ExportCSV[Export to CSV<br/>P2 feature]
    ExportCSV --> End2([Download file])
    
    style Start fill:#e3f2fd
    style End1 fill:#c8e6c9
    style End2 fill:#c8e6c9
    style DisplayResults fill:#fff9c4
    style ShowEmpty fill:#ffcdd2
```

---

## 📋 Search Features

### 1. Full-Text Search
**Fields searched**:
- Title (highest weight)
- Abstract
- Keywords
- Author names

**Query**:
```sql
MATCH(title, abstract, keywords) AGAINST ('query' IN NATURAL LANGUAGE MODE)
```

### 2. Filters

| Filter | Options | Default |
|--------|---------|---------|
| **Year** | 1900-current, range | All years |
| **Publication Type** | Journal, Conference, Book, etc. | All types |
| **Faculty** | List from database | All faculties |
| **Has PDF** (P1) | Yes/No checkbox | All |
| **Quartile** (P2) | Q1, Q2, Q3, Q4 | All |

### 3. Sorting

**Default**: Relevance DESC, Year DESC

**Options** (P1):
- Newest first
- Oldest first
- Title A-Z
- Citation count (P2)

### 4. Pagination
- 20 results per page
- Page numbers: 1, 2, 3... (max 10 visible)
- "Previous" / "Next" buttons

---

## 👁️ Visibility Rules

### Public Visitor (Unauthenticated)
```sql
WHERE status = 'PUBLISHED'
```
**Can see**: Only published publications

### Researcher (Authenticated)
```sql
WHERE status = 'PUBLISHED' 
   OR owner_id = {current_user_id}
```
**Can see**: Published + own publications (all statuses)

---

## 📊 Result Display

Each result shows:
- **Title** (clickable)
- **Authors** (first 3, then "et al.")
- **Year**, **Type** (Journal/Conference)
- **Journal/Conference name**
- **DOI** (if available)
- **PDF badge** (if PDF uploaded)

**Highlighted**: Search keywords highlighted in yellow

---

## 🚨 Edge Cases

### Empty Results
**Message**: "No publications found matching your criteria"

**Suggestions**:
- Try fewer filters
- Check spelling
- Try different keywords

### Query Too Short
**Message**: "Please enter at least 3 characters"

### Too Many Results
**Message**: "Showing top 1000 results. Please refine your search."
(Limit: max 1000 results = 50 pages)

---

## ⏱️ Performance

**Target**: < 500ms response time

**Optimizations**:
- Full-text index on title, abstract, keywords
- Caching popular searches (P1)
- Database query optimization

---

**Related**: UC-D3-01, seq_search_publications.md  
**Created**: 11/02/2026
