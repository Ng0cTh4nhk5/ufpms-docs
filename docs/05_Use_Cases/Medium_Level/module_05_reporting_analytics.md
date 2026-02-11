# Module 5: Báo Cáo & Phân Tích - Use Cases Cấp Trung

> **Module**: 5 - Báo Cáo & Phân Tích  
> **Use Case Cấp Cao**: [UC-HL-005](../High_Level/uc_hl_05_reporting_analytics.md)

---

## UC-M5-001: Tạo Báo Cáo Khoa (Generate Faculty Report)
**ID**: UC-M5-001 | **Độ Ưu Tiên**: 🟡 P1 | **Tác Nhân**: Faculty Reviewer  
**Liên Quan**: US-FCR-008, FR-REP-002

**Mục Tiêu**: Tạo báo cáo bài báo cấp khoa  
**Điều Kiện Tiên Quyết**: Người dùng là Faculty Reviewer  
**Luồng Chính**:
1. Reviewer chọn tham số:
   - Khoảng năm (từ-đến)
   - Nhóm theo: Researcher, Xếp hạng (Quartile), Loại
2. Reviewer nhấn "Tạo Báo Cáo"
3. Hệ thống truy vấn các bài báo MÀ khoa = khoa của reviewer VÀ trạng thái = PUBLISHED
4. Hệ thống tạo báo cáo:
   - Tóm tắt: Tổng cộng, theo xếp hạng, theo loại
   - Chi tiết theo Researcher
   - Danh sách bài báo chi tiết
5. Hệ thống hiển thị bản xem trước

**Quy Tắc Nghiệp Vụ**: BR-REP-001 (chỉ khoa của mình), BR-REP-002 (chỉ PUBLISHED)

---

## UC-M5-002: Tạo Báo Cáo Trường (Generate University Report)
**ID**: UC-M5-002 | **Độ Ưu Tiên**: 🟡 P1 | **Tác Nhân**: University Reviewer  
**Liên Quan**: US-UNR-008, FR-REP-002, FR-REP-005

**Mục Tiêu**: Tạo báo cáo toàn trường  
**Điều Kiện Tiên Quyết**: Người dùng là University Reviewer hoặc SuperAdmin  
**Luồng Chính**:
1. Reviewer chọn tham số:
   - Khoảng năm
   - Bộ lọc khoa (tất cả hoặc cụ thể)
   - Tùy chọn nhóm
2. Reviewer nhấn "Tạo Báo Cáo"
3. Hệ thống truy vấn tất cả các khoa
4. Hệ thống tạo báo cáo toàn diện:
   - Tóm tắt toàn trường
   - So sánh theo khoa
   - Theo nhà nghiên cứu (top researchers)
   - Danh sách chi tiết
5. Hệ thống hiển thị thanh tiến trình (có thể mất 30s-5phút)

**Điều Kiện Hậu Quyết**: Báo cáo sẵn sàng để xuất  
**Quy Tắc Nghiệp Vụ**: BR-REP-001 (truy cập toàn trường), BR-REP-004 (thời gian < 5phút)

---

## UC-M5-003: Xuất Excel (Export to Excel)
**ID**: UC-M5-003 | **Độ Ưu Tiên**: 🟡 P1 | **Tác Nhân**: Faculty/University Reviewer  
**Liên Quan**: FR-REP-006

**Mục Tiêu**: Xuất báo cáo ra định dạng Excel  
**Luồng Chính**:
1. Người dùng đã tạo báo cáo
2. Người dùng nhấn "Xuất ra Excel"
3. Hệ thống tạo file .xlsx với nhiều sheet:
   - Tóm tắt
   - Theo Khoa
   - Theo Researcher
   - Chi tiết (tất cả bài báo)
4. Hệ thống tải xuống file: `report_YYYY-MM-DD.xlsx`

**Quy Tắc Nghiệp Vụ**: BR-REP-005 (lưu trữ 30 ngày)

---

## UC-M5-004: Xuất PDF (Export to PDF)
**ID**: UC-M5-004 | **Độ Ưu Tiên**: 🟡 P1 | **Tác Nhân**: Faculty/University Reviewer  
**Liên Quan**: FR-REP-006

**Mục Tiêu**: Xuất báo cáo định dạng PDF  
**Luồng Chính**:
1. Người dùng đã tạo báo cáo
2. Người dùng nhấn "Xuất ra PDF"
3. Hệ thống tạo file PDF được định dạng với:
   - Trang bìa (logo trường, ngày)
   - Trang tóm tắt với biểu đồ
   - Các bảng chi tiết
4. Hệ thống tải xuống file

---

## UC-M5-005: Xem Thống Kê Dashboard (View Dashboard Statistics)
**ID**: UC-M5-005 | **Độ Ưu Tiên**: 🟡 P1 | **Tác Nhân**: Faculty/University Reviewer  
**Liên Quan**: US-UNR-007, FR-REP-001

**Mục Tiêu**: Xem thống kê dashboard thời gian thực  
**Luồng Chính**:
1. Reviewer truy cập dashboard
2. Hệ thống hiển thị các chỉ số chính:
   - Tổng số bài báo (năm nay, mọi thời đại)
   - Phân bố theo xếp hạng (biểu đồ tròn)
   - Phân bố theo khoa (biểu đồ cột)
   - Đường xu hướng (5 năm qua)
   - Các nhà nghiên cứu hàng đầu
3. Các biểu đồ có tính tương tác
4. Dữ liệu cập nhật khi tải trang

**Quy Tắc Nghiệp Vụ**: BR-REP-003 (cache 1 giờ)

---

## UC-M5-006: Theo Dõi Xu Hướng Năng Suất (Track Productivity Trends)
**ID**: UC-M5-006 | **Độ Ưu Tiên**: 🟢 P2 | **Tác Nhân**: University Reviewer  
**Liên Quan**: US-UNR-010, FR-REP-004

**Mục Tiêu**: Phân tích xu hướng năng suất  
**Luồng Chính**:
1. Reviewer truy cập Phân Tích Xu Hướng
2. Hệ thống tính toán:
   - Tỷ lệ tăng trưởng theo năm (Year-over-year)
   - Các khoa tăng trưởng hàng đầu
   - Các lĩnh vực nghiên cứu mới nổi (tần suất từ khóa)
   - Các nhà nghiên cứu năng suất nhất năm nay
3. Hệ thống trực quan hóa bằng biểu đồ

---

## UC-M5-007: Đối Sánh Các Khoa (Benchmark Faculties)
**ID**: UC-M5-007 | **Độ Ưu Tiên**: 🟢 P2 | **Tác Nhân**: University Reviewer  
**Liên Quan**: FR-REP-007

**Mục Tiêu**: So sánh các khoa cạnh nhau  
**Luồng Chính**:
1. Reviewer chọn 2 khoa trở lên
2. Reviewer chọn khoảng năm
3. Hệ thống hiển thị bảng so sánh:
   - Tổng số bài báo
   - Theo xếp hạng (quartile)
   - Top researchers
4. Hệ thống làm nổi bật các bên có hiệu suất tốt nhất

---

**Tài liệu liên quan**:
- [Use Case Cấp Cao UC-HL-005](../High_Level/uc_hl_05_reporting_analytics.md)
- [User Stories - Reviewers](../../04_User_Stories/By_Role/)
- [Yêu Cầu - Báo Cáo](../../03_Requirements/Functional/module_reporting.md)
