# P0 User Stories - Must Have (MVP)

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục đích**: User stories bắt buộc cho MVP  
> ⚠️ **Priority**: P0 - Must Have

---

## Tổng Quan

**Tổng số User Story P0**: 40  

---

## Phân Bổ Theo Vai Trò

| Vai trò | Số lượng P0 Stories |
|------|-----------|
| Giảng viên (Researcher) | 18 |
| Cán bộ Duyệt Khoa (Faculty Reviewer) | 6 |
| Cán bộ Duyệt Trường (University Reviewer) | 6 |
| Quản trị viên (SuperAdmin) | 8 |
| Khách (Public Visitor) | 2 |

---

## Giảng viên (Researcher) (18 Stories)

### Quản lý Bài báo (Publication Management)
- **US-RES-001**: Tạo Bài Báo Mới (FR-PUB-001)
- **US-RES-002**: Upload File PDF (FR-PUB-002)
- **US-RES-003**: Sửa Bài Báo Nháp (FR-PUB-004)
- **US-RES-004**: Xóa Bài Báo Nháp (FR-PUB-005)
- **US-RES-005**: Xem Danh Sách Bài Báo (FR-PUB-006)
- **US-RES-008**: Xem Chi Tiết Bài Báo (FR-PUB-010)
- **US-RES-009**: Download File PDF (FR-PUB-011)

### Quy trình Xét duyệt (Approval Workflow)
- **US-RES-010**: Nộp Xét Duyệt (FR-APR-001)
- **US-RES-011**: Xem Trạng Thái Xét Duyệt (FR-APR-002)
- **US-RES-012**: Chỉnh Sửa Theo Yêu Cầu (FR-APR-003)

**Total**: 10 P0 stories

---

## Cán bộ Duyệt Khoa (Faculty Reviewer) (6 Stories)

### Quy trình Xét duyệt (Approval Workflow)
- **US-FCR-001**: Xem Dashboard Chờ Duyệt Khoa (FR-APR-005)
- **US-FCR-002**: Phê Duyệt Bài Báo (FR-APR-006)
- **US-FCR-003**: Yêu Cầu Bổ Sung (FR-APR-007)
- **US-FCR-004**: Từ Chối Bài Báo (FR-APR-008)
- **US-FCR-005**: Xem Lịch Sử Xét Duyệt (FR-APR-015)
- **US-FCR-006**: Nhận Thông Báo Email (FR-APR-016)

---

## Cán bộ Duyệt Trường (University Reviewer) (6 Stories)

### Quy trình Xét duyệt (Approval Workflow)
- **US-UNR-001**: Xem Dashboard Chờ Duyệt Trường (FR-APR-010)
- **US-UNR-002**: Xem Ý Kiến Cấp Khoa (FR-APR-011)
- **US-UNR-003**: Phê Duyệt và Công Bố (FR-APR-012)
- **US-UNR-004**: Từ Chối Cấp Trường (FR-APR-013)
- **US-UNR-005**: Xem Audit Trail (FR-APR-015)
- **US-UNR-006**: Nhận Thông Báo Email (FR-APR-016)

---

## Quản trị viên (SuperAdmin) (8 Stories)

### Quản trị & Quản lý Người dùng (Admin & User Management)
- **US-ADM-001**: Quản Lý Người Dùng (CRUD) (FR-ADM-001)
- **US-ADM-002**: Gán Vai Trò Người Dùng (FR-ADM-002)
- **US-ADM-003**: Quản Lý Khoa/Đơn Vị (FR-ADM-003)
- **US-ADM-004**: Cấu Hình LDAP/AD (FR-ADM-004)
- **US-ADM-005**: Cấu Hình Email (FR-ADM-005)
- **US-ADM-006**: Xem Audit Logs (FR-ADM-006)
- **US-ADM-007**: Backup và Restore (FR-ADM-007)
- **US-ADM-010**: Thao Tác Hàng Loạt (FR-ADM-010)

---

## Khách (Public Visitor) (2 Stories)

### Tìm kiếm & Duyệt (Search & Browse)
- **US-VIW-005**: Phân Trang Kết Quả (FR-SEA-005)
- **US-VIW-006**: Xem Chi Tiết Công Trình (FR-SEA-006)

---

## Thứ tự Triển khai MVP (MVP Implementation Priority)

### Sprint 1: Quản lý Bài báo Cốt lõi + Quy trình
**Thời gian**: 2-3 tuần

**Tính năng**:
- CRUD Bài báo (US-RES-001 đến US-RES-009)
- Nộp để xét duyệt (US-RES-010, US-RES-011, US-RES-012)

**Bàn giao**:
- Giảng viên có thể tạo, sửa, xóa bài báo
- Giảng viên có thể nộp bài báo
- Quy trình nháp cơ bản hoàn thiện

---

### Sprint 2: Quy trình Duyệt cấp Khoa
**Thời gian**: 2 tuần

**Tính năng**:
- Dashboard cho Cán bộ Khoa (US-FCR-001)
- Duyệt/Từ chối/Yêu cầu chỉnh sửa (US-FCR-002, US-FCR-003, US-FCR-004)
- Thông báo email (US-FCR-006)
- Dấu vết kiểm toán (Audit trail) (US-FCR-005)

**Bàn giao**:
- Cán bộ khoa có thể duyệt bài báo
- Quy trình phê duyệt 2 cấp hoạt động

---

### Sprint 3: Duyệt cấp Trường + Quản trị (Admin)
**Thời gian**: 2 tuần

**Tính năng**:
- Dashboard cho Cán bộ Trường (US-UNR-001 đến US-UNR-006)
- Quản lý người dùng admin (US-ADM-001 đến US-ADM-007, US-ADM-010)

**Bàn giao**:
- Quy trình phê duyệt hoàn chỉnh
- Chức năng quản trị hệ thống hoạt động
- Xác thực LDAP hoạt động

---

### Sprint 4: Truy cập Công khai (Public Access)
**Thời gian**: 1 tuần

**Tính năng**:
- Tìm kiếm công khai có phân trang (US-VIW-005, US-VIW-006)

**Bàn giao**:
- Khách có thể xem các bài báo đã công bố
- Chức năng tìm kiếm cơ bản

---

## Tóm tắt Tiêu chí Chấp nhận (Acceptance Criteria Summary)

### Định nghĩa Hoàn thành cho User Story P0 (Definition of Done)

✅ **Hoàn thành Code**:
- Unit tests thông qua
- Integration tests thông qua
- Code đã được review và merge

✅ **Chức năng (Functional)**:
- Đạt các tiêu chí chấp nhận (Acceptance criteria met)
- Đã test thủ công
- Đã xử lý các trường hợp ngoại lệ (Edge cases)

✅ **Phi chức năng (Non-Functional)**:
- Đạt mục tiêu hiệu năng (page load < 2s)
- Đạt yêu cầu bảo mật (LDAP auth, RBAC)
- Audit logging đã sẵn sàng

✅ **Tài liệu**:
- Tài liệu API đã cập nhật
- Tài liệu hướng dẫn sử dụng đã tạo
- Hướng dẫn triển khai đã cập nhật

---

## Các sự phụ thuộc (Dependencies)

### Hệ thống Bên ngoài (Bắt buộc)
- ✅ LDAP/AD server cho xác thực
- ✅ Email server (SMTP) cho thông báo
- ✅ MySQL 8.0+ database

### Stack Kỹ thuật (P0)
- ✅ Backend: Java Spring Boot 3.x
- ✅ Frontend: React 18 + TypeScript
- ✅ Database: MySQL 8.0+
- ✅ Authentication: LDAP/AD + JWT

---

## Rủi ro & Biện pháp Giảm thiểu (Risks & Mitigation)

| Rủi ro | Tác động | Biện pháp |
|------|--------|-----------|
| Chậm tích hợp LDAP | Cao | Sử dụng mock authentication để phát triển |
| Email server không khả dụng | Trung bình | Xếp hàng email (Queue), cơ chế thử lại (retry) |
| Vấn đề lưu trữ file | Trung bình | Triển khai lưu trữ cục bộ trước, đám mây sau |
| Phức tạp của State machine | Cao | Unit testing kỹ lưỡng, validate trạng thái |

---

**Tài liệu liên quan**:
- [All User Stories by Role](../By_Role/)
- [Functional Requirements](../../03_Requirements/Functional/)
- [P1 Should Have Stories](./p1_should_have.md)
