# Module 4: Hồ Sơ Nhà Nghiên Cứu - Use Cases Cấp Trung

> **Module**: 4 - Hồ Sơ Nhà Nghiên Cứu  
> **Use Case Cấp Cao**: [UC-HL-004](../High_Level/uc_hl_04_researcher_profile.md)

---

## UC-M4-001: Xem Hồ Sơ Công Khai (View Public Profile)
**ID**: UC-M4-001 | **Độ Ưu Tiên**: 🟡 P1 | **Tác Nhân**: Public Visitor, Tất Cả Người Dùng  
**Liên Quan**: US-RES-014, US-VIW-008, FR-PRO-001

**Mục Tiêu**: Xem hồ sơ công khai của nhà nghiên cứu  
**Điều Kiện Tiên Quyết**: Không (truy cập công khai)  
**Luồng Chính**:
1. Người dùng truy cập `/profile/[tên_người_dùng]`
2. Hệ thống lấy dữ liệu nhà nghiên cứu
3. Hệ thống hiển thị trang hồ sơ:
   - Header: Ảnh, tên, chức danh, khoa
   - Tiểu sử: Lĩnh vực nghiên cứu, thông tin liên hệ
   - Liên kết ngoài: ORCID, Google Scholar
   - Bài báo: CHỈ các bài PUBLISHED, sắp xếp theo năm
   - Biểu đồ phân tích (nếu được bật)
4. Người dùng có thể nhấn vào bài báo để xem chi tiết

**Điều Kiện Hậu Quyết**: Hồ sơ được hiển thị  
**Quy Tắc Nghiệp Vụ**: BR-PRO-001 (chỉ PUBLISHED), BR-PRO-005 (SEO)

---

## UC-M4-002: Chỉnh Sửa Hồ Sơ (Edit Profile)
**ID**: UC-M4-002 | **Độ Ưu Tiên**: 🟡 P1 | **Tác Nhân**: Researcher  
**Liên Quan**: US-RES-015, FR-PRO-002

**Mục Tiêu**: Chỉnh sửa thông tin hồ sơ công khai  
**Điều Kiện Tiên Quyết**: Người dùng đã đăng nhập, đang xem hồ sơ của mình  
**Luồng Chính**:
1. Researcher nhấn "Chỉnh Sửa Hồ Sơ"
2. Hệ thống hiển thị biểu mẫu chỉnh sửa:
   - Tiểu sử (tối đa 500 ký tự)
   - Lĩnh vực nghiên cứu
   - ORCID
   - Liên kết Google Scholar
   - Website cá nhân
3. Researcher thực hiện thay đổi
4. Researcher nhấn "Lưu"
5. Hệ thống xác thực đầu vào
6. Hệ thống cập nhật cơ sở dữ liệu
7. Hệ thống hiển thị "Lưu thành công"

**Quy Tắc Nghiệp Vụ**: BR-PRO-002 (chỉ chủ sở hữu mới được sửa)

---

## UC-M4-003: Cập Nhật Ảnh Đại Diện (Update Profile Photo)
**ID**: UC-M4-003 | **Độ Ưu Tiên**: 🟡 P1 | **Tác Nhân**: Researcher  
**Liên Quan**: FR-PRO-002

**Mục Tiêu**: Tải lên hoặc thay đổi ảnh đại diện  
**Luồng Chính**:
1. Researcher nhấn "Chỉnh Sửa Hồ Sơ"
2. Researcher nhấn "Đổi Ảnh"
3. Researcher chọn file ảnh (JPG/PNG, < 2MB)
4. Hệ thống xác thực file
5. Hệ thống tự động thay đổi kích thước về 300x300px
6. Hệ thống lưu ảnh
7. Hệ thống hiển thị ảnh mới

**Quy Tắc Nghiệp Vụ**: BR-PRO-004 (định dạng, kích thước, resize)

---

## UC-M4-004: Liên Kết ORCID (Link ORCID)
**ID**: UC-M4-004 | **Độ Ưu Tiên**: 🟡 P1 | **Tác Nhân**: Researcher  
**Liên Quan**: FR-PRO-002

**Mục Tiêu**: Liên kết hồ sơ ORCID  
**Luồng Chính**:
1. Researcher nhập ID ORCID trong hồ sơ
2. Hệ thống xác thực định dạng (0000-0000-0000-000X)
3. Hệ thống lưu ORCID
4. Hệ thống hiển thị huy hiệu ORCID trên hồ sơ
5. Huy hiệu liên kết đến `orcid.org/[ORCID]`

**Quy Tắc Nghiệp Vụ**: Xác thực định dạng ORCID

---

## UC-M4-005: Xem Phân Tích Bài Báo (View Publication Analytics)
**ID**: UC-M4-005 | **Độ Ưu Tiên**: 🟢 P2 | **Tác Nhân**: Researcher, Public Visitor  
**Liên Quan**: US-RES-022, FR-PRO-004

**Mục Tiêu**: Xem biểu đồ năng suất bài báo  
**Luồng Chính**:
1. Người dùng xem hồ sơ
2. Hệ thống tạo biểu đồ:
   - Biểu đồ cột: Bài báo theo năm
   - Biểu đồ tròn: Phân bố theo xếp hạng (quartile)
3. Biểu đồ có tính tương tác (di chuột để xem số lượng)
4. Dữ liệu cập nhật khi có bài báo mới xuất bản

**Quy Tắc Nghiệp Vụ**: Dựa trên CHỈ các bài báo PUBLISHED

---

## UC-M4-006: Tạo Word Cloud (Generate Word Cloud)
**ID**: UC-M4-006 | **Độ Ưu Tiên**: 🟢 P2 | **Tác Nhân**: Researcher, Public Visitor  
**Liên Quan**: US-RES-023, FR-PRO-005

**Mục Tiêu**: Trực quan hóa lĩnh vực nghiên cứu qua đám mây từ khóa (word cloud)  
**Luồng Chính**:
1. Người dùng xem hồ sơ
2. Hệ thống trích xuất từ khóa từ tất cả bài báo
3. Hệ thống tính toán tần suất
4. Hệ thống tạo word cloud (kích thước chữ = tần suất)
5. Hệ thống hiển thị trên hồ sơ

**Quy Tắc Nghiệp Vụ**: Từ khóa từ các bài báo PUBLISHED

---

**Tài liệu liên quan**:
- [Use Case Cấp Cao UC-HL-004](../High_Level/uc_hl_04_researcher_profile.md)
- [User Stories - Researcher](../../04_User_Stories/By_Role/researcher_stories.md)
- [Yêu Cầu - Hồ Sơ](../../03_Requirements/Functional/module_profile.md)
