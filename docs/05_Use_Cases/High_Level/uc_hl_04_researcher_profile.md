# UC-HL-004: Quản Lý Hồ Sơ Nhà Nghiên Cứu (Researcher Profile Management)

> **Module**: 4 - Hồ Sơ Nhà Nghiên Cứu  
> **Độ Ưu Tiên**: 🟡 P1 - Nên Có  
> **Tác Nhân**: Researcher, Public Visitor

---

## 📋 Tổng Quan Use Case

**ID**: UC-HL-004  
**Tên**: Quản Lý Hồ Sơ Nhà Nghiên Cứu  
**Mô Tả**: Giảng viên quản lý hồ sơ công khai của mình, hiển thị thông tin cá nhân, danh sách công trình ĐÃ XUẤT BẢN (PUBLISHED), và các phân tích (analytics). Public visitors có thể xem hồ sơ để tìm hiểu về giảng viên.

---

## 👥 Tác Nhân

### Tác Nhân Chính
- **Researcher**: Chỉnh sửa hồ sơ và xem phân tích
- **Public Visitor**: Xem hồ sơ công khai (không cần đăng nhập)

---

## 🎯 Mục Tiêu

- Tăng độ hiển thị (visibility) và mức độ ảnh hưởng (impact) của giảng viên
- Tạo danh mục (portfolio) nghiên cứu chuyên nghiệp
- Hỗ trợ kết nối (networking) học thuật
- Tối ưu SEO cho Google Scholar

---

## 🔗 Tài Liệu Liên Quan

**User Stories** (6 stories):
- US-RES-014: Xem Profile Công Khai Của Mình (P1)
- US-RES-015: Chỉnh Sửa Profile (P1)
- US-RES-016: Xem Danh Sách Bài Báo Trên Profile (P1)
- US-RES-022: Xem Biểu Đồ Năng Suất (P2)
- US-RES-023: Xem Word Cloud Lĩnh Vực (P2)
- US-VIW-008: Xem Profile Giảng Viên (P2)

**Yêu Cầu Chức Năng**: FR-PRO-001 đến FR-PRO-006

---

## 📊 Cấu Trúc Hồ Sơ

```mermaid
graph TB
    A[Trang Hồ Sơ Công Khai] --> B[Phần Header]
    A --> C[Phần Tiểu Sử]
    A --> D[Phần Bài Báo]
    A --> E[Phần Phân Tích]
    
    B --> B1[Ảnh Đại Diện]
    B --> B2[Tên & Chức Danh]
    B --> B3[Khoa/Viện]
    B --> B4[Thông Tin Liên Hệ]
    
    C --> C1[Văn Bản Tiểu Sử]
    C --> C2[Lĩnh Vực Nghiên Cứu]
    C --> C3[Liên Kết Ngoài<br/>ORCID, Scholar]
    
    D --> D1[Danh Sách Bài Báo]
    D --> D2[Lọc Theo Loại]
    D --> D3[Tùy Chọn Sắp Xếp]
    
    E --> E1[Biểu Đồ Bài Báo/Năm]
    E --> E2[Phân Bố Theo Hạng (Quartile)]
    E --> E3[Word Cloud Từ Khóa]
    
    style A fill:#ffd93d
    style D fill:#6bcf7f
    style E fill:#c8b6ff
```

---

## 🔄 Luồng Chính (Main Flows)

### Flow 1: Xem Hồ Sơ Công Khai (Bất kỳ ai)

1. Người dùng truy cập `/profile/[tên_người_dùng]` (không cần đăng nhập)
2. Hệ thống lấy dữ liệu giảng viên
3. Hệ thống hiển thị trang hồ sơ bao gồm:
   - Header: Ảnh, tên, chức danh, khoa
   - Tiểu sử: Lĩnh vực nghiên cứu, liên hệ
   - Bài báo: Chỉ hiển thị bài đã PUBLISHED, sắp xếp theo năm
   - Phân tích: Biểu đồ và word cloud
4. Người dùng có thể nhấn vào bài báo để xem chi tiết
5. Người dùng có thể nhấn vào liên kết ngoài (ORCID, Scholar)

---

### Flow 2: Chỉnh Sửa Hồ Sơ (Chỉ Researcher)

1. Researcher đăng nhập
2. Researcher nhấn "Chỉnh Sửa Hồ Sơ"
3. Hệ thống hiển thị biểu mẫu chỉnh sửa:
   - Tải lên ảnh đại diện
   - Chỉnh sửa tiểu sử (tối đa 500 ký tự)
   - Chỉnh sửa lĩnh vực nghiên cứu
   - Thêm liên kết ORCID, Google Scholar
   - Thêm trang web cá nhân
4. Researcher thực hiện thay đổi
5. Researcher nhấn "Lưu"
6. Hệ thống xác thực đầu vào
7. Hệ thống cập nhật cơ sở dữ liệu
8. Hệ thống hiển thị "Lưu thành công"

---

### Flow 3: Xem Danh Sách Bài Báo Trên Hồ Sơ

1. Bất kỳ ai xem hồ sơ giảng viên
2. Hệ thống hiển thị phần bài báo
3. Hiển thị: Tiêu đề, Tạp chí, Năm, DOI, Loại
4. Người dùng có thể lọc theo:
   - Loại bài báo (Tạp chí/Hội nghị)
   - Khoảng năm
5. Người dùng có thể sắp xếp theo:
   - Năm (mới nhất trước - mặc định)
   - Chỉ số ảnh hưởng (Impact factor)
6. Nhấn vào bài báo → chuyển đến trang chi tiết

---

### Flow 4: Xem Phân Tích (P2)

1. Người dùng xem hồ sơ có bật tính năng phân tích
2. Hệ thống tạo:
   - **Biểu Đồ Cột**: Số bài báo theo năm
   - **Biểu Đồ Tròn**: Phân bố theo xếp hạng (Q1/Q2/Q3/Q4)
   - **Word Cloud**: Các từ khóa phổ biến nhất từ tất cả các bài báo
3. Các biểu đồ có tính tương tác (di chuột để xem chi tiết)
4. Dữ liệu tự động cập nhật khi có bài báo mới được xuất bản

---

## ✅ Điều Kiện Tiên Quyết

- Tài khoản Researcher tồn tại trong hệ thống
- Để xem công khai: Có ít nhất 1 bài báo PUBLISHED (khuyến nghị)
- Để chỉnh sửa: Người dùng đã xác thực (đăng nhập)

---

## 📝 Điều Kiện Hậu Quyết

**Thành Công**:
- Hồ sơ hiển thị tại `/profile/[tên_người_dùng]`
- Các thay đổi được lưu vào cơ sở dữ liệu
- Phân tích phản ánh dữ liệu bài báo hiện tại

---

## 🔒 Quy Tắc Nghiệp Vụ

### BR-PRO-001: Tính Hiển Thị
- Hồ sơ là CÔNG KHAI (không yêu cầu đăng nhập để xem)
- CHỈ hiển thị các bài báo PUBLISHED
- KHÔNG hiển thị: DRAFT, SUBMITTED, REVIEWING

### BR-PRO-002: Quyền Chỉnh Sửa
- CHỈ chủ sở hữu (owner) mới được chỉnh sửa hồ sơ
- Admin có thể xem nhưng không được chỉnh sửa (quyền riêng tư)

### BR-PRO-003: Nguồn Dữ Liệu
- Thông tin cơ bản: Từ LDAP/AD (tên, email, khoa)
- Thông tin tùy chọn: Người dùng tự chỉnh sửa (tiểu sử, sở thích, liên kết)
- Bài báo: Tự động điền từ bảng danh sách bài báo (publications table)

### BR-PRO-004: Tải Ảnh
- Định dạng cho phép: JPG, PNG
- Kích thước tối đa: 2MB
- Tự động thay đổi kích thước về 300x300px
- Mặc định: Logo trường hoặc tên viết tắt

### BR-PRO-005: SEO
- URL duy nhất cho mỗi giảng viên
- Thẻ Meta chứa tên giảng viên
- Open Graph để chia sẻ mạng xã hội

---

## 📐 Use Cases Con (Cấp Trung)

- [UC-M4-001: Xem Hồ Sơ Công Khai](../Medium_Level/module_04_researcher_profile.md)
- [UC-M4-002: Chỉnh Sửa Hồ Sơ](../Medium_Level/module_04_researcher_profile.md)
- [UC-M4-003: Cập Nhật Ảnh Đại Diện](../Medium_Level/module_04_researcher_profile.md)
- [UC-M4-004: Liên Kết ORCID](../Medium_Level/module_04_researcher_profile.md)
- [UC-M4-005: Xem Phân Tích Bài Báo](../Medium_Level/module_04_researcher_profile.md)
- [UC-M4-006: Tạo Word Cloud](../Medium_Level/module_04_researcher_profile.md)

---

## 📊 Chỉ Số Chính

- **Mức độ áp dụng**: % giảng viên có hồ sơ đầy đủ
- **Độ hiển thị**: Số lượt xem trang hồ sơ
- **Tương tác**: Số lượt click vào liên kết ngoài (ORCID, Scholar)
- **Hiệu năng**: Tải trang < 2 giây

---

## 🚨 Ngoại Lệ

| Lỗi | Điều Kiện | Phản Hồi Hệ Thống |
|-------|-----------|-----------------|
| Không tìm thấy hồ sơ | Tên người dùng không tồn tại | Hiển thị trang 404 |
| Không có bài báo | Giảng viên có 0 bài PUBLISHED | Hiển thị trạng thái trống kèm thông báo |
| Tải ảnh thất bại | File quá lớn/sai định dạng | Hiển thị lỗi kèm yêu cầu |
| ORCID không hợp lệ | Định dạng ORCID sai | Xác thực định dạng, hiển thị lỗi |

---

**Tài liệu liên quan**:
- [User Stories - Researcher](../../04_User_Stories/By_Role/researcher_stories.md#module-4-researcher-profile)
- [Yêu Cầu - Hồ Sơ Nhà Nghiên Cứu](../../03_Requirements/Functional/module_profile.md)
