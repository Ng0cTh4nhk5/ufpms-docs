# User Stories - Researcher

> 👤 **Role**: Researcher (Giảng viên)  
> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục tiêu**: Quản lý bài báo khoa học và theo dõi tiến độ phê duyệt

---

## Tổng Quan

**Total Stories**: 28  
**P0 (Must Have)**: 18  
**P1 (Should Have)**: 7  
**P2 (Nice to Have)**: 3

---

## Module 1: Publication Management

### US-RES-001: Tạo Bài Báo Mới
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-PUB-001

**User Story**:
```
As a researcher (Là một giảng viên),
I want to create a new publication entry with required metadata (Tôi muốn tạo mới một bài báo với các thông tin bắt buộc),
So that I can submit it for review and eventual publication (Để tôi có thể gửi nó đi xét duyệt và công bố sau này).
```

**Acceptance Criteria**:
```
GIVEN I am logged in as a researcher (KHI tôi đã đăng nhập với vai trò giảng viên)
WHEN I click "Add New Publication" (VÀ tôi nhấn nút "Thêm bài báo mới")
THEN I see a form with required fields (Title, Authors, Year, Journal Type) (THÌ tôi thấy một biểu mẫu với các trường bắt buộc: Tiêu đề, Tác giả, Năm, Loại tạp chí)
AND optional fields (DOI, ISSN, Abstract, Keywords, PDF) (VÀ các trường tùy chọn: DOI, ISSN, Tóm tắt, Từ khóa, File PDF)
AND the publication status is set to DRAFT by default (VÀ trạng thái bài báo được đặt mặc định là DRAFT - Nháp)
```

---

### US-RES-002: Upload File PDF
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-PUB-002

**User Story**:
```
As a researcher (Là một giảng viên),
I want to upload the PDF file of my publication (Tôi muốn tải lên file PDF của bài báo),
So that reviewers and readers can access the full text (Để người duyệt và người đọc có thể truy cập toàn văn).
```

**Acceptance Criteria**:
```
GIVEN I am creating or editing a publication (KHI tôi đang tạo hoặc chỉnh sửa bài báo)
WHEN I select a PDF file (< 10MB) and upload it (VÀ tôi chọn một file PDF < 10MB và tải lên)
THEN the file is uploaded to the server (THÌ file được tải lên máy chủ)
AND the path is saved to database (VÀ đường dẫn được lưu vào cơ sở dữ liệu)
AND I see a preview thumbnail (VÀ tôi thấy hình thu nhỏ xem trước)
AND I can download it again to verify (VÀ tôi có thể tải xuống lại để kiểm tra)
```

---

### US-RES-003: Sửa Bài Báo Nháp
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-PUB-004

**User Story**:
```
As a researcher (Là một giảng viên),
I want to edit my draft or revision-required publications (Tôi muốn chỉnh sửa các bài báo nháp hoặc bài cần chỉnh sửa),
So that I can correct errors or add missing information (Để tôi có thể sửa lỗi hoặc bổ sung thông tin thiếu).
```

**Acceptance Criteria**:
```
GIVEN my publication is in DRAFT or REVISION_REQUIRED status (KHI bài báo của tôi ở trạng thái NHÁP hoặc YÊU CẦU CHỈNH SỬA)
AND I am the owner (VÀ tôi là người sở hữu)
WHEN I edit the information and click Save (VÀ tôi chỉnh sửa thông tin rồi nhấn Lưu)
THEN the database is updated (THÌ cơ sở dữ liệu được cập nhật)
AND an audit log is created (who edited, when) (VÀ nhật ký hệ thống được tạo: ai sửa, khi nào)
AND I see "Saved successfully" message (VÀ tôi thấy thông báo "Lưu thành công")
```

---

### US-RES-004: Xóa Bài Báo Nháp
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-PUB-005

**User Story**:
```
As a researcher (Là một giảng viên),
I want to delete my draft publications (Tôi muốn xóa các bài báo nháp của mình),
So that I can remove entries I no longer want to submit (Để tôi có thể loại bỏ các mục tôi không còn muốn nộp nữa).
```

**Acceptance Criteria**:
```
GIVEN my publication is in DRAFT status (KHI bài báo của tôi ở trạng thái NHÁP)
AND I am the owner (VÀ tôi là người sở hữu)
WHEN I click "Delete" and confirm (VÀ tôi nhấn "Xóa" và xác nhận)
THEN the publication is soft deleted (deleted_at timestamp set) (THÌ bài báo bị xóa mềm - đặt thời gian deleted_at)
AND the PDF file is removed from storage (VÀ file PDF bị xóa khỏi bộ nhớ)
AND I am redirected to my publications list (VÀ tôi được chuyển hướng về danh sách bài báo của mình)
```

---

### US-RES-005: Xem Danh Sách Bài Báo
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-PUB-006

**User Story**:
```
As a researcher (Là một giảng viên),
I want to view all my publications filtered by status (Tôi muốn xem tất cả bài báo của mình được lọc theo trạng thái),
So that I can easily find and manage them (Để tôi có thể dễ dàng tìm và quản lý chúng).
```

**Acceptance Criteria**:
```
GIVEN I am logged in as a researcher (KHI tôi đã đăng nhập với vai trò giảng viên)
WHEN I go to "My Publications" (VÀ tôi vào trang "Bài báo của tôi")
THEN I see my publications list with: (THÌ tôi thấy danh sách bài báo với:)
- Filter options: All / Draft / Submitted / Approved / Rejected (Tùy chọn lọc: Tất cả / Nháp / Đã nộp / Đã duyệt / Bị từ chối)
- Sort: Newest first (Sắp xếp: Mới nhất trước)
- Columns: Title, Status, Update Date, Actions (Edit/Delete/View) (Các cột: Tiêu đề, Trạng thái, Ngày cập nhật, Hành động)
```

---

### US-RES-006: Thêm Đồng Tác Giả
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-PUB-007

**User Story**:
```
As a researcher (Là một giảng viên),
I want to add co-authors from my university to my publication (Tôi muốn thêm đồng tác giả từ trường của mình vào bài báo),
So that we are all properly credited for our collaborative work (Để tất cả chúng tôi đều được ghi nhận đúng mức cho công việc hợp tác).
```

**Acceptance Criteria**:
```
GIVEN I am creating or editing a publication (KHI tôi đang tạo hoặc chỉnh sửa bài báo)
WHEN I type a researcher's name in the co-authors field (VÀ tôi nhập tên giảng viên vào trường đồng tác giả)
THEN I see autocomplete suggestions from the system's user list (THÌ tôi thấy gợi ý tự động từ danh sách người dùng hệ thống)
AND I can add them to the co-authors list (VÀ tôi có thể thêm họ vào danh sách đồng tác giả)
AND I can remove co-authors from the list (VÀ tôi có thể xóa đồng tác giả khỏi danh sách)
AND I cannot remove myself as the corresponding author (VÀ tôi không thể xóa chính mình khỏi vai trò tác giả liên hệ)
```

---

### US-RES-007: Gắn Tags/Keywords
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-PUB-008

**User Story**:
```
As a researcher (Là một giảng viên),
I want to add keywords/tags to my publication (Tôi muốn thêm từ khóa/thẻ cho bài báo của mình),
So that it can be easily found through search (Để nó có thể dễ dàng được tìm thấy qua tìm kiếm).
```

**Acceptance Criteria**:
```
GIVEN I am creating or editing a publication (KHI tôi đang tạo hoặc chỉnh sửa bài báo)
WHEN I enter keywords separated by commas (VÀ tôi nhập từ khóa phân cách bằng dấu phẩy)
THEN they are saved as an array (THÌ chúng được lưu dưới dạng mảng)
AND displayed as colored tags (VÀ hiển thị dưới dạng thẻ màu)
AND I can remove individual tags by clicking X (VÀ tôi có thể xóa từng thẻ bằng cách nhấn X)
```

---

### US-RES-008: Xem Chi Tiết Bài Báo
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-PUB-010

**User Story**:
```
As a researcher (Là một giảng viên),
I want to view all details of my publication (Tôi muốn xem tất cả chi tiết bài báo của mình),
So that I can review the complete information and status (Để tôi có thể xem lại toàn bộ thông tin và trạng thái).
```

**Acceptance Criteria**:
```
GIVEN I have permission to view a publication (owner/admin/reviewer) (KHI tôi có quyền xem bài báo - chủ sở hữu/admin/người duyệt)
WHEN I click "View Details" (VÀ tôi nhấn "Xem chi tiết")
THEN I see all metadata, current status, review history (if any), (THÌ tôi thấy tất cả metadata, trạng thái hiện tại, lịch sử duyệt nếu có)
AND PDF file link (if uploaded) (VÀ link file PDF nếu đã tải lên)
AND DOI link (if available) (VÀ link DOI nếu có)
```

---

### US-RES-009: Download File PDF
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-PUB-011

**User Story**:
```
As a researcher (Là một giảng viên),
I want to download the PDF of my publication (Tôi muốn tải xuống file PDF của bài báo),
So that I can verify the uploaded file or share it offline (Để tôi có thể kiểm tra file đã tải lên hoặc chia sẻ offline).
```

**Acceptance Criteria**:
```
GIVEN the publication has a PDF file (KHI bài báo có file PDF)
AND I have permission to view it (owner/admin/reviewer/or PUBLISHED) (VÀ tôi có quyền xem - chủ sở hữu/admin/người duyệt/hoặc ĐÃ CÔNG BỐ)
WHEN I click "Download PDF" (VÀ tôi nhấn "Tải PDF")
THEN the file is downloaded to my computer (THÌ file được tải xuống máy tính của tôi)
AND an audit log records who downloaded it and when (VÀ nhật ký hệ thống ghi lại ai đã tải và khi nào)
```

---

## Module 2: Approval Workflow (Researcher Actions)

### US-RES-010: Nộp Xét Duyệt
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-001

**User Story**:
```
As a researcher (Là một giảng viên),
I want to submit my publication for review (Tôi muốn nộp bài báo để xét duyệt),
So that it can go through the approval process and be published (Để nó có thể đi qua quy trình phê duyệt và được công bố).
```

**Acceptance Criteria**:
```
GIVEN my publication is in DRAFT status (KHI bài báo của tôi ở trạng thái NHÁP)
AND all required fields are filled (Title, Authors, Journal, Year, PDF) (VÀ tất cả các trường bắt buộc đã được điền: Tiêu đề, Tác giả, Tạp chí, Năm, PDF)
WHEN I click "Submit for Review" (VÀ tôi nhấn "Nộp để xét duyệt")
THEN the status changes from DRAFT to SUBMITTED (THÌ trạng thái chuyển từ NHÁP sang ĐÃ NỘP)
AND an email is sent to the Faculty Reviewer (VÀ email được gửi đến Cán bộ duyệt Khoa)
AND an audit log is created (VÀ nhật ký hệ thống được tạo)
AND I see "Submitted successfully" message (VÀ tôi thấy thông báo "Nộp thành công")
```

---

### US-RES-011: Xem Trạng Thái Xét Duyệt
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-002

**User Story**:
```
As a researcher (Là một giảng viên),
I want to track the review status of my submitted publication (Tôi muốn theo dõi trạng thái xét duyệt của bài báo đã nộp),
So that I know where it is in the approval process (Để tôi biết nó đang ở đâu trong quy trình phê duyệt).
```

**Acceptance Criteria**:
```
GIVEN I have submitted a publication (KHI tôi đã nộp một bài báo)
WHEN I view its details (VÀ tôi xem chi tiết của nó)
THEN I see a visual timeline: DRAFT → SUBMITTED → REVIEWING → APPROVED (THÌ tôi thấy dòng thời gian trực quan: NHÁP -> ĐÃ NỘP -> ĐANG DUYỆT -> ĐÃ DUYỆT)
AND the current status is highlighted (VÀ trạng thái hiện tại được làm nổi bật)
AND I can see reviewer comments (if any) (VÀ tôi có thể thấy nhận xét của người duyệt nếu có)
AND the date of each status transition (VÀ ngày của mỗi lần chuyển trạng thái)
```

---

### US-RES-012: Chỉnh Sửa Theo Yêu Cầu
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-003

**User Story**:
```
As a researcher (Là một giảng viên),
I want to revise my publication based on reviewer feedback (Tôi muốn chỉnh sửa bài báo dựa trên phản hồi của người duyệt),
So that I can address concerns and resubmit for approval (Để tôi có thể giải quyết các vấn đề và nộp lại để xét duyệt).
```

**Acceptance Criteria**:
```
GIVEN my publication is in REVISION_REQUIRED status (KHI bài báo của tôi ở trạng thái YÊU CẦU CHỈNH SỬA)
AND there are comments from the reviewer (VÀ có nhận xét từ người duyệt)
WHEN I make edits and click "Resubmit" (VÀ tôi thực hiện chỉnh sửa và nhấn "Nộp lại")
THEN the status changes from REVISION_REQUIRED to SUBMITTED (THÌ trạng thái chuyển từ YÊU CẦU CHỈNH SỬA sang ĐÃ NỘP)
AND an email is sent to the Faculty Reviewer: "Revised and resubmitted" (VÀ email được gửi đến Cán bộ duyệt Khoa: "Đã sửa và nộp lại")
AND an audit log is created (VÀ nhật ký hệ thống được tạo)
```

---

### US-RES-013: Rút Lại Đơn Nộp
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-APR-019

**User Story**:
```
As a researcher (Là một giảng viên),
I want to withdraw my submission before it's approved (Tôi muốn rút lại bài nộp trước khi được duyệt),
So that I can make significant changes or reconsider submission (Để tôi có thể thay đổi lớn hoặc cân nhắc lại việc nộp).
```

**Acceptance Criteria**:
```
GIVEN my publication is in SUBMITTED or FACULTY_REVIEWING status (KHI bài báo của tôi ở trạng thái ĐÃ NỘP hoặc KHOA ĐANG DUYỆT)
WHEN I click "Withdraw" and confirm (VÀ tôi nhấn "Rút lại" và xác nhận)
THEN the status changes back to DRAFT (THÌ trạng thái chuyển về NHÁP)
AND an email is sent to the reviewer (if already reviewing) (VÀ email được gửi đến người duyệt nếu đang duyệt)
AND an audit log is created (VÀ nhật ký hệ thống được tạo)
```

---

## Module 4: Researcher Profile

### US-RES-014: Xem Profile Công Khai Của Mình
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-PRO-001

**User Story**:
```
As a researcher (Là một giảng viên),
I want to view my public profile page (Tôi muốn xem trang hồ sơ công khai của mình),
So that I can see how my information and publications appear to others (Để tôi có thể xem thông tin và bài báo của mình hiển thị thế nào với người khác).
```

**Acceptance Criteria**:
```
GIVEN I have at least 1 PUBLISHED publication (KHI tôi có ít nhất 1 bài báo ĐÃ CÔNG BỐ)
WHEN I access /profile/[my-username] (VÀ tôi truy cập /profile/[tên-đăng-nhập-của-tôi])
THEN I see my profile photo, name, title, faculty, (THÌ tôi thấy ảnh đại diện, tên, chức danh, khoa,)
AND contact info (email, ORCID), (VÀ thông tin liên hệ - email, ORCID,)
AND bio/research interests, (VÀ tiểu sử/hướng nghiên cứu,)
AND list of PUBLISHED publications only, (VÀ danh sách bài báo ĐÃ CÔNG BỐ,)
AND a chart showing publications by year (VÀ biểu đồ bài báo theo năm)
AND a word cloud from my keywords (VÀ word cloud từ các từ khóa của tôi)
```

---

### US-RES-015: Chỉnh Sửa Profile
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-PRO-002

**User Story**:
```
As a researcher (Là một giảng viên),
I want to edit my public profile information (Tôi muốn chỉnh sửa thông tin hồ sơ công khai),
So that I can keep my professional information up to date (Để tôi có thể cập nhật thông tin chuyên môn của mình).
```

**Acceptance Criteria**:
```
GIVEN I am logged in (KHI tôi đã đăng nhập)
WHEN I go to "Edit Profile" (VÀ tôi vào trang "Sửa hồ sơ")
THEN I can edit: Profile photo, Bio (max 500 chars), Research interests, (THÌ tôi có thể sửa: Ảnh, Tiểu sử - tối đa 500 ký tự, Hướng nghiên cứu,)
ORCID, Google Scholar link, Personal website (ORCID, Link Google Scholar, Website cá nhân)
AND changes are saved when I click "Save" (VÀ thay đổi được lưu khi tôi nhấn "Lưu")
```

---

### US-RES-016: Xem Danh Sách Bài Báo Trên Profile
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-PRO-003

**User Story**:
```
As a researcher (Là một giảng viên),
I want my publications displayed on my profile page (Tôi muốn bài báo của mình hiển thị trên trang hồ sơ),
So that visitors can see my research output (Để khách truy cập có thể thấy kết quả nghiên cứu của tôi).
```

**Acceptance Criteria**:
```
GIVEN I am viewing my public profile (KHI tôi đang xem hồ sơ công khai của mình)
WHEN the page loads (VÀ trang tải xong)
THEN I see my publications (PUBLISHED only) sorted by year (newest first) (THÌ tôi thấy bài báo của mình - CHỈ ĐÃ CÔNG BỐ - sắp xếp theo năm, mới nhất trước)
AND I can filter by type (Journal/Conference) (VÀ tôi có thể lọc theo loại: Tạp chí/Hội nghị)
AND each entry shows: Title, Journal, Year, DOI link (VÀ mỗi mục hiện: Tiêu đề, Tạp chí, Năm, Link DOI)
AND visitors can click to view details (VÀ khách có thể nhấn xem chi tiết)
```

---

## Advanced Features

### US-RES-017: Validate DOI Format
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-PUB-012

**User Story**:
```
As a researcher (Là một giảng viên),
I want the system to validate my DOI format (Tôi muốn hệ thống kiểm tra định dạng DOI),
So that I don't submit publications with incorrect DOI (Để tôi không nộp bài báo với DOI sai).
```

**Acceptance Criteria**:
```
GIVEN I am entering a DOI in the publication form (KHI tôi nhập DOI vào form bài báo)
WHEN I move to the next field (blur) (VÀ tôi chuyển sang trường tiếp theo)
THEN the system validates the format (10.xxxx/xxxxx) (THÌ hệ thống kiểm tra định dạng 10.xxxx/xxxxx)
AND shows an error message if incorrect (VÀ hiện thông báo lỗi nếu sai)
AND creates a clickable link to https://doi.org/[DOI] if correct (VÀ tạo link https://doi.org/[DOI] nếu đúng)
```

---

### US-RES-018: Validate ISSN Format
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-PUB-013

**User Story**:
```
As a researcher (Là một giảng viên),
I want the system to validate the ISSN format (Tôi muốn hệ thống kiểm tra định dạng ISSN),
So that I enter correct journal ISSN numbers (Để tôi nhập đúng số ISSN của tạp chí).
```

**Acceptance Criteria**:
```
GIVEN I am entering an ISSN in the publication form (KHI tôi nhập ISSN vào form)
WHEN I move to the next field (VÀ tôi chuyển sang trường tiếp theo)
THEN the system validates the format (xxxx-xxxx) (THÌ hệ thống kiểm tra định dạng xxxx-xxxx)
AND shows an error message if incorrect (VÀ hiện thông báo lỗi nếu sai)
```

---

### US-RES-019: Cảnh Báo Trùng Lặp
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-PUB-014

**User Story**:
```
As a researcher (Là một giảng viên),
I want to be notified if a publication with the same DOI already exists (Tôi muốn được thông báo nếu bài báo có cùng DOI đã tồn tại),
So that I can add myself as co-author instead of creating a duplicate (Để tôi có thể thêm mình làm đồng tác giả thay vì tạo bản trùng lặp).
```

**Acceptance Criteria**:
```
GIVEN I enter a DOI that already exists in the system (KHI tôi nhập DOI đã tồn tại trong hệ thống)
WHEN I save the publication (VÀ tôi lưu bài báo)
THEN I see a warning: "This publication has been entered by [Researcher Name]" (THÌ tôi thấy cảnh báo: "Bài báo này đã được nhập bởi [Tên giảng viên]")
AND a suggestion: "Would you like to add yourself as co-author?" (VÀ gợi ý: "Bạn có muốn thêm mình làm đồng tác giả không?")
```

---

### US-RES-020: Auto-Fetch Metadata từ DOI
**Priority**: 🟢 P2 - Nice to Have  
**Related FR**: FR-PUB-003

**User Story**:
```
As a researcher (Là một giảng viên),
I want to automatically fetch publication metadata from DOI (Tôi muốn tự động lấy thông tin bài báo từ DOI),
So that I don't have to manually enter all information (Để tôi không phải nhập thủ công tất cả thông tin).
```

**Acceptance Criteria**:
```
GIVEN I have entered a valid DOI (10.xxxx/xxxxx) (KHI tôi đã nhập DOI hợp lệ)
WHEN I click "Fetch from DOI" (VÀ tôi nhấn "Lấy dữ liệu từ DOI")
THEN the system calls CrossRef API (THÌ hệ thống gọi API CrossRef)
AND auto-fills: Title, Authors, Journal, Year, ISSN (VÀ tự động điền: Tiêu đề, Tác giả, Tạp chí, Năm, ISSN)
AND allows me to manually edit the auto-filled data (VÀ cho phép tôi chỉnh sửa dữ liệu đã điền)
```

---

### US-RES-021: Import từ ORCID
**Priority**: 🟢 P2 - Nice to Have  
**Related FR**: FR-PUB-015

**User Story**:
```
As a researcher (Là một giảng viên),
I want to import my publications from my ORCID profile (Tôi muốn import bài báo từ hồ sơ ORCID của mình),
So that I can quickly add my existing publications to the system (Để tôi có thể nhanh chóng thêm các bài báo hiện có vào hệ thống).
```

**Acceptance Criteria**:
```
GIVEN I have linked my ORCID account (KHI tôi đã liên kết tài khoản ORCID)
WHEN I click "Import from ORCID" (VÀ tôi nhấn "Import từ ORCID")
THEN the system calls ORCID API (THÌ hệ thống gọi API ORCID)
AND displays a list of my publications (VÀ hiển thị danh sách bài báo của tôi)
AND I can select which ones to import (VÀ tôi có thể chọn bài nào để import)
AND metadata is auto-filled for selected publications (VÀ metadata được tự động điền cho các bài đã chọn)
```

---

### US-RES-022: Xem Biểu Đồ Năng Suất
**Priority**: 🟢 P2 - Nice to Have  
**Related FR**: FR-PRO-004

**User Story**:
```
As a researcher (Là một giảng viên),
I want to see charts of my publication productivity (Tôi muốn xem biểu đồ năng suất bài báo của mình),
So that I can visualize my research output over time (Để tôi có thể trực quan hóa kết quả nghiên cứu theo thời gian).
```

**Acceptance Criteria**:
```
GIVEN I am viewing my profile (KHI tôi đang xem hồ sơ của mình)
WHEN the analytics section loads (VÀ phần phân tích tải xong)
THEN I see: (THÌ tôi thấy:)
- Bar chart: Publications per year (Biểu đồ cột: Bài báo theo năm)
- Pie chart: Publications by journal type (Q1/Q2/Q3/Q4/Conference) (Biểu đồ tròn: Bài báo theo loại tạp chí)
- Highlight: Most productive years (Nổi bật: Những năm năng suất nhất)
```

---

### US-RES-023: Xem Word Cloud Lĩnh Vực
**Priority**: 🟢 P2 - Nice to Have  
**Related FR**: FR-PRO-005

**User Story**:
```
As a researcher (Là một giảng viên),
I want to see a word cloud of my research fields (Tôi muốn xem word cloud các lĩnh vực nghiên cứu của mình),
So that I can visualize my areas of expertise (Để tôi có thể hình dung các lĩnh vực chuyên môn của mình).
```

**Acceptance Criteria**:
```
GIVEN I am viewing my profile (KHI tôi đang xem hồ sơ của mình)
WHEN the page loads (VÀ trang tải xong)
THEN I see a word cloud generated from: (THÌ tôi thấy word cloud được tạo từ:)
- Keywords of all my publications (Từ khóa của tất cả bài báo)
- Frequent words in abstracts (Các từ thường gặp trong tóm tắt)
AND font size is based on frequency (VÀ kích thước chữ dựa trên tần xuất)
```

---

## Traceability Matrix

| Story ID | Title | Priority | FR ID | Module |
|----------|-------|----------|-------|--------|
| US-RES-001 | Tạo Bài Báo Mới | P0 | FR-PUB-001 | 1 |
| US-RES-002 | Upload File PDF | P0 | FR-PUB-002 | 1 |
| US-RES-003 | Sửa Bài Báo Nháp | P0 | FR-PUB-004 | 1 |
| US-RES-004 | Xóa Bài Báo Nháp | P0 | FR-PUB-005 | 1 |
| US-RES-005 | Xem Danh Sách Bài Báo | P0 | FR-PUB-006 | 1 |
| US-RES-006 | Thêm Đồng Tác Giả | P1 | FR-PUB-007 | 1 |
| US-RES-007 | Gắn Tags/Keywords | P1 | FR-PUB-008 | 1 |
| US-RES-008 | Xem Chi Tiết Bài Báo | P0 | FR-PUB-010 | 1 |
| US-RES-009 | Download File PDF | P0 | FR-PUB-011 | 1 |
| US-RES-010 | Nộp Xét Duyệt | P0 | FR-APR-001 | 2 |
| US-RES-011 | Xem Trạng Thái Xét Duyệt | P0 | FR-APR-002 | 2 |
| US-RES-012 | Chỉnh Sửa Theo Yêu Cầu | P0 | FR-APR-003 | 2 |
| US-RES-013 | Rút Lại Đơn Nộp | P1 | FR-APR-019 | 2 |
| US-RES-014 | Xem Profile Công Khai | P1 | FR-PRO-001 | 4 |
| US-RES-015 | Chỉnh Sửa Profile | P1 | FR-PRO-002 | 4 |
| US-RES-016 | Xem Danh Sách Bài Báo Trên Profile | P1 | FR-PRO-003 | 4 |
| US-RES-017 | Validate DOI Format | P1 | FR-PUB-012 | 1 |
| US-RES-018 | Validate ISSN Format | P1 | FR-PUB-013 | 1 |
| US-RES-019 | Cảnh Báo Trùng Lặp | P1 | FR-PUB-014 | 1 |
| US-RES-020 | Auto-Fetch Metadata từ DOI | P2 | FR-PUB-003 | 1 |
| US-RES-021 | Import từ ORCID | P2 | FR-PUB-015 | 1 |
| US-RES-022 | Xem Biểu Đồ Năng Suất | P2 | FR-PRO-004 | 4 |
| US-RES-023 | Xem Word Cloud Lĩnh Vực | P2 | FR-PRO-005 | 4 |

---

**Tài liệu liên quan**:
- [Requirements - Publication Management](../../03_Requirements/Functional/module_publication_management.md)
- [Requirements - Approval Workflow](../../03_Requirements/Functional/module_approval_workflow.md)
- [Requirements - Researcher Profile](../../03_Requirements/Functional/module_profile.md)
