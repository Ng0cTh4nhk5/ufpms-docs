# Yêu Cầu Bảo Mật - Security Requirements

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Danh mục**: Yêu cầu Phi Chức Năng

---

## 1. Yêu cầu Xác thực (Authentication Requirements)

### NFR-SEC-001: Tích hợp LDAP/AD (SSO)
**Yêu cầu**: Tất cả người dùng nội bộ (internal users) PHẢI đăng nhập qua LDAP/AD

**Triển khai**:
- Spring Security + LDAP
- Không lưu mật khẩu cục bộ
- Thời gian hết hạn phiên (Session timeout): 8 giờ
- Ghi nhớ đăng nhập (Remember me): 30 ngày (tùy chọn)

---

### NFR-SEC-002: Bảo mật JWT Token
**Yêu cầu**:
- Thuật toán: HS256 hoặc RS256
- Hết hạn: 24 giờ
- Token làm mới (Refresh token): 7 ngày
- Lưu trong HttpOnly cookie (không dùng localStorage)

---

## 2. Yêu cầu Phân quyền (Authorization Requirements)

### NFR-SEC-010: Kiểm soát Truy cập Dựa trên Vai trò (RBAC)
**Các vai trò**: Quản trị viên cấp cao (SuperAdmin), Nhà nghiên cứu, Người duyệt Khoa, Người duyệt Trường, Người xem

**Thực thi**:
- Backend: Kiểm tra vai trò trước mọi cuộc gọi API
- Frontend: Ẩn các thành phần giao diện dựa trên vai trò
- Cơ sở dữ liệu: Bảo mật cấp hàng (Row-level security - tùy chọn)

---

### NFR-SEC-011: Kiểm soát Truy cập Bài báo
**Quy tắc**:
- DRAFT (Nháp): CHỈ chủ sở hữu (owner) + admin
- SUBMITTED/REVIEWING (Đã nộp/Đang duyệt): Chủ sở hữu + người duyệt (theo khoa) + admin
- PUBLISHED (Đã xuất bản): Tất cả mọi người

---

## 3. Bảo vệ Dữ liệu (Data Protection)

### NFR-SEC-020: Bắt buộc HTTPS
**Yêu cầu**: Tất cả lưu lượng truy cập PHẢI qua HTTPS

- Tối thiểu TLS 1.2 (ưu tiên TLS 1.3)
- Chứng chỉ từ Let's Encrypt hoặc CA thương mại
- HSTS (HTTP Strict Transport Security)
- Chuyển hướng HTTP → HTTPS

---

### NFR-SEC-021: Bảo vệ Dữ liệu Cá nhân
**Tuân thủ**: Nghị định 13/2023/NĐ-CP

**Dữ liệu được bảo vệ**:
- Địa chỉ email
- ORCID
- Thông tin liên hệ cá nhân

**Biện pháp**:
- Không hiển thị công khai nếu không có sự đồng ý
- Mã hóa trong cơ sở dữ liệu (tùy chọn)
- Nhật ký kiểm toán cho mọi truy cập

---

### NFR-SEC-022: Bảo mật Tải lên Tệp
**Kiểm tra**:
- Loại tệp: CHỈ PDF (kiểm tra magic bytes, không chỉ phần mở rộng)
- Quét virus (ClamAV - tùy chọn)
- Làm sạch tên tệp
- Lưu trữ bên ngoài thư mục webroot
- Tạo tên tệp ngẫu nhiên

---

## 4. Kiểm tra Dữ liệu Đầu vào (Input Validation)

### NFR-SEC-030: Chống XSS (Cross-Site Scripting)
**Biện pháp**:
- Làm sạch (Sanitize) tất cả đầu vào của người dùng
- Thoát (Escape) đầu ra trong HTML
- Header Chính sách Bảo mật Nội dung (CSP)
- Sử dụng React (tự động escaping)

---

### NFR-SEC-031: Chống SQL Injection
**Biện pháp**:
- Câu lệnh chuẩn bị sẵn (Prepared statements - JDBC)
- ORM (JPA/Hibernate)
- KHÔNG nối chuỗi SQL

---

### NFR-SEC-032: Chống CSRF (Cross-Site Request Forgery)
**Biện pháp**:
- CSRF tokens (Mặc định trong Spring Security)
- Thuộc tính cookie SameSite
- Xác minh Origin header

---

## 5. Bảo mật API

### NFR-SEC-040: Giới hạn Tốc độ API
**Giới hạn**:
- Public API: 100 yêu cầu/giờ mỗi IP
- Authenticated API: 1000 yêu cầu/giờ mỗi người dùng
- Admin API: Không giới hạn

**Phản hồi**: HTTP 429 Too Many Requests

---

### NFR-SEC-041: Kiểm tra Đầu vào API
**Kiểm tra**:
- Kích thước yêu cầu tối đa: 15MB (cho tải lên PDF)
- Xác thực lược đồ JSON (JSON schema)
- Danh sách trắng các trường cho phép
- Từ chối các tham số không xác định

---

## 6. Kiểm toán & Ghi nhật ký (Audit & Logging)

### NFR-SEC-050: Vết Kiểm toán (Audit Trail)
**Sự kiện ghi log**:
- Người dùng đăng nhập/đăng xuất
- Thử đăng nhập thất bại
- Thay đổi trạng thái bài báo
- Thay đổi vai trò người dùng
- Tải xuống tệp
- Thao tác quản trị

**Trường ghi log**:
- User ID, Địa chỉ IP
- Dấu thời gian (Timestamp)
- Loại hành động
- Resource ID
- Giá trị Trước/Sau (cho các thay đổi)

---

### NFR-SEC-051: Nhật ký Bảo mật
**Ghi log ra tệp riêng**:
- Lỗi xác thực
- Lỗi phân quyền
- Hoạt động đáng ngờ
- Lỗi 500 (lỗi máy chủ)

**Lưu trữ**: Tối thiểu 1 năm

---

## 7. Chính sách Mật khẩu (nếu có tài khoản cục bộ)

### NFR-SEC-060: Yêu cầu Mật khẩu
**Lưu ý**: Xác thực chính là LDAP/AD, nhưng nếu có tài khoản cục bộ:

- Độ dài tối thiểu: 8 ký tự
- Yêu cầu: Chữ hoa + Chữ thường + Số
- Ký tự đặc biệt: Khuyến nghị
- Không dùng mật khẩu phổ biến (kiểm tra với danh sách)
- Hết hạn: 90 ngày
- Lịch sử: Không dùng lại 5 mật khẩu gần nhất

---

## 8. Quản lý Phiên (Session Management)

### NFR-SEC-070: Bảo mật Phiên
**Yêu cầu**:
- Session ID: Ngẫu nhiên, không thể đoán trước
- Xoay vòng Session ID sau khi đăng nhập
- Vô hiệu hóa khi đăng xuất
- Hết hạn phiên: 8 giờ không hoạt động
- Phiên đồng thời: Cho phép (cùng người dùng, thiết bị khác)

---

## 9. Quản lý Lỗ hổng (Vulnerability Management)

### NFR-SEC-080: Quét Phụ thuộc (Dependency Scanning)
**Công cụ**: OWASP Dependency-Check, npm audit

**Tần suất**: Hàng tuần

**Hành động**: Vá các lỗ hổng nghiêm trọng trong vòng 7 ngày

---

### NFR-SEC-081: Kiểm thử Xâm nhập (Penetration Testing)
**Tần suất**: Hàng năm hoặc trước các bản phát hành lớn

**Phạm vi**: OWASP Top 10

---

## 10. Bảo mật Sao lưu & Phục hồi

### NFR-SEC-090: Mã hóa Sao lưu
**Yêu cầu**: Tất cả các bản sao lưu PHẢI được mã hóa

- Mã hóa: AES-256
- Khóa (Keys): Lưu trữ an toàn (không trong mã nguồn)
- Lưu trữ ngoại vi (Offsite): Khuyến nghị

---

### NFR-SEC-091: Truy cập Sao lưu
**Hạn chế**: CHỈ Quản trị viên cấp cao + Nhóm IT

---

## 11. Xử lý Lỗi (Error Handling)

### NFR-SEC-100: Thông báo Lỗi An toàn
**Yêu cầu**:
- KHÔNG lộ stack traces cho người dùng
- Thông báo lỗi chung chung
- Ghi log chi tiết chỉ cho máy chủ

**Ví dụ**:
- ✅ "Thông tin đăng nhập không hợp lệ"
- ❌ "Người dùng 'admin' không tìm thấy trong cơ sở dữ liệu 'ufpms'"

---

## 12. Bảo mật Tích hợp Bên thứ ba

### NFR-SEC-110: Quản lý Khóa API
**Cho các tích hợp**: ORCID, DOI Resolver, Email

**Yêu cầu**:
- Lưu trong biến môi trường (KHÔNG hard-code)
- Xoay vòng khóa hàng quý
- Chỉ sử dụng HTTPS
- Giám sát việc sử dụng

---

## 13. Danh sách Kiểm tra Tuân thủ

### NFR-SEC-120: Tuân thủ An ninh
**Các tiêu chuẩn cần tuân theo**:
- ✅ OWASP Top 10 (2021)
- ✅ Các nguyên tắc GDPR (nếu áp dụng)
- ✅ Nghị định 13/2023/NĐ-CP (Bảo vệ dữ liệu Việt Nam)

---

**Tài liệu liên quan**:
- [Constraints](../../01_System_Specification/constraints.md)
- [Khung pháp lý](../../00_Problem_Context/legal_framework.md)
