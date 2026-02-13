# Phân hệ 1: Quản lý Bài báo - Yêu Cầu Chức Năng

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Phân hệ**: Quản lý Bài báo Khoa học  
> 👥 **Người dùng**: Nhà nghiên cứu, Quản trị viên cấp cao

---

## 1. Tổng Quan Phân hệ

**Mục đích**: Quản lý bài báo khoa học (Thêm/Xóa/Sửa + metadata)

**Phạm vi**:
- ✅ Thêm/Xóa/Sửa bài báo
- ✅ Tải lên tệp PDF
- ✅ Quản lý metadata
- ✅ Liên kết đồng tác giả
- ❌ KHÔNG bao gồm: Quy trình phê duyệt (Phân hệ 2)

---

## 2. Yêu Cầu Chức Năng

### FR-PUB-001: Tạo Bài Báo Mới
**Độ ưu tiên**: 🔴 P0 - Phải Có

**Mô tả**:  
Giảng viên có thể tạo bài báo mới với các thông tin bắt buộc và tùy chọn.

**User Story**: US-RES-001

**Tiêu chí chấp nhận**:
```
GIVEN giảng viên đã đăng nhập
WHEN nhấn "Thêm bài báo mới"
THEN hiển thị form với các trường:
  - Bắt buộc: Tiêu đề, Tác giả, Năm xuất bản, Loại tạp chí
  - Tùy chọn: DOI, ISSN, Tóm tắt (Abstract), Từ khóa (Keywords), Tệp PDF
```

**Quy tắc nghiệp vụ**:
- Trạng thái mặc định: DRAFT (Nháp)
- Chỉ tác giả chính (chủ sở hữu) mới có quyền sửa/xóa

**Ghi chú kỹ thuật**:
- Validate form theo thời gian thực (Real-time)
- Tự động lưu mỗi 30s (nháp)

---

### FR-PUB-002: Tải lên Tệp PDF
**Độ ưu tiên**: 🔴 P0 - Phải Có

**Mô tả**:  
Giảng viên có thể upload file PDF bài báo toàn văn (full-text).

**Tiêu chí chấp nhận**:
```
GIVEN đang tạo/sửa bài báo
WHEN chọn file PDF (< 10MB)
THEN
  - Tải file lên máy chủ
  - Lưu đường dẫn vào cơ sở dữ liệu
  - Hiển thị hình thu nhỏ (thumbnail) xem trước
  - Cho phép tải xuống lại
```

**Quy tắc kiểm tra**:
- Loại tệp: Chỉ PDF (`.pdf`)
- Kích thước tệp: Tối đa 10MB
- Tên tệp: Làm sạch để tránh SQL injection

---

### FR-PUB-003: Tự động lấy Metadata từ DOI
**Độ ưu tiên**: 🟢 P2 - Có Thể Có (Giai đoạn 2)

**Mô tả**:  
Khi nhập DOI, tự động lấy metadata từ Bộ giải quyết DOI (DOI Resolver).

**Tiêu chí chấp nhận**:
```
GIVEN giảng viên nhập DOI hợp lệ (10.xxxx/xxxxx)
WHEN nhấn "Lấy thông tin từ DOI"
THEN
  - Gọi API CrossRef
  - Tự động điền: Tiêu đề, Tác giả, Tạp chí, Năm, ISSN
  - Cho phép chỉnh sửa thủ công
```

**Sự phụ thuộc**:
- API CrossRef hoặc API DOI.org

---

### FR-PUB-004: Sửa Bài Báo
**Độ ưu tiên**: 🔴 P0 - Phải Có

**Mô tả**:  
Giảng viên có thể sửa bài báo của mình.

**Tiêu chí chấp nhận**:
```
GIVEN bài báo ở trạng thái DRAFT hoặc REVISION_REQUIRED
AND người dùng là chủ sở hữu
WHEN sửa thông tin và Lưu
THEN
  - Cập nhật cơ sở dữ liệu
  - Lưu nhật ký kiểm toán (ai sửa, khi nào)
  - Hiển thị thông báo "Đã lưu"
```

**Quy tắc nghiệp vụ**:
- CHỈ sửa được khi: DRAFT hoặc REVISION_REQUIRED
- KHÔNG sửa được khi: SUBMITTED, REVIEWING, PUBLISHED

---

### FR-PUB-005: Xóa Bài Báo
**Độ ưu tiên**: 🔴 P0 - Phải Có

**Mô tả**:  
Giảng viên có thể xóa bài báo nháp của mình.

**Tiêu chí chấp nhận**:
```
GIVEN bài báo ở trạng thái DRAFT
AND người dùng là chủ sở hữu
WHEN nhấn "Xóa" và xác nhận
THEN
  - Xóa mềm (đặt dấu thời gian deleted_at)
  - Xóa file PDF khỏi lưu trữ
  - Chuyển hướng về danh sách
```

**Quy tắc nghiệp vụ**:
- CHỈ xóa được khi: DRAFT
- KHÔNG xóa được: Đã nộp hoặc đã duyệt

---

### FR-PUB-006: Xem Danh Sách Bài Báo Của Mình
**Độ ưu tiên**: 🔴 P0 - Phải Có

**Mô tả**:  
Giảng viên xem danh sách bài báo của mình, phân loại theo trạng thái.

**Tiêu chí chấp nhận**:
```
GIVEN giảng viên đã đăng nhập
WHEN vào "Bài báo của tôi"
THEN hiển thị danh sách với:
  - Bộ lọc: Tất cả / Nháp / Đã nộp / Đã duyệt / Bị từ chối
  - Sắp xếp: Mới nhất trước
  - Thông tin: Tiêu đề, Trạng thái, Ngày cập nhật, Hành động
```

---

### FR-PUB-007: Thêm Đồng Tác Giả (Co-authors)
**Độ ưu tiên**: 🟡 P1 - Nên Có

**Mô tả**:  
Liên kết bài báo với đồng tác giả (giảng viên khác trong trường).

**Tiêu chí chấp nhận**:
```
GIVEN đang tạo/sửa bài báo
WHEN nhập tên giảng viên
THEN
  - Tự động hoàn thành từ danh sách GV trong hệ thống
  - Thêm vào danh sách đồng tác giả
  - Có thể xóa khỏi danh sách
```

**Quy tắc nghiệp vụ**:
- Tác giả chính (chủ sở hữu) không thể bị xóa
- Đồng tác giả không có quyền sửa/xóa bài báo

---

### FR-PUB-008: Gắn Thẻ/Từ khóa
**Độ ưu tiên**: 🟡 P1 - Nên Có

**Mô tả**:  
Gắn từ khóa cho bài báo để hỗ trợ tìm kiếm và phân loại.

**Tiêu chí chấp nhận**:
```
GIVEN đang tạo/sửa bài báo
WHEN nhập từ khóa (phân tách bằng dấu phẩy)
THEN
  - Lưu dưới dạng mảng
  - Hiển thị dạng thẻ
  - Cho phép xóa từng thẻ
```

---

### FR-PUB-009: Phân Loại Theo Nhóm tứ phân vị (Q1/Q2/Q3/Q4)
**Độ ưu tiên**: 🟡 P1 - Nên Có

**Mô tả**:  
Tự động phân loại tạp chí theo Quartile (Scopus).

**Tiêu chí chấp nhận**:
```
GIVEN nhập ISSN của tạp chí
WHEN lưu bài báo
THEN
  - Tra cứu xếp hạng Scopus (nếu có API)
  - Gắn nhãn Q1/Q2/Q3/Q4
  - Hiển thị huy hiệu (badge)
```

**Sự phụ thuộc**:
- API Scopus (hoặc danh sách cứng từ Excel)

---

### FR-PUB-010: Xem Chi Tiết Bài Báo
**Độ ưu tiên**: 🔴 P0 - Phải Có

**Mô tả**:  
Xem đầy đủ thông tin bài báo.

**Tiêu chí chấp nhận**:
```
GIVEN có quyền xem bài báo (chủ sở hữu hoặc admin hoặc người duyệt)
WHEN nhấn "Xem Chi tiết"
THEN hiển thị:
  - Tất cả metadata
  - Trạng thái hiện tại
  - Lịch sử xét duyệt (nếu có)
  - Tệp PDF (nếu đã tải lên)
  - Liên kết DOI (nếu có)
```

---

### FR-PUB-011: Tải xuống Tệp PDF
**Độ ưu tiên**: 🔴 P0 - Phải Có

**Mô tả**:  
Tải xuống file PDF đã upload.

**Tiêu chí chấp nhận**:
```
GIVEN bài báo có file PDF
AND người dùng có quyền xem (chủ sở hữu / admin / người duyệt / hoặc ĐÃ XUẤT BẢN)
WHEN nhấn "Tải xuống PDF"
THEN
  - Tải file về máy
  - Ghi nhật ký kiểm toán (ai tải, khi nào)
```

**Bảo mật**:
- CHỈ cho tải nếu có quyền
- PDF không có link công khai (cần xác thực)

---

### FR-PUB-012: Kiểm tra Định dạng DOI
**Độ ưu tiên**: 🟡 P1 - Nên Có

**Mô tả**:  
Kiểm tra format DOI hợp lệ.

**Quy tắc nghiệp vụ**:
```
Định dạng DOI: 10.xxxx/xxxxx
Regex: ^10\.\d{4,9}/[-._;()/:A-Z0-9]+$
```

**Tiêu chí chấp nhận**:
```
GIVEN giảng viên nhập DOI
WHEN rời khỏi trường nhập (blur)
THEN
  - Kiểm tra định dạng
  - Hiển thị lỗi nếu sai
  - Liên kết đến https://doi.org/[DOI] nếu đúng
```

---

### FR-PUB-013: Kiểm tra Định dạng ISSN
**Độ ưu tiên**: 🟡 P1 - Nên Có

**Mô tả**:  
Kiểm tra format ISSN hợp lệ.

**Quy tắc nghiệp vụ**:
```
Định dạng ISSN: xxxx-xxxx
Regex: ^\d{4}-\d{3}[0-9X]$
```

---

### FR-PUB-014: Phát hiện Trùng lặp (Đồng tác giả)
**Độ ưu tiên**: 🟡 P1 - Nên Có

**Mô tả**:  
Cảnh báo khi có nhiều giảng viên khai báo cùng 1 bài.

**Tiêu chí chấp nhận**:
```
GIVEN bài báo có DOI
WHEN lưu bài báo
THEN
  - Kiểm tra DOI đã tồn tại chưa
  - Nếu có: Hiển thị cảnh báo "Bài này đã được [Tên GV] khai báo"
  - Gợi ý: "Thêm làm đồng tác giả?"
```

---

### FR-PUB-015: Nhập từ ORCID
**Độ ưu tiên**: 🟢 P2 - Có Thể Có (Giai đoạn 2)

**Mô tả**:  
Import danh sách bài báo từ ORCID tự động.

**Tiêu chí chấp nhận**:
```
GIVEN giảng viên có ORCID
WHEN nhấn "Nhập từ ORCID"
THEN
  - Gọi API ORCID
  - Hiển thị danh sách bài báo
  - Cho phép chọn bài nào muốn thêm
  - Tự động điền metadata
```

---

### FR-PUB-016: Dashboard Giờ Làm cho Giảng Viên
**Độ ưu tiên**: 🟡 P1 - Nên Có

**Mô tả**:  
Giảng viên có thể xem tổng số giờ làm trong năm và chi tiết giờ làm từ từng bài báo đã được phê duyệt.

**User Story**: US-RES-016

**Tiêu chí chấp nhận**:
```
GIVEN giảng viên đã có bài báo được phê duyệt (PUBLISHED)
WHEN vào trang "Dashboard Giờ Làm"
THEN hiển thị:
  - Tổng giờ làm trong năm hiện tại (ví dụ: "Năm 2026: 120 giờ")
  - Danh sách các bài báo đã được duyệt
  - Mỗi bài báo hiển thị:
    * Tiêu đề bài báo
    * Loại tạp chí (Q1/Q2/Q3/Q4/Conference)
    * Số giờ được ghi nhận
    * Ngày phê duyệt
  - Nút "Xuất báo cáo Excel"
```

**Quy tắc nghiệp vụ**:
- Chỉ tính các bài báo có trạng thái PUBLISHED
- Số giờ được nhập thủ công bởi University Reviewer khi phê duyệt
- Dashboard cập nhật ngay khi bài báo được phê duyệt

**Ghi chú kỹ thuật**:
- Lọc theo năm (mặc định: năm hiện tại)
- Sắp xếp theo ngày phê duyệt (mới nhất trước)
- Cache tổng giờ để tối ưu performance

---

## 3. Mô hình Dữ liệu (Thực thể Bài báo)

```typescript
interface Publication {
  // Khóa chính
  id: UUID;
  
  // Metadata
  title: string; // Bắt buộc
  abstract?: string; // Tùy chọn
  authors: Author[]; // Bắt buộc, ít nhất 1
  correspondingAuthor: User; // Chủ sở hữu
  
  // Thông tin Tạp chí
  journalName: string; // Bắt buộc
  journalISSN?: string;
  journalQuartile?: 'Q1' | 'Q2' | 'Q3' | 'Q4';
  impactFactor?: number;
  
  // Thông tin Xuất bản
  publicationYear: number; // Bắt buộc
  publicationDate?: Date;
  volume?: string;
  issue?: string;
  pages?: string;
  doi?: string;
  url?: string;
  
  // Phân loại
  publicationType: 'journal' | 'conference';
  keywords?: string[];
  researchField?: string;
  
  // Tệp tin
  pdfPath?: string;
  pdfSize?: number;
  
  // Trạng thái
  status: PublicationStatus;
  
  // Kiểm toán
  createdAt: Date;
  updatedAt: Date;
  createdBy: UUID;
  updatedBy: UUID;
  deletedAt?: Date; // Xóa mềm
}

enum PublicationStatus {
  DRAFT,
  SUBMITTED,
  FACULTY_REVIEWING,
  REVISION_REQUIRED,
  FACULTY_APPROVED,
  FACULTY_REJECTED,
  UNIVERSITY_REVIEWING,
  PUBLISHED,
  UNIVERSITY_REJECTED
}
```

---

## 4. API Endpoints (Mẫu)

| Phương thức | Endpoint | Mô tả | Xác thực |
|--------|----------|-------------|------|
| POST | `/api/publications` | Tạo bài báo mới | Researcher |
| GET | `/api/publications` | Danh sách của mình | Researcher |
| GET | `/api/publications/:id` | Chi tiết bài báo | Owner/Admin/Reviewer |
| PUT | `/api/publications/:id` | Cập nhật bài báo | Owner (if DRAFT) |
| DELETE | `/api/publications/:id` | Xóa bài báo | Owner (if DRAFT) |
| POST | `/api/publications/:id/upload-pdf` | Upload PDF | Owner |
| GET | `/api/publications/:id/download-pdf` | Download PDF | Authorized |

---

## 5. Truy xuất nguồn gốc

| ID Yêu cầu | Nhu cầu Người dùng | User Story | Test Case |
|-------|-----------|------------|-----------|
| FR-PUB-001 | Nhập bài báo nhanh | US-RES-001 | TC-PUB-001 |
| FR-PUB-002 | Upload PDF | US-RES-002 | TC-PUB-002 |
| FR-PUB-004 | Sửa bài báo | US-RES-003 | TC-PUB-004 |
| FR-PUB-005 | Xóa bài báo | US-RES-004 | TC-PUB-005 |

---

**Tài liệu liên quan**:
- [Phân hệ 2: Quy trình Phê duyệt](./module_approval_workflow.md)
- [Nhu cầu Người dùng - Nhà nghiên cứu](../../02_System_Clarification/User_Analysis/user_needs.md#1-researcher)
- [Quy tắc Nghiệp vụ](./business_rules.md)
