# Quy Tắc Nghiệp Vụ - UFPMS

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục đích**: Định nghĩa quy tắc nghiệp vụ cốt lõi

---

## 1. Quy Tắc Chuyển Đổi Trạng Thái (State Transition Rules)

### BR-001: Quyền Chuyển Trạng Thái

| Từ trạng thái | Đến trạng thái | Ai có thể | Điều kiện |
|-----------|----------|---------|-----------|
| DRAFT (Nháp) | SUBMITTED (Đã nộp) | Nhà nghiên cứu (chủ sở hữu) | Đủ các trường bắt buộc |
| SUBMITTED | FACULTY_REVIEWING (Khoa đang duyệt) | Người duyệt cấp Khoa | Tự động hoặc thủ công |
| FACULTY_REVIEWING | FACULTY_APPROVED (Khoa đã duyệt) | Người duyệt cấp Khoa | - |
| FACULTY_REVIEWING | REVISION_REQUIRED (Yêu cầu chỉnh sửa) | Người duyệt cấp Khoa | Phải có bình luận |
| FACULTY_REVIEWING | FACULTY_REJECTED (Khoa từ chối) | Người duyệt cấp Khoa | Phải có lý do |
| REVISION_REQUIRED | DRAFT | Nhà nghiên cứu (chủ sở hữu) | - |
| FACULTY_APPROVED | UNIVERSITY_REVIEWING (Trường đang duyệt) | Người duyệt cấp Trường | Tự động hoặc thủ công |
| UNIVERSITY_REVIEWING | PUBLISHED (Đã xuất bản) | Người duyệt cấp Trường | - |
| UNIVERSITY_REVIEWING | UNIVERSITY_REJECTED (Trường từ chối) | Người duyệt cấp Trường | Phải có lý do |

---

## 2. Quy Tắc Hiển Thị (Visibility Rules)

### BR-010: Quy Tắc Hiển Thị Công Trình

```
DRAFT (Nháp):
  - Hiển thị cho: Chủ sở hữu + Quản trị viên cấp cao
  - KHÔNG hiển thị: Người duyệt, Công chúng

SUBMITTED, FACULTY_REVIEWING, REVISION_REQUIRED, FACULTY_REJECTED:
  - Hiển thị cho: Chủ sở hữu + Người duyệt cấp Khoa (cùng khoa) + Quản trị viên cấp cao
  - KHÔNG hiển thị: Công chúng

FACULTY_APPROVED, UNIVERSITY_REVIEWING, UNIVERSITY_REJECTED:
  - Hiển thị cho: Chủ sở hữu + Người duyệt cấp Khoa + Người duyệt cấp Trường + Quản trị viên cấp cao
  - KHÔNG hiển thị: Công chúng

PUBLISHED (Đã xuất bản):
  - Hiển thị cho: MỌI NGƯỜI (Công chúng)
  - Xuất hiện trong: Tìm kiếm, Hồ sơ, Báo cáo
```

---

## 3. Quy Tắc Kiểm Tra Dữ Liệu (Data Validation Rules)

### BR-020: Định dạng DOI
```
Mẫu: 10.xxxx/xxxxx
Regex: ^10\.\d{4,9}/[-._;()/:A-Z0-9]+$
Ví dụ: 10.1000/xyz123
```

### BR-021: Định dạng ISSN
```
Mẫu: xxxx-xxxx
Regex: ^\d{4}-\d{3}[0-9X]$
Ví dụ: 1234-567X
```

### BR-022: Định dạng ORCID
```
Mẫu: 0000-0002-xxxx-xxxx
Regex: ^\d{4}-\d{4}-\d{4}-\d{3}[0-9X]$
Ví dụ: 0000-0002-1825-0097
```

### BR-023: Quy Tắc Tải Tệp
- Loại tệp: Chỉ PDF (`.pdf`)
- Kích thước tối đa: 10MB
- Làm sạch tên tệp (loại bỏ ký tự đặc biệt)

---

## 4. Quy Tắc Đồng Tác Giả (Co-author Rules)

### BR-030: Quyền Sở Hữu và Quyền Hạn

```
Tác giả liên hệ (Chủ sở hữu):
  - Có thể: Sửa, Xóa (nếu là NHÁP), Nộp, Rút lại
  - Là người đầu tiên tạo bài báo

Đồng tác giả:
  - Có thể: Chỉ xem
  - KHÔNG thể: Sửa, Xóa, Nộp
  - Xuất hiện trong hồ sơ của họ (khi ĐÃ XUẤT BẢN)
```

### BR-031: Phát Hiện Trùng Lặp
```
NẾU bài báo có DOI
VÀ DOI đã tồn tại trong hệ thống
THÌ
  - Hiển thị cảnh báo: "Bài này đã được [Tên Nhà Nghiên Cứu] khai báo"
  - Gợi ý: "Thêm làm đồng tác giả?"
  - Cho phép tiếp tục (có thể cùng DOI nhưng khác chủ sở hữu)
```

---

## 5. Quy Tắc Phân Công Duyệt (Review Assignment Rules)

### BR-040: Phân Công Duyệt Cấp Khoa

```
Người duyệt cấp Khoa CHỈ xem được:
  - Các bài báo từ Khoa của mình
  - Trạng thái: SUBMITTED (Đã nộp) hoặc FACULTY_REVIEWING (Khoa đang duyệt)
```

### BR-041: Phân Công Duyệt Cấp Trường

```
Người duyệt cấp Trường xem được:
  - Các bài báo từ TẤT CẢ các khoa
  - Trạng thái: FACULTY_APPROVED (Khoa đã duyệt) hoặc UNIVERSITY_REVIEWING (Trường đang duyệt)
```

---

## 6. Quy Tắc Vết Kiểm Toán (Audit Trail Rules)

### BR-050: Yêu Cầu Ghi Nhật Ký

**Mọi chuyển đổi trạng thái phải được ghi lại**:
- ID bài báo
- Từ Trạng thái → Đến Trạng thái
- ID Người duyệt, Tên, Vai trò
- Dấu thời gian (Timestamp)
- Bình luận/Lý do (nếu có)

**Không được xóa nhật ký kiểm toán** (bất biến)

---

## 7. Quy Tắc Thông Báo Email (Email Notification Rules)

### BR-060: Sự Kiện Kích Hoạt

| Sự kiện | Người nhận | Mẫu |
|-------|-----------|----------|
| Bài báo đã nộp | Người duyệt cấp Khoa | "Bài báo mới chờ duyệt" |
| Khoa đã duyệt | Nhà nghiên cứu + Người duyệt cấp Trường | "Được khoa phê duyệt" |
| Yêu cầu chỉnh sửa | Nhà nghiên cứu | "Cần chỉnh sửa" |
| Khoa từ chối | Nhà nghiên cứu | "Bị khoa từ chối" |
| Trường đã duyệt (Xuất bản) | Nhà nghiên cứu | "Chúc mừng! Đã xuất bản" |
| Trường từ chối | Nhà nghiên cứu + Người duyệt cấp Khoa | "Bị trường từ chối" |

---

## 8. Quy Tắc Hiệu Năng (Performance Rules)

### BR-070: Mục Tiêu SLA

```
Thời gian duyệt mục tiêu:
  - Duyệt cấp Khoa: 3-7 ngày
  - Duyệt cấp Trường: 3-7 ngày
  - Tổng cộng: 6-14 ngày (từ khi nộp đến khi xuất bản)

Làm nổi bật bài báo:
  - > 7 ngày trong FACULTY_REVIEWING: Vàng
  - > 14 ngày trong FACULTY_REVIEWING: Đỏ
```

---

## 9. Quy Tắc Lưu Giữ Dữ Liệu (Data Retention Rules)

### BR-080: Xóa Mềm (Soft Delete)
```
Khi xóa bài báo (chỉ NHÁP):
  - Đặt dấu thời gian deleted_at
  - KHÔNG xóa vật lý khỏi cơ sở dữ liệu
  - Tệp PDF: Chuyển vào thùng rác (xóa sau 30 ngày)
```

---

## 10. Quy Tắc Bảo Mật (Security Rules)

### BR-090: Xác Thực (Authentication)
```
Người dùng nội bộ (Nhà nghiên cứu, Người duyệt, Quản trị viên):
  - PHẢI đăng nhập qua LDAP/AD
  - Hết phiên (timeout): 8 giờ
  - Hết hạn token JWT: 24 giờ

Người dùng công cộng (Người xem):
  - KHÔNG cần đăng nhập
  - CHỈ truy cập được nội dung ĐÃ XUẤT BẢN
```

### BR-091: Ủy Quyền (Authorization)
```
RBAC (Kiểm soát truy cập dựa trên vai trò):
  - Kiểm tra vai trò trước mọi thao tác
  - Điểm cuối riêng tư (Private endpoints): Yêu cầu xác thực
  - Điểm cuối công khai (Public endpoints): Không yêu cầu xác thực

Tải xuống PDF:
  - DRAFT/REVIEWING: CHỈ chủ sở hữu + người duyệt + quản trị viên
  - PUBLISHED: Mọi người (nếu được chủ sở hữu cho phép)
```

---

**Tài liệu liên quan**:
- [Quy trình Tương lai](../../02_System_Clarification/Business_Context/to_be_process.md)
- [Phân hệ 2: Quy trình Phê duyệt](./module_approval_workflow.md)
