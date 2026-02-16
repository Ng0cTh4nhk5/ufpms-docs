# SOP - Business Analyst (BA)
## Version 1.0: Core Publication Management

> 👤 **Vai trò**: Business Analyst  
> 🎯 **Phạm vi**: V1.0 - Phân tích 9 User Stories  
> 📅 **Áp dụng cho**: Requirements Analysis, Documentation

---

## 🎯 Mục Tiêu Tổng Quan

Đảm bảo requirements rõ ràng, đầy đủ, và testable. BA là cầu nối giữa business needs và technical implementation, làm rõ mọi ambiguity trước khi development bắt đầu.

---

## 📋 Trách Nhiệm Chính

### 1. Requirements Analysis
- Phân tách chi tiết 9 user stories
- Define acceptance criteria rõ ràng
- Identify edge cases

### 2. Documentation
- Viết business rules document
- Tạo process flow diagrams
- Document test scenarios

### 3. Collaboration
- Support Dev team với clarifications
- Support QA team với test scenarios
- Review deliverables với business logic

---

## 📐 PHASE 1: DESIGN (Tuần 0-1)

### 1. Phân Tích Chi Tiết User Stories

- [ ] **Template Phân Tích**

  ```
  Cho mỗi user story, document:
  
  1. User Story ID & Title
  2. Business Value (tại sao cần feature này?)
  3. Detailed Description
  4. Acceptance Criteria (danh sách chi tiết)
  5. Business Rules
  6. Edge Cases / Special Scenarios
  7. Dependencies (phụ thuộc user stories khác?)
  8. Test Scenarios (để QA reference)
  ```

- [ ] **US-RES-001: Tạo Bài Báo Mới**

  ```
  Business Value:
  - Cho phép researchers ghi nhận research outputs vào hệ thống
  - Bước đầu tiên trong workflow quản lý publications
  
  Detailed Description:
  - Researcher login vào hệ thống
  - Điều hướng đến "Create New Publication"
  - Điền form với publication metadata
  - Save as DRAFT (không submit ngay)
  
  Acceptance Criteria:
  1. Form có tất cả required fields: Title, Type, Year
  2. Optional fields: Journal Name, Volume, Issue, Pages, DOI, Abstract, Keywords
  3. Validation errors hiển thị inline cho từng field
  4. Save button tạo publication với status = DRAFT
  5. Sau khi save, redirect đếnPublication Detail page hoặc List
  
  Business Rules:
  BR-001: Title max length = 500 characters
  BR-002: Year phải trong khoảng 1900 đến năm hiện tại
  BR-003: Publication Type: JOURNAL, CONFERENCE, BOOK_CHAPTER, OTHER
  BR-004: DOI format (nếu nhập): XX.XXXX/... (basic validation)
  BR-005: Status mặc định = DRAFT khi tạo mới
  
  Edge Cases:
  - User nhập title bằng tiếng Việt có dấu → Cho phép
  - User nhập ký tự đặc biệt trong title → Cho phép (sanitize cho security)
  - User nhập year = 1899 → Error
  - User nhập year = 2027 (năm tương lai) → Error
  - User không chọn Publication Type → Error
  
  Dependencies: None (first feature)
  
  Test Scenarios: (Gửi cho QA)
  - TS-001: Happy path - Tạo publication thành công
  - TS-002: Missing Title → Validation error
  - TS-003: Missing Year → Validation error
  - TS-004: Invalid Year → Validation error
  - TS-005: Title quá dài → Validation error
  ```

- [ ] **US-RES-002: Upload File PDF**

  ```
  Business Value:
  - Lưu trữ full-text của publications
  - Cho phép chia sẻ và download sau này
  
  Detailed Description:
  - Từ Publication Detail page (của own publication)
  - Click "Upload PDF"
  - Select file từ computer
  - File được upload lên server
  - Filename và path lưu vào database
  
  Acceptance Criteria:
  1. Upload button chỉ visible cho own publications
  2. File picker chỉ accept .pdf files
  3. Progress bar hiển thị trong khi upload
  4. Success message sau khi upload xong
  5. PDF preview hiển thị sau khi upload
  
  Business Rules:
  BR-006: Chỉ accept PDF files
  BR-007: Max file size = 20MB
  BR-008: Filename được rename để tránh conflicts
  BR-009: Upload mới sẽ replace PDF cũ (nếu có)
  
  Edge Cases:
  - Upload file .docx → Error "Only PDF allowed"
  - Upload file 25MB → Error "File too large"
  - Upload bị interrupt (mất connection) → Graceful error handling
  - Upload trùng filename → Auto-rename
  
  Test Scenarios:
  - TS-006: Upload PDF hợp lệ → Success
  - TS-007: Upload non-PDF → Error
  - TS-008: Upload quá lớn → Error
  ```

- [ ] **Tương tự cho 7 user stories còn lại...**

  ```
  BA phải document chi tiết cho:
  - US-RES-003: Sửa bài báo nháp
  - US-RES-004: Xóa bài báo nháp
  - US-RES-005: Xem danh sách bài báo
  - US-RES-006: Thêm đồng tác giả
  - US-RES-008: Xem chi tiết bài báo
  - US-RES-009: Download file PDF
  - US-RES-024: Xem dashboard giờ làm
  ```

---

### 2. Business Rules Document (BRD)

- [ ] **Tổng Hợp Tất Cả Business Rules**

  ```
  BUSINESS RULES DOCUMENT - V1.0
  
  1. Publication Rules
     BR-001: Title max length = 500 chars
     BR-002: Year range: 1900 - current year
     BR-003: Publication Types: JOURNAL, CONFERENCE, BOOK_CHAPTER, OTHER
     BR-004: DOI format: XX.XXXX/...
     BR-005: Default status = DRAFT
     BR-006: Chỉ DRAFT publications có thể edit/delete
     BR-007: Status không thể thay đổi directly (submit button sẽ change status)
  
  2. File Upload Rules
     BR-008: File type: PDF only
     BR-009: Max size: 20MB
     BR-010: Filename auto-rename để avoid conflicts
     BR-011: Upload mới replaces old PDF
  
  3. Co-Author Rules
     BR-012: Co-authors ordered by sequence (1st author, 2nd author, etc.)
     BR-013: Có thể add internal users (search by name) hoặc external (manual entry)
     BR-014: Mỗi publication có thể có 1 corresponding author (flag)
     BR-015: Creator của publication tự động là main author (không cần add)
  
  4. Authorization Rules
     BR-016: User chỉ xem/edit own publications + publications mình là co-author
     BR-017: User không thể edit/delete publications của người khác
     BR-018: Status != DRAFT không thể edit/delete (read-only)
  
  5. Dashboard Rules
     BR-019: Work hours calculation:
                 - JOURNAL articles: 40 giờ/article
                 - CONFERENCE papers: 20 giờ/paper
                 - BOOK_CHAPTER: 60 giờ/chapter
                 - OTHER: 10 giờ
     BR-020: Dashboard chỉ tính publications với status = PUBLISHED
     BR-021: Filter by date range: "This Month", "This Year", "Custom"
  
  6. Validation Rules
     BR-022: Required fields cannot be empty
     BR-023: Email format: standard email regex
     BR-024: Year: Integer only, no decimals
  ```

---

### 3. Process Flow Diagrams

- [ ] **Vẽ Process Flows Chính**

  **Flow 1: Create Publication**
  ```
  [Start] 
    ↓
  [User clicks "Create New"]
    ↓
  [System shows Create Form]
    ↓
  [User fills required fields]
    ↓
  [User clicks "Save as Draft"]
    ↓
  <Validation OK?> 
    No → [Show errors] → (back to fill form)
    Yes ↓
  [System creates Publication (status=DRAFT)]
    ↓
  [System redirects to Detail page]
    ↓
  [End]
  ```

  **Flow 2: Upload PDF**
  ```
  [Start - User on Publication Detail page]
    ↓
  <Is own publication?> 
    No → [Hide Upload button] → [End]
    Yes ↓
  [User clicks "Upload PDF"]
    ↓
  [System shows file picker]
    ↓
  [User selects file]
    ↓
  <File valid? (PDF, < 20MB)>
    No → [Show error] → [End]
    Yes ↓
  [System uploads file]
    ↓
  [System saves filename & path to DB]
    ↓
  [System shows PDF preview]
    ↓
  [End]
  ```

  **Flow 3: Edit Publication**
  ```
  [Start - User on Detail page]
    ↓
  <Status = DRAFT?>
    No → [Edit button disabled] → [End]
    Yes ↓
  [User clicks "Edit"]
    ↓
  [System shows Edit Form pre-filled]
    ↓
  [User modifies fields]
    ↓
  [User clicks "Save"]
    ↓
  <Validation OK?>
    No → [Show errors]
    Yes ↓
  [System updates publication]
    ↓
  [System redirects back to Detail]
    ↓
  [End]
  ```

---

### 4. Screen Requirements

- [ ] **Detailed Screen Specs (6 Screens)**

  **Screen 1: Login**
  ```
  Elements:
  - Logo (top center)
  - Title: "UFPMS Login"
  - Username input (required)
  - Password input (required, masked)
  - "Login" button
  - Error message area (if login fails)
  
  Behaviors:
  - Login button disabled until both fields filled
  - On success: Redirect to Dashboard
  - On fail: Show error "Invalid credentials"
  ```

  **Screen 2: Dashboard**
  ```
  Elements:
  - Header: "Dashboard", User info (top right), Logout button
  - Statistics Cards (Grid 2x2):
    * Total Publications
    * Published Count
    * Draft Count
    * Total Work Hours
  - Recent Publications table (5 items)
  - "Create New" floating button (bottom right)
  
  Behaviors:
  - Statistics auto-load on page load
  - Click table row → Navigate to Detail
  - Click "Create New" → Navigate to Create Form
  ```

  **Screen 3: Publication List**
  ```
  Elements:
  - Header: "My Publications"
  - Filters: Status dropdown, Year input, Search box
  - "Create New" button (top right)
  - Data table: Title, Year, Status (badge), Created Date, Actions (icons)
  - Pagination controls (bottom)
  - Empty state: "No publications yet"
  
  Behaviors:
  - Filters apply on change (auto-reload data)
  - Click row → Navigate to Detail
  - Action icons:
    * Eye icon → View detail
    * Pencil icon → Edit (chỉ cho DRAFT)
    * Trash icon → Delete (chỉ cho DRAFT)
  - Pagination: 10 items/page, navigate between pages
  ```

  **Screen 4 & 5: Create/Edit Publication**
  ```
  Elements:
  - Page title: "Create Publication" hoặc "Edit Publication"
  - Form (Grid 2 columns):
    * Publication Type (dropdown) - required
    * Title (text input, full width) - required
    * Year (number input) - required
    * Journal/Conference Name
    * Volume, Issue, Pages
    * DOI
    * Abstract (textarea, full width)
    * Keywords (text input)
  - Co-Authors section
  - PDF Upload section
  - Buttons: "Save as Draft", "Cancel"
  - (Edit mode only) "Delete" button (red, confirm dialog)
  
  Behaviors:
  - Validation on blur (per field)
  - Validation on submit
  - Save → Create/Update publication, redirect to Detail
  - Cancel → Go back to List
  - Delete → Confirm dialog, then delete, redirect to List
  ```

  **Screen 6: Publication Detail**
  ```
  Layout: 2 columns
  
  Left column (60%): PDF Viewer
  - iframe showing PDF (if uploaded)
  - Fallback: "No PDF uploaded. Click to upload."
  
  Right column (40%): Metadata Panel
  - Publication Info (Type, Year, Journal, etc.)
  - Authors list
  - Abstract
  - Keywords
  - Status badge
  - File info (filename, size, upload date)
  - Actions: "Edit" button (if DRAFT), "Download PDF", "Back"
  
  Behaviors:
  - PDF viewer loads PDF file
  - Edit button → Navigate to Edit form
  - Download PDF → Trigger download
  - Back → Go to List
  ```

---

### 5. Test Scenarios Document

- [ ] **Tạo Test Scenarios cho QA**

  ```
  Mỗi test scenario mô tả 1 user journey:
  
  TS-001: Complete workflow - Create → Upload → View
  Precondition: User logged in
  Steps:
  1. Go to Dashboard
  2. Click "Create New"
  3. Fill form: Title="Test", Type=JOURNAL, Year=2024
  4. Click "Save as Draft"
  5. Verify: Redirected to Detail page
  6. Click "Upload PDF"
  7. Select valid PDF file
  8. Verify: PDF displays in viewer
  Expected: All steps succeed
  
  TS-002: Edit workflow - Edit title → Save
  Precondition: DRAFT publication exists
  Steps:
  1. Go to Publication List
  2. Click Edit icon
  3. Change title to "Updated Title"
  4. Click "Save"
  5. Verify: Title updated in Detail view
  Expected: Title updated successfully
  
  ... (Total ~30 test scenarios cho all user journeys)
  ```

---

## 💻 PHASE 2: DEVELOPMENT (Tuần 2-4)

### 6. Hỗ Trợ Development Team

- [ ] **Clarify Ambiguities**

  ```
  Dev team sẽ có questions. BA phải luôn available để trả lời:
  
  Example questions:
  Q: "Nếu user nhập title 501 characters thì error message nên là gì?"
  A: "Title cannot exceed 500 characters"
  
  Q: "Khi delete publication, có cần confirm dialog không?"
  A: "Có, confirm: 'Are you sure you want to delete this publication?'"
  
  Q: "PDF viewer hiển thị như thế nào nếu file quá lớn?"
  A: "Nếu > 10MB, show download link thay vì inline preview"
  
  Response time: < 4 hours (trong business hours)
  Document câu trả lời để reference sau
  ```

- [ ] **Participate trong Sprint Reviews (Nếu Agile)**

  ```
  Review completed user stories:
  - Demo có match acceptance criteria không?
  - Business logic đúng không?
  - Edge cases được handle chưa?
  
  Provide feedback:
  - "This looks good, approval"
  - "Issue: Error message không rõ ràng, cần sửa"
  - "Missing: Co-author ordering không hoạt động"
  ```

---

## ✅ PHASE 3: VERIFICATION (Tuần 5-6)

### 7. Support QA Testing

- [ ] **Answer QA Questions**

  ```
  QA sẽ hỏi để clarify expected behaviors:
  
  Q: "Khi user upload PDF lần 2, file cũ có bị xóa không?"
  A: "Có, file mới sẽ replace file cũ"
  
  Q: "Dashboard work hours có tính publications với status DRAFT không?"
  A: "Không, chỉ tính PUBLISHED"
  ```

- [ ] **Review Bug Reports**

  ```
  Verify bugs QA tìm ra có phải là bugs thật hay expected behavior:
  
  Bug Report: "User không thể delete SUBMITTED publication"
  BA Review: "This is expected behavior per BR-006, not a bug"
  → Close as "Working as Intended"
  
  Bug Report: "Year field accepts letters"
  BA Review: "This is a real bug, should only accept numbers"
  → Confirm bug, assign to Dev
  ```

---

### 8. UAT Support

- [ ] **Participate trong UAT Sessions**

  ```
  - Prepare test data for stakeholders
  - Guide stakeh,olders through test scenarios
  - Document UAT feedback
  
  UAT Feedback Example:
  - "Feature works great!"
  - "Request: Can we add a 'Duplicate' button?" → Note cho V2.0
  - "Issue: DOI field should allow longer format" → Evaluate: Bug hay change request?
  ```

---

### 9. Document Assumptions & Decisions

- [ ] **Assumptions Log**

  ```
  Document assumptions made during development:
  
  ASSUMPTION-001: V1.0 assumes users know what DOI is (no help text)
  → Future: Add tooltip in V2.0
  
  ASSUMPTION-002: PDF viewer works on Chrome (primary browser)
  → Firefox support deferred to V2.0
  
  ASSUMPTION-003: Max 10 co-authors per publication
  → Document in business rules if confirmed
  ```

---

## ✅ Tiêu Chí Thành Công

BA làm tốt khi:

✅ Tất cả 9 user stories có acceptance criteria rõ ràng  
✅ Business rules document đầy đủ  
✅ Process flows giúp team hiểu workflows  
✅ Test scenarios giúp QA coverage 100%  
✅ Dev team không bị blocked vì ambiguous requirements  
✅ UAT sign-off nhận được vì features match expectations

---

## 📋 Deliverables (Sản Phẩm Bàn Giao)

1. **Detailed User Stories** - 9 user stories với acceptance criteria đầy đủ
2. **Business Rules Document (BRD)** - Tất cả business rules
3. **Process Flow Diagrams** - Workflows chính
4. **Test Scenarios Document** - Cho QA reference
5. **Screen Requirements** - Chi tiết cho 6 screens
6. **Assumptions Log** - Decisions & assumptions documented
7. **UAT Sign-Off** - Stakeholder approval

---

## 🔍 BA Best Practices

### 1. Be Specific
- Tránh ngôn ngữ mơ hồ
- ❌ "System should be user-friendly"
- ✅ "Error messages must clearly state what field is invalid and why"

### 2. Think in Edge Cases
- Đừng chỉ document happy paths
- Hỏi "What if...?" cho mọi scenario

### 3. Collaborate Early
- Involve QA trong requirements phase
- Involve UI/UX để align screen requirements vs. designs

### 4. Single Source of Truth
- Tất cả requirements phải documented
- Avoid "Anh X nói trong meeting" mà không có written record

---

**Prepared by**: Business Analysis Team  
**Version**: 1.0  
**Last Updated**: 16/02/2026
