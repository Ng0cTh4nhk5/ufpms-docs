# BA Deliverable 5: Test Scenarios Document

> 📋 **Phiên bản**: V1.0  
> 👤 **Chuẩn bị bởi**: Business Analyst (để QA tham khảo)  
> 📅 **Ngày tạo**: 20/02/2026  
> 🎯 **Phạm vi**: 9 User Stories - 40+ Test Scenarios

---

## Tổng Quan

Tài liệu này cung cấp **test scenarios** chi tiết cho QA team. Mỗi scenario mô tả một user journey cụ thể với điều kiện ban đầu, các bước thực hiện và kết quả mong đợi.

### Phân Loại Test Scenarios

| Ký hiệu | Loại | Mô tả |
|---|---|---|
| ✅ Positive | Happy Path | Flow thành công bình thường |
| ❌ Negative | Error Path | Input sai, thiếu data |
| ⚠️ Boundary | Boundary Value | Giá trị ở biên giới |
| 🔒 Auth | Authorization | Kiểm tra quyền truy cập |
| 🔄 Integration | Integration | Nhiều features liên kết |

---

## Group 1: Authentication

### TS-AUTH-001 ✅ Đăng nhập thành công
**Precondition**: User có tài khoản hợp lệ  
**Steps**:
1. Truy cập `/login`
2. Nhập username đúng
3. Nhập password đúng
4. Click "Đăng nhập"

**Expected**: Redirect đến `/dashboard`, hiển thị tên user ở header

---

### TS-AUTH-002 ❌ Đăng nhập sai mật khẩu
**Precondition**: User có tài khoản  
**Steps**:
1. Nhập username đúng
2. Nhập password SAI
3. Click "Đăng nhập"

**Expected**: Hiển thị error "Tên đăng nhập hoặc mật khẩu không đúng", ở lại trang login

---

### TS-AUTH-003 ❌ Đăng nhập với form rỗng
**Steps**:
1. Để trống cả 2 fields
2. Click "Đăng nhập"

**Expected**: Validation error hoặc button bị disabled (không gọi API)

---

## Group 2: Tạo Bài Báo (US-RES-001)

### TS-001-1 ✅ Tạo publication thành công (happy path)
**Precondition**: User đã đăng nhập  
**Steps**:
1. Click "Tạo bài báo mới"
2. Chọn Publication Type = JOURNAL
3. Nhập Title = "Test Publication Article"
4. Nhập Year = 2024
5. Click "Lưu nháp"

**Expected**: Publication được tạo với status=DRAFT, redirect về Detail page, title đúng

---

### TS-001-2 ❌ Tạo publication thiếu Title
**Steps**:
1. Mở form Create
2. Chọn Type = JOURNAL, Year = 2024
3. Để Title trống
4. Click "Lưu nháp"

**Expected**: Lỗi inline "Tiêu đề là bắt buộc", KHÔNG submit API

---

### TS-001-3 ❌ Tạo publication shiếu Year
**Steps**:
1. Nhập Title hợp lệ, chọn Type
2. Để Year trống
3. Click "Lưu nháp"

**Expected**: Lỗi "Năm công bố là bắt buộc"

---

### TS-001-4 ❌ Year = 1899 (quá cũ)
**Steps**:
1. Điền đầy đủ form
2. Nhập Year = 1899
3. Click "Lưu nháp"

**Expected**: Lỗi "Năm phải từ 1900 đến [năm hiện tại]"

---

### TS-001-5 ❌ Year = năm tương lai
**Steps**:
1. Nhập Year = 2030 (hoặc năm lớn hơn năm hiện tại)

**Expected**: Lỗi "Năm phải từ 1900 đến [năm hiện tại]"

---

### TS-001-6 ⚠️ Title = 500 ký tự (boundary)
**Steps**:
1. Nhập Title có đúng 500 ký tự
2. Submit form hợp lệ

**Expected**: Tạo thành công (500 là giới hạn cho phép)

---

### TS-001-7 ⚠️ Title = 501 ký tự (over limit)
**Steps**:
1. Nhập Title có 501 ký tự

**Expected**: Lỗi "Tiêu đề không được vượt quá 500 ký tự"

---

### TS-001-8 ✅ Tạo với đầy đủ optional fields
**Steps**:
1. Điền tất cả fields: Title, Type, Year, Journal, DOI, Abstract, Keywords
2. Submit

**Expected**: Tất cả thông tin được lưu và hiển thị đúng trên Detail page

---

### TS-001-9 ✅ Nhấn Hủy khi đang nhập
**Steps**:
1. Nhập Title = "bài báo test"
2. Click "Hủy"

**Expected**: Quay về /publications, KHÔNG tạo publication

---

## Group 3: Upload PDF (US-RES-002)

### TS-002-1 ✅ Upload PDF thành công
**Precondition**: DRAFT publication tồn tại  
**Steps**:
1. Vào Detail page của DRAFT publication (own)
2. Click "Tải lên PDF"
3. Chọn file PDF hợp lệ (1MB)
4. Confirm upload

**Expected**: Progress bar hiển thị, sau đó PDF preview xuất hiện, toast success

---

### TS-002-2 ❌ Upload file Word (.docx)
**Steps**:
1. Trong file picker, chọn file .docx

**Expected**: File picker từ chối hoặc error "Chỉ chấp nhận file PDF"

---

### TS-002-3 ❌ Upload file PDF quá lớn (> 20MB)
**Steps**:
1. Chọn file PDF 25MB

**Expected**: Error "File vượt quá giới hạn 20MB"

---

### TS-002-4 ⚠️ Upload file PDF đúng 20MB (boundary)
**Steps**:
1. Chọn file PDF = 20MB

**Expected**: Upload thành công

---

### TS-002-5 🔄 Upload PDF lần 2 (replace)
**Precondition**: Publication đã có PDF  
**Steps**:
1. Vào Detail page
2. Upload PDF mới

**Expected**: PDF mới thay thế PDF cũ, preview cập nhật

---

### TS-002-6 🔒 Xem Detail page của publication người khác
**Steps**:
1. Truy cập /publications/{id} của người khác

**Expected**: Upload button KHÔNG hiển thị (hoặc page trả 403)

---

## Group 4: Sửa Bài Báo (US-RES-003)

### TS-003-1 ✅ Sửa DRAFT publication thành công
**Steps**:
1. Vào List → Click Edit icon của DRAFT publication
2. Thay đổi Title
3. Click "Lưu"

**Expected**: Title được cập nhật, redirect Detail, audit log ghi nhận

---

### TS-003-2 ✅ Sửa REVISION_REQUIRED publication
**Steps**:
1. Tìm publication REVISION_REQUIRED
2. Click Edit → Thay đổi thông tin
3. Lưu

**Expected**: Cập nhật thành công

---

### TS-003-3 🔒 Cố sửa SUBMITTED publication
**Steps**:
1. Vào Detail của SUBMITTED publication (own)

**Expected**: Edit button ẩn hoặc disabled

---

### TS-003-4 ❌ Sửa title thành rỗng
**Steps**:
1. Mở Edit form
2. Xóa hết Title
3. Click "Lưu"

**Expected**: Lỗi "Tiêu đề là bắt buộc"

---

## Group 5: Xóa Bài Báo (US-RES-004)

### TS-004-1 ✅ Xóa DRAFT publication không có PDF
**Steps**:
1. Trong List, click Delete icon của DRAFT publication (không có PDF)
2. Nhấn "Xác nhận" trong dialog

**Expected**: Publication biến mất khỏi list, toast success

---

### TS-004-2 ✅ Xóa DRAFT publication có PDF
**Steps**:
1. Delete DRAFT publication có PDF

**Expected**: Publication bị xóa, PDF file cũng được xóa khỏi storage

---

### TS-004-3 🔒 Cố xóa SUBMITTED publication
**Steps**:
1. Vào Detail/List của SUBMITTED publication

**Expected**: Delete button không hiển thị

---

### TS-004-4 ✅ Hủy xóa (nhấn Cancel trong dialog)
**Steps**:
1. Click Delete icon
2. Nhấn "Hủy" trong confirm dialog

**Expected**: Dialog đóng, publication vẫn còn

---

## Group 6: Danh Sách Bài Báo (US-RES-005)

### TS-005-1 ✅ Xem danh sách bình thường
**Precondition**: User có ≥ 1 publications  
**Steps**:
1. Vào /publications

**Expected**: Hiển thị danh sách với columns đúng, status badges đúng màu

---

### TS-005-2 ✅ Filter theo Status = DRAFT
**Steps**:
1. Chọn "Nháp" trong Status dropdown

**Expected**: Chỉ hiển thị DRAFT publications

---

### TS-005-3 ✅ Tìm kiếm theo title
**Steps**:
1. Nhập keyword vào search box

**Expected**: Sau 300ms, danh sách cập nhật chỉ hiện publications có keyword trong title

---

### TS-005-4 ✅ Pagination
**Precondition**: User có > 10 publications  
**Steps**:
1. Vào /publications
2. Click trang 2

**Expected**: Hiển thị items 11-20, pagination controls đúng

---

### TS-005-5 ⚠️ Danh sách rỗng (không có publications)
**Steps**:
1. Vào /publications với user không có publications

**Expected**: Empty state: "Bạn chưa có bài báo nào"

---

## Group 7: Đồng Tác Giả (US-RES-006)

### TS-006-1 ✅ Thêm internal co-author
**Steps**:
1. Trong Create/Edit form, search tên user "Nguyen"
2. Chọn user từ dropdown

**Expected**: User được thêm vào danh sách co-authors với sequence=2

---

### TS-006-2 ✅ Thêm external co-author
**Steps**:
1. Search không tìm thấy → Click "Thêm tác giả ngoài"
2. Nhập tên "John Doe"

**Expected**: External author được thêm vào list

---

### TS-006-3 ❌ Thêm trùng co-author
**Steps**:
1. Thêm user "Nguyen" vào list
2. Search "Nguyen" và chọn lại user đó

**Expected**: Warning "Tác giả này đã được thêm"

---

### TS-006-4 🔒 Creator không thể xóa chính mình
**Steps**:
1. Trong co-authors list, tìm mục của creator (Author #1)

**Expected**: Không có nút xóa (X) cạnh creator

---

## Group 8: Chi Tiết Bài Báo (US-RES-008)

### TS-008-1 ✅ Xem chi tiết có PDF
**Steps**:
1. Click vào publication có PDF

**Expected**: PDF hiển thị trong iframe bên trái, metadata bên phải

---

### TS-008-2 ✅ Xem chi tiết không có PDF
**Steps**:
1. Click vào publication KHÔNG có PDF

**Expected**: Bên trái hiện placeholder "Chưa có file PDF", nếu là owner có nút "Tải lên"

---

### TS-008-3 🔒 Truy cập URL publication người khác
**Steps**:
1. Browse thủ công đến /publications/{id_cua_nguoi_khac}

**Expected**: 403 Forbidden page

---

## Group 9: Download PDF (US-RES-009)

### TS-009-1 ✅ Download PDF thành công
**Steps**:
1. Vào Detail page của publication có PDF
2. Click "Tải PDF"

**Expected**: Browser download file, audit log ghi nhận

---

### TS-009-2 ⚠️ Publication không có PDF
**Steps**:
1. Vào Detail page publication không có PDF

**Expected**: Download button ẩn hoặc disabled

---

## Group 10: Dashboard Giờ Làm (US-RES-024)

### TS-024-1 ✅ Dashboard hiển thị đúng năm hiện tại
**Precondition**: User có PUBLISHED publications  
**Steps**:
1. Vào /work-hours

**Expected**: Hiển thị "Năm [năm hiện tại]: [X] giờ", bảng có dữ liệu

---

### TS-024-2 ✅ Tính giờ đúng theo loại
**Precondition**: 1 JOURNAL + 1 CONFERENCE PUBLISHED  
**Steps**:
1. Vào dashboard

**Expected**: Tổng = 40 + 20 = 60 giờ

---

### TS-024-3 ✅ Filter năm
**Steps**:
1. Chọn năm 2023 trong dropdown

**Expected**: Hiển thị publications PUBLISHED trong năm 2023, tổng giờ đúng

---

### TS-024-4 ⚠️ Không có PUBLISHED publications
**Steps**:
1. Vào dashboard với user chỉ có DRAFT publications

**Expected**: "Năm [YYYY]: 0 giờ", bảng rỗng

---

### TS-024-5 ✅ Xuất Excel
**Steps**:
1. Trong dashboard, click "Xuất Excel"

**Expected**: File .xlsx download, có header và dữ liệu đúng

---

### TS-024-6 ✅ DRAFT publication không tính
**Precondition**: User có DRAFT publication năm hiện tại  
**Steps**:
1. Vào dashboard

**Expected**: DRAFT publication KHÔNG xuất hiện trong bảng và KHÔNG được tính vào tổng giờ

---

## Tổng Kết Test Coverage

| US ID | Tên | Số TS | Positive | Negative | Boundary | Auth |
|---|---|---|---|---|---|---|
| US-RES-001 | Tạo Bài Báo | 9 | 4 | 4 | 2 | 0 |
| US-RES-002 | Upload PDF | 6 | 3 | 2 | 1 | 1 |
| US-RES-003 | Sửa Bài Báo | 4 | 2 | 1 | 0 | 1 |
| US-RES-004 | Xóa Bài Báo | 4 | 3 | 0 | 0 | 1 |
| US-RES-005 | Xem Danh Sách | 5 | 4 | 0 | 1 | 0 |
| US-RES-006 | Đồng Tác Giả | 4 | 3 | 1 | 0 | 1 |
| US-RES-008 | Xem Chi Tiết | 3 | 2 | 0 | 0 | 1 |
| US-RES-009 | Download PDF | 2 | 1 | 0 | 1 | 0 |
| US-RES-024 | Dashboard Giờ | 6 | 5 | 0 | 1 | 0 |
| **TOTAL** | | **43** | **27** | **8** | **6** | **5** |

---

**Prepared by**: Business Analysis Team  
**Version**: 1.0  
**Date**: 20/02/2026  
**Note**: QA team cần bổ sung thêm regression tests và performance tests theo phân công.
