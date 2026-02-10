# P1 User Stories - Should Have

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục đích**: User stories quan trọng, nên có trong MVP  
> ⚠️ **Priority**: P1 - Should Have

---

## Tổng Quan

**Total P1 Stories**: 18  

---

## Phân Bổ Theo Role

| Role | P1 Stories |
|------|-----------|
| Researcher | 7 |
| Faculty Reviewer | 2 |
| University Reviewer | 3 |
| SuperAdmin | 2 |
| Public Visitor | 4 |

---

## Researcher (7 Stories)

### Publication Management
- **US-RES-006**: Thêm Đồng Tác Giả (FR-PUB-007)
- **US-RES-007**: Gắn Tags/Keywords (FR-PUB-008)
- **US-RES-017**: Validate DOI Format (FR-PUB-012)
- **US-RES-018**: Validate ISSN Format (FR-PUB-013)
- **US-RES-019**: Cảnh Báo Trùng Lặp (FR-PUB-014)

### Workflow
- **US-RES-013**: Rút Lại Đơn Nộp (FR-APR-019)

### Profile
- **US-RES-014**: Xem Profile Công Khai Của Mình (FR-PRO-001)
- **US-RES-015**: Chỉnh Sửa Profile (FR-PRO-002)
- **US-RES-016**: Xem Danh Sách Bài Báo Trên Profile (FR-PRO-003)

---

## Faculty Reviewer (2 Stories)

### Workflow
- **US-FCR-007**: Duyệt Nhiều Bài Cùng Lúc (FR-APR-009)

### Reporting
- **US-FCR-008**: Xem Báo Cáo Khoa (FR-REP-002)

---

## University Reviewer (3 Stories)

### Reporting & Analytics
- **US-UNR-007**: Xem Dashboard Analytics Toàn Trường (FR-REP-001)
- **US-UNR-008**: Tạo Báo Cáo Toàn Trường (FR-REP-002, FR-REP-005)
- **US-UNR-009**: Xem Báo Cáo Theo Quartile (FR-REP-003)

---

## SuperAdmin (2 Stories)

### Admin Features
- **US-ADM-008**: Xem System Dashboard (FR-ADM-008)
- **US-ADM-009**: Import Người Dùng từ Excel (FR-ADM-009)

---

## Public Visitor (4 Stories)

### Search & Browse
- **US-VIW-001**: Tìm Kiếm Full-Text (FR-SEA-001)
- **US-VIW-002**: Lọc Kết Quả Nâng Cao (FR-SEA-002)
- **US-VIW-003**: Duyệt Theo Danh Mục (FR-SEA-003)
- **US-VIW-004**: Sắp Xếp Kết Quả (FR-SEA-007)

---

## Implementation Roadmap

### Phase 1.5: Enhanced Publication Management
**After MVP Core**

**Features**:
- Co-author linking (US-RES-006)
- Keywords/tags (US-RES-007)
- DOI/ISSN validation (US-RES-017, US-RES-018)
- Duplicate detection (US-RES-019)
- Withdraw submission (US-RES-013)

**Value**:
- Prevents duplicate entries
- Better data quality
- Improved metadata management
- More flexible workflow

---

### Phase 2: Advanced Search & Profile
**After Approval Workflow Complete**

**Features**:
- Full-text search (US-VIW-001)
- Advanced filtering (US-VIW-002, US-VIW-003, US-VIW-004)
- Public profiles (US-RES-014, US-RES-015, US-RES-016)

**Value**:
- Public visibility
- Better discoverability
- Researcher showcase

---

### Phase 3: Reporting & Analytics
**After Public Access**

**Features**:
- Faculty reports (US-FCR-008)
- University-wide analytics (US-UNR-007, US-UNR-008, US-UNR-009)
- System dashboard (US-ADM-008)

**Value**:
- Data-driven decisions
- Performance tracking
- Automated reporting (vs 2-3 days manual work)

---

### Phase 4: Admin Enhancements
**Ongoing**

**Features**:
- Bulk approval (US-FCR-007)
- Excel import (US-ADM-009)

**Value**:
- Administrative efficiency
- Bulk onboarding

---

## Business Value

### Reduced Manual Work
- **US-FCR-008 + US-UNR-008**: Report generation < 5 minutes (vs 2-3 days)
- **US-ADM-009**: Bulk user import (vs manual entry)
- **US-FCR-007**: Bulk approval (faster processing)

### Improved Data Quality
- **US-RES-017, US-RES-018**: Format validation
- **US-RES-019**: Duplicate prevention
- **US-RES-006**: Proper co-author tracking

### Enhanced User Experience
- **US-VIW-001 to US-VIW-004**: Better search and discovery
- **US-RES-014 to US-RES-016**: Professional profiles
- **US-RES-013**: More flexible workflow

---

## Dependencies

### For Search Features
- Consider Elasticsearch for better performance (optional)
- MySQL full-text search sufficient for MVP

### For Profile Features
- Chart library (e.g., Chart.js, D3.js)
- Image upload and storage

### For Reporting
- Excel export library (e.g., Apache POI)
- PDF generation library

---

## Feature Flags (Recommended)

Enable P1 features incrementally:

```javascript
{
  "coAuthorLinking": true,
  "duplicateDetection": true,
  "publicSearch": true,
  "publicProfiles": false,  // Enable after testing
  "advancedReporting": false  // Enable when ready
}
```

---

**Tài liệu liên quan**:
- [P0 Must Have Stories](./p0_must_have.md)
- [P2 Nice to Have Stories](./p2_nice_to_have.md)
- [All User Stories by Role](../By_Role/)
