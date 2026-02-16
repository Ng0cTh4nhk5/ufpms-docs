# SOP - QA/Tester
## Version 1.0: Core Publication Management

> 👤 **Vai trò**: QA/Tester  
> 🎯 **Phạm vi**: V1.0 - Testing cho Core Publication CRUD  
> 📅 **Áp dụng cho**: 9 User Stories + Integration Testing

---

## 🎯 Mục Tiêu Tổng Quan

Đảm bảo chất lượng sản phẩm V1.0 thông qua comprehensive testing. QA/Tester chịu trách nhiệm tìm bugs, verify acceptance criteria, và đảm bảo product đáp ứng yêu cầu người dùng trước khi release.

---

## 📋 Trách Nhiệm Chính

### 1. Lập Kế Hoạch Test
- Review user stories và acceptance criteria
- Tạo test cases coverage matrix
- Chuẩn bị test data

### 2. Thực Thi Testing
- Manual testing (functional, UI/UX, exploratory)
- API testing (Postman)
- Cross-browser testing (nếu cần)

### 3. Quản Lý Bugs
- Log bugs với reproduction steps chi tiết
- Verify bug fixes
- Maintain bug tracking (Jira/Trello)

### 4. Báo Cáo Testing
- Báo cáo test status hàng ngày
- Tracking bug metrics
- Final test summary report

---

## 📐 PHASE 1: DESIGN

### 1. Review Requirements

- [ ] **Tham Gia Design Review Meeting**
  - Hiểu Figma designs
  - Ghi chú expected behaviors
  - Đặt câu hỏi làm rõ

- [ ] **Review 9 User Stories với BA**
  
  Cho mỗi user story, xác nhận:
  - [ ] US-RES-001: Tạo bài báo mới
    - Acceptance criteria rõ ràng? ✅
    - Edge cases đã documented? ✅
    - Expected error messages? ✅
  
  - Tương tự cho 8 user stories còn lại...

---

### 2. Tạo Test Cases

- [ ] **Template Test Case**
  
  ```
  Cấu trúc 1 test case:
  - ID: TC-001
  - User Story: US-RES-001
  - Tiêu đề: Mô tả ngắn gọn test case
  - Preconditions: Điều kiện ban đầu (ví dụ: User đã login)
  - Steps: Các bước thực hiện chi tiết
  - Expected Result: Kết quả mong đợi
  - Priority: P0 (Critical), P1 (High), P2 (Medium), P3 (Low)
  ```

- [ ] **Tạo Test Cases Toàn Diện**

  **US-RES-001: Tạo bài báo mới (10 test cases)**
  
  - TC-001: Tạo publication - Happy path (tất cả required fields hợp lệ)
  - TC-002: Tạo publication - Thiếu Title → Hiện validation error
  - TC-003: Tạo publication - Thiếu Year → Hiện validation error
  - TC-004: Tạo publication - Year không hợp lệ (< 1900) → Error
  - TC-005: Tạo publication - Year không hợp lệ (> năm hiện tại) → Error
  - TC-006: Tạo publication - Title quá dài (> 500 ký tự) → Error
  - TC-007: Tạo publication - Title có ký tự tiếng Việt → OK
  - TC-008: Tạo publication - Title có ký tự đặc biệt → OK hoặc escaped
  - TC-009: Tạo publication - Trùng (title + authors + year) → Cảnh báo?
  - TC-010: Tạo publication - Verify status mặc định = DRAFT
  
  **US-RES-002: Upload file PDF (8 test cases)**
  
  - TC-011: Upload PDF hợp lệ (< 20MB) → Thành công
  - TC-012: Upload PDF quá lớn (> 20MB) → Error "File too large"
  - TC-013: Upload file .docx → Error "Only PDF allowed"
  - TC-014: Upload file .jpg → Error "Only PDF allowed"
  - TC-015: Upload file empty (0 bytes) → Error
  - TC-016: Upload PDF bị corrupt → Error hoặc warning
  - TC-017: Upload bị gián đoạn (mất kết nối) → Xử lý gracefully
  - TC-018: Upload PDF mới để replace PDF cũ → Replace thành công
  
  **US-RES-003: Sửa bài báo nháp (5 test cases)**
  
  - TC-019: Edit DRAFT publication - Thay đổi title → Lưu thành công
  - TC-020: Edit DRAFT - Thay đổi nhiều fields → Lưu thành công
  - TC-021: Edit DRAFT - Nhập dữ liệu không hợp lệ → Validation error
  - TC-022: Edit SUBMITTED publication → Button disabled/error
  - TC-023: 2 users edit cùng lúc → Xử lý conflict
  
  **US-RES-004: Xóa bài báo nháp (4 test cases)**
  
  - TC-024: Delete DRAFT - Confirm → Xóa thành công
  - TC-025: Delete DRAFT - Cancel → Không xóa
  - TC-026: Delete SUBMITTED → Button disabled/error
  - TC-027: Delete publication có PDF → File cũng bị xóa
  
  **US-RES-005: Xem danh sách bài báo (8 test cases)**
  
  - TC-028: View list - Default sort order
  - TC-029: View list - Sort by title (A-Z, Z-A)
  - TC-030: View list - Sort by date (newest first, oldest first)
  - TC-031: View list - Filter by status (DRAFT)
  - TC-032: View list - Filter by year (2024)
  - TC-033: View list - Pagination (10 items/page)
  - TC-034: View list - Empty state (chưa có publications)
  - TC-035: View list - Performance với > 100 publications
  
  **US-RES-006: Thêm đồng tác giả (6 test cases)**
  
  - TC-036: Add co-author - Search by name, thêm thành công
  - TC-037: Add nhiều co-authors → OK
  - TC-038: Reorder co-authors (drag & drop) → Thứ tự thay đổi
  - TC-039: Mark co-author là corresponding author → OK
  - TC-040: Remove co-author → Xóa thành công
  - TC-041: Add external author (không có trong system) → OK
  
  **US-RES-008: Xem chi tiết bài báo (4 test cases)**
  
  - TC-042: View detail - Own publication → OK
  - TC-043: View detail - Publication mình là co-author → OK
  - TC-044: View detail - PDF hiển thị inline → OK
  - TC-045: View detail - PDF quá lớn → Hiện download link
  - TC-046: View detail - PDF bị missing → Error message
  
  **US-RES-009: Download file PDF (3 test cases)**
  
  - TC-047: Download PDF - File hợp lệ → Download thành công
  - TC-048: Download PDF - Filename đúng format
  - TC-049: Download PDF - File missing → Error
  
  **US-RES-024: Xem dashboard giờ làm (6 test cases)**
  
  - TC-050: Dashboard - Hiển thị total work hours
  - TC-051: Dashboard - Filter by "This month"
  - TC-052: Dashboard - Filter by "This year"
  - TC-053: Dashboard - Filter by custom date range
  - TC-054: Dashboard - Breakdown by publication type
  - TC-055: Dashboard - Empty state (chưa có publications)

  **Tổng: ~55 test cases cho V1.0**

---

### 3. Chuẩn Bị Test Environment

- [ ] **Setup Test Accounts**
  ```
  Tạo test users:
  - researcher1 / password123 (người dùng thường)
  - researcher2 / password123 (người dùng khác để test permissions)
  - reviewer1 / password123 (dành cho V3.0 sau này)
  ```

- [ ] **Chuẩn Bị Test Data**
  ```
  Sample publications:
  - Bài báo tiếng Việt: "Nghiên cứu về..."
  - Bài báo tiếng Anh: "Research on..."
  - Publications với các status khác nhau
  
  Sample PDF files:
  - valid_5mb.pdf (để test upload thành công)
  - large_25mb.pdf (để test file quá lớn)
  - corrupted.pdf (để test file bị hỏng)
  - sample.docx (để test format không hợp lệ)
  ```

- [ ] **Setup Testing Tools**
  - Browsers: Chrome (primary), Firefox (optional)
  - Postman hoặc Insomnia cho API testing
  - Screenshot tool: Snagit / Greenshot / Windows Snip
  - Bug tracking: Jira / Trello access

---

## 💻 PHASE 2: DEVELOPMENT

### 4. API Testing (Backend)

- [ ] **Tạo Postman Collections**

  **Collection 1: Authentication**
  ```
  Các test cases:
  - POST /api/auth/login (credentials hợp lệ) → 200, returns JWT
  - POST /api/auth/login (credentials sai) → 401 Unauthorized
  - GET /api/auth/me (có JWT token) → 200, returns user info
  - GET /api/auth/me (không có JWT) → 401 Unauthorized
  ```

  **Collection 2: Publications CRUD**
  ```
  Các test cases:
  - POST /api/publications (data hợp lệ) → 201 Created
  - POST /api/publications (thiếu required field) → 400 Bad Request
  - GET /api/publications (không có auth) → 401
  - GET /api/publications (có auth) → 200, returns list
  - GET /api/publications?status=DRAFT → 200, filtered list
  - GET /api/publications/{id} (exists) → 200
  - GET /api/publications/{id} (không tồn tại) → 404
  - PUT /api/publications/{id} (status=DRAFT) → 200
  - PUT /api/publications/{id} (status=SUBMITTED) → 400
  - DELETE /api/publications/{id} (DRAFT) → 204
  - DELETE /api/publications/{id} (SUBMITTED) → 400
  ```

  **Collection 3: File Upload**
  ```
  Các test cases:
  - POST /api/publications/{id}/upload-pdf (PDF hợp lệ) → 200
  - POST /api/publications/{id}/upload-pdf (file quá lớn) → 400
  - GET /api/publications/{id}/download-pdf → 200, trả về PDF file
  ```

- [ ] **Chạy API Tests Hàng Ngày**
  - Sau mỗi lần backend deploy
  - Log tests thất bại thành bugs

---

### 5. UI Testing (Frontend)

- [ ] **Test Từng Screen Khi Được Develop**

  **Login Page**
  ```
  Checklist:
  - UI match Figma design
  - Username input hoạt động
  - Password input được mask
  - Login button chỉ enabled khi đã nhập đủ
  - Error message hiển thị cho invalid credentials
  - Login thành công redirect đến Dashboard
  ```

  **Dashboard**
  ```
  Checklist:
  - Statistics cards hiển thị đúng data
  - Recent publications table hiển thị 5 items
  - "View All" link hoạt động
  - "Create New" button hoạt động
  ```

  **Publication List**
  ```
  Checklist:
  - Table hiển thị publications
  - Filters hoạt động (status, year)
  - Sorting hoạt động (title, date)
  - Pagination hoạt động
  - Action icons (View, Edit, Delete) visible và hoạt động
  - Empty state hiển thị khi không có data
  ```

  **Create Publication Form**
  ```
  Checklist:
  - Tất cả form fields render đúng
  - Required fields được đánh dấu với *
  - Validation errors hiển thị rõ ràng
  - PDF upload drag & drop hoạt động
  - Co-authors section hoạt động
  - Save button tạo publication thành công
  - Cancel button quay về list
  ```

  **Edit Publication Form**
  ```
  Checklist:
  - Form pre-filled với existing data
  - Có thể modify fields và save
  - Delete button hiện confirmation dialog
  - Chỉ enabled cho DRAFT publications
  ```

  **Publication Detail**
  ```
  Checklist:
  - Metadata hiển thị đầy đủ và đúng
  - PDF viewer hiển thị PDF (nếu có)
  - Download button hoạt động
  - Edit button (nếu DRAFT) hoạt động
  ```

---

### 6. Exploratory Testing

- [ ] **Session 1: "Phá" Create Form**
  ```
  Thử các input bất thường:
  - Emoji trong title: "Bài báo 😀"
  - Text rất dài (> 500 chars)
  - SQL injection strings: "'; DROP TABLE publications; --"
  - XSS scripts: "<script>alert('XSS')</script>"
  - Double-click nút Save (rapid clicking)
  - Browser back button trong khi đang save
  - Refresh page trong khi upload
  
  Document bất kỳ hành vi bất thường nào
  ```

- [ ] **Session 2: "Luồng Điều Hướng"**
  ```
  Test tất cả navigation paths:
  - Dashboard → Create → Save → List
  - List → Detail → Edit → Save → Detail
  - Browser back/forward buttons
  - Logout và login lại
  - Breadcrumbs (nếu có)
  ```

- [ ] **Session 3: "Tính Toàn Vẹn Dữ Liệu"**
  ```
  - Tạo publication, edit, verify changes đã lưu
  - Delete publication, verify đã bị xóa
  - Upload PDF, download, verify file giống nhau
  - Refresh page, verify data không mất
  ```

---

## ✅ PHASE 3: VERIFICATION

### 7. Regression Testing

- [ ] **Chạy Toàn Bộ Test Suite (~55 test cases)**
  ```
  Execution tracking:
  - Pass: Test cases đạt
  - Fail: Test cases fail
  - Blocked: Test cases bị block (do bugs hoặc features chưa có)
  
  Target: 100% pass rate
  ```

- [ ] **Re-test Fixed Bugs**
  ```
  Cho mỗi bug đã fix:
  1. Verify fix hoạt động
  2. Mark bug "Verified" trong Jira
  3. Kiểm tra regression (fix có làm hỏng gì khác không?)
  ```

---

### 8. User Acceptance Testing (UAT)

- [ ] **Collaborate với PM cho UAT**
  ```
  - Chuẩn bị UAT environment (staging server)
  - Chuẩn bị UAT test data
  - Tham gia UAT sessions
  - Log UAT feedback thành bugs/change requests
  ```

---

### 9. Bug Tracking & Reporting

- [ ] **Bug Report Template**

  ```
  BUG-001: Tạo publication thất bại khi title có emoji
  
  Priority: P2 (Medium)
  Severity: Medium
  Environment: Staging, Chrome 120, Windows 11
  
  Steps to Reproduce:
  1. Login với researcher1
  2. Vào trang Create Publication
  3. Nhập title: "Bài báo về AI 😀"
  4. Điền các required fields khác
  5. Click "Save as Draft"
  
  Expected: Publication được tạo thành công
  Actual: Error 500, publication không được tạo
  
  Screenshot: [Đính kèm]
  Assigned To: Backend Developer
  Status: Open
  ```

- [ ] **Tracking Bug Metrics**
  ```
  Dashboard cần track:
  - Total bugs found: __
  - By priority:
    * P0 (Critical): __
    * P1 (High): __
    * P2 (Medium): __
    * P3 (Low): __
  - By status:
    * Open: __
    * In Progress: __
    * Fixed: __
    * Verified: __
    * Closed: __
  ```

---

### 10. Test Summary Report

- [ ] **Tạo Final Test Report**

  ```
  BÁO CÁO TESTING V1.0
  
  1. Tóm Tắt Thực Thi Test:
     - Total test cases: 55
     - Executed: 55
     - Passed: 52 (94.5%)
     - Failed: 3 (5.5%)
     - Blocked: 0
  
  2. Tóm Tắt Bugs:
     - Total bugs: 15
     - P0/Critical: 0 ✅
     - P1/High: 1 (đã fix và verified)
     - P2/Medium: 8 (7 đã fix, 1 defer to V2.0)
     - P3/Low: 6 (3 đã fix, 3 defer)
  
  3. Test Coverage:
     - Functional testing: 100% (tất cả 9 user stories)
     - API testing: 100%
     - UI testing: 100%
     - Cross-browser: Chrome only (Firefox defer)
     - Responsive: Desktop + Tablet tested
  
  4. Known Issues/Limitations:
     - [List các issues đã biết được chấp nhận cho V1.0]
     - Ví dụ: PDF viewer không hoạt động trên Firefox (dùng download thay thế)
  
  5. Khuyến Nghị:
     ✅ Ready for release (với known limitations đã note)
     HOẶC
     ❌ Not ready (còn critical bugs)
  
  6. Sign-Off:
     QA Lead: [Tên] [Chữ ký] [Ngày]
  ```

---

## 🔍 QA Best Practices

### 1. Test Sớm, Test Thường Xuyên
- Đừng đợi đến khi tất cả features hoàn thành
- Test incrementally khi features được develop
- Phát hiện bugs sớm → rẻ hơn để fix

### 2. Suy Nghĩ Như User
- Đừng chỉ test happy paths
- Cố gắng "phá" hệ thống
- Hỏi "What if...?"

### 3. Bug Reports Rõ Ràng
- Luôn bao gồm reproduction steps chi tiết
- Luôn có screenshots/videos (nếu applicable)
- Ghi rõ environment (browser, OS, etc.)

### 4. Good vs. Bad Bug Reports

  ❌ **Báo cáo tệ**: "Create publication không hoạt động"

  ✅ **Báo cáo tốt**: 
  ```
  Title: Create publication fails với 500 error khi title > 500 ký tự
  
  Steps:
  1. Login với researcher1
  2. Vào Create Publication
  3. Nhập title 501 ký tự
  4. Fill các fields khác
  5. Click Save
  
  Expected: Validation error "Title quá dài, max 500 chars"
  Actual: 500 Internal Server Error
  Screenshot: [attached]
  ```

### 5. Đừng Over-Test
- Focus vào V1.0 scope (9 user stories)
- Đừng test features ngoài scope (ví dụ: review workflow - đó là V3.0)

### 6. Giao Tiếp Chủ Động
- Daily standup: Báo cáo test status, blockers
- Alert PM/Dev ngay khi tìm thấy critical bug
- Update bug status promptly

---

## 📊 Testing Tools & Checklists

### Testing Tools:
- **Postman/Insomnia**: API testing
- **Chrome DevTools**: Network, console debugging
- **Jira/Trello**: Bug tracking
- **Snagit/Greenshot**: Screenshots
- **Loom/ShareX**: Screen recording (cho bugs phức tạp)

### Browser Testing:
- ✅ Chrome (latest) - Primary
- ⚠️ Firefox (latest) - Optional cho V1.0
- ❌ Safari - Defer to V2.0
- ❌ Edge - Defer to V2.0

### Device Testing:
- ✅ Desktop (1920x1080, 1366x768)
- ✅ Tablet (1024x768)
- ❌ Mobile - Out of scope cho V1.0

---

## ✅ Tiêu Chí Thành Công

QA làm tốt khi:

✅ Tất cả 9 user stories được test kỹ lưỡng  
✅ Test coverage matrix 100% hoàn thành  
✅ Tất cả critical/high bugs được tìm ra và fix trước release  
✅ Test reports rõ ràng và actionable  
✅ UAT passed by PM  
✅ Không có major bugs escaped to production (sau release)

---

## 📋 Deliverables (Sản Phẩm Bàn Giao)

1. **Test Plan Document** - Test scope, approach, schedule
2. **Test Cases** (55 test cases) - Organized by user story
3. **Bug Reports** - Tất cả bugs logged trong Jira/Trello
4. **Test Execution Report** - Daily status updates
5. **Final Test Summary Report** - Overall results, sign-off

---

**Prepared by**: QA Team  
**Version**: 1.0  
**Last Updated**: 16/02/2026
