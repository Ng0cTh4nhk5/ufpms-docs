# User Stories - SuperAdmin

> 👤 **Role**: SuperAdmin  
> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục tiêu**: Quản trị hệ thống, người dùng, và cấu hình

---

## Tổng Quan

**Total Stories**: 10  
**P0 (Must Have)**: 8  
**P1 (Should Have)**: 2  
**P2 (Nice to Have)**: 0

---

## Module 6: Admin & User Management

### US-ADM-001: Quản Lý Người Dùng (CRUD)
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-ADM-001

**User Story**:
```
As a SuperAdmin (Là Admin),
I want to create, edit, and delete user accounts (Tôi muốn tạo, sửa và xóa tài khoản người dùng),
So that I can manage who has access to the system (Để tôi có thể quản lý quyền truy cập hệ thống).
```

**Acceptance Criteria**:
```
GIVEN I am logged in as SuperAdmin (KHI tôi đã đăng nhập là Admin)
WHEN I access the User Management page (VÀ tôi truy cập trang Quản lý người dùng)
THEN I can: (THÌ tôi có thể:)
- Create new users manually or import from Excel (Tạo người dùng mới thủ công hoặc import từ Excel)
- Edit user details (name, email, faculty, role) (Sửa thông tin người dùng: tên, email, khoa, vai trò)
- Delete users (soft delete) (Xóa người dùng - xóa mềm)
- Lock/Unlock accounts (Khóa/Mở khóa tài khoản)
- Reset passwords (Đặt lại mật khẩu)
```

---

### US-ADM-002: Gán Vai Trò Người Dùng
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-ADM-002

**User Story**:
```
As a SuperAdmin (Là Admin),
I want to assign and manage user roles (Tôi muốn gán và quản lý vai trò người dùng),
So that users have appropriate permissions for their responsibilities (Để người dùng có quyền hạn phù hợp với trách nhiệm của họ).
```

**Acceptance Criteria**:
```
GIVEN I am editing a user (KHI tôi đang chỉnh sửa một người dùng)
WHEN I access the roles section (VÀ tôi truy cập phần vai trò)
THEN I can assign multiple roles: (THÌ tôi có thể gán nhiều vai trò:)
- SuperAdmin
- Researcher (default) (Giảng viên - mặc định)
- Faculty Reviewer (Cán bộ duyệt khoa)
- University Reviewer (Cán bộ duyệt trường)
- Viewer (Người xem)
AND a user can have multiple roles simultaneously (VÀ một người dùng có thể có nhiều vai trò cùng lúc)
```

---

### US-ADM-003: Quản Lý Khoa/Đơn Vị
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-ADM-003

**User Story**:
```
As a SuperAdmin (Là Admin),
I want to manage faculty/department information (Tôi muốn quản lý thông tin khoa/phòng ban),
So that the organizational structure is up to date (Để cấu trúc tổ chức luôn được cập nhật).
```

**Acceptance Criteria**:
```
GIVEN I am in Faculty Management (KHI tôi ở trang Quản lý Khoa)
WHEN I perform CRUD operations (VÀ tôi thực hiện các thao tác thêm/sửa/xóa)
THEN I can: (THÌ tôi có thể:)
- Add/Edit/Delete faculties (Thêm/Sửa/Xóa khoa)
- Assign Faculty Reviewers to each faculty (Gán người duyệt cấp khoa cho từng khoa)
- View list of researchers by faculty (Xem danh sách giảng viên theo khoa)
```

---

### US-ADM-004: Cấu Hình LDAP/AD
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-ADM-004

**User Story**:
```
As a SuperAdmin (Là Admin),
I want to configure LDAP/AD authentication settings (Tôi muốn cấu hình xác thực LDAP/AD),
So that users can log in with university credentials (Để người dùng có thể đăng nhập bằng tài khoản trường).
```

**Acceptance Criteria**:
```
GIVEN I am in System Configuration (KHI tôi ở trang Cấu hình hệ thống)
WHEN I access LDAP settings (VÀ tôi truy cập cài đặt LDAP)
THEN I can configure: (THÌ tôi có thể cấu hình:)
- LDAP server URL
- Base DN
- Bind DN and password
AND I can test the connection before saving (VÀ tôi có thể kiểm tra kết nối trước khi lưu)
```

---

### US-ADM-005: Cấu Hình Email
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-ADM-005

**User Story**:
```
As a SuperAdmin (Là Admin),
I want to configure email server settings (Tôi muốn cấu hình máy chủ email),
So that the system can send notifications to users (Để hệ thống có thể gửi thông báo cho người dùng).
```

**Acceptance Criteria**:
```
GIVEN I am in System Configuration (KHI tôi ở trang Cấu hình hệ thống)
WHEN I access Email settings (VÀ tôi truy cập cài đặt Email)
THEN I can configure: (THÌ tôi có thể cấu hình:)
- SMTP Host and Port
- Username and Password
- From address (Địa chỉ gửi)
AND I can send a test email to verify settings (VÀ tôi có thể gửi email thử nghiệm để kiểm tra cài đặt)
```

---

### US-ADM-006: Xem Audit Logs
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-ADM-006

**User Story**:
```
As a SuperAdmin (Là Admin),
I want to view system audit logs (Tôi muốn xem nhật ký hệ thống),
So that I can monitor user activities and system changes (Để tôi có thể giám sát hoạt động người dùng và thay đổi hệ thống).
```

**Acceptance Criteria**:
```
GIVEN I am on the Audit Logs page (KHI tôi ở trang Nhật ký hệ thống)
WHEN I view the logs (VÀ tôi xem danh sách log)
THEN I see all events: (THÌ tôi thấy tất cả sự kiện:)
- User login/logout (Đăng nhập/Đăng xuất)
- Publication state changes (Thay đổi trạng thái bài báo)
- User role changes (Thay đổi vai trò người dùng)
- System configuration changes (Thay đổi cấu hình hệ thống)
AND I can filter by: User, Action Type, Date Range (VÀ tôi có thể lọc theo: Người dùng, Loại hành động, Khoảng thời gian)
AND I can export logs to CSV (VÀ tôi có thể xuất log ra file CSV)
```

---

### US-ADM-007: Backup và Restore
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-ADM-007

**User Story**:
```
As a SuperAdmin (Là Admin),
I want to backup and restore the system (Tôi muốn sao lưu và khôi phục hệ thống),
So that data is protected and can be recovered if needed (Để dữ liệu được bảo vệ và có thể khôi phục khi cần).
```

**Acceptance Criteria**:
```
GIVEN I am on the Backup page (KHI tôi ở trang Sao lưu)
WHEN I trigger a backup (VÀ tôi thực hiện sao lưu)
THEN the system: (THÌ hệ thống:)
- Backs up the database (Sao lưu cơ sở dữ liệu)
- Backs up uploaded files (Sao lưu các tệp đã tải lên)
- Can be scheduled (daily automatic backup) (Có thể lên lịch sao lưu tự động hàng ngày)
AND I can select a backup file to restore (VÀ tôi có thể chọn tệp sao lưu để khôi phục)
WITH confirmation before restoring (VÀ có xác nhận trước khi khôi phục)
```

---

### US-ADM-008: Xem System Dashboard
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-ADM-008

**User Story**:
```
As a SuperAdmin (Là Admin),
I want to see system health and usage statistics (Tôi muốn xem thống kê sức khỏe hệ thống và mức sử dụng),
So that I can monitor system performance (Để tôi có thể giám sát hiệu năng hệ thống).
```

**Acceptance Criteria**:
```
GIVEN I am on the Admin Dashboard (KHI tôi ở trang Dashboard Admin)
WHEN the page loads (VÀ trang tải xong)
THEN I see: (THÌ tôi thấy:)
- Users currently online (Số người dùng đang online)
- Total users by role (Tổng số người dùng theo vai trò)
- Total publications by status (Tổng số bài báo theo trạng thái)
- System health metrics (CPU, Memory, Disk usage) (Các chỉ số sức khỏe hệ thống: CPU, RAM, Ổ cứng)
```

---

### US-ADM-009: Import Người Dùng từ Excel
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-ADM-009

**User Story**:
```
As a SuperAdmin (Là Admin),
I want to bulk import users from an Excel file (Tôi muốn import nhiều người dùng từ file Excel),
So that I can efficiently onboard many users at once (Để tôi có thể thêm nhiều người dùng cùng lúc một cách hiệu quả).
```

**Acceptance Criteria**:
```
GIVEN I have an Excel file with format: Name, Email, Faculty, Role (KHI tôi có file Excel với định dạng: Tên, Email, Khoa, Vai trò)
WHEN I upload and process the file (VÀ tôi tải lên và xử lý file)
THEN the system: (THÌ hệ thống:)
- Validates email format (Kiểm tra định dạng email)
- Validates faculty exists (Kiểm tra khoa có tồn tại)
- Validates role is valid (Kiểm tra vai trò hợp lệ)
- Creates users (Tạo người dùng)
- Shows a summary report (success/failed) (Hiển thị báo cáo tóm tắt: thành công/thất bại)
```

---

### US-ADM-010: Thao Tác Hàng Loạt
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-ADM-010

**User Story**:
```
As a SuperAdmin (Là Admin),
I want to perform bulk operations on multiple users (Tôi muốn thực hiện thao tác hàng loạt trên nhiều người dùng),
So that I can manage users efficiently (Để tôi có thể quản lý người dùng hiệu quả).
```

**Acceptance Criteria**:
```
GIVEN I have selected multiple users (checkboxes) (KHI tôi chọn nhiều người dùng)
WHEN I choose a bulk action (VÀ tôi chọn một hành động hàng loạt)
THEN I can: (THÌ tôi có thể:)
- Assign roles to all selected users (Gán vai trò cho tất cả người dùng đã chọn)
- Move users to a different faculty (Chuyển người dùng sang khoa khác)
- Lock/Unlock multiple accounts (Khóa/Mở khóa nhiều tài khoản)
- Delete multiple users (Xóa nhiều người dùng)
WITH a confirmation dialog before executing (VÀ có hộp thoại xác nhận trước khi thực hiện)
```

---

## Traceability Matrix

| Story ID | Title | Priority | FR ID | Module |
|----------|-------|----------|-------|--------|
| US-ADM-001 | Quản Lý Người Dùng (CRUD) | P0 | FR-ADM-001 | 6 |
| US-ADM-002 | Gán Vai Trò Người Dùng | P0 | FR-ADM-002 | 6 |
| US-ADM-003 | Quản Lý Khoa/Đơn Vị | P0 | FR-ADM-003 | 6 |
| US-ADM-004 | Cấu Hình LDAP/AD | P0 | FR-ADM-004 | 6 |
| US-ADM-005 | Cấu Hình Email | P0 | FR-ADM-005 | 6 |
| US-ADM-006 | Xem Audit Logs | P0 | FR-ADM-006 | 6 |
| US-ADM-007 | Backup và Restore | P0 | FR-ADM-007 | 6 |
| US-ADM-008 | Xem System Dashboard | P1 | FR-ADM-008 | 6 |
| US-ADM-009 | Import Người Dùng từ Excel | P1 | FR-ADM-009 | 6 |
| US-ADM-010 | Thao Tác Hàng Loạt | P0 | FR-ADM-010 | 6 |

---

**Tài liệu liên quan**:
- [Requirements - Admin & User Management](../../03_Requirements/Functional/module_admin.md)
