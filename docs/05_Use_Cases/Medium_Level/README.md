# Medium-Level Use Cases - README

> 📁 **Cấp Độ**: Medium-Level Use Cases (Use Case Cấp Trung)  
> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục đích**: Chi tiết 54 use cases theo chức năng của từng module

---

## 📊 Tổng Quan

Medium-level use cases chia nhỏ các high-level use cases thành các chức năng cụ thể, mỗi chức năng là 1 use case độc lập với điều kiện tiên quyết (preconditions), luồng chính (main flow), và điều kiện hậu quyết (postconditions) rõ ràng.

### 54 Use Cases Cấp Trung

| Module | Tập Tin | SL Use Cases | P0 | P1 | P2 |
|--------|---------|---------|----|----|---- |
| 1. Quản Lý Bài Báo | [module_01_publication_management.md](./module_01_publication_management.md) | 9 | 7 | 2 | 0 |
| 2. Quy Trình Xét Duyệt | [module_02_approval_workflow.md](./module_02_approval_workflow.md) | 15 | 10 | 3 | 2 |
| 3. Tìm Kiếm & Duyệt | [module_03_search_browse.md](./module_03_search_browse.md) | 7 | 2 | 4 | 1 |
| 4. Hồ Sơ Nhà Nghiên Cứu | [module_04_researcher_profile.md](./module_04_researcher_profile.md) | 6 | 0 | 3 | 3 |
| 5. Báo Cáo & Phân Tích | [module_05_reporting_analytics.md](./module_05_reporting_analytics.md) | 7 | 0 | 5 | 2 |
| 6. Quản Trị Hệ Thống | [module_06_admin_management.md](./module_06_admin_management.md) | 10 | 8 | 2 | 0 |
| **TỔNG** | | **54** | **27** | **19** | **8** |

---

## 📋 Định Dạng Use Case

Mỗi medium-level use case bao gồm:

```markdown
## UC-MX-XXX: [Tên Use Case]

**ID**: UC-MX-XXX
**Độ Ưu Tiên**: P0/P1/P2
**Tác Nhân**: [Tên các tác nhân]
**User Stories Liên Quan**: US-XXX-XXX, ...
**Yêu Cầu Chức Năng Liên Quan**: FR-XXX-XXX

### Mục Tiêu
Mô tả ngắn gọn về những gì tác nhân muốn đạt được.

### Điều Kiện Tiên Quyết
- Các trạng thái hệ thống/người dùng bắt buộc

### Luồng Chính
1. Bước 1
2. Bước 2
...

### Điều Kiện Hậu Quyết
**Thành Công**: Điều gì xảy ra khi thành công
**Thất Bại**: Điều gì xảy ra khi thất bại

### Quy Tắc Nghiệp Vụ
- BR-XXX-001: Mô tả quy tắc
```

---

## 📖 Các Module

### [Module 1: Quản Lý Bài Báo](./module_01_publication_management.md)
9 use cases cho các thao tác CRUD, tải lên tập tin, và xác thực.

- UC-M1-001: Tạo Bài Báo
- UC-M1-002: Sửa Bài Báo  
- UC-M1-003: Xóa Bài Báo
- UC-M1-004: Xem Danh Sách Bài Báo
- UC-M1-005: Xem Chi Tiết Bài Báo
- UC-M1-006: Tải Lên File PDF
- UC-M1-007: Tải Xuống File PDF
- UC-M1-008: Thêm Đồng Tác Giả
- UC-M1-009: Xác Thực DOI/ISSN

---

### [Module 2: Quy Trình Xét Duyệt](./module_02_approval_workflow.md)
15 use cases cho quy trình phê duyệt 2 cấp.

**Hành Động Của Researcher** (4):
- UC-M2-001: Gửi Xét Duyệt
- UC-M2-002: Theo Dõi Trạng Thái
- UC-M2-003: Chỉnh Sửa Bài Báo
- UC-M2-004: Rút Bài Báo

**Hành Động Của Faculty Reviewer** (4):
- UC-M2-005: Khoa Phê Duyệt
- UC-M2-006: Khoa Yêu Cầu Chỉnh Sửa
- UC-M2-007: Khoa Từ Chối
- UC-M2-012: Phê Duyệt Hàng Loạt (Khoa)

**Hành Động Của University Reviewer** (4):
- UC-M2-008: Trường Phê Duyệt & Xuất Bản
- UC-M2-009: Trường Từ Chối
- UC-M2-013: Phê Duyệt Hàng Loạt (Trường)
- UC-M2-014: Phân Công Lại Reviewer

**Hành Động Hệ Thống** (3):
- UC-M2-010: Xem Lịch Sử Xét Duyệt
- UC-M2-011: Gửi Email Thông Báo
- UC-M2-015: Giám Sát SLA

---

### [Module 3: Tìm Kiếm & Duyệt](./module_03_search_browse.md)
7 use cases tìm kiếm và duyệt công khai.

- UC-M3-001: Tìm Kiếm Cơ Bản
- UC-M3-002: Tìm Kiếm Nâng Cao
- UC-M3-003: Lọc Kết Quả
- UC-M3-004: Sắp Xếp Kết Quả
- UC-M3-005: Xem Chi Tiết Bài Báo (Public)
- UC-M3-006: Duyệt Theo Khoa
- UC-M3-007: Duyệt Theo Năm/Xếp Hạng

---

### [Module 4: Hồ Sơ Nhà Nghiên Cứu](./module_04_researcher_profile.md)
6 use cases quản lý hồ sơ công khai.

- UC-M4-001: Xem Hồ Sơ Công Khai
- UC-M4-002: Chỉnh Sửa Hồ Sơ
- UC-M4-003: Cập Nhật Ảnh Đại Diện
- UC-M4-004: Liên Kết ORCID
- UC-M4-005: Xem Phân Tích Bài Báo
- UC-M4-006: Tạo Word Cloud

---

### [Module 5: Báo Cáo & Phân Tích](./module_05_reporting_analytics.md)
7 use cases báo cáo và phân tích.

- UC-M5-001: Tạo Báo Cáo Khoa
- UC-M5-002: Tạo Báo Cáo Trường
- UC-M5-003: Xuất Excel
- UC-M5-004: Xuất PDF
- UC-M5-005: Xem Thống Kê Dashboard
- UC-M5-006: Theo Dõi Xu Hướng Năng Suất
- UC-M5-007: Đối Sánh Các Khoa

---

### [Module 6: Quản Trị Hệ Thống](./module_06_admin_management.md)
10 use cases quản trị hệ thống.

- UC-M6-001: Tạo Người Dùng
- UC-M6-002: Sửa Người Dùng
- UC-M6-003: Xóa Người Dùng
- UC-M6-004: Gán Vai Trò
- UC-M6-005: Quản Lý Khoa
- UC-M6-006: Cấu Hình LDAP
- UC-M6-007: Cấu Hình Email
- UC-M6-008: Xem Audit Logs
- UC-M6-009: Sao Lưu Hệ Thống
- UC-M6-010: Import Người Dùng từ Excel

---

**Tài liệu liên quan**:
- [Use Case Cấp Cao (High-Level)](../High_Level/)
- [Use Case Chi Tiết (Detailed-Level)](../Detailed_Level/)
- [README Chính](../README.md)
