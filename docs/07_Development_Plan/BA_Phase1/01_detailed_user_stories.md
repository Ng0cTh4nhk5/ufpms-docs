# BA Deliverable 1: Phân Tích Chi Tiết User Stories

> 📋 **Phiên bản**: V1.0  
> 👤 **Vai trò**: Business Analyst  
> 📅 **Ngày tạo**: 20/02/2026  
> 🎯 **Phạm vi**: 9 User Stories - Core Publication Management

---

## Tổng Quan

Phase 1 tập trung vào **9 user stories** cốt lõi của Researcher trong module Publication Management:

| ID | Tên | Độ ưu tiên |
|---|---|---|
| US-RES-001 | Tạo Bài Báo Mới | 🔴 P0 |
| US-RES-002 | Upload File PDF | 🔴 P0 |
| US-RES-003 | Sửa Bài Báo Nháp | 🔴 P0 |
| US-RES-004 | Xóa Bài Báo Nháp | 🔴 P0 |
| US-RES-005 | Xem Danh Sách Bài Báo | 🔴 P0 |
| US-RES-006 | Thêm Đồng Tác Giả | 🔴 P0 |
| US-RES-008 | Xem Chi Tiết Bài Báo | 🔴 P0 |
| US-RES-009 | Download File PDF | 🔴 P0 |
| US-RES-024 | Xem Dashboard Giờ Làm | 🔴 P0 |

---

## US-RES-001: Tạo Bài Báo Mới

### 1. Business Value
- Cho phép researchers ghi nhận research outputs vào hệ thống một cách chính thức
- Là bước đầu tiên bắt buộc trong toàn bộ publication workflow
- Tạo nền tảng để quản lý trạng thái, đồng tác giả và file đính kèm

### 2. Detailed Description
- Researcher đã đăng nhập vào hệ thống
- Điều hướng đến trang "Tạo bài báo mới" (qua menu hoặc nút Create)
- Điền thông tin publication vào form
- Nhấn "Lưu nháp" để lưu với status = DRAFT
- Hệ thống redirect đến trang Publication Detail

### 3. Acceptance Criteria (Chi Tiết)

| # | Điều kiện | Kết quả mong đợi |
|---|---|---|
| AC-001-1 | Form hiển thị khi user click "Tạo mới" | Form có đầy đủ required fields và optional fields |
| AC-001-2 | Required fields: Title, Publication Type, Year | Không thể save nếu thiếu bất kỳ field nào |
| AC-001-3 | Optional fields: Journal/Conference Name, Volume, Issue, Pages, DOI, Abstract, Keywords | Có thể save mà không điền |
| AC-001-4 | Validation hiển thị inline realtime | Mỗi field có error message riêng biệt ngay bên dưới field |
| AC-001-5 | Nhấn "Lưu nháp" khi form hợp lệ | Tạo publication với status = DRAFT, redirect về Detail page |
| AC-001-6 | Nhấn "Hủy" | Quay về trang danh sách, không lưu dữ liệu |

### 4. Business Rules

| Rule ID | Mô tả |
|---|---|
| BR-001 | Title: bắt buộc, tối đa 500 ký tự |
| BR-002 | Year: bắt buộc, phải là số nguyên trong khoảng 1900 đến năm hiện tại |
| BR-003 | Publication Type: bắt buộc, chỉ chấp nhận JOURNAL \| CONFERENCE \| BOOK_CHAPTER \| OTHER |
| BR-004 | DOI (nếu nhập): phải đúng format `10.XXXX/...` |
| BR-005 | Status mặc định = DRAFT khi tạo mới |

### 5. Edge Cases

| Tình huống | Hành vi hệ thống |
|---|---|
| Title bằng tiếng Việt có dấu | Cho phép, lưu đúng encoding UTF-8 |
| Title có ký tự đặc biệt (`<`, `>`, `"`, `'`) | Cho phép nhập nhưng sanitize (escape) khi lưu/hiển thị |
| Title = 500 ký tự | Cho phép (boundary value) |
| Title = 501 ký tự | Validation error: "Tiêu đề không được vượt quá 500 ký tự" |
| Year = 1900 | Cho phép (boundary value) |
| Year = 1899 | Validation error: "Năm phải từ 1900 đến năm hiện tại" |
| Year = năm tương lai (ví dụ 2027) | Validation error: "Năm phải từ 1900 đến năm hiện tại" |
| Không chọn Publication Type | Validation error: "Vui lòng chọn loại bài báo" |
| DOI sai format | Validation warning (không block save): "Định dạng DOI không hợp lệ" |
| Form submit khi network offline | Toast error: "Không thể kết nối. Vui lòng thử lại." |

### 6. Dependencies
- **Không có** (đây là feature đầu tiên trong workflow)
- User phải đã đăng nhập (Authentication - ngoài phạm vi story này)

### 7. Test Scenarios

| TS ID | Mô tả | Loại |
|---|---|---|
| TS-001-1 | Happy path: Tạo publication thành công với đủ required fields | Positive |
| TS-001-2 | Thiếu Title → Validation error | Negative |
| TS-001-3 | Thiếu Year → Validation error | Negative |
| TS-001-4 | Thiếu Publication Type → Validation error | Negative |
| TS-001-5 | Year = 1899 (invalid) → Validation error | Negative |
| TS-001-6 | Year = năm tương lai → Validation error | Negative |
| TS-001-7 | Title = 501 ký tự → Validation error | Boundary |
| TS-001-8 | Title = 500 ký tự → Thành công | Boundary |
| TS-001-9 | DOI sai format → Warning (vẫn lưu được) | Negative |
| TS-001-10 | Nhấn Cancel → Không lưu, quay về List | Positive |
| TS-001-11 | Title có ký tự tiếng Việt → Lưu thành công | Special Characters |
| TS-001-12 | Sau khi save → Redirect đến Detail page | Post-condition |

---

## US-RES-002: Upload File PDF

### 1. Business Value
- Lưu trữ full-text của publications để người duyệt và đọc có thể truy cập
- Là pre-requisite cho US-RES-009 (Download PDF) và US-RES-008 (View Detail with PDF preview)
- Hỗ trợ workflow xét duyệt khi reviewer cần đọc nội dung đầy đủ

### 2. Detailed Description
- Từ Publication Detail page (của publication thuộc về mình)
- Click nút "Tải lên PDF"
- Hộp file picker hiện ra, chỉ chấp nhận file .pdf
- User chọn file → Upload bắt đầu với progress indicator
- File được upload lên server, path lưu vào database
- Sau khi upload thành công: hiển thị PDF preview và thông báo thành công

### 3. Acceptance Criteria (Chi Tiết)

| # | Điều kiện | Kết quả mong đợi |
|---|---|---|
| AC-002-1 | User vào Detail page của own publication | Upload button hiển thị |
| AC-002-2 | User vào Detail page của publication người khác | Upload button KHÔNG hiển thị |
| AC-002-3 | File picker mở | Chỉ accept file với extension .pdf |
| AC-002-4 | Đang upload | Progress bar/spinner hiển thị, button bị disabled |
| AC-002-5 | Upload thành công | Toast success, PDF preview hiển thị ngay |
| AC-002-6 | Upload lần 2 (đã có PDF cũ) | PDF mới thay thế PDF cũ, thông báo "PDF đã được cập nhật" |
| AC-002-7 | Cancel chọn file (đóng hộp thoại) | Không có thay đổi gì |

### 4. Business Rules

| Rule ID | Mô tả |
|---|---|
| BR-006 | Chỉ chấp nhận file có extension .pdf và MIME type application/pdf |
| BR-007 | Kích thước file tối đa 20MB |
| BR-008 | Filename trên server được rename bằng UUID để tránh conflicts |
| BR-009 | Upload mới sẽ replace PDF cũ (cả file vật lý trên storage) |
| BR-010 | Chỉ owner của publication mới có thể upload |

### 5. Edge Cases

| Tình huống | Hành vi hệ thống |
|---|---|
| Upload file .docx | Error: "Chỉ chấp nhận file PDF" |
| Upload file đổi tên thành .pdf nhưng nội dung không phải PDF | Error: "File không hợp lệ, vui lòng chọn file PDF thực sự" |
| Upload file 20MB (boundary) | Cho phép |
| Upload file 20.1MB (over limit) | Error: "File vượt quá giới hạn 20MB" |
| Mất kết nối trong khi upload | Toast error: "Upload thất bại. Vui lòng thử lại." File không được lưu |
| Upload trùng tên file | Server tự đổi tên bằng UUID (user không thấy) |
| Publication status ≠ DRAFT (đã submitted) | Upload button vẫn hiển thị (cho phép update PDF kể cả khi đang review) |

> **⚠️ Open Question OQ-001**: Có cho phép upload/update PDF sau khi publication đã SUBMITTED không? Cần xác nhận với stakeholder.

### 6. Dependencies
- US-RES-001 (Publication đã tồn tại trong hệ thống)
- File storage service phải sẵn sàng

### 7. Test Scenarios

| TS ID | Mô tả | Loại |
|---|---|---|
| TS-002-1 | Upload PDF hợp lệ (< 20MB) → Success, preview hiển thị | Positive |
| TS-002-2 | Upload file .docx → Error "Only PDF allowed" | Negative |
| TS-002-3 | Upload file 20.1MB → Error "File too large" | Negative |
| TS-002-4 | Upload file 20MB đúng limit → Success | Boundary |
| TS-002-5 | Upload lần 2 → PDF mới thay thế PDF cũ | Replacement |
| TS-002-6 | Simulate network failure khi upload → Error message | Error handling |
| TS-002-7 | Vào Detail page của publication người khác → Không có upload button | Authorization |
| TS-002-8 | Cancel file picker → Không thay đổi gì | Cancel |

---

## US-RES-003: Sửa Bài Báo Nháp

### 1. Business Value
- Cho phép researcher hoàn thiện thông tin trước khi submit
- Hỗ trợ workflow khi reviewer yêu cầu chỉnh sửa (REVISION_REQUIRED)
- Đảm bảo dữ liệu publication luôn chính xác

### 2. Detailed Description
- User điều hướng đến publication ở status DRAFT hoặc REVISION_REQUIRED
- Click nút "Chỉnh sửa" (Edit icon hoặc Edit button)
- Form hiện ra với dữ liệu đã điền sẵn (pre-filled)
- User sửa thông tin cần thiết
- Nhấn "Lưu" để cập nhật
- Hệ thống lưu thay đổi, redirect về Detail page

### 3. Acceptance Criteria (Chi Tiết)

| # | Điều kiện | Kết quả mong đợi |
|---|---|---|
| AC-003-1 | Publication ở status DRAFT, user là owner | Edit button hiển thị và click được |
| AC-003-2 | Publication ở status REVISION_REQUIRED, user là owner | Edit button hiển thị và click được |
| AC-003-3 | Publication ở status SUBMITTED/APPROVED/PUBLISHED | Edit button bị disabled hoặc ẩn |
| AC-003-4 | Publication thuộc người khác | Edit button không hiển thị |
| AC-003-5 | Mở form Edit | Tất cả trường hiển thị với giá trị hiện tại |
| AC-003-6 | Lưu thay đổi hợp lệ | Database cập nhật, audit log ghi lại (ai sửa, khi nào), redirect về Detail |
| AC-003-7 | Lưu với invalid data | Validation error hiển thị inline |

### 4. Business Rules

| Rule ID | Mô tả |
|---|---|
| BR-011 | Chỉ DRAFT và REVISION_REQUIRED có thể Edit |
| BR-012 | Chỉ owner (creator) mới có quyền Edit |
| BR-013 | Mọi thay đổi phải được ghi vào audit log |
| BR-014 | Validation rules giống US-RES-001 khi lưu |

### 5. Edge Cases

| Tình huống | Hành vi hệ thống |
|---|---|
| User sửa Title thành rỗng rồi nhấn Save | Validation error: "Tiêu đề là bắt buộc" |
| User sửa nhưng không thay đổi gì rồi nhấn Save | Lưu thành công (không cần detect change) |
| Người khác cũng đang mở form Edit cùng lúc | Last write wins (không cần lock cho V1.0) |
| Publication bị chuyển sang SUBMITTED trong khi đang Edit | Khi user nhấn Save, hệ thống kiểm tra status hiện tại → Error: "Bài báo đã được submit, không thể chỉnh sửa" |

### 6. Dependencies
- US-RES-001 (Publication đã tồn tại)

### 7. Test Scenarios

| TS ID | Mô tả | Loại |
|---|---|---|
| TS-003-1 | Sửa title DRAFT publication → Lưu thành công | Positive |
| TS-003-2 | Sửa REVISION_REQUIRED publication → Lưu thành công | Positive |
| TS-003-3 | Cố edit SUBMITTED publication → Edit button disabled | Authorization |
| TS-003-4 | Sửa title thành rỗng → Validation error | Negative |
| TS-003-5 | Sửa year thành 1899 → Validation error | Negative |
| TS-003-6 | Nhấn Cancel khi đang edit → Không lưu | Cancel |
| TS-003-7 | Audit log ghi nhận thay đổi | Audit |

---

## US-RES-004: Xóa Bài Báo Nháp

### 1. Business Value
- Cho phép researcher dọn dẹp các publications không cần thiết
- Giảm "noise" trong danh sách publications
- Quyền xóa chỉ áp dụng cho DRAFT để bảo vệ dữ liệu đã submit

### 2. Detailed Description
- User ở Publication List hoặc Detail page của DRAFT publication
- Click biểu tượng "Xóa" (Trash icon)
- Confirm dialog hiện ra: "Bạn có chắc muốn xóa bài báo này không? Hành động này không thể hoàn tác."
- Nhấn "Xác nhận" → Xóa thực hiện (soft delete + xóa PDF file)
- Redirect về Publication List

### 3. Acceptance Criteria (Chi Tiết)

| # | Điều kiện | Kết quả mong đợi |
|---|---|---|
| AC-004-1 | Publication ở DRAFT, user là owner | Delete icon/button hiển thị |
| AC-004-2 | Publication status ≠ DRAFT | Delete icon không hiển thị |
| AC-004-3 | Publication thuộc người khác | Delete icon không hiển thị |
| AC-004-4 | Click Delete → Confirm dialog | Dialog xuất hiện với warning text |
| AC-004-5 | Nhấn Xác nhận trong dialog | Publication soft deleted (deleted_at set), PDF file bị xóa khỏi storage |
| AC-004-6 | Nhấn Hủy trong dialog | Không có thay đổi, dialog đóng |
| AC-004-7 | Sau khi xóa thành công | Redirect về Publication List, toast success |

### 4. Business Rules

| Rule ID | Mô tả |
|---|---|
| BR-015 | Chỉ DRAFT publications có thể xóa |
| BR-016 | Chỉ owner mới có quyền xóa |
| BR-017 | Xóa kiểu soft delete: set `deleted_at` timestamp (không xóa row khỏi DB) |
| BR-018 | File PDF vật lý bị xóa khỏi storage khi publication bị xóa |
| BR-019 | Phải có confirm dialog (2-step confirmation) |

### 5. Edge Cases

| Tình huống | Hành vi hệ thống |
|---|---|
| Xóa publication không có PDF | Chỉ soft delete record, không có bước xóa file |
| Xóa thất bại khi network offline | Error toast: "Không thể xóa. Vui lòng thử lại." |
| Publication là co-author relation với người khác | Chỉ owner mới xóa được, co-author không thấy nút Delete |

### 6. Dependencies
- US-RES-001 (Publication đã tồn tại)

### 7. Test Scenarios

| TS ID | Mô tả | Loại |
|---|---|---|
| TS-004-1 | Xóa DRAFT publication (không có PDF) → Thành công | Positive |
| TS-004-2 | Xóa DRAFT publication (có PDF) → Thành công, PDF bị xóa | Positive |
| TS-004-3 | Cố xóa SUBMITTED publication → Delete button không có | Authorization |
| TS-004-4 | Click Delete → Nhấn Hủy trong dialog → Không xóa | Cancel |
| TS-004-5 | Sau xóa → Redirect về List, không còn trong List | Post-condition |
| TS-004-6 | Xóa publication của người khác → Không thể | Authorization |

---

## US-RES-005: Xem Danh Sách Bài Báo

### 1. Business Value
- Cung cấp cái nhìn tổng quan về tất cả publications của researcher
- Cho phép filter/search để tìm publication nhanh chóng
- Entry point cho các actions: Edit, Delete, View Detail

### 2. Detailed Description
- User điều hướng đến trang "Bài báo của tôi" từ menu
- Hệ thống load danh sách publications (pagination, 10 items/trang)
- User có thể filter theo: Status, Year, hoặc tìm kiếm theo title
- Click vào row để xem Detail, hoặc dùng action icons

### 3. Acceptance Criteria (Chi Tiết)

| # | Điều kiện | Kết quả mong đợi |
|---|---|---|
| AC-005-1 | Vào trang "Bài báo của tôi" | Chỉ hiện publications của user đăng nhập |
| AC-005-2 | Danh sách columns | Title, Publication Type, Year, Status (badge màu), Ngày cập nhật, Actions |
| AC-005-3 | Status badge | DRAFT=xám, SUBMITTED=xanh dương, REVISION_REQUIRED=cam, APPROVED=xanh lá, PUBLISHED=tím |
| AC-005-4 | Filter theo Status | Dropdown: Tất cả / DRAFT / SUBMITTED / ... |
| AC-005-5 | Tìm kiếm theo Title | Search box, search khi user gõ (debounce 300ms) |
| AC-005-6 | Filter theo Year | Number input, filter khi blur |
| AC-005-7 | Pagination | 10 items/trang, hiển thị tổng số, Next/Prev buttons |
| AC-005-8 | Không có publications | Empty state: "Bạn chưa có bài báo nào. Tạo bài báo mới?" |
| AC-005-9 | Action icons | Edit (chỉ DRAFT/REVISION_REQUIRED), Delete (chỉ DRAFT), View (tất cả) |

### 4. Business Rules

| Rule ID | Mô tả |
|---|---|
| BR-020 | Chỉ hiển thị publications của user đăng nhập (hoặc là co-author) |
| BR-021 | Mặc định sort: ngày cập nhật mới nhất trước |
| BR-022 | Pagination: 10 items/trang |
| BR-023 | Edit icon chỉ hiện cho DRAFT và REVISION_REQUIRED |
| BR-024 | Delete icon chỉ hiện cho DRAFT |

### 5. Edge Cases

| Tình huống | Hành vi hệ thống |
|---|---|
| User có 0 publications | Empty state message + link "Tạo mới" |
| Filter trả về 0 kết quả | "Không tìm thấy bài báo phù hợp" |
| Title quá dài trong bảng | Truncate với "..." và tooltip khi hover |
| User xóa publication → reload list | List tự re-fetch sau delete thành công |

### 6. Dependencies
- US-RES-001 (có publications để hiển thị)

### 7. Test Scenarios

| TS ID | Mô tả | Loại |
|---|---|---|
| TS-005-1 | Xem danh sách bình thường → Hiển thị đúng publications | Positive |
| TS-005-2 | Filter theo Status=DRAFT → Chỉ hiện DRAFT | Filter |
| TS-005-3 | Search title "test" → Chỉ hiện bài có "test" trong title | Search |
| TS-005-4 | Filter Year=2024 → Chỉ hiện publications 2024 | Filter |
| TS-005-5 | Empty list → Hiện empty state | Edge case |
| TS-005-6 | Action icons đúng theo status | Authorization |
| TS-005-7 | Pagination: 11 publications → 2 trang | Pagination |
| TS-005-8 | Click vào row → Navigate đến Detail | Navigation |

---

## US-RES-006: Thêm Đồng Tác Giả

### 1. Business Value
- Đảm bảo tất cả contributors được ghi nhận đúng mức
- Hỗ trợ tìm kiếm user nội bộ và thêm user ngoài hệ thống
- Thứ tự tác giả ảnh hưởng đến tính toán giờ làm và báo cáo

### 2. Detailed Description
- Từ Create/Edit Publication form
- Trong section "Đồng tác giả"
- User gõ tên để search trong hệ thống (internal) hoặc thêm thủ công (external)
- Có thể kéo thả để sắp xếp thứ tự tác giả
- Có thể đánh dấu 1 người là "Corresponding Author"

### 3. Acceptance Criteria (Chi Tiết)

| # | Điều kiện | Kết quả mong đợi |
|---|---|---|
| AC-006-1 | Gõ tên trong search box | Autocomplete gợi ý từ user list hệ thống (debounce 300ms) |
| AC-006-2 | Chọn user từ autocomplete | User thêm vào danh sách co-authors |
| AC-006-3 | Thêm external author (không có trong hệ thống) | Nhập tên thủ công, không có user account link |
| AC-006-4 | Danh sách co-authors | Hiển thị tên, có thứ tự (sequence number) |
| AC-006-5 | Sắp xếp thứ tự | Kéo thả hoặc up/down arrows |
| AC-006-6 | Đánh dấu Corresponding Author | Checkbox/flag, chỉ 1 người được là Corresponding Author |
| AC-006-7 | Xóa co-author | Click X để remove khỏi list |
| AC-006-8 | Creator của publication | Tự động là Author #1, không thể remove |

### 4. Business Rules

| Rule ID | Mô tả |
|---|---|
| BR-025 | Co-authors có thứ tự sequence (1st, 2nd, ...) |
| BR-026 | Tìm kiếm internal: search trong bảng Users theo name/email |
| BR-027 | External author: nhập thủ công (tên + email optional) |
| BR-028 | Mỗi publication có đúng 1 Corresponding Author (optional, default = creator) |
| BR-029 | Creator tự động là Author #1, không thể remove hoặc thay đổi thứ tự xuống dưới |

### 5. Edge Cases

| Tình huống | Hành vi hệ thống |
|---|---|
| Search không tìm thấy user | "Không tìm thấy. Thêm làm tác giả ngoài?" (external author option) |
| Thêm duplicate (đã có trong list) | Warning: "Tác giả này đã được thêm" |
| Max co-authors reached (nếu có limit) | Error: "Đã đạt giới hạn [N] đồng tác giả" |
| Xóa Corresponding Author flag | Corresponding Author field trống (hoặc tự reset về creator) |

> **⚠️ Open Question OQ-002**: Giới hạn số co-authors tối đa? Đề xuất: không giới hạn cho V1.0

### 6. Dependencies
- US-RES-001 (có publication để add co-authors)
- User Account Management (users phải tồn tại trong hệ thống)

### 7. Test Scenarios

| TS ID | Mô tả | Loại |
|---|---|---|
| TS-006-1 | Search và thêm internal co-author → Thành công | Positive |
| TS-006-2 | Thêm external author (nhập tay) → Thành công | Positive |
| TS-006-3 | Xóa co-author khỏi list → Thành công | Positive |
| TS-006-4 | Thêm duplicate co-author → Warning | Negative |
| TS-006-5 | Kéo thả thứ tự tác giả → Sequence được cập nhật | Drag-drop |
| TS-006-6 | Đánh dấu Corresponding Author → Chỉ 1 người | Business Rule |
| TS-006-7 | Cố remove creator khỏi danh sách → Không thể | Authorization |
| TS-006-8 | Search không có kết quả → Hiển thị option thêm external | Empty State |

---

## US-RES-008: Xem Chi Tiết Bài Báo

### 1. Business Value
- Cung cấp full view về tất cả thông tin của publication
- Hiển thị PDF viewer inline để reviewer/researcher xem nội dung ngay trên web
- Cho thấy review history và current status trong workflow

### 2. Detailed Description
- User click vào publication từ list hoặc từ link
- Trang Detail hiển thị layout 2 cột: PDF viewer (trái) và metadata panel (phải)
- Metadata bao gồm: thông tin cơ bản, co-authors, abstract, keywords, status badge
- Nếu có PDF: hiển thị iframe PDF viewer; nếu không có: placeholder "Chưa có PDF"
- Action buttons theo quyền và status

### 3. Acceptance Criteria (Chi Tiết)

| # | Điều kiện | Kết quả mong đợi |
|---|---|---|
| AC-008-1 | User có quyền xem (owner/admin/reviewer) | Full detail hiển thị |
| AC-008-2 | Thông tin hiển thị | Title, Type, Year, Journal, Volume, Issue, Pages, DOI, Abstract, Keywords |
| AC-008-3 | Co-authors section | Danh sách tác giả theo thứ tự, badge "Corresponding Author" |
| AC-008-4 | Status badge | Màu sắc theo status, rõ ràng |
| AC-008-5 | Publication có PDF | PDF viewer (iframe) hiển thị bên trái |
| AC-008-6 | Publication không có PDF | Left panel hiển thị "Chưa có tệp PDF. Nhấn để tải lên." (nếu là owner) |
| AC-008-7 | DOI có giá trị | DOI hiển thị dạng clickable link tới https://doi.org/[DOI] |
| AC-008-8 | Action buttons | Edit (DRAFT/REVISION_REQUIRED + owner), Delete (DRAFT + owner), Download PDF (có PDF) |

### 4. Business Rules

| Rule ID | Mô tả |
|---|---|
| BR-030 | Owner + co-authors có thể xem Detail của publication mình |
| BR-031 | PDF viewer sử dụng iframe với src = file URL |
| BR-032 | Review history: danh sách status transitions với timestamp và reviewer name |

### 5. Edge Cases

| Tình huống | Hành vi hệ thống |
|---|---|
| PDF file bị xóa khỏi storage nhưng path vẫn trong DB | Show error placeholder: "Không tìm thấy file PDF" |
| Abstract rất dài (> 2000 chars) | Hiển thị "Xem thêm/Thu gọn" toggle |
| DOI URL không hợp lệ (doi.org trả về 404) | Link vẫn hiển thị (không kiểm tra validity realtime) |
| User navigate trực tiếp đến URL của publication không thuộc mình | 403 Forbidden page |

### 6. Dependencies
- US-RES-001 (publication đã có)
- US-RES-002 (để xem PDF viewer)
- US-RES-006 (để hiển thị co-authors)

### 7. Test Scenarios

| TS ID | Mô tả | Loại |
|---|---|---|
| TS-008-1 | Xem Detail publication có đủ thông tin + PDF | Positive |
| TS-008-2 | Xem Detail publication không có PDF | Edge case |
| TS-008-3 | DOI hiển thị dạng clickable link | UI |
| TS-008-4 | Action buttons đúng với status DRAFT | Authorization |
| TS-008-5 | Action buttons đúng với status SUBMITTED | Authorization |
| TS-008-6 | Truy cập publication của người khác → 403 | Security |
| TS-008-7 | Co-authors hiển thị đúng thứ tự | Data |

---

## US-RES-009: Download File PDF

### 1. Business Value
- Cho phép researcher lưu file về máy để chia sẻ offline
- Hỗ trợ reviewer download về để đọc chi tiết
- Audit trail ghi lại ai download giúp tracking

### 2. Detailed Description
- Từ Publication Detail page
- Click nút "Tải PDF"
- Browser trigger download file về máy
- Hệ thống ghi audit log

### 3. Acceptance Criteria (Chi Tiết)

| # | Điều kiện | Kết quả mong đợi |
|---|---|---|
| AC-009-1 | Publication có PDF, user là owner | Download button hiển thị |
| AC-009-2 | Publication không có PDF | Download button ẩn hoặc disabled |
| AC-009-3 | Click Download | Browser bắt đầu download file, filename là tên gốc hoặc publication title |
| AC-009-4 | Audit log | Ghi lại: user_id, publication_id, action=DOWNLOAD, timestamp |

### 4. Business Rules

| Rule ID | Mô tả |
|---|---|
| BR-033 | Chỉ owner có thể download PDF của DRAFT publication |
| BR-034 | PUBLISHED publications: tất cả user đăng nhập có thể download |
| BR-035 | Mọi download action đều được ghi vào audit log |

### 5. Edge Cases

| Tình huống | Hành vi hệ thống |
|---|---|
| File không tồn tại trên storage | Error: "File không tìm thấy trên server" |
| File quá lớn (> 20MB không download được qua browser) | Download vẫn hoạt động (browser xử lý) |
| User download nhiều lần | Mỗi lần được ghi log riêng |

### 6. Dependencies
- US-RES-002 (PDF đã được upload)

### 7. Test Scenarios

| TS ID | Mô tả | Loại |
|---|---|---|
| TS-009-1 | Download PDF thành công | Positive |
| TS-009-2 | Publication không có PDF → Download button ẩn | Edge case |
| TS-009-3 | Audit log ghi nhận download action | Audit |
| TS-009-4 | File không tìm thấy → Error message | Error handling |

---

## US-RES-024: Xem Dashboard Giờ Làm

### 1. Business Value
- Giúp researcher tính được tổng giờ làm quy đổi từ publications PUBLISHED
- Hỗ trợ chuẩn bị báo cáo giờ làm hàng năm
- Cơ sở để tính KPI nghiên cứu của giảng viên

### 2. Detailed Description
- User truy cập "Dashboard Giờ Làm" từ menu
- Hệ thống hiển thị summary tổng giờ năm hiện tại (default)
- Có thể filter theo năm (2020 đến hiện tại)
- Bảng chi tiết từng publication với số giờ quy đổi
- Nút "Xuất Excel" để download báo cáo

### 3. Acceptance Criteria (Chi Tiết)

| # | Điều kiện | Kết quả mong đợi |
|---|---|---|
| AC-024-1 | Default khi vào Dashboard | Hiển thị năm hiện tại, tổng giờ |
| AC-024-2 | Summary card | "Năm [YYYY]: [X] giờ" |
| AC-024-3 | Filter year dropdown | 2020 → năm hiện tại |
| AC-024-4 | Bảng chi tiết columns | Title, Publication Type, Work Hours, Approval Date |
| AC-024-5 | Sort bảng | Theo Approval Date, mới nhất trước |
| AC-024-6 | Nút "Xuất Excel" | Download file .xlsx với dữ liệu hiện tại |
| AC-024-7 | Không có PUBLISHED publication trong năm | Hiển thị "Năm [YYYY]: 0 giờ", bảng rỗng |

### 4. Business Rules

| Rule ID | Mô tả |
|---|---|
| BR-036 | Giờ quy đổi: JOURNAL = 40h, CONFERENCE = 20h, BOOK_CHAPTER = 60h, OTHER = 10h |
| BR-037 | Chỉ tính publications với status = PUBLISHED |
| BR-038 | Filter theo năm dựa trên `approval_date` (năm được approver approve publication) |
| BR-039 | Nếu user là co-author, publication vẫn được tính (giờ toàn bộ, không chia) |

### 5. Edge Cases

| Tình huống | Hành vi hệ thống |
|---|---|
| User không có PUBLISHED publications | 0 giờ, bảng rỗng |
| User có publications DRAFT/SUBMITTED nhưng không PUBLISHED | Không tính vào dashboard |
| Xuất Excel khi bảng rỗng | File Excel rỗng (chỉ có header) |
| Filter năm không có publications | "Không có bài báo được duyệt trong năm [YYYY]" |

> **⚠️ Open Question OQ-003**: Nếu user là co-author, có tính giờ hay không? Theo BR-039 đề xuất tính toàn bộ. Cần xác nhận stakeholder.

### 6. Dependencies
- US-RES-001 (publications phải tồn tại)
- Approval workflow (publications phải được approve → PUBLISHED)

### 7. Test Scenarios

| TS ID | Mô tả | Loại |
|---|---|---|
| TS-024-1 | User có 1 JOURNAL PUBLISHED → Hiển thị 40h | Positive |
| TS-024-2 | User có mix JOURNAL+CONFERENCE → Tổng đúng | Calculation |
| TS-024-3 | Filter năm khác → Hiển thị đúng năm đó | Filter |
| TS-024-4 | Không có PUBLISHED → 0 giờ | Edge case |
| TS-024-5 | Export Excel → File download thành công | Export |
| TS-024-6 | DRAFT publications không tính vào Dashboard | Business Rule |

---

## Open Questions Cần Xác Nhận

| ID | Câu hỏi | Ảnh hưởng | Do ai quyết |
|---|---|---|---|
| OQ-001 | Có cho phép upload PDF sau khi publication đã SUBMITTED? | US-RES-002 | Stakeholder |
| OQ-002 | Giới hạn số co-authors tối đa? | US-RES-006 | Dev + BA |
| OQ-003 | Co-author có được tính giờ làm không? | US-RES-024 | Stakeholder |

---

**Prepared by**: Business Analysis Team  
**Version**: 1.0  
**Date**: 20/02/2026  
**Status**: Draft - Chờ review
