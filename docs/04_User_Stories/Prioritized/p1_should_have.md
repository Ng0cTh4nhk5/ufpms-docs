# P1 User Stories - Should Have

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục đích**: User stories quan trọng, nên có trong MVP  
> ⚠️ **Priority**: P1 - Should Have

---

## Tổng Quan

**Tổng số User Story P1**: 16  

---

## Phân Bổ Theo Vai Trò

| Vai trò | Số lượng P1 Stories |
|------|-----------|
| Giảng viên (Researcher) | 5 |
| Cán bộ Duyệt Khoa (Faculty Reviewer) | 2 |
| Cán bộ Duyệt Trường (University Reviewer) | 3 |
| Quản trị viên (SuperAdmin) | 2 |
| Khách (Public Visitor) | 4 |

---

## Giảng viên (Researcher) (7 Stories)

### Quản lý Bài báo (Publication Management)
- **US-RES-006**: Thêm Đồng Tác Giả (FR-PUB-007)
- **US-RES-007**: Gắn Tags/Keywords (FR-PUB-008)
- **US-RES-017**: Validate DOI Format (FR-PUB-012)
- **US-RES-018**: Validate ISSN Format (FR-PUB-013)
- **US-RES-019**: Cảnh Báo Trùng Lặp (FR-PUB-014)

### Quy trình (Workflow)
- **US-RES-013**: Rút Lại Đơn Nộp (FR-APR-019)

### Hồ sơ (Profile)
- **US-RES-014**: Xem Profile Công Khai Của Mình (FR-PRO-001)
- **US-RES-015**: Chỉnh Sửa Profile (FR-PRO-002)
- **US-RES-016**: Xem Danh Sách Bài Báo Trên Profile (FR-PRO-003)

---

## Cán bộ Duyệt Khoa (Faculty Reviewer) (2 Stories)

### Quy trình (Workflow)
- **US-FCR-007**: Duyệt Nhiều Bài Cùng Lúc (FR-APR-009)

### Báo cáo (Reporting)
- **US-FCR-008**: Xem Báo Cáo Khoa (FR-REP-002)

---

## Cán bộ Duyệt Trường (University Reviewer) (3 Stories)

### Báo cáo & Phân tích (Reporting & Analytics)
- **US-UNR-007**: Xem Dashboard Analytics Toàn Trường (FR-REP-001)
- **US-UNR-008**: Tạo Báo Cáo Toàn Trường (FR-REP-002, FR-REP-005)
- **US-UNR-009**: Xem Báo Cáo Theo Quartile (FR-REP-003)

---

## Quản trị viên (SuperAdmin) (2 Stories)

### Tính năng Quản trị (Admin Features)
- **US-ADM-008**: Xem System Dashboard (FR-ADM-008)
- **US-ADM-009**: Import Người Dùng từ Excel (FR-ADM-009)

---

## Khách (Public Visitor) (4 Stories)

### Tìm kiếm & Duyệt (Search & Browse)
- **US-VIW-001**: Tìm Kiếm Full-Text (FR-SEA-001)
- **US-VIW-002**: Lọc Kết Quả Nâng Cao (FR-SEA-002)
- **US-VIW-003**: Duyệt Theo Danh Mục (FR-SEA-003)
- **US-VIW-004**: Sắp Xếp Kết Quả (FR-SEA-007)

---

## Lộ trình Triển khai (Implementation Roadmap)

### Giai đoạn 1.5: Quản lý Bài báo Nâng cao
**Sau MVP Cốt lõi**

**Tính năng**:
- Thêm đồng tác giả (US-RES-006)
- Tags/Keywords (US-RES-007)
- Validate DOI/ISSN (US-RES-017, US-RES-018)
- Phát hiện trùng lặp (US-RES-019)
- Rút lại đơn nộp (US-RES-013)

**Giá trị**:
- Ngăn chặn nhập liệu trùng lặp
- Chất lượng dữ liệu tốt hơn
- Quản lý siêu dữ liệu (metadata) cải thiện
- Quy trình linh hoạt hơn

---

### Giai đoạn 2: Tìm kiếm Nâng cao & Hồ sơ (Profile)
**Sau khi Hoàn thành Quy trình Duyệt**

**Tính năng**:
- Tìm kiếm full-text (US-VIW-001)
- Bộ lọc nâng cao (US-VIW-002, US-VIW-003, US-VIW-004)
- Hồ sơ công khai (US-RES-014, US-RES-015, US-RES-016)

**Giá trị**:
- Hiển thị công khai
- Khả năng khám phá tốt hơn
- Trưng bày kết quả nghiên cứu của giảng viên

---

### Giai đoạn 3: Báo cáo & Phân tích
**Sau khi Truy cập Công khai**

**Tính năng**:
- Báo cáo cấp Khoa (US-FCR-008)
- Phân tích cấp Trường (US-UNR-007, US-UNR-008, US-UNR-009)
- Dashboard hệ thống (US-ADM-008)

**Giá trị**:
- Quyết định dựa trên dữ liệu
- Theo dõi hiệu suất
- Báo cáo tự động (so với 2-3 ngày làm thủ công)

---

### Giai đoạn 4: Cải tiến Quản trị (Admin)
**Đang diễn ra**

**Tính năng**:
- Duyệt hàng loạt (US-FCR-007)
- Import Excel (US-ADM-009)

**Giá trị**:
- Hiệu quả quản trị
- Thêm mới hàng loạt (Bulk onboarding)

---

## Giá trị Kinh doanh (Business Value)

### Giảm công việc thủ công
- **US-FCR-008 + US-UNR-008**: Report generation < 5 minutes (vs 2-3 days)
- **US-ADM-009**: Bulk user import (vs manual entry)
- **US-FCR-007**: Bulk approval (faster processing)

### Cải thiện chất lượng dữ liệu
- **US-RES-017, US-RES-018**: Format validation
- **US-RES-019**: Duplicate prevention
- **US-RES-006**: Proper co-author tracking

### Nâng cao trải nghiệm người dùng
- **US-VIW-001 to US-VIW-004**: Better search and discovery
- **US-RES-014 to US-RES-016**: Professional profiles
- **US-RES-013**: More flexible workflow

---

## Các sự phụ thuộc (Dependencies)

### Cho Tìm kiếm
- Consider Elasticsearch for better performance (optional)
- MySQL full-text search sufficient for MVP

### Cho Hồ sơ (Profile)
- Chart library (e.g., Chart.js, D3.js)
- Image upload and storage

### Cho Báo cáo
- Excel export library (e.g., Apache POI)
- PDF generation library

---

## Cờ Tính năng (Feature Flags) (Khuyến nghị)

Bật tính năng P1 theo từng bước:

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
