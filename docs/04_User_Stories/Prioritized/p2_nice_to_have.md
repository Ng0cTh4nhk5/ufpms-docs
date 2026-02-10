# P2 User Stories - Nice to Have (Phase 2)

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục đích**: User stories cho Phase 2 enhancement  
> ⚠️ **Priority**: P2 - Nice to Have

---

## Tổng Quan

**Total P2 Stories**: 7  

---

## Phân Bổ Theo Role

| Role | P2 Stories |
|------|-----------|
| Researcher | 3 |
| Faculty Reviewer | 1 |
| University Reviewer | 1 |
| SuperAdmin | 0 |
| Public Visitor | 2 |

---

## Researcher (3 Stories)

### Advanced Features
- **US-RES-020**: Auto-Fetch Metadata từ DOI (FR-PUB-003)
  - **Value**: Tự động điền metadata từ CrossRef API
  - **Dependency**: CrossRef API integration
  - **Effort**: Medium

- **US-RES-021**: Import từ ORCID (FR-PUB-015)
  - **Value**: Bulk import publications từ ORCID profile
  - **Dependency**: ORCID API integration
  - **Effort**: High

### Analytics & Visualization
- **US-RES-022**: Xem Biểu Đồ Năng Suất (FR-PRO-004)
  - **Value**: Visual analytics trên profile
  - **Dependency**: Chart library
  - **Effort**: Low

- **US-RES-023**: Xem Word Cloud Lĩnh Vực (FR-PRO-005)
  - **Value**: Research field visualization
  - **Dependency**: Word cloud library
  - **Effort**: Low

---

## Faculty Reviewer (1 Story)

### Workflow Analytics
- **US-FCR-009**: Theo Dõi SLA Xét Duyệt (FR-APR-020)
  - **Value**: Track review performance metrics
  - **Metrics**:
    - Average time: SUBMITTED → FACULTY_APPROVED
    - % reviewed within 7 days
  - **Effort**: Medium

---

## University Reviewer (1 Story)

### Advanced Reporting
- **US-UNR-010**: Xem Xu Hướng Phát Triển (FR-REP-004)
  - **Value**: Trend analysis, emerging research areas
  - **Features**:
    - Year-over-year growth
    - Top growing faculties
    - Emerging research fields from keywords
  - **Effort**: Medium

---

## Public Visitor (2 Stories)

### Export & Discovery
- **US-VIW-007**: Export Kết Quả Tìm Kiếm (FR-SEA-004)
  - **Value**: Export to BibTeX, RIS, CSV, JSON
  - **Use Case**: Reference manager integration
  - **Effort**: Low

- **US-VIW-008**: Xem Profile Giảng Viên (FR-PRO-001, FR-PRO-006)
  - **Value**: Public researcher profiles with SEO
  - **Features**: Bio, publications, charts, word cloud
  - **Effort**: Medium (depends on US-RES-022, US-RES-023)

---

## Implementation Strategy

### Phase 2A: External Integrations
**Timeline**: 3-4 weeks after MVP

**Features**:
1. **US-RES-020**: DOI metadata auto-fetch
   - Integrate CrossRef API
   - Auto-fill publication metadata
   - Reduce manual data entry

2. **US-RES-021**: ORCID import
   - OAuth integration with ORCID
   - Bulk import publications
   - Match with existing entries

**Dependencies**:
- CrossRef API account
- ORCID API credentials
- Network access to external APIs

---

### Phase 2B: Analytics & Visualization
**Timeline**: 2 weeks after Phase 2A

**Features**:
1. **US-RES-022**: Publication productivity charts
2. **US-RES-023**: Research field word cloud
3. **US-FCR-009**: SLA tracking
4. **US-UNR-010**: Trend analysis

**Dependencies**:
- Chart.js or D3.js library
- Word cloud library (e.g., react-wordcloud)
- Analytics data processing

---

### Phase 2C: Export & Public Profiles
**Timeline**: 2 weeks after Phase 2B

**Features**:
1. **US-VIW-007**: Export search results
2. **US-VIW-008**: Full public profiles

**Dependencies**:
- BibTeX/RIS generation libraries
- SEO optimization (meta tags, Open Graph)
- Static site generation for profiles (optional)

---

## Business Value (Phase 2)

### Time Savings
- **US-RES-020**: Save 2-3 minutes per publication (auto-fill)
- **US-RES-021**: Import 10-50 publications in minutes vs hours

### User Satisfaction
- **US-RES-022, US-RES-023**: Visual representation of research output
- **US-VIW-008**: Professional online presence for researchers

### Research Management
- **US-FCR-009**: Identify bottlenecks in review process
- **US-UNR-010**: Strategic planning based on trends

### Integration
- **US-VIW-007**: Better integration with reference managers
- **US-RES-021**: Leverage existing ORCID data

---

## ROI Analysis

### Development Cost
- **Total Effort**: ~6-8 weeks (1 developer)
- **External APIs**: Free tier available (CrossRef, ORCID)

### Benefits
- **Automation**: 50-70% reduction in metadata entry time
- **Visibility**: Improved researcher profiles → more citations
- **Insights**: Data-driven review process improvements

### Priority Justification
- Not critical for MVP launch
- High value for user satisfaction
- Good for Phase 2 "polish" release

---

## Technical Considerations

### API Rate Limits
- **CrossRef**: 50 requests/second (free tier)
- **ORCID**: Rate limits apply, need to handle gracefully

### Caching Strategy
- Cache DOI metadata (reduce API calls)
- Cache analytics charts (regenerate daily)

### Data Storage
- Store fetched metadata
- Keep audit trail of imports

---

## Feature Flags for P2

```javascript
{
  // External Integrations
  "doiAutoFetch": false,
  "orcidImport": false,
  
  // Analytics
  "profileCharts": false,
  "wordCloud": false,
  "slaTracking": false,
  "trendAnalysis": false,
  
  // Export & Public
  "exportResults": false,
  "publicProfiles": false
}
```

Enable features incrementally based on:
- API integration completion
- User feedback
- Performance testing

---

## Success Metrics

### Adoption
- % of researchers using DOI auto-fetch
- % of researchers importing from ORCID
- % of researchers with complete profiles

### Performance
- API response time < 2s
- Chart rendering < 1s
- Export generation < 5s

### User Satisfaction
- Survey: "How useful are the charts?" (1-5 scale)
- Survey: "How much time saved with auto-fetch?" (minutes)

---

**Tài liệu liên quan**:
- [P0 Must Have Stories](./p0_must_have.md)
- [P1 Should Have Stories](./p1_should_have.md)
- [All User Stories by Role](../By_Role/)
- [Functional Requirements](../../03_Requirements/Functional/)
