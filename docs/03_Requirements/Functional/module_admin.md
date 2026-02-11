# Module 6: Admin & User Management - Yêu Cầu Chức Năng

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Phân hệ**: Quản trị Hệ thống  
> 👥 **Người dùng**: Quản trị viên cấp cao (SuperAdmin)

---

## 1. Yêu Cầu Chức Năng (Functional Requirements)

### FR-ADM-001: Quản lý Người dùng (Thêm/Xóa/Sửa)
**Độ ưu tiên**: 🔴 P0 - Phải Có

**Hành động**:
- Tạo người dùng (thủ công hoặc nhập từ Excel)
- Sửa người dùng (tên, email, khoa, vai trò)
- Xóa người dùng (xóa mềm)
- Khóa/Mở khóa tài khoản
- Đặt lại mật khẩu

---

### FR-ADM-002: Phân quyền Vai trò
**Độ ưu tiên**: 🔴 P0 - Phải Có

**Vai trò**:
- Quản trị viên cấp cao (SuperAdmin)
- Nhà nghiên cứu (Researcher)
- Người duyệt cấp Khoa (Faculty Reviewer)
- Người duyệt cấp Trường (University Reviewer)
- Người xem (Viewer) - mặc định

**Quy tắc nghiệp vụ**:
- 1 người dùng có thể có nhiều vai trò
- Nhà nghiên cứu + Người duyệt cấp Khoa (phổ biến)

---

### FR-ADM-003: Quản lý Khoa/Bộ môn
**Độ ưu tiên**: 🔴 P0 - Phải Có

**Thao tác CRUD**:
- Thêm/Sửa/Xóa Khoa
- Phân công Người duyệt cấp Khoa
- Danh sách nhà nghiên cứu theo khoa

---

### FR-ADM-004: Cấu hình LDAP/AD
**Độ ưu tiên**: 🔴 P0 - Phải Có

**Cài đặt**:
- URL máy chủ LDAP
- Base DN
- Bind DN, mật khẩu
- Kiểm tra kết nối

---

### FR-ADM-005: Cấu hình Email
**Độ ưu tiên**: 🔴 P0 - Phải Có

**Cài đặt SMTP**:
- Máy chủ (Host), Cổng (Port)
- Tên đăng nhập, Mật khẩu
- Địa chỉ gửi (From address)
- Gửi email kiểm tra

---

### FR-ADM-006: Nhật ký Kiểm toán (Audit Logs)
**Độ ưu tiên**: 🔴 P0 - Phải Có

**Sự kiện được ghi lại**:
- Người dùng đăng nhập/đăng xuất
- Thay đổi trạng thái bài báo
- Thay đổi vai trò người dùng
- Thay đổi cấu hình hệ thống

**Xem**:
- Lọc theo người dùng, loại hành động, khoảng thời gian
- Xuất ra CSV

---

### FR-ADM-007: Sao lưu & Khôi phục
**Độ ưu tiên**: 🔴 P0 - Phải Có

**Sao lưu**:
- Kích hoạt thủ công
- Lên lịch (hàng ngày)
- Cơ sở dữ liệu + Tệp tin

**Khôi phục**:
- Chọn tệp sao lưu
- Khôi phục với xác nhận

---

### FR-ADM-008: Bảng điều khiển Hệ thống
**Độ ưu tiên**: 🟡 P1 - Nên Có

**Các chỉ số**:
- Người dùng trực tuyến
- Tổng số người dùng theo vai trò
- Tổng số bài báo theo trạng thái
- Sức khỏe hệ thống (CPU, Bộ nhớ, Đĩa)

---

### FR-ADM-009: Nhập Người dùng từ Excel
**Độ ưu tiên**: 🟡 P1 - Nên Có

**Định dạng**: Tên, Email, Khoa, Vai trò

**Kiểm tra hợp lệ**:
- Định dạng Email
- Khoa tồn tại
- Vai trò hợp lệ

---

### FR-ADM-010: Thao tác Hàng loạt (Bulk Operations)
**Độ ưu tiên**: 🟡 P1 - Nên Có

**Hành động**:
- Phân vai trò cho nhiều người dùng
- Chuyển người dùng sang khoa khác
- Khóa/Mở khóa nhiều tài khoản

---

## 2. Quyền hạn (Permissions)

| Hành động | Quản trị viên cấp cao | Người khác |
|--------|-----------|--------|
| Tất cả chức năng quản trị | ✅ | ❌ |

---

**Tài liệu liên quan**:
- [Nhu cầu Người dùng - SuperAdmin](../../02_System_Clarification/User_Analysis/user_needs.md#5-superadmin)
