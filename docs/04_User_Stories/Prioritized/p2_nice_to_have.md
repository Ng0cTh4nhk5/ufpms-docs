# P2 User Stories - Nice to Have (Phase 2)

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục đích**: User stories cho Phase 2 enhancement  
> ⚠️ **Priority**: P2 - Nice to Have

---

## Tổng Quan

**Tổng số User Story P2**: 7  

---

## Phân Bổ Theo Vai Trò

| Vai trò | Số lượng P2 Stories |
|------|-----------|
| Giảng viên (Researcher) | 3 |
| Cán bộ Duyệt Khoa (Faculty Reviewer) | 1 |
| Cán bộ Duyệt Trường (University Reviewer) | 1 |
| Quản trị viên (SuperAdmin) | 0 |
| Khách (Public Visitor) | 2 |

---

## Giảng viên (Researcher) (3 Stories)

### Tính năng Nâng cao (Advanced Features)
- **US-RES-020**: Auto-Fetch Metadata từ DOI (FR-PUB-003)
  - **Giá trị**: Tự động điền metadata từ CrossRef API
  - **Phụ thuộc**: CrossRef API integration
  - **Effort**: Medium

- **US-RES-021**: Import từ ORCID (FR-PUB-015)
  - **Giá trị**: Bulk import publications từ ORCID profile
  - **Phụ thuộc**: ORCID API integration
  - **Effort**: High

### Phân tích & Trực quan hóa (Analytics & Visualization)
- **US-RES-022**: Xem Biểu Đồ Năng Suất (FR-PRO-004)
  - **Giá trị**: Visual analytics trên profile
  - **Phụ thuộc**: Chart library
  - **Effort**: Low

- **US-RES-023**: Xem Word Cloud Lĩnh Vực (FR-PRO-005)
  - **Giá trị**: Research field visualization
  - **Phụ thuộc**: Word cloud library
  - **Effort**: Low

---

## Cán bộ Duyệt Khoa (Faculty Reviewer) (1 Story)

### Phân tích Quy trình (Workflow Analytics)
- **US-FCR-009**: Theo Dõi SLA Xét Duyệt (FR-APR-020)
  - **Giá trị**: Track review performance metrics
  - **Metrics**:
    - Average time: SUBMITTED → FACULTY_APPROVED
    - % reviewed within 7 days
  - **Effort**: Medium

---

## Cán bộ Duyệt Trường (University Reviewer) (1 Story)

### Báo cáo Nâng cao (Advanced Reporting)
- **US-UNR-010**: Xem Xu Hướng Phát Triển (FR-REP-004)
  - **Giá trị**: Trend analysis, emerging research areas
  - **Tính năng**:
    - Year-over-year growth
    - Top growing faculties
    - Emerging research fields from keywords
  - **Effort**: Medium

---

## Khách (Public Visitor) (2 Stories)

### Xuất dữ liệu & Khám phá (Export & Discovery)
- **US-VIW-007**: Export Kết Quả Tìm Kiếm (FR-SEA-004)
  - **Giá trị**: Export to BibTeX, RIS, CSV, JSON
  - **Use Case**: Reference manager integration
  - **Effort**: Low

- **US-VIW-008**: Xem Profile Giảng Viên (FR-PRO-001, FR-PRO-006)
  - **Giá trị**: Public researcher profiles with SEO
  - **Tính năng**: Bio, publications, charts, word cloud
  - **Effort**: Medium (depends on US-RES-022, US-RES-023)

---

## Chiến lược Triển khai (Implementation Strategy)

### Giai đoạn 2A: Tích hợp Bên ngoài
**Thời gian**: 3-4 tuần sau MVP

**Tính năng**:
1. **US-RES-020**: DOI metadata auto-fetch
   - Integrate CrossRef API
   - Auto-fill publication metadata
   - Reduce manual data entry

2. **US-RES-021**: ORCID import
   - OAuth integration with ORCID
   - Bulk import publications
   - Match with existing entries

**Sự phụ thuộc**:
- CrossRef API account
- ORCID API credentials
- Network access to external APIs

---

### Giai đoạn 2B: Phân tích & Trực quan hóa
**Thời gian**: 2 tuần sau Giai đoạn 2A

**Tính năng**:
1. **US-RES-022**: Publication productivity charts
2. **US-RES-023**: Research field word cloud
3. **US-FCR-009**: SLA tracking
4. **US-UNR-010**: Trend analysis

**Sự phụ thuộc**:
- Chart.js or D3.js library
- Word cloud library (e.g., react-wordcloud)
- Analytics data processing

---

### Giai đoạn 2C: Xuất dữ liệu & Hồ sơ Công khai
**Thời gian**: 2 tuần sau Giai đoạn 2B

**Tính năng**:
1. **US-VIW-007**: Export search results
2. **US-VIW-008**: Full public profiles

**Sự phụ thuộc**:
- BibTeX/RIS generation libraries
- SEO optimization (meta tags, Open Graph)
- Static site generation for profiles (optional)

---

## Giá trị Kinh doanh (Giai đoạn 2)

### Tiết kiệm Thời gian
- **US-RES-020**: Save 2-3 minutes per publication (auto-fill)
- **US-RES-021**: Import 10-50 publications in minutes vs hours

### Sự hài lòng của Người dùng
- **US-RES-022, US-RES-023**: Visual representation of research output
- **US-VIW-008**: Professional online presence for researchers

### Quản lý Nghiên cứu
- **US-FCR-009**: Identify bottlenecks in review process
- **US-UNR-010**: Strategic planning based on trends

### Tích hợp
- **US-VIW-007**: Better integration with reference managers
- **US-RES-021**: Leverage existing ORCID data

---

## Phân tích ROI (ROI Analysis)

### Chi phí Phát triển
- **Tổng Nỗ lực**: ~6-8 tuần (1 developer)
- **API Bên ngoài**: Free tier available (CrossRef, ORCID)

### Lợi ích
- **Tự động hóa**: 50-70% reduction in metadata entry time
- **Khả năng hiển thị**: Improved researcher profiles → more citations
- **Thông tin chi tiết**: Data-driven review process improvements

### Biện minh cho Ưu tiên
- Not critical for MVP launch
- High value for user satisfaction
- Good for Phase 2 "polish" release

---

## Cân nhắc Kỹ thuật (Technical Considerations)

### Giới hạn Tốc độ API
- **CrossRef**: 50 requests/second (free tier)
- **ORCID**: Rate limits apply, need to handle gracefully

### Chiến lược Caching
- Cache DOI metadata (reduce API calls)
- Cache analytics charts (regenerate daily)

### Lưu trữ Dữ liệu
- Store fetched metadata
- Keep audit trail of imports

---

## Cờ Tính năng cho P2

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

## Chỉ số Thành công (Success Metrics)

### Sự chấp nhận
- % of researchers using DOI auto-fetch
- % of researchers importing from ORCID
- % of researchers with complete profiles

### Hiệu năng
- API response time < 2s
- Chart rendering < 1s
- Export generation < 5s

### Sự hài lòng của Người dùng
- Survey: "How useful are the charts?" (1-5 scale)
- Survey: "How much time saved with auto-fetch?" (minutes)

---

**Tài liệu liên quan**:
- [P0 Must Have Stories](./p0_must_have.md)
- [P1 Should Have Stories](./p1_should_have.md)
- [All User Stories by Role](../By_Role/)
- [Functional Requirements](../../03_Requirements/Functional/)
