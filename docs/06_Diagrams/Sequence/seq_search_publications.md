# Sequence Diagram: Search Publications

> 📊 **Diagram ID**: SEQ-06  
> 🎯 **Use Case**: UC-D3-01 - Search Publications  
> 👤 **Actor**: Public Visitor (unauthenticated)  
> ⚙️ **Key**: Public access, visibility filtering

---

## 📊 Sequence Diagram

```mermaid
sequenceDiagram
    actor Visitor as 👤 Public Visitor
    participant UI as 🖥️ UI
    participant API as 🔌 SearchController
    participant Service as ⚙️ SearchService
    participant Repo as 💾 PublicationRepository
    participant DB as 🗄️ Database
    
    %% Open search page
    Visitor->>UI: Navigate to /search
    activate UI
    UI->>API: GET /api/search/filters
    API->>Service: getAvailableFilters()
    Service->>Repo: getPublicationTypes(), getYears(), getFaculties()
    Repo->>DB: SELECT DISTINCT ...
    DB-->>Repo: Filter options
    Repo-->>Service: Options
    Service-->>API: FilterOptions
    API-->>UI: Available filters
    UI-->>Visitor: Show search form + filters
    deactivate UI
    
    %% Enter search query
    Visitor->>UI: Enter keywords:<br/>"machine learning"
    Visitor->>UI: Select filters:<br/>Year: 2023, Type: Journal
    Visitor->>UI: Click "Search"
    
    activate UI
    UI->>API: GET /api/search?q=machine learning&year=2023&type=journal&page=1
    activate API
    Note over API: No authentication required<br/>Public endpoint
    
    API->>Service: search(query, filters, pagination)
    activate Service
    
    %% Build query
    Note over Service: Build SQL:<br/>- WHERE status = 'PUBLISHED'<br/>- AND text match<br/>- AND filters<br/>- ORDER BY relevance
    
    Service->>Repo: searchPublications(criteria)
    activate Repo
    
    Repo->>DB: Full-text search query
    Note over DB: SELECT p.*, u.name as author<br/>FROM publications p<br/>JOIN publication_authors pa<br/>JOIN users u<br/>WHERE p.status = 'PUBLISHED'<br/>AND MATCH(title, abstract)<br/>AGAINST ('machine learning')<br/>AND year = 2023<br/>LIMIT 20 OFFSET 0
    
    DB-->>Repo: Result rows
    Repo-->>Service: Publications[] + totalCount
    deactivate Repo
    
    Service-->>API: SearchResult {<br/>  items: Publications[],<br/>  total: 45,<br/>  page: 1,<br/>  pageSize: 20<br/>}
    deactivate Service
    
    API-->>UI: 200 OK + JSON
    deactivate API
    
    UI-->>Visitor: Display results<br/>(20 per page, 45 total)
    deactivate UI
    
    %% View details
    Visitor->>UI: Click publication title
    activate UI
    UI->>API: GET /api/publications/{id}
    activate API
    
    API->>Service: getPublicationDetails(id)
    activate Service
    
    Service->>Repo: findById(id)
    activate Repo
    Repo->>DB: SELECT * WHERE id = ?<br/>AND status = 'PUBLISHED'
    
    alt Publication is PUBLISHED
        DB-->>Repo: Publication data
        Repo-->>Service: Publication
        
        %% Log view (analytics - async)
        Service->>Repo: logView(pubId)
        Note over Repo: Analytics: track views
        
        Service-->>API: Publication details
        deactivate Service
        API-->>UI: 200 OK + Full publication
        deactivate API
        UI-->>Visitor: Show full details +<br/>PDF download link
    else Not published or not found
        DB-->>Repo: null
        Repo-->>Service: null
        Service-->>API: NotFoundError
        API-->>UI: 404 Not Found
        UI-->>Visitor: "Publication not found"
    end
    deactivate UI
```

---

## 📋 Search Features

### 1. Full-Text Search
- Search in: title, abstract, keywords
- MySQL `MATCH ... AGAINST` or ElasticSearch (P2)
- Ranking by relevance

### 2. Filters
- **Year**: dropdown or range
- **Publication Type**: Journal, Conference,Book Chapter
- **Faculty**: All faculties
- **Quartile**: Q1, Q2, Q3, Q4 (if available)
- **Has PDF**: checkbox

### 3. Pagination
- 20 results per page (default)
- Page navigation
- Show total count

---

## 🔒 Visibility Rule

**CRITICAL**: CHỈ publications với `status = 'PUBLISHED'` mới visible cho public

```sql
-- Always include this WHERE clause for public search
WHERE status = 'PUBLISHED'
```

**For logged-in researchers**:
```sql
-- Can see PUBLISHED + own publications
WHERE status = 'PUBLISHED' 
   OR owner_id = {current_user_id}
```

---

## 📊 Search Query Example

```sql
SELECT 
    p.id,
    p.title,
    p.year,
    p.journal,
    p.publication_type,
    p.doi,
    GROUP_CONCAT(u.name) as authors,
    MATCH(p.title, p.abstract) AGAINST ('machine learning') as relevance
FROM publications p
LEFT JOIN publication_authors pa ON p.id = pa.publication_id
LEFT JOIN users u ON pa.user_id = u.id
WHERE p.status = 'PUBLISHED'
  AND MATCH(p.title, p.abstract) AGAINST ('machine learning' IN NATURAL LANGUAGE MODE)
  AND p.year = 2023
  AND p.publication_type = 'JOURNAL'
GROUP BY p.id
ORDER BY relevance DESC, p.year DESC
LIMIT 20 OFFSET 0;
```

---

## 📈 Response Format

```json
{
  "query": "machine learning",
  "filters": {
    "year": 2023,
    "type": "journal"
  },
  "results": {
    "items": [
      {
        "id": 123,
        "title": "Machine Learning for...",
        "authors": ["Nguyen Van A", "Tran Thi B"],
        "year": 2023,
        "journal": "IEEE Transactions...",
        "doi": "10.1234/example",
        "relevance": 0.95
      }
    ],
    "pagination": {
      "page": 1,
      "pageSize": 20,
      "total": 45,
      "totalPages": 3
    }
  }
}
```

---

## 🚀 Performance Optimization

### Database Indexes
```sql
-- Full-text index
CREATE FULLTEXT INDEX idx_search ON publications(title, abstract, keywords);

-- Filter indexes
CREATE INDEX idx_year ON publications(year);
CREATE INDEX idx_type ON publications(publication_type);
CREATE INDEX idx_status ON publications(status);

-- Composite index for common queries
CREATE INDEX idx_status_year ON publications(status, year);
```

### Caching (P1)
- Cache filter options (rarely change)
- Cache popular searches (Redis)
- Cache publication details (frequently viewed)

---

**Related**: FR-SRC-001 to FR-SRC-005, US-VIW-001, US-VIW-005  
**Created**: 10/02/2026
