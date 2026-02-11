# Module 3: Tìm Kiếm & Duyệt - Use Cases Cấp Trung

> **Module**: 3 - Tìm Kiếm & Duyệt  
> **Use Case Cấp Cao**: [UC-HL-003](../High_Level/uc_hl_03_search_browse.md)

---

## UC-M3-001: Tìm Kiếm Cơ Bản (Basic Search)
**ID**: UC-M3-001 | **Độ Ưu Tiên**: 🟡 P1 | **Tác Nhân**: Public Visitor, Tất Cả Người Dùng  
**Liên Quan**: US-VIW-001, FR-SEA-001

**Mục Tiêu**: Tìm kiếm bài báo sử dụng từ khóa  
**Điều Kiện Tiên Quyết**: Không (truy cập công khai)  
**Luồng Chính**:
1. Người dùng nhập từ khóa vào ô tìm kiếm
2. Người dùng nhấn "Tìm Kiếm"
3. Hệ thống tìm kiếm trong: Tiêu đề, Tóm tắt, Từ khóa, Tên tác giả
4. Hệ thống trả về CHỈ các bài báo ĐÃ XUẤT BẢN (PUBLISHED)
5. Hệ thống làm nổi bật từ khóa khớp
6. Hệ thống sắp xếp theo độ liên quan
7. Hệ thống phân trang (mặc định 20 kết quả/trang)

**Điều Kiện Hậu Quyết**: Kết quả được hiển thị  
**Quy Tắc Nghiệp Vụ**: BR-SEA-001 (chỉ PUBLISHED), BR-SEA-005 (hiệu năng < 1s)

---

## UC-M3-002: Tìm Kiếm Nâng Cao (Advanced Search)
**ID**: UC-M3-002 | **Độ Ưu Tiên**: 🟡 P1 | **Tác Nhân**: Public Visitor, Tất Cả Người Dùng  
**Liên Quan**: FR-SEA-002

**Mục Tiêu**: Tìm kiếm đa tiêu chí  
**Luồng Chính**:
1. Người dùng nhấn "Tìm Kiếm Nâng Cao"
2. Hệ thống hiển thị biểu mẫu với các trường:
   - Từ khóa, Tên tác giả, Tiêu đề
   - Khoảng năm, Khoa, Xếp hạng (Quartile)
3. Người dùng điền các tiêu chí
4. Hệ thống kết hợp với logic VÀ (AND)
5. Hệ thống trả về các bài báo khớp

**Quy Tắc Nghiệp Vụ**: Tất cả bộ lọc kết hợp với logic AND

---

## UC-M3-003: Lọc Kết Quả (Filter Results)
**ID**: UC-M3-003 | **Độ Ưu Tiên**: 🟡 P1 | **Tác Nhân**: Public Visitor  
**Liên Quan**: US-VIW-002, FR-SEA-002

**Mục Tiêu**: Lọc kết quả tìm kiếm theo nhiều tiêu chí  
**Luồng Chính**:
1. Người dùng có kết quả tìm kiếm
2. Người dùng áp dụng bộ lọc (thanh bên):
   - Khoảng năm (thanh trượt hoặc từ-đến)
   - Khoa (chọn nhiều)
   - Xếp hạng (Q1/Q2/Q3/Q4/Hội nghị)
   - Loại bài báo (Tạp chí/Hội nghị)
3. Hệ thống cập nhật kết quả động (AJAX)
4. Hệ thống hiển thị số lượng kết quả
5. Người dùng có thể xóa từng bộ lọc hoặc tất cả

**Quy Tắc Nghiệp Vụ**: Các bộ lọc được cộng dồn (logic AND)

---

## UC-M3-004: Sắp Xếp Kết Quả (Sort Results)
**ID**: UC-M3-004 | **Độ Ưu Tiên**: 🟡 P1 | **Tác Nhân**: Public Visitor  
**Liên Quan**: US-VIW-004, FR-SEA-007

**Mục Tiêu**: Sắp xếp kết quả tìm kiếm  
**Luồng Chính**:
1. Người dùng có kết quả tìm kiếm
2. Người dùng chọn tùy chọn sắp xếp:
   - Mới nhất trước (mặc định)
   - Cũ nhất trước
   - Được trích dẫn nhiều nhất (nếu có)
   - Chỉ số ảnh hưởng (cao xuống thấp)
3. Hệ thống sắp xếp lại kết quả
4. Phân trang reset về trang 1

---

## UC-M3-005: Xem Chi Tiết Bài Báo (View Publication Details)
**ID**: UC-M3-005 | **Độ Ưu Tiên**: 🔴 P0 | **Tác Nhân**: Public Visitor  
**Liên Quan**: US-VIW-006, FR-SEA-006

**Mục Tiêu**: Xem thông tin đầy đủ của bài báo  
**Điều Kiện Tiên Quyết**: Trạng thái bài báo = PUBLISHED  
**Luồng Chính**:
1. Người dùng nhấn vào bài báo từ kết quả tìm kiếm
2. Hệ thống hiển thị trang chi tiết:
   - Metadata đầy đủ
   - Tóm tắt (Abstract)
   - Link DOI (có thể nhấp)
   - Link hồ sơ tác giả
   - Nút tải PDF (nếu được phép)
   - Thông tin trích dẫn
3. Trang được tối ưu SEO (thẻ meta)

**Quy Tắc Nghiệp Vụ**: BR-SEA-006 (thẻ SEO), URL duy nhất cho mỗi bài báo

---

## UC-M3-006: Duyệt Theo Khoa (Browse by Faculty)
**ID**: UC-M3-006 | **Độ Ưu Tiên**: 🟡 P1 | **Tác Nhân**: Public Visitor  
**Liên Quan**: US-VIW-003, FR-SEA-003

**Mục Tiêu**: Duyệt bài báo theo khoa/phòng ban  
**Luồng Chính**:
1. Người dùng nhấn "Duyệt Theo Khoa"
2. Hệ thống hiển thị danh sách các khoa
3. Người dùng chọn một khoa
4. Hệ thống hiển thị tất cả các bài báo PUBLISHED từ khoa đó
5. Người dùng có thể đi sâu (drill down) theo năm hoặc nhà nghiên cứu

---

## UC-M3-007: Duyệt Theo Năm/Xếp Hạng (Browse by Year/Quartile)
**ID**: UC-M3-007 | **Độ Ưu Tiên**: 🟡 P1 | **Tác Nhân**: Public Visitor  
**Liên Quan**: US-VIW-003, FR-SEA-003

**Mục Tiêu**: Duyệt theo năm hoặc xếp hạng tạp chí  
**Luồng Chính**:
1. Người dùng nhấn "Duyệt Theo Năm" hoặc "Duyệt Theo Xếp Hạng"
2. Hệ thống hiển thị các tùy chọn (các năm hoặc Q1/Q2/Q3/Q4)
3. Người dùng chọn
4. Hệ thống hiển thị các bài báo khớp

---

**Tài liệu liên quan**:
- [Use Case Cấp Cao UC-HL-003](../High_Level/uc_hl_03_search_browse.md)
- [User Stories - Public Visitor](../../04_User_Stories/By_Role/public_visitor_stories.md)
- [Yêu Cầu - Tìm Kiếm](../../03_Requirements/Functional/module_search.md)
