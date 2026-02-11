# User Stories - Faculty Reviewer

> 👤 **Role**: Faculty Reviewer (Cán bộ Khoa)  
> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục tiêu**: Xét duyệt bài báo cấp Khoa và quản lý báo cáo

---

## Tổng Quan

**Total Stories**: 9  
**P0 (Must Have)**: 6  
**P1 (Should Have)**: 2  
**P2 (Nice to Have)**: 1

---

## Module 2: Approval Workflow - Faculty Review

### US-FCR-001: Xem Dashboard Chờ Duyệt Khoa
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-005

**User Story**:
```
As a Faculty Reviewer (Là Cán bộ Khoa),
I want to see all publications pending my review from my faculty (Tôi muốn xem tất cả các bài báo đang chờ tôi duyệt từ khoa của tôi),
So that I can manage my review workload effectively (Để tôi có thể quản lý khối lượng công việc xét duyệt hiệu quả).
```

**Acceptance Criteria**:
```
GIVEN I am logged in as a Faculty Reviewer (KHI tôi đã đăng nhập là Cán bộ Khoa)
WHEN I access "Faculty Review Dashboard" (VÀ tôi truy cập "Dashboard Duyệt Khoa")
THEN I see ONLY publications from my faculty (THÌ tôi CHỈ thấy các bài báo từ khoa của tôi)
AND with status: SUBMITTED or FACULTY_REVIEWING (VÀ có trạng thái: ĐÃ_NỘP hoặc KHOA_ĐANG_DUYỆT)
AND I can filter by: All / New / In Review (VÀ tôi có thể lọc theo: Tất cả / Mới / Đang duyệt)
AND results are sorted: Oldest first (VÀ kết quả được sắp xếp: Cũ nhất trước)
AND publications over 7 days old are highlighted (VÀ các bài báo quá 7 ngày sẽ được làm nổi bật)
```

---

### US-FCR-002: Phê Duyệt Bài Báo
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-006

**User Story**:
```
As a Faculty Reviewer (Là Cán bộ Khoa),
I want to approve publications that meet our faculty standards (Tôi muốn phê duyệt các bài báo đạt chuẩn của khoa),
So that they can proceed to university-level review (Để chúng có thể chuyển sang cấp trường xét duyệt).
```

**Acceptance Criteria**:
```
GIVEN a publication is in FACULTY_REVIEWING status (KHI bài báo đang ở trạng thái KHOA_ĐANG_DUYỆT)
WHEN I click "Approve" and optionally add a comment (VÀ tôi nhấn "Duyệt" và có thể thêm nhận xét)
THEN the status changes to FACULTY_APPROVED (THÌ trạng thái chuyển sang KHOA_ĐÃ_DUYỆT)
AND an email is sent to the researcher: "Approved by Faculty" (VÀ một email được gửi đến giảng viên: "Khoa đã duyệt")
AND an email is sent to University Reviewer: "New publication pending review" (VÀ một email được gửi đến Cán bộ Trường: "Bài báo mới chờ duyệt")
AND an audit log is created (reviewer, timestamp, comment) (VÀ nhật ký hệ thống được tạo: người duyệt, thời gian, nhận xét)
```

---

### US-FCR-003: Yêu Cầu Bổ Sung
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-007

**User Story**:
```
As a Faculty Reviewer (Là Cán bộ Khoa),
I want to request revisions on publications that need improvement (Tôi muốn yêu cầu chỉnh sửa các bài báo cần cải thiện),
So that researchers can address issues before full approval (Để giảng viên có thể khắc phục vấn đề trước khi được duyệt hoàn toàn).
```

**Acceptance Criteria**:
```
GIVEN a publication is in FACULTY_REVIEWING status (KHI bài báo đang ở trạng thái KHOA_ĐANG_DUYỆT)
WHEN I click "Request Revision" and enter a comment (required, min 10 chars) (VÀ tôi nhấn "Yêu cầu chỉnh sửa" và nhập nhận xét - bắt buộc, tối thiểu 10 ký tự)
THEN the status changes to REVISION_REQUIRED (THÌ trạng thái chuyển sang YÊU_CẦU_CHỈNH_SỬA)
AND an email is sent to the researcher with my comment (VÀ một email được gửi đến giảng viên kèm nhận xét của tôi)
AND an audit log is created (VÀ nhật ký hệ thống được tạo)
```

---

### US-FCR-004: Từ Chối Bài Báo
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-008

**User Story**:
```
As a Faculty Reviewer (Là Cán bộ Khoa),
I want to reject publications that don't meet standards (Tôi muốn từ chối các bài báo không đạt chuẩn),
So that only quality work proceeds to the next level (Để chỉ những bài chất lượng mới được đi tiếp).
```

**Acceptance Criteria**:
```
GIVEN a publication is in FACULTY_REVIEWING status (KHI bài báo đang ở trạng thái KHOA_ĐANG_DUYỆT)
WHEN I click "Reject" and enter a reason (required) (VÀ tôi nhấn "Từ chối" và nhập lý do - bắt buộc)
THEN the status changes to FACULTY_REJECTED (THÌ trạng thái chuyển sang KHOA_TỪ_CHỐI)
AND an email is sent to the researcher with the reason (VÀ một email được gửi đến giảng viên kèm lý do)
AND an audit log is created (VÀ nhật ký hệ thống được tạo)
AND this decision cannot be reverted (VÀ quyết định này không thể hoàn tác)
```

---

### US-FCR-005: Xem Lịch Sử Xét Duyệt
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-015

**User Story**:
```
As a Faculty Reviewer (Là Cán bộ Khoa),
I want to see the complete review history of a publication (Tôi muốn xem toàn bộ lịch sử xét duyệt của một bài báo),
So that I can understand previous decisions and revisions (Để tôi có thể hiểu các quyết định và chỉnh sửa trước đó).
```

**Acceptance Criteria**:
```
GIVEN I am viewing a publication's details (KHI tôi đang xem chi tiết bài báo)
WHEN I check the audit trail section (VÀ tôi kiểm tra phần lịch sử)
THEN I see all status transitions with: (THÌ tôi thấy tất cả các lần chuyển trạng thái với:)
- From/To status (Trạng thái Từ/Đến)
- Reviewer name and role (Tên người duyệt và vai trò)
- Comments (Nhận xét)
- Timestamp (Thời gian)
```

---

### US-FCR-006: Nhận Thông Báo Email
**Priority**: 🔴 P0 - Must Have  
**Related FR**: FR-APR-016

**User Story**:
```
As a Faculty Reviewer (Là Cán bộ Khoa),
I want to receive email notifications when new publications need review (Tôi muốn nhận thông báo email khi có bài báo mới cần duyệt),
So that I don't miss submissions requiring my attention (Để tôi không bỏ lỡ các bài cần xử lý).
```

**Acceptance Criteria**:
```
GIVEN a researcher has submitted a publication from my faculty (KHI một giảng viên thuộc khoa tôi nộp bài báo)
WHEN the status changes to SUBMITTED (VÀ trạng thái chuyển sang ĐÃ_NỘP)
THEN I receive an email with: (THÌ tôi nhận được email với:)
- Subject: "[UFPMS] New publication pending review" (Tiêu đề: "[UFPMS] Bài báo mới chờ duyệt")
- Author name and publication title (Tên tác giả và tiêu đề bài báo)
- Direct link to review the publication (Link trực tiếp để duyệt bài)
```

---

### US-FCR-007: Duyệt Nhiều Bài Cùng Lúc
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-APR-009

**User Story**:
```
As a Faculty Reviewer (Là Cán bộ Khoa),
I want to approve multiple publications at once (Tôi muốn duyệt nhiều bài báo cùng lúc),
So that I can process routine approvals more efficiently (Để tôi có thể xử lý các bài duyệt định kỳ nhanh hơn).
```

**Acceptance Criteria**:
```
GIVEN I have selected multiple publications (checkboxes) (KHI tôi chọn nhiều bài báo)
WHEN I click "Approve Selected" (VÀ tôi nhấn "Duyệt các bài đã chọn")
THEN all selected publications change to FACULTY_APPROVED (THÌ tất cả bài báo đã chọn chuyển sang KHOA_ĐÃ_DUYỆT)
AND individual emails are sent to each researcher (VÀ email riêng được gửi đến từng giảng viên)
AND one summary email is sent to the University Reviewer (VÀ một email tổng hợp được gửi đến Cán bộ Trường)
```

---

## Module 5: Reporting & Analytics

### US-FCR-008: Xem Báo Cáo Khoa
**Priority**: 🟡 P1 - Should Have  
**Related FR**: FR-REP-002

**User Story**:
```
As a Faculty Reviewer (Là Cán bộ Khoa),
I want to generate reports for my faculty's publications (Tôi muốn tạo báo cáo về các bài báo của khoa tôi),
So that I can track our research productivity (Để tôi có thể theo dõi năng suất nghiên cứu).
```

**Acceptance Criteria**:
```
GIVEN I select my faculty and a year range (KHI tôi chọn khoa của mình và khoảng thời gian)
WHEN I click "Generate Report" (VÀ tôi nhấn "Tạo báo cáo")
THEN I see a report with: (THÌ tôi thấy báo cáo gồm:)
- List of all publications (Danh sách tất cả bài báo)
- Grouped by researcher (Nhóm theo giảng viên)
- Summary statistics (total, by quartile) (Thống kê tóm tắt: tổng số, theo phân hạng)
AND I can export to Excel/PDF format (VÀ tôi có thể xuất ra Excel/PDF)
```

---

### US-FCR-009: Theo Dõi SLA Xét Duyệt
**Priority**: 🟢 P2 - Nice to Have  
**Related FR**: FR-APR-020

**User Story**:
```
As a Faculty Reviewer (Là Cán bộ Khoa),
I want to see which publications are approaching or past the review deadline (Tôi muốn xem bài báo nào sắp hết hoặc đã quá hạn duyệt),
So that I can prioritize my review work (Để tôi có thể ưu tiên công việc xét duyệt).
```

**Acceptance Criteria**:
```
GIVEN I am on my review dashboard (KHI tôi ở dashboard duyệt bài)
WHEN I view the pending list (VÀ tôi xem danh sách chờ)
THEN publications over 7 days old are highlighted in yellow/red (THÌ các bài quá 7 ngày được tô màu vàng/đỏ)
AND I can see average review time metrics: (VÀ tôi thấy các chỉ số thời gian duyệt trung bình:)
- Average time: SUBMITTED → FACULTY_APPROVED (Thời gian trung bình: ĐÃ_NỘP -> KHOA_ĐÃ_DUYỆT)
- % reviewed within 7 days (% được duyệt trong vòng 7 ngày)
```

---

## Traceability Matrix

| Story ID | Title | Priority | FR ID | Module |
|----------|-------|----------|-------|--------|
| US-FCR-001 | Xem Dashboard Chờ Duyệt Khoa | P0 | FR-APR-005 | 2 |
| US-FCR-002 | Phê Duyệt Bài Báo | P0 | FR-APR-006 | 2 |
| US-FCR-003 | Yêu Cầu Bổ Sung | P0 | FR-APR-007 | 2 |
| US-FCR-004 | Từ Chối Bài Báo | P0 | FR-APR-008 | 2 |
| US-FCR-005 | Xem Lịch Sử Xét Duyệt | P0 | FR-APR-015 | 2 |
| US-FCR-006 | Nhận Thông Báo Email | P0 | FR-APR-016 | 2 |
| US-FCR-007 | Duyệt Nhiều Bài Cùng Lúc | P1 | FR-APR-009 | 2 |
| US-FCR-008 | Xem Báo Cáo Khoa | P1 | FR-REP-002 | 5 |
| US-FCR-009 | Theo Dõi SLA Xét Duyệt | P2 | FR-APR-020 | 2 |

---

**Tài liệu liên quan**:
- [Requirements - Approval Workflow](../../03_Requirements/Functional/module_approval_workflow.md)
- [Requirements - Reporting](../../03_Requirements/Functional/module_reporting.md)
- [To-Be Process](../../02_System_Clarification/Business_Context/to_be_process.md)
