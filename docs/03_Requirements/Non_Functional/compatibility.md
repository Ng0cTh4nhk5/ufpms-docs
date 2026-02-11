# Yêu Cầu Tương Thích - Compatibility Requirements

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Danh mục**: Yêu cầu Phi Chức Năng

---

## 1. Tương Thích Trình Duyệt (Browser Compatibility)

### NFR-COM-001: Trình Duyệt Được Hỗ Trợ
**Máy tính (Desktop)**:
- ✅ Google Chrome 90+ (Chính)
- ✅ Mozilla Firefox 88+
- ✅ Microsoft Edge 90+
- ✅ Safari 14+ (macOS)

**Di động (Mobile)**:
- ✅ Chrome Mobile (Android)
- ✅ Safari Mobile (iOS 13+)

**KHÔNG hỗ trợ**:
- ❌ Internet Explorer (bất kỳ phiên bản nào)

**Kiểm thử**: BrowserStack hoặc kiểm thử thủ công

---

## 2. Tương Thích Hệ Điều Hành (Operating System Compatibility)

### NFR-COM-010: Hệ Điều Hành Máy Chủ (Server OS)
**Được hỗ trợ**:
- ✅ Windows Server 2019+
- ✅ Linux (Ubuntu 20.04+, CentOS 8+)

**Ưu tiên**: Linux (hiệu năng tốt hơn)

---

### NFR-COM-011: Hệ Điều Hành Máy Khách (Client OS)
**Người dùng cuối** (bất kỳ hệ điều hành hiện đại nào):
- Windows 10/11
- macOS 10.15+
- Linux (Ubuntu, Fedora...)
- iOS, Android

---

## 3. Tương Thích Thiết Bị (Device Compatibility)

### NFR-COM-020: Kích thước Màn hình
**Máy tính**:
- 1920x1080 (Full HD)
- 1366x768 (Laptop phổ biến)
- 2560x1440 (2K)

**Máy tính bảng**:
- 768x1024 (iPad)
- 800x1280 (Máy tính bảng Android)

**Di động**:
- 375x667 (iPhone 8)
- 414x896 (iPhone 11)
- 360x640 (Android)

**Cách tiếp cận**: Thiết kế đáp ứng (Responsive design - mobile-first)

---

## 4. Tương Thích Cơ Sở Dữ Liệu (Database Compatibility)

### NFR-COM-030: Phiên bản MySQL
**Được hỗ trợ**:
- MySQL 8.0+ (Ưu tiên)
- MySQL 5.7 (Hỗ trợ cũ)
- MariaDB 10.5+ (Tương thích)

**KHÔNG hỗ trợ**:
- MySQL < 5.7

---

## 5. Tương Thích Tích Hợp (Integration Compatibility)

### NFR-COM-040: Phiên bản LDAP/AD
**Được hỗ trợ**:
- Active Directory (Windows Server 2016+)
- OpenLDAP 2.4+

**Giao thức**: LDAPv3

---

### NFR-COM-041: Máy chủ Email
**Tương thích SMTP**:
- Microsoft Exchange Server
- Postfix, Sendmail
- Gmail SMTP
- Bất kỳ máy chủ nào tuân thủ SMTP

---

### NFR-COM-042: Tích hợp API
**API bên thứ ba**:
- ORCID API (REST)
- CrossRef API (REST)
- DOI.org resolver (HTTP)

**Phiên bản**: Client thích ứng với thay đổi API

---

## 6. Tương Thích Định Dạng Tệp (File Format Compatibility)

### NFR-COM-050: Tải lên Tệp tin
**Chấp nhận**:
- ✅ CHỈ PDF (`.pdf`)

**Phiên bản PDF**: 1.4 trở lên

---

### NFR-COM-051: Định dạng Xuất
**Báo cáo**:
- Excel (.xlsx) - Excel 2007+
- PDF (PDF/A để lưu trữ lâu dài)
- CSV (UTF-8)

**Trích dẫn**:
- BibTeX
- RIS
- JSON

---

## 7. Tương Thích Mạng (Network Compatibility)

### NFR-COM-060: Giao thức
**Được hỗ trợ**:
- HTTPS (TLS 1.2+)
- WebSocket (cho thời gian thực - tùy chọn)
- SMTP (email)
- LDAP (xác thực)

---

### NFR-COM-061: Yêu cầu Tường lửa (Firewall)
**Cổng vào (Inbound)**:
- 443 (HTTPS)
- 80 (HTTP chuyển hướng sang HTTPS)

**Cổng ra (Outbound)**:
- 443 (HTTPS cho API)
- 25/587 (SMTP)
- 389/636 (LDAP/LDAPS)

---

## 8. Mã hóa & Bản địa hóa (Encoding & Localization)

### NFR-COM-070: Mã hóa Ký tự
**Tiêu chuẩn**: UTF-8 (tất cả các lớp)

**Hỗ trợ**:
- Tiếng Việt (có dấu)
- Tiếng Anh
- Ký tự đặc biệt (trong trích dẫn)

---

### NFR-COM-071: Định dạng Ngày/Giờ
**Hiển thị**: dd/MM/yyyy HH:mm (Việt Nam)

**Lưu trữ**: ISO 8601 (yyyy-MM-dd'T'HH:mm:ss'Z')

**Múi giờ**: UTC trong DB, chuyển đổi sang ICT (+7) khi hiển thị

---

## 9. Tương Thích Ngược (Backward Compatibility)

### NFR-COM-080: Phiên bản API
**Bảo đảm**: API v1 hỗ trợ ít nhất 1 năm sau khi ra v2

**Thông báo ngừng hỗ trợ**: Trước 6 tháng

---

### NFR-COM-081: Di chuyển Cơ sở dữ liệu (Database Migrations)
**Yêu cầu**: Di chuyển không thời gian chết (Zero-downtime)

**Chiến lược**:
- Thay đổi bổ sung (thêm cột, không xóa)
- Thay đổi lược đồ tương thích ngược

---

## 10. Tương Thích Thư Viện Bên Thứ Ba

### NFR-COM-090: Phiên bản Phụ thuộc
**Backend** (Java):
- Spring Boot 3.x
- JDK 17+

**Frontend** (JavaScript):
- React 18+
- Node.js 18+ (để build)

**Chính sách nâng cấp**: Theo các bản phát hành LTS (Hỗ trợ dài hạn)

---

**Tài liệu liên quan**:
- [Technology Stack](../../01_System_Specification/technology_stack.md)
- [Constraints](../../01_System_Specification/constraints.md)
