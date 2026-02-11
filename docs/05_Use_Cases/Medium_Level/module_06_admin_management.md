# Module 6: Quản Trị Hệ Thống & Người Dùng - Use Cases Cấp Trung

> **Module**: 6 - Quản Trị Hệ Thống & Người Dùng  
> **Use Case Cấp Cao**: [UC-HL-006](../High_Level/uc_hl_06_admin_management.md)

---

## UC-M6-001: Tạo Người Dùng (Create User)
**ID**: UC-M6-001 | **Độ Ưu Tiên**: 🔴 P0 | **Tác Nhân**: SuperAdmin  
**Liên Quan**: US-ADM-001, FR-ADM-001

**Mục Tiêu**: Tạo tài khoản người dùng mới  
**Điều Kiện Tiên Quyết**: Người dùng là SuperAdmin  
**Luồng Chính**:
1. Admin nhấn "Thêm Người Dùng"
2. Hệ thống hiển thị biểu mẫu: Tên, Email, Khoa, Vai trò
3. Admin nhập thông tin
4. Hệ thống xác thực:
   - Định dạng và tính duy nhất của Email
   - Khoa tồn tại
   - Vai trò hợp lệ
5. Hệ thống tạo người dùng với mật khẩu mặc định
6. Hệ thống gửi email chào mừng (tùy chọn)
7. Hệ thống hiển thị "Tạo người dùng thành công"

**Điều Kiện Hậu Quyết**: Tài khoản người dùng được tạo  
**Quy Tắc Nghiệp Vụ**: BR-ADM-006 (email duy nhất), vai trò mặc định = Researcher

---

## UC-M6-002: Sửa Người Dùng (Edit User)
**ID**: UC-M6-002 | **Độ Ưu Tiên**: 🔴 P0 | **Tác Nhân**: SuperAdmin  
**Liên Quan**: US-ADM-001, FR-ADM-001

**Mục Tiêu**: Chỉnh sửa người dùng hiện có  
**Luồng Chính**:
1. Admin chọn người dùng từ danh sách
2. Admin nhấn "Sửa"
3. Hệ thống hiển thị biểu mẫu có thể chỉnh sửa
4. Admin sửa đổi: Tên, Email, Khoa, Vai trò
5. Admin lưu lại
6. Hệ thống xác thực và cập nhật
7. Hệ thống ghi nhận thay đổi vào nhật ký kiểm toán

**Quy Tắc Nghiệp Vụ**: BR-ADM-002 (không thể sửa chính mình để gỡ quyền SuperAdmin)

---

## UC-M6-003: Xóa Người Dùng (Delete User)
**ID**: UC-M6-003 | **Độ Ưu Tiên**: 🔴 P0 | **Tác Nhân**: SuperAdmin  
**Liên Quan**: US-ADM-001, FR-ADM-001

**Mục Tiêu**: Xóa tài khoản người dùng  
**Luồng Chính**:
1. Admin chọn người dùng
2. Admin nhấn "Xóa"
3. Hệ thống xác nhận: "Bạn có chắc chắn không? Hành động này không thể hoàn tác."
4. Admin xác nhận
5. Hệ thống xóa mềm (đặt deleted_at)
6. Người dùng bị đăng xuất ngay lập tức

**Quy Tắc Nghiệp Vụ**: BR-ADM-002 (không thể xóa chính mình), BR-ADM-002 (phải có ít nhất 1 SuperAdmin)

---

## UC-M6-004: Gán Vai Trò (Assign Roles)
**ID**: UC-M6-004 | **Độ Ưu Tiên**: 🔴 P0 | **Tác Nhân**: SuperAdmin  
**Liên Quan**: US-ADM-002, FR-ADM-002

**Mục Tiêu**: Gán hoặc gỡ bỏ vai trò người dùng  
**Luồng Chính**:
1. Admin xem chi tiết người dùng
2. Admin thấy các vai trò hiện tại
3. Admin chọn/bỏ chọn các vai trò:
   - SuperAdmin
   - Researcher (Nhà nghiên cứu)
   - Faculty Reviewer (Người duyệt cấp Khoa)
   - University Reviewer (Người duyệt cấp Trường)
4. Người dùng có thể có NHIỀU vai trò
5. Hệ thống cập nhật quyền hạn ngay lập tức
6. Hệ thống ghi nhận thay đổi vai trò

**Quy Tắc Nghiệp Vụ**: BR-ADM-001 (chỉ SuperAdmin mới được gán), BR-ADM-003 (phân cấp vai trò)

---

## UC-M6-005: Quản Lý Khoa (Manage Faculties)
**ID**: UC-M6-005 | **Độ Ưu Tiên**: 🔴 P0 | **Tác Nhân**: SuperAdmin  
**Liên Quan**: US-ADM-003, FR-ADM-003

**Mục Tiêu**: CRUD khoa/phòng ban  
**Luồng Chính**:
1. Admin nhấn "Quản Lý Khoa"
2. Admin có thể:
   - Thêm khoa mới (tên, mã)
   - Sửa thông tin khoa
   - Xóa khoa (chỉ khi không có người dùng được gán)
   - Gán Faculty Reviewer cho từng khoa
3. Thay đổi được lưu vào cơ sở dữ liệu

**Quy Tắc Nghiệp Vụ**: Không thể xóa khoa đang có người dùng

---

## UC-M6-006: Cấu Hình LDAP (Configure LDAP)
**ID**: UC-M6-006 | **Độ Ưu Tiên**: 🔴 P0 | **Tác Nhân**: SuperAdmin  
**Liên Quan**: US-ADM-004, FR-ADM-004

**Mục Tiêu**: Cấu hình xác thực LDAP/AD  
**Luồng Chính**:
1. Admin nhấn "Cấu Hình Hệ Thống" → "LDAP"
2. Admin nhập:
   - LDAP Server URL
   - Base DN
   - Bind DN và Mật khẩu
   - Bộ lọc tìm kiếm
3. Admin nhấn "Kiểm Tra Kết Nối"
4. Hệ thống thử kết nối LDAP (bind)
5. Nếu thành công: "Kết nối thành công ✓"
6. Admin lưu cấu hình

**Điều Kiện Hậu Quyết**: Người dùng có thể đăng nhập bằng tài khoản trường  
**Quy Tắc Nghiệp Vụ**: Phải kiểm tra kết nối trước khi lưu

---

## UC-M6-007: Cấu Hình Email (Configure Email)
**ID**: UC-M6-007 | **Độ Ưu Tiên**: 🔴 P0 | **Tác Nhân**: SuperAdmin  
**Liên Quan**: US-ADM-005, FR-ADM-005

**Mục Tiêu**: Cấu hình cài đặt email SMTP  
**Luồng Chính**:
1. Admin nhấn "Cấu Hình Hệ Thống" → "Email"
2. Admin nhập:
   - SMTP Host, Port
   - Username, Password
   - Địa chỉ gửi đi (From Address)
   - Sử dụng TLS: Có/Không
3. Admin nhấn "Gửi Email Thử"
4. Hệ thống gửi email thử nghiệm
5. Admin xác nhận đã nhận được
6. Admin lưu cấu hình

**Điều Kiện Hậu Quyết**: Thông báo có thể được gửi đi

---

## UC-M6-008: Xem Nhật Ký Kiểm Toán (View Audit Logs)
**ID**: UC-M6-008 | **Độ Ưu Tiên**: 🔴 P0 | **Tác Nhân**: SuperAdmin  
**Liên Quan**: US-ADM-006, FR-ADM-006

**Mục Tiêu**: Xem nhật ký kiểm toán hệ thống  
**Luồng Chính**:
1. Admin nhấn "Nhật Ký Kiểm Toán"
2. Hệ thống hiển thị nhật ký có thể lọc:
   - Người dùng đăng nhập/đăng xuất
   - Thay đổi trạng thái bài báo
   - Thay đổi vai trò người dùng
   - Thay đổi cấu hình
3. Admin lọc theo: Khoảng thời gian, Người dùng, Loại hành động
4. Admin có thể xuất ra CSV

**Quy Tắc Nghiệp Vụ**: BR-ADM-004 (ghi nhật ký mọi thứ, bất biến, lưu trữ 2 năm)

---

## UC-M6-009: Sao Lưu Hệ Thống (Backup System)
**ID**: UC-M6-009 | **Độ Ưu Tiên**: 🔴 P0 | **Tác Nhân**: SuperAdmin  
**Liên Quan**: US-ADM-007, FR-ADM-007

**Mục Tiêu**: Tạo bản sao lưu hệ thống  
**Luồng Chính**:
1. Admin nhấn "Sao Lưu"
2. Hệ thống cảnh báo: "Có thể mất vài phút"
3. Hệ thống sao lưu:
   - Cơ sở dữ liệu (SQL dump)
   - Các tập tin đã tải lên
4. Hệ thống tạo file .zip
5. Hệ thống cung cấp liên kết tải xuống
6. Admin có thể lên lịch sao lưu hàng ngày

**Quy Tắc Nghiệp Vụ**: BR-ADM-005 (sao lưu tự động hàng ngày, giữ 30 ngày)

---

## UC-M6-010: Import Người Dùng từ Excel (Import Users from Excel)
**ID**: UC-M6-010 | **Độ Ưu Tiên**: 🟡 P1 | **Tác Nhân**: SuperAdmin  
**Liên Quan**: US-ADM-009, FR-ADM-009

**Mục Tiêu**: Import người dùng hàng loạt  
**Luồng Chính**:
1. Admin tải mẫu Excel
2. Admin điền: Tên, Email, Khoa, Vai trò
3. Admin tải lên file
4. Hệ thống xác thực từng dòng
5. Hệ thống hiển thị xem trước với các lỗi (nếu có)
6. Admin xác nhận import
7. Hệ thống tạo người dùng
8. Hệ thống hiển thị tóm tắt: "50 đã tạo, 3 thất bại"

**Quy Tắc Nghiệp Vụ**: Xác thực tất cả các dòng trước khi import

---

**Tài liệu liên quan**:
- [Use Case Cấp Cao UC-HL-006](../High_Level/uc_hl_06_admin_management.md)
- [User Stories - SuperAdmin](../../04_User_Stories/By_Role/admin_stories.md)
- [Yêu Cầu - Admin](../../03_Requirements/Functional/module_admin.md)
