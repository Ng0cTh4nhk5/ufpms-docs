# Module 1: Quản Lý Bài Báo - Use Cases Cấp Trung

> **Module**: 1 - Quản Lý Bài Báo  
> **Use Case Cấp Cao**: [UC-HL-001](../High_Level/uc_hl_01_manage_publications.md)

---

## UC-M1-001: Tạo Bài Báo (Create Publication)

**ID**: UC-M1-001  
**Độ Ưu Tiên**: 🔴 P0  
**Tác Nhân**: Researcher  
**User Stories Liên Quan**: US-RES-001  
**Yêu Cầu Chức Năng Liên Quan**: FR-PUB-001

### Mục Tiêu
Researcher tạo mới một mục bài báo với các siêu dữ liệu (metadata) bắt buộc.

### Điều Kiện Tiên Quyết
- Researcher đã đăng nhập
- Cơ sở dữ liệu có thể truy cập được

### Luồng Chính
1. Researcher nhấn "Thêm Bài Báo Mới"
2. Hệ thống hiển thị biểu mẫu với các trường:
   - Bắt buộc: Tiêu đề, Tác giả, Năm, Loại Tạp chí/Hội nghị
   - Tùy chọn: DOI, ISSN, Tóm tắt, Từ khóa, File PDF
3. Researcher nhập thông tin
4. Hệ thống xác thực đầu vào (thời gian thực)
5. Researcher nhấn "Lưu"
6. Hệ thống đặt trạng thái = DRAFT (Nháp)
7. Hệ thống lưu vào cơ sở dữ liệu
8. Hệ thống hiển thị "Tạo bài báo thành công"

### Điều Kiện Hậu Quyết
**Thành Công**: Bài báo tồn tại với trạng thái DRAFT, Researcher là chủ sở hữu  
**Thất Bại**: Không có dữ liệu nào được lưu, hiển thị thông báo lỗi

### Quy Tắc Nghiệp Vụ
- BR-PUB-001: Trạng thái mặc định là DRAFT
- BR-PUB-004: Xác thực năm: 1900 ≤ năm ≤ năm hiện tại + 1
- BR-PUB-005: Created_by = người dùng hiện tại

---

## UC-M1-002: Sửa Bài Báo (Edit Publication)

**ID**: UC-M1-002  
**Độ Ưu Tiên**: 🔴 P0  
**Tác Nhân**: Researcher  
**User Stories Liên Quan**: US-RES-003  
**Yêu Cầu Chức Năng Liên Quan**: FR-PUB-004

### Mục Tiêu
Researcher chỉnh sửa một bài báo hiện có.

### Điều Kiện Tiên Quyết
- Trạng thái bài báo = DRAFT hoặc REVISION_REQUIRED
- Người dùng là chủ sở hữu (tác giả liên hệ)

### Luồng Chính
1. Researcher chọn bài báo từ danh sách
2. Researcher nhấn "Sửa"
3. Hệ thống hiển thị biểu mẫu đã điền sẵn dữ liệu hiện tại
4. Researcher sửa đổi các trường
5. Researcher nhấn "Lưu"
6. Hệ thống xác thực các thay đổi
7. Hệ thống cập nhật cơ sở dữ liệu
8. Hệ thống ghi nhật ký kiểm toán (ai, khi nào, thay đổi gì)
9. Hệ thống hiển thị "Đã lưu thay đổi"

### Điều Kiện Hậu Quyết
**Thành Công**: Bài báo được cập nhật, nhật ký kiểm toán được tạo  
**Thất Bại**: Không có thay đổi, hiển thị lỗi

### Quy Tắc Nghiệp Vụ
- BR-PUB-002: Chỉ sửa được nếu trạng thái là DRAFT hoặc REVISION_REQUIRED
- BR-PUB-001: Chỉ chủ sở hữu mới được sửa

---

## UC-M1-003: Xóa Bài Báo (Delete Publication)

**ID**: UC-M1-003  
**Độ Ưu Tiên**: 🔴 P0  
**Tác Nhân**: Researcher  
**User Stories Liên Quan**: US-RES-004  
**Yêu Cầu Chức Năng Liên Quan**: FR-PUB-005

### Mục Tiêu
Researcher xóa một bài báo nháp.

### Điều Kiện Tiên Quyết
- Trạng thái bài báo = DRAFT
- Người dùng là chủ sở hữu

### Luồng Chính
1. Researcher chọn bài báo
2. Researcher nhấn "Xóa"
3. Hệ thống hiển thị xác nhận: "Bạn có chắc chắn không?"
4. Researcher xác nhận
5. Hệ thống xóa mềm (đặt timestamp deleted_at)
6. Hệ thống xóa file PDF khỏi kho lưu trữ
7. Hệ thống chuyển hướng về danh sách bài báo

### Điều Kiện Hậu Quyết
**Thành Công**: Bài báo bị xóa mềm, PDF bị xóa  
**Thất Bại**: Không có thay đổi

### Quy Tắc Nghiệp Vụ
- BR-PUB-002: Chỉ có thể xóa nếu trạng thái = DRAFT
- BR-PUB-003: File PDF phải được xóa khỏi kho lưu trữ

---

## UC-M1-004: Xem Danh Sách Bài Báo (View Publication List)

**ID**: UC-M1-004  
**Độ Ưu Tiên**: 🔴 P0  
**Tác Nhân**: Researcher  
**User Stories Liên Quan**: US-RES-005  
**Yêu Cầu Chức Năng Liên Quan**: FR-PUB-006

### Mục Tiêu
Researcher xem tất cả các bài báo của mình được lọc theo trạng thái.

### Điều Kiện Tiên Quyết
- Researcher đã đăng nhập

### Luồng Chính
1. Researcher điều hướng đến "Bài Báo Của Tôi"
2. Hệ thống truy vấn các bài báo mà:
   - created_by = người dùng hiện tại HOẶC người dùng là đồng tác giả
   - deleted_at LÀ NULL
3. Hệ thống hiển thị danh sách với các cột:
   - Tiêu đề, Trạng thái, Ngày cập nhật, Hành động
4. Researcher có thể lọc theo trạng thái: Tất cả/Nháp/Đã nộp/Đã duyệt/Bị từ chối
5. Hệ thống cho phép sắp xếp: Mới nhất trước (mặc định)

### Điều Kiện Hậu Quyết
**Thành Công**: Danh sách được hiển thị  

### Quy Tắc Nghiệp Vụ
- Hiển thị các bài báo mà người dùng là chủ sở hữu HOẶC đồng tác giả
- Sắp xếp mặc định: Cập nhật gần nhất trước

---

## UC-M1-005: Xem Chi Tiết Bài Báo (View Publication Details)

**ID**: UC-M1-005  
**Độ Ưu Tiên**: 🔴 P0  
**Tác Nhân**: Researcher, Faculty Reviewer, University Reviewer, Admin  
**User Stories Liên Quan**: US-RES-008  
**Yêu Cầu Chức Năng Liên Quan**: FR-PUB-010

### Mục Tiêu
Xem chi tiết đầy đủ của một bài báo.

### Điều Kiện Tiên Quyết
- Người dùng có quyền (chủ sở hữu/người duyệt/admin HOẶC bài báo là PUBLISHED)

### Luồng Chính
1. Người dùng nhấn "Xem Chi Tiết" trên bài báo
2. Hệ thống kiểm tra quyền hạn
3. Hệ thống hiển thị:
   - Tất cả metadata
   - Trạng thái hiện tại
   - Lịch sử xét duyệt (nếu có)
   - Link tải PDF (nếu đã upload)
   - Link DOI (nếu có)

### Điều Kiện Hậu Quyết
**Thành Công**: Chi tiết được hiển thị

### Quy Tắc Nghiệp Vụ
- Công khai (Public) CHỈ xem được nếu trạng thái = PUBLISHED
- Người dùng nội bộ xem được dựa trên vai trò

---

## UC-M1-006: Tải Lên File PDF (Upload PDF File)

**ID**: UC-M1-006  
**Độ Ưu Tiên**: 🔴 P0  
**Tác Nhân**: Researcher  
**User Stories Liên Quan**: US-RES-002  
**Yêu Cầu Chức Năng Liên Quan**: FR-PUB-002

### Mục Tiêu
Tải lên file PDF cho một bài báo.

### Điều Kiện Tiên Quyết
- Người dùng là chủ sở hữu
- Bài báo tồn tại

### Luồng Chính
1. Researcher chọn bài báo
2. Researcher nhấn "Upload PDF"
3. Researcher chọn file PDF từ máy tính (< 10MB)
4. Hệ thống xác thực:
   - Loại file = PDF
   - Kích thước file < 10MB
5. Hệ thống tải file lên kho lưu trữ
6. Hệ thống lưu đường dẫn file vào cơ sở dữ liệu
7. Hệ thống hiển thị ảnh thumbnail xem trước
8. Hệ thống hiển thị "Upload thành công"

### Điều Kiện Hậu Quyết
**Thành Công**: PDF được lưu trữ, đường dẫn được lưu  
**Thất Bại**: Không có file nào được lưu

### Quy Tắc Nghiệp Vụ
- BR-PUB-003: Chỉ PDF, tối đa 10MB
- Tên file được làm sạch để ngăn chặn các vấn đề bảo mật

---

## UC-M1-007: Tải Xuống File PDF (Download PDF File)

**ID**: UC-M1-007  
**Độ Ưu Tiên**: 🔴 P0  
**Tác Nhân**: Researcher, Reviewer, Admin, Public (nếu đã xuất bản)  
**User Stories Liên Quan**: US-RES-009  
**Yêu Cầu Chức Năng Liên Quan**: FR-PUB-011

### Mục Tiêu
Tải xuống file PDF của một bài báo.

### Điều Kiện Tiên Quyết
- Bài báo có PDF đã upload
- Người dùng có quyền

### Luồng Chính
1. Người dùng xem chi tiết bài báo
2. Người dùng nhấn "Download PDF"
3. Hệ thống kiểm tra quyền hạn
4. Hệ thống phục vụ file để tải xuống
5. Hệ thống ghi nhật ký kiểm toán (ai tải, khi nào)

### Điều Kiện Hậu Quyết
**Thành Công**: File được tải xuống, audit được ghi  

### Quy Tắc Nghiệp Vụ
- Public có thể tải xuống CHỈ nếu trạng thái = PUBLISHED
- Tất cả lượt tải xuống đều được ghi nhật ký

---

## UC-M1-008: Thêm Đồng Tác Giả (Add Co-Authors)

**ID**: UC-M1-008  
**Độ Ưu Tiên**: 🟡 P1  
**Tác Nhân**: Researcher  
**User Stories Liên Quan**: US-RES-006  
**Yêu Cầu Chức Năng Liên Quan**: FR-PUB-007

### Mục Tiêu
Thêm đồng tác giả từ trường vào bài báo.

### Điều Kiện Tiên Quyết
- Người dùng là chủ sở hữu
- Bài báo là DRAFT hoặc REVISION_REQUIRED

### Luồng Chính
1. Researcher sửa bài báo
2. Researcher nhập tên vào trường đồng tác giả
3. Hệ thống hiển thị gợi ý tự động (autocomplete) từ cơ sở dữ liệu người dùng
4. Researcher chọn đồng tác giả
5. Hệ thống thêm vào danh sách đồng tác giả
6. Researcher có thể xóa đồng tác giả (trừ chính mình)

### Điều Kiện Hậu Quyết
**Thành Công**: Đồng tác giả được liên kết với bài báo

### Quy Tắc Nghiệp Vụ
- BR-PUB-001: Tác giả liên hệ (chủ sở hữu) không thể bị xóa
- Đồng tác giả có thể xem nhưng không thể sửa/xóa

---

## UC-M1-009: Xác Thực DOI/ISSN (Validate DOI/ISSN)

**ID**: UC-M1-009  
**Độ Ưu Tiên**: 🟡 P1  
**Tác Nhân**: Hệ Thống  
**User Stories Liên Quan**: US-RES-017, US-RES-018  
**Yêu Cầu Chức Năng Liên Quan**: FR-PUB-012, FR-PUB-013

### Mục Tiêu
Xác thực định dạng DOI và ISSN trong thời gian thực.

### Luồng Chính
1. Researcher nhập DOI hoặc ISSN
2. Researcher chuyển sang trường tiếp theo (sự kiện blur)
3. Hệ thống xác thực định dạng:
   - DOI: `^10\\.\\d{4,9}/[-._;()/:A-Z0-9]+$`
   - ISSN: `^\\d{4}-\\d{3}[0-9X]$`
4. Nếu hợp lệ: Hiển thị dấu tích xanh, tạo liên kết có thể nhấp (DOI)
5. Nếu không hợp lệ: Hiển thị thông báo lỗi màu đỏ với gợi ý định dạng

### Điều Kiện Hậu Quyết
**Thành Công**: Định dạng hợp lệ, liên kết được tạo  
**Thất Bại**: Lỗi hiển thị, phải sửa trước khi nộp

### Quy Tắc Nghiệp Vụ
- BR-PUB-004: Định dạng DOI và ISSN được xác thực nghiêm ngặt

---

## UC-M1-010: Xem Dashboard Giờ Làm (View Work Hours Dashboard)

**ID**: UC-M1-010  
**Độ Ưu Tiên**: 🟡 P1  
**Tác Nhân**: Researcher  
**User Stories Liên Quan**: US-RES-024  
**Yêu Cầu Chức Năng Liên Quan**: FR-PUB-016

### Mục Tiêu
Researcher xem dashboard giờ làm với tổng số giờ trong năm và chi tiết từng bài báo.

### Điều Kiện Tiên Quyết
- Researcher đã đăng nhập
- Có ít nhất 1 bài báo PUBLISHED với giờ làm được ghi nhận

### Luồng Chính
1. Researcher điều hướng đến "Dashboard Giờ Làm"
2. Hệ thống truy vấn các bài báo:
   - Trạng thái = PUBLISHED
   - created_by = researcher hiện tại
   - Có work_hour_conversions
3. Hệ thống hiển thị:
   - Tóm tắt: "Năm 2026: [X] giờ" (mặc định: năm hiện tại)
   - Bộ lọc năm (dropdown: 2020-2026)
   - Bảng với cột: Tiêu đề, Loại Tạp chí, Số Giờ, Ngày Phê Duyệt
   - Nút "Xuất Excel"
4. Researcher có thể lọc theo năm
5. Researcher có thể xuất báo cáo Excel

### Điều Kiện Hậu Quyết
**Thành Công**: Dashboard hiển thị đầy đủ thông tin giờ làm

### Quy Tắc Nghiệp Vụ
- Chỉ tính bài báo PUBLISHED
- Sắp xếp theo ngày phê duyệt (mới nhất trước)
- Tổng giờ được cache để tối ưu hiệu suất
- Excel export bao gồm: Tiêu đề, Năm, Loại, Số Giờ, Ngày Duyệt

---

**Tài liệu liên quan**:
- [Use Case Cấp Cao UC-HL-001](../High_Level/uc_hl_01_manage_publications.md)
- [User Stories - Researcher](../../04_User_Stories/By_Role/researcher_stories.md)
- [Yêu Cầu - Quản Lý Bài Báo](../../03_Requirements/Functional/module_publication_management.md)
