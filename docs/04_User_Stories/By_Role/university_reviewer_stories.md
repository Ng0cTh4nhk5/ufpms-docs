# User Stories - University Reviewer

> 👤 **Role**: University Reviewer (Cán bộ Trường)  
> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục tiêu**: Phê duyệt cuối cùng và công bố, quản lý báo cáo toàn trường

---

## Tổng Quan

**Total Stories**: 10  
**P0 (Must Have)**: 6  
**P1 (Should Have)**: 3  
**P2 (Nice to Have)**: 1

---

## Module 2: Approval Workflow - University Review

### US-UNR-001: Xem Dashboard Chờ Duyệt Trường
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-010

**User Story**:
```
As a University Reviewer (Là Cán bộ Trường),
I want to see all university-wide publications pending final approval (Tôi muốn xem tất cả bài báo toàn trường chờ duyệt cuối cùng),
So that I can manage the final review process (Để tôi có thể quản lý quy trình xét duyệt cuối cùng).
```

**Acceptance Criteria**:
```
GIVEN I am logged in as a University Reviewer (KHI tôi đã đăng nhập là Cán bộ Trường)
WHEN I access "University Review Dashboard" (VÀ tôi truy cập "Dashboard Duyệt của Trường")
THEN I see ONLY publications with status FACULTY_APPROVED (THÌ tôi CHỈ thấy các bài báo có trạng thái KHOA_ĐÃ_DUYỆT)
AND I can filter by: Faculty, Journal Type, Year (VÀ tôi có thể lọc theo: Khoa, Loại tạp chí, Năm)
AND results are sorted: Oldest first (VÀ kết quả sắp xếp: Cũ nhất trước)
AND columns show: Title, Author, Faculty, Faculty Review Date (VÀ các cột hiển thị: Tiêu đề, Tác giả, Khoa, Ngày khoa duyệt)
```

---

### US-UNR-002: Xem Ý Kiến Cấp Khoa
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-011

**User Story**:
```
As a University Reviewer (Là Cán bộ Trường),
I want to see the faculty reviewer's comments and decision (Tôi muốn xem nhận xét và quyết định của cán bộ khoa),
So that I can make an informed final approval decision (Để tôi có thể đưa ra quyết định duyệt cuối cùng chính xác).
```

**Acceptance Criteria**:
```
GIVEN a publication is in FACULTY_APPROVED status
WHEN I view its details
THEN I see:
- Faculty reviewer's name
- Faculty approval date  
- Faculty reviewer's comments (if any)
- Revision history (if there were revisions)
```

---

### US-UNR-003: Phê Duyệt và Công Bố
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-012

**User Story**:
```
As a University Reviewer (Là Cán bộ Trường),
I want to give final approval and publish publications (Tôi muốn duyệt cuối cùng và công bố bài báo),
So that they become publicly visible on the platform (Để chúng được hiển thị công khai trên hệ thống).
```

**Acceptance Criteria**:
```
GIVEN a publication is in UNIVERSITY_REVIEWING status (KHI bài báo ở trạng thái TRƯỜNG_ĐANG_DUYỆT)
WHEN I click "Approve & Publish" (VÀ tôi nhấn "Duyệt & Công bố")
THEN the status changes to PUBLISHED (THÌ trạng thái chuyển sang ĐÃ_CÔNG_BỐ)
AND an email is sent to the researcher: "Your publication is now published!" (VÀ email gửi đến giảng viên: "Bài báo của bạn đã được công bố!")
AND the publication appears publicly in Search and on the researcher's profile (VÀ bài báo xuất hiện công khai trong Tìm kiếm và trên hồ sơ giảng viên)
AND an audit log is created (VÀ nhật ký hệ thống được tạo)
```

---

### US-UNR-004: Từ Chối Cấp Trường
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-013

**User Story**:
```
As a University Reviewer (Là Cán bộ Trường),
I want to reject publications at the university level if needed (Tôi muốn từ chối bài báo ở cấp trường nếu cần),
So that publications not meeting university standards aren't published (Để các bài báo không đạt chuẩn trường không được công bố).
```

**Acceptance Criteria**:
```
GIVEN a publication is in UNIVERSITY_REVIEWING status (KHI bài báo ở trạng thái TRƯỜNG_ĐANG_DUYỆT)
WHEN I click "Reject" and enter a reason (required) (VÀ tôi nhấn "Từ chối" và nhập lý do - bắt buộc)
THEN the status changes to UNIVERSITY_REJECTED (THÌ trạng thái chuyển sang TRƯỜNG_TỪ_CHỐI)
AND an email is sent to both the researcher and Faculty Reviewer (VÀ email gửi đến cả giảng viên và Cán bộ Khoa)
AND an audit log is created (VÀ nhật ký hệ thống được tạo)
```

---

### US-UNR-005: Xem Audit Trail
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-015

**User Story**:
```
As a University Reviewer (Là Cán bộ Trường),
I want to see the complete audit trail of all publications (Tôi muốn xem toàn bộ dấu vết kiểm toán của tất cả bài báo),
So that I can track the entire approval process (Để tôi có thể theo dõi toàn bộ quy trình phê duyệt).
```

**Acceptance Criteria**:
```
GIVEN I am viewing any publication (KHI tôi xem bất kỳ bài báo nào)
WHEN I access the audit trail (VÀ tôi truy cập dấu vết kiểm toán)
THEN I see all status transitions from all levels (Faculty and University) (THÌ tôi thấy tất cả chuyển đổi trạng thái từ mọi cấp - Khoa và Trường)
WITH reviewer names, roles, comments, and timestamps (VỚI tên người duyệt, vai trò, nhận xét và thời gian)
```

---

### US-UNR-006: Nhận Thông Báo Email
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-016

**User Story**:
```
As a University Reviewer (Là Cán bộ Trường),
I want to receive notifications when publications are approved at faculty level (Tôi muốn nhận thông báo khi bài báo được duyệt ở cấp khoa),
So that I know when new publications need my final review (Để tôi biết khi nào có bài báo mới cần tôi duyệt lần cuối).
```

**Acceptance Criteria**:
```
GIVEN a publication has been approved at faculty level (KHI bài báo đã được duyệt ở cấp khoa)
WHEN the status changes to FACULTY_APPROVED (VÀ trạng thái chuyển sang KHOA_ĐÃ_DUYỆT)
THEN I receive an email with: (THÌ tôi nhận được email với:)
- Subject: "[UFPMS] Publication awaiting university review" (Tiêu đề: "[UFPMS] Bài báo chờ trường duyệt")
- Author name, faculty, and publication title (Tên tác giả, khoa, và tiêu đề bài báo)
- Faculty reviewer's name and approval date (Tên cán bộ khoa và ngày duyệt)
- Direct link to review (Link trực tiếp để duyệt)
```

---

## Module 5: Reporting & Analytics

### US-UNR-007: Xem Dashboard Analytics Toàn Trường
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-REP-001

**User Story**:
```
As a University Reviewer (Là Cán bộ Trường),
I want to see university-wide publication analytics (Tôi muốn xem phân tích bài báo toàn trường),
So that I can monitor overall research productivity (Để tôi có thể giám sát năng suất nghiên cứu tổng thể).
```

**Acceptance Criteria**:
```
GIVEN I am on the analytics dashboard (KHI tôi ở dashboard phân tích)
WHEN the page loads (VÀ trang tải xong)
THEN I see: (THÌ tôi thấy:)
- Total publications (all time and this year) (Tổng số bài báo - mọi lúc và năm nay)
- Distribution by quartile (Q1/Q2/Q3/Q4) (Phân bố theo phân hạng)
- Distribution by faculty (Phân bố theo khoa)
- Top researchers (Các nhà nghiên cứu hàng đầu)
WITH visualizations: (VỚI các biểu đồ:)
- Line chart: Trend by year (Biểu đồ đường: Xu hướng theo năm)
- Pie chart: Distribution by quartile (Biểu đồ tròn: Phân bố theo phân hạng)
- Bar chart: By faculty (Biểu đồ cột: Theo khoa)
```

---

### US-UNR-008: Tạo Báo Cáo Toàn Trường
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-REP-002, FR-REP-005

**User Story**:
```
As a University Reviewer (Là Cán bộ Trường),
I want to generate comprehensive university-wide reports (Tôi muốn tạo báo cáo toàn diện toàn trường),
So that I can provide leadership with research output data (Để tôi có thể cung cấp dữ liệu đầu ra nghiên cứu cho lãnh đạo).
```

**Acceptance Criteria**:
```
GIVEN I select parameters (year range, faculty filter, etc.) (KHI tôi chọn tham số - khoảng thời gian, lọc theo khoa, v.v.)
WHEN I click "Generate Report" (VÀ tôi nhấn "Tạo báo cáo")
THEN the system generates a report with: (THÌ hệ thống tạo báo cáo với:)
- All published publications (Tất cả bài báo đã công bố)
- Grouped by faculty and researcher (Nhóm theo khoa và giảng viên)
- Summary statistics (Thống kê tóm tắt)
AND I can export in Excel/PDF/CSV format (VÀ tôi có thể xuất ra Excel/PDF/CSV)
AND generation completes in < 5 minutes (VÀ việc tạo báo cáo hoàn tất trong < 5 phút)
```

---

### US-UNR-009: Xem Báo Cáo Theo Quartile
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-REP-003

**User Story**:
```
As a University Reviewer (Là Cán bộ Trường),
I want to see publication breakdown by journal quartile (Tôi muốn xem phân tích bài báo theo phân hạng tạp chí),
So that I can assess research quality metrics (Để tôi có thể đánh giá chỉ số chất lượng nghiên cứu).
```

**Acceptance Criteria**:
```
GIVEN I access the quartile report (KHI tôi truy cập báo cáo phân hạng)
WHEN I select a year range (VÀ tôi chọn khoảng thời gian)
THEN I see breakdown: (THÌ tôi xem phân tích:)
- Q1 publications (count and list) (Bài báo Q1 - số lượng và danh sách)
- Q2 publications (count and list) (Bài báo Q2 - số lượng và danh sách)
- Q3/Q4 publications (count and list) (Bài báo Q3/Q4 - số lượng và danh sách)
- Conference papers (count and list) (Bài kỷ yếu hội nghị - số lượng và danh sách)
WITH comparisons to previous years (VỚI so sánh các năm trước)
```

---

### US-UNR-010: Xem Xu Hướng Phát Triển
**Priority**: 🟢 P2 - Nice to Have  
**Related FR**: FR-REP-004

**User Story**:
```
As a University Reviewer (Là Cán bộ Trường),
I want to see trend analysis and emerging research areas (Tôi muốn xem phân tích xu hướng và các lĩnh vực nghiên cứu mới nổi),
So that I can identify growth opportunities (Để tôi có thể xác định cơ hội phát triển).
```

**Acceptance Criteria**:
```
GIVEN I access trend analysis (KHI tôi truy cập phân tích xu hướng)
WHEN the report loads (VÀ báo cáo tải xong)
THEN I see: (THÌ tôi thấy:)
- Year-over-year growth rate (Tỷ lệ tăng trưởng theo năm)
- Top growing faculties (Các khoa tăng trưởng nhanh nhất)
- Emerging research fields (from keywords) (Lĩnh vực nghiên cứu mới nổi - từ từ khóa)
- Most productive researchers this year (Giảng viên năng suất nhất năm nay)
```

---

## Traceability Matrix

| Story ID | Title | Priority | FR ID | Module |
|----------|-------|----------|-------|--------|
| US-UNR-001 | Xem Dashboard Chờ Duyệt Trường | P0 | FR-APR-010 | 2 |
| US-UNR-002 | Xem Ý Kiến Cấp Khoa | P0 | FR-APR-011 | 2 |
| US-UNR-003 | Phê Duyệt và Công Bố | P0 | FR-APR-012 | 2 |
| US-UNR-004 | Từ Chối Cấp Trường | P0 | FR-APR-013 | 2 |
| US-UNR-005 | Xem Audit Trail | P0 | FR-APR-015 | 2 |
| US-UNR-006 | Nhận Thông Báo Email | P0 | FR-APR-016 | 2 |
| US-UNR-007 | Xem Dashboard Analytics Toàn Trường | P1 | FR-REP-001 | 5 |
| US-UNR-008 | Tạo Báo Cáo Toàn Trường | P1 | FR-REP-002, FR-REP-005 | 5 |
| US-UNR-009 | Xem Báo Cáo Theo Quartile | P1 | FR-REP-003 | 5 |
| US-UNR-010 | Xem Xu Hướng Phát Triển | P2 | FR-REP-004 | 5 |

---

**Tài liệu liên quan**:
- [Requirements - Approval Workflow](../../03_Requirements/Functional/module_approval_workflow.md)
- [Requirements - Reporting](../../03_Requirements/Functional/module_reporting.md)
- [To-Be Process](../../02_System_Clarification/Business_Context/to_be_process.md)
