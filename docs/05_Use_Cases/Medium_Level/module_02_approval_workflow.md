# Module 2: Quy Trình Xét Duyệt - Use Cases Cấp Trung

> **Module**: 2 - Quy Trình Xét Duyệt  
> **Use Case Cấp Cao**: [UC-HL-002](../High_Level/uc_hl_02_approval_workflow.md)

---

## Hành Động Của Researcher

### UC-M2-001: Gửi Xét Duyệt (Submit for Review)
**ID**: UC-M2-001 | **Độ Ưu Tiên**: 🔴 P0 | **Tác Nhân**: Researcher  
**Liên Quan**: US-RES-010, FR-APR-001

**Mục Tiêu**: Gửi bài báo để khoa xét duyệt  
**Điều Kiện Tiên Quyết**: Trạng thái bài báo = DRAFT (Nháp), tất cả các trường bắt buộc đã được điền  
**Luồng Chính**:  
1. Researcher nhấn "Gửi Xét Duyệt"
2. Hệ thống xác thực các trường bắt buộc (Tiêu đề, Tác giả, Năm, PDF)
3. Hệ thống đổi trạng thái: DRAFT → SUBMITTED (Đã Nộp)
4. Hệ thống gửi email cho Faculty Reviewer (Người duyệt cấp Khoa)
5. Hệ thống ghi nhật ký kiểm toán

**Điều Kiện Hậu Quyết**: Trạng thái = SUBMITTED, thông báo đã được gửi  
**Quy Tắc Nghiệp Vụ**: BR-APR-001, BR-APR-004

---

### UC-M2-002: Theo Dõi Trạng Thái Xét Duyệt (Track Review Status)
**ID**: UC-M2-002 | **Độ Ưu Tiên**: 🔴 P0 | **Tác Nhân**: Researcher  
**Liên Quan**: US-RES-011, FR-APR-002

**Mục Tiêu**: Xem trạng thái xét duyệt hiện tại và lịch sử  
**Luồng Chính**:
1. Researcher xem chi tiết bài báo
2. Hệ thống hiển thị dòng thời gian trạng thái (timeline)
3. Hệ thống hiển thị trạng thái hiện tại được làm nổi bật
4. Hệ thống hiển thị bình luận của người duyệt (nếu có)
5. Hệ thống hiển thị ngày của mỗi lần chuyển đổi trạng thái

**Quy Tắc Nghiệp Vụ**: Hiển thị nhật ký kiểm toán đầy đủ

---

### UC-M2-003: Chỉnh Sửa Bài Báo (Revise Publication)
**ID**: UC-M2-003 | **Độ Ưu Tiên**: 🔴 P0 | **Tác Nhân**: Researcher  
**Liên Quan**: US-RES-012, FR-APR-003

**Mục Tiêu**: Chỉnh sửa và nộp lại sau khi nhận phản hồi từ người duyệt  
**Điều Kiện Tiên Quyết**: Trạng thái = REVISION_REQUIRED (Yêu Cầu Chỉnh Sửa)  
**Luồng Chính**:
1. Researcher xem bình luận của người duyệt
2. Researcher nhấn "Sửa"
3. Researcher thực hiện thay đổi
4. Researcher nhấn "Nộp Lại" (Resubmit)
5. Hệ thống đổi trạng thái: REVISION_REQUIRED → SUBMITTED
6. Hệ thống gửi email cho Faculty Reviewer

**Quy Tắc Nghiệp Vụ**: BR-APR-001

---

### UC-M2-004: Rút Bài Báo (Withdraw Submission)
**ID**: UC-M2-004 | **Độ Ưu Tiên**: 🟡 P1 | **Tác Nhân**: Researcher  
**Liên Quan**: US-RES-013, FR-APR-019

**Mục Tiêu**: Rút lại bài nộp trước khi được phê duyệt  
**Điều Kiện Tiên Quyết**: Trạng thái = SUBMITTED hoặc FACULTY_REVIEWING  
**Luồng Chính**:
1. Researcher nhấn "Rút Bài" (Withdraw)
2. Hệ thống xác nhận hành động
3. Hệ thống đổi trạng thái trở lại DRAFT
4. Hệ thống gửi email cho reviewer (nếu đang xét duyệt)

---

## Hành Động Của Faculty Reviewer (Người Duyệt Cấp Khoa)

### UC-M2-005: Khoa Xét Duyệt - Phê Duyệt (Faculty Review - Approve)
**ID**: UC-M2-005 | **Độ Ưu Tiên**: 🔴 P0 | **Tác Nhân**: Faculty Reviewer  
**Liên Quan**: US-FCR-002, FR-APR-006

**Mục Tiêu**: Phê duyệt bài báo ở cấp khoa  
**Điều Kiện Tiên Quyết**: Trạng thái = FACULTY_REVIEWING, người dùng là faculty reviewer  
**Luồng Chính**:
1. Reviewer xem bài báo
2. Reviewer nhấn "Phê Duyệt"
3. Reviewer thêm bình luận tùy chọn
4. Hệ thống đổi trạng thái: FACULTY_REVIEWING → FACULTY_APPROVED
5. Hệ thống gửi email cho:
   - Researcher: "Đã được Khoa phê duyệt"
   - University Reviewer: "Chờ bạn xét duyệt"
6. Hệ thống ghi nhật ký kiểm toán

**Điều Kiện Hậu Quyết**: Trạng thái = FACULTY_APPROVED  
**Quy Tắc Nghiệp Vụ**: BR-APR-001, BR-APR-002, BR-APR-004

---

### UC-M2-006: Khoa Xét Duyệt - Yêu Cầu Chỉnh Sửa (Faculty Review - Request Revision)
**ID**: UC-M2-006 | **Độ Ưu Tiên**: 🔴 P0 | **Tác Nhân**: Faculty Reviewer  
**Liên Quan**: US-FCR-003, FR-APR-007

**Mục Tiêu**: Yêu cầu Researcher chỉnh sửa  
**Luồng Chính**:
1. Reviewer nhấn "Yêu Cầu Chỉnh Sửa"
2. Reviewer nhập bình luận (bắt buộc, tối thiểu 10 ký tự)
3. Hệ thống đổi trạng thái: FACULTY_REVIEWING → REVISION_REQUIRED
4. Hệ thống gửi email cho Researcher kèm bình luận
5. Hệ thống ghi nhật ký kiểm toán

**Quy Tắc Nghiệp Vụ**: BR-APR-005 (bình luận là bắt buộc)

---

### UC-M2-007: Khoa Xét Duyệt - Từ Chối (Faculty Review - Reject)
**ID**: UC-M2-007 | **Độ Ưu Tiên**: 🔴 P0 | **Tác Nhân**: Faculty Reviewer  
**Liên Quan**: US-FCR-004, FR-APR-008

**Mục Tiêu**: Từ chối bài báo (quyết định cuối cùng)  
**Luồng Chính**:
1. Reviewer nhấn "Từ Chối"
2. Reviewer nhập lý do (bắt buộc, tối thiểu 20 ký tự)
3. Hệ thống đổi trạng thái: FACULTY_REVIEWING → FACULTY_REJECTED
4. Hệ thống gửi email cho Researcher
5. Hệ thống ghi nhật ký kiểm toán

**Điều Kiện Hậu Quyết**: Trạng thái = FACULTY_REJECTED (không thể nộp lại)  
**Quy Tắc Nghiệp Vụ**: BR-APR-003 (tính chung thẩm)

---

### UC-M2-012: Phê Duyệt Hàng Loạt - Khoa (Bulk Approve)
**ID**: UC-M2-012 | **Độ Ưu Tiên**: 🟡 P1 | **Tác Nhân**: Faculty Reviewer  
**Liên Quan**: US-FCR-007, FR-APR-009

**Mục Tiêu**: Phê duyệt nhiều bài báo cùng lúc  
**Luồng Chính**:
1. Reviewer chọn nhiều bài báo (checkboxes)
2. Reviewer nhấn "Phê Duyệt Đã Chọn"
3. Hệ thống xác nhận hành động
4. Hệ thống phê duyệt tất cả các bài đã chọn
5. Hệ thống gửi email riêng lẻ
6. Hệ thống gửi email tóm tắt cho University Reviewer

---

## Hành Động Của University Reviewer (Người Duyệt Cấp Trường)

### UC-M2-008: Trường Xét Duyệt - Phê Duyệt & Xuất Bản + Nhập Giờ Làm
**ID**: UC-M2-008 | **Độ Ưu Tiên**: 🔴 P0 | **Tác Nhân**: University Reviewer  
**Liên Quan**: US-UNR-003, FR-APR-012

**Mục Tiêu**: Phê duyệt cuối cùng, nhập giờ làm và công khai ra công chúng  
**Điều Kiện Tiên Quyết**: Trạng thái = UNIVERSITY_REVIEWING  
**Luồng Chính**:
1. Reviewer xem bài báo và các bình luận của Khoa
2. Reviewer nhấn "Phê Duyệt & Xuất Bản"
3. Hệ thống hiển thị form:
   - Nhập số giờ làm/giờ dạy (bắt buộc, số, > 0, <= 200)
   - Ghi chú (tùy chọn)
4. Reviewer nhập số giờ và nhấn "Xác Nhận"
5. Hệ thống đổi trạng thái: UNIVERSITY_REVIEWING → PUBLISHED
6. Hệ thống lưu giờ làm vào bảng work_hour_conversions
7. Hệ thống cập nhật tổng giờ làm năm của Researcher
8. Hệ thống làm cho bài báo hiển thị trong tìm kiếm công khai
9. Hệ thống hiển thị trên hồ sơ công khai của Researcher
10. Hệ thống gửi email cho Researcher: "Đã Xuất Bản - Ghi nhận [X] giờ!"
11. Hệ thống ghi nhật ký kiểm toán

**Điều Kiện Hậu Quyết**: Trạng thái = PUBLISHED, hiển thị công khai, giờ làm đã được lưu  
**Quy Tắc Nghiệp Vụ**: BR-APR-002, BR-SEA-001, BR-WRK-001 (work hour validation)

---

### UC-M2-009: Trường Xét Duyệt - Từ Chối (Reject)
**ID**: UC-M2-009 | **Độ Ưu Tiên**: 🔴 P0 | **Tác Nhân**: University Reviewer  
**Liên Quan**: US-UNR-004, FR-APR-013

**Mục Tiêu**: Từ chối ở cấp trường  
**Luồng Chính**:
1. Reviewer nhấn "Từ Chối"
2. Reviewer nhập lý do (bắt buộc)
3. Hệ thống đổi trạng thái: UNIVERSITY_REVIEWING → UNIVERSITY_REJECTED
4. Hệ thống gửi email cho Researcher và Faculty Reviewer

**Điều Kiện Hậu Quyết**: Trạng thái = UNIVERSITY_REJECTED (chung thẩm)  
**Quy Tắc Nghiệp Vụ**: BR-APR-003

---

### UC-M2-013: Phê Duyệt Hàng Loạt - Trường (Bulk Approve)
**ID**: UC-M2-013 | **Độ Ưu Tiên**: 🟡 P1 | **Tác Nhân**: University Reviewer  
**Mục Tiêu**: Phê duyệt và xuất bản nhiều bài báo  

**Luồng Chính**: Tương tự như UC-M2-012 nhưng kết quả là trạng thái PUBLISHED

---

### UC-M2-014: Phân Công Lại Reviewer (Reassign Reviewer)
**ID**: UC-M2-014 | **Độ Ưu Tiên**: 🟡 P1 | **Tác Nhân**: SuperAdmin  
**Liên Quan**: FR-APR-018

**Mục Tiêu**: Thay đổi người duyệt được phân công  
**Luồng Chính**:
1. Admin xem bài báo
2. Admin nhấn "Phân Công Lại"
3. Admin chọn reviewer mới
4. Hệ thống gửi thông báo cho reviewer mới

---

## Hành Động Hệ Thống (System Actions)

### UC-M2-010: Xem Lịch Sử Xét Duyệt (View Review History)
**ID**: UC-M2-010 | **Độ Ưu Tiên**: 🔴 P0 | **Tác Nhân**: Tất cả reviewers  
**Liên Quan**: US-FCR-005, US-UNR-005, FR-APR-015

**Mục Tiêu**: Xem nhật ký kiểm toán đầy đủ  
**Luồng Chính**:
1. User xem chi tiết bài báo
2. User nhấn tab "Lịch Sử Xét Duyệt"
3. Hệ thống hiển thị tất cả các chuyển đổi trạng thái:
   - Thời gian (Timestamp)
   - Trạng thái Từ/Đến
   - Tên và vai trò Reviewer
   - Bình luận
4. Sắp xếp: Mới nhất trước

---

### UC-M2-011: Gửi Email Thông Báo (Send Email Notifications)
**ID**: UC-M2-011 | **Độ Ưu Tiên**: 🔴 P0 | **Tác Nhân**: Hệ thống  
**Liên Quan**: US-FCR-006, US-UNR-006, FR-APR-016

**Mục Tiêu**: Gửi email tự động khi trạng thái thay đổi  
**Luồng Chính**:
1. Trạng thái bài báo thay đổi
2. Hệ thống xác định người nhận dựa trên trạng thái mới
3. Hệ thống tạo nội dung email
4. Hệ thống gửi email qua SMTP
5. Hệ thống ghi nhật ký sự kiện gửi email

**Mẫu Email**:
- SUBMITTED → Faculty Reviewer
- REVISION_REQUIRED → Researcher
- FACULTY_APPROVED → Researcher + University Reviewer
- PUBLISHED → Researcher

**Quy Tắc Nghiệp Vụ**: BR-APR-004 (phải bao gồm liên kết trực tiếp)

---

### UC-M2-015: Giám Sát SLA (SLA Monitoring)
**ID**: UC-M2-015 | **Độ Ưu Tiên**: 🟢 P2 | **Tác Nhân**: Hệ thống/Reviewers  
**Liên Quan**: US-FCR-009, FR-APR-020

**Mục Tiêu**: Theo dõi và làm nổi bật các bài xét duyệt quá hạn  
**Luồng Chính**:
1. Hệ thống tính toán thời gian ở trạng thái hiện tại
2. Nếu > 7 ngày: Đánh dấu là quá hạn (overdue)
3. Dashboard hiển thị:
   - Các bài quá hạn SLA
   - Thời gian xét duyệt trung bình
   - % trong hạn SLA

**Quy Tắc Nghiệp Vụ**: BR-APR-006 (Mục tiêu SLA)

---

**Tài liệu liên quan**:
- [Use Case Cấp Cao UC-HL-002](../High_Level/uc_hl_02_approval_workflow.md)
- [User Stories - Researcher, Reviewers](../../04_User_Stories/By_Role/)
- [Yêu Cầu - Quy Trình Xét Duyệt](../../03_Requirements/Functional/module_approval_workflow.md)
