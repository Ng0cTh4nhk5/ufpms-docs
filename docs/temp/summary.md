# Tổng Hợp Nội Dung Đã Nghiên Cứu

## Nguồn
Tài liệu này tổng hợp từ file `temp/temp.md` - nội dung nghiên cứu ban đầu về hệ thống quản lý công trình NCKH.

---

## 1. Ngữ Cảnh Bài Toán ✅

### Đã Phân Tích
**Hệ thống mục tiêu**: Xây dựng hệ thống quản lý công trình nghiên cứu khoa học

**Định nghĩa cốt lõi**: 
- Công trình NCKH là sản phẩm hình thành từ việc thực hiện "Đề tài nghiên cứu khoa học"
- Tồn tại dưới 7 nhóm dạng thức chính với 28 loại cụ thể

### Tài Liệu Đã Tạo
✅ [`docs/01_System_Specification/system_overview.md`](file:///d:/HomeworkProject/DoAnPTHTWeb/DoAnCuoiKy/docs/01_System_Specification/system_overview.md)
- Tổng quan hệ thống
- Ngữ cảnh và vấn đề
- Mục đích hệ thống
- Môi trường triển khai

✅ [`docs/01_System_Specification/system_scope.md`](file:///d:/HomeworkProject/DoAnPTHTWeb/DoAnCuoiKy/docs/01_System_Specification/system_scope.md)
- Phạm vi chi tiết của 7 nhóm công trình
- Ranh giới rõ ràng (trong/ngoài scope)
- Ranh giới dữ liệu, tích hợp, công nghệ

✅ [`docs/02_System_Clarification/Business_Context/problem_statement.md`](file:///d:/HomeworkProject/DoAnPTHTWeb/DoAnCuoiKy/docs/02_System_Clarification/Business_Context/problem_statement.md)
- 7 vấn đề chính cần giải quyết
- Nguyên nhân và tác động
- Tiêu chí thành công

---

## 2. Dạng Thức Công Trình NCKH ✅

### Đã Phân Loại Chi Tiết

**Nhóm 1: Công bố và Ấn phẩm** (7 loại)
- Sách chuyên khảo, giáo trình, sách tham khảo
- Bài báo tạp chí, kỷ yếu hội thảo
- Báo cáo kiến nghị, báo cáo tổng kết

**Nhóm 2: Tài sản Trí tuệ** (5 loại)
- Bằng sáng chế, giải pháp hữu ích
- Bảo hộ giống cây trồng, kiểu dáng công nghiệp
- Đăng ký quyền tác giả

**Nhóm 3: Sản phẩm Kỹ thuật & Công nghệ** (5 loại)
- Vật liệu mới, mẫu vật/chế phẩm
- Thiết bị máy móc, dây chuyền công nghệ
- Mô hình vật lý

**Nhóm 4: Tiêu chuẩn & Quy phạm** (3 loại)
- TCVN, QCVN, TCCS

**Nhóm 5: Thiết kế & Quy hoạch** (3 loại)
- Bản vẽ thiết kế, đồ án quy hoạch
- Tác phẩm kiến trúc

**Nhóm 6: Dữ liệu & Số hóa** (3 loại)
- Phần mềm, cơ sở dữ liệu, bản đồ chuyên đề

**Nhóm 7: Văn hóa - Nghệ thuật** (2 loại)
- Tác phẩm nghệ thuật, chương trình biểu diễn

### Tài Liệu Đã Tạo
✅ [`docs/03_Requirements/Functional/research_output_catalog.md`](file:///d:/HomeworkProject/DoAnPTHTWeb/DoAnCuoiKy/docs/03_Requirements/Functional/research_output_catalog.md)
- Chi tiết 28 dạng thức
- Thông tin cần quản lý cho từng loại
- Cơ sở cho thiết kế database

---

## 3. Mục Đích Hệ Thống ✅

### Đã Xác Định

**Mục tiêu chính**: 
1. Lưu trữ số hóa thông tin công trình
2. Quản lý phân loại theo dạng thức
3. Tra cứu nhanh theo nhiều tiêu chí
4. Báo cáo thống kê tự động
5. Khai thác giá trị công trình

**Lợi ích**:
- Cơ quan quản lý: Nắm bắt tổng quan, hỗ trợ quyết định
- Nhà nghiên cứu: Quản lý hồ sơ, chứng minh năng lực
- Tổ chức: Quản lý tài sản trí tuệ, nâng cao uy tín

### Tài Liệu Đã Tạo
✅ Đã tích hợp trong [`system_overview.md`](file:///d:/HomeworkProject/DoAnPTHTWeb/DoAnCuoiKy/docs/01_System_Specification/system_overview.md)
- Phần 3: Mục Đích Của Hệ Thống
- Phần 7: Các Bên Liên Quan

---

## 4. Phạm Vi Hệ Thống ✅

### Đã Xác Định Ranh Giới

**Trong phạm vi**:
- Quản lý 7 nhóm công trình với thông tin đầy đủ
- Tra cứu, tìm kiếm nâng cao
- Thống kê, báo cáo linh hoạt
- Phân quyền người dùng
- Quản trị hệ thống

**Ngoài phạm vi**:
- Quản lý quy trình thực hiện đề tài
- Quản lý tài chính, kinh phí
- Hệ thống peer review chi tiết
- Nền tảng xuất bản trực tuyến
- Quản lý thiết bị phòng lab

### Tài Liệu Đã Tạo
✅ [`docs/01_System_Specification/system_scope.md`](file:///d:/HomeworkProject/DoAnPTHTWeb/DoAnCuoiKy/docs/01_System_Specification/system_scope.md)
- Ma trận scope rõ ràng
- 5 ranh giới: chức năng, dữ liệu, tích hợp, người dùng, công nghệ

---

## 5. Các Bên Liên Quan ✅

### Đã Phân Loại

**Stakeholders Chính**:
1. Nhà nghiên cứu (⭐⭐⭐⭐⭐)
2. Cán bộ QLKH (⭐⭐⭐⭐⭐)
3. Lãnh đạo cơ quan (⭐⭐⭐⭐)

**Stakeholders Phụ**:
4. Sinh viên/NCS (⭐⭐⭐)
5. Ban TCCB (⭐⭐⭐)
6. IT Team (⭐⭐⭐⭐)

**Stakeholders Bên Ngoài**:
7. Bộ KH&CN, Bộ GD&ĐT (⭐⭐⭐)
8. Doanh nghiệp (⭐⭐)
9. Cộng đồng quốc tế (⭐⭐)

### Tài Liệu Đã Tạo
✅ [`docs/01_System_Specification/stakeholders.md`](file:///d:/HomeworkProject/DoAnPTHTWeb/DoAnCuoiKy/docs/01_System_Specification/stakeholders.md)
- Vai trò, trách nhiệm mỗi nhóm
- Ma trận stakeholder
- Nhu cầu và chiến lược tiếp cận

---

## 6. Công Nghệ 🚧

### Ghi Chú Từ Nghiên Cứu
- Item 4 trong temp.md chỉ ghi "Công nghệ" chưa có chi tiết

### Đã Đề Xuất Sơ Bộ
Trong [`system_overview.md`](file:///d:/HomeworkProject/DoAnPTHTWeb/DoAnCuoiKy/docs/01_System_Specification/system_overview.md), phần 6:
- Frontend: HTML5, CSS3, JavaScript (React/Vue/Angular)
- Backend: .NET Core, Java Spring Boot, hoặc Node.js
- Database: PostgreSQL, MySQL, hoặc SQL Server
- Authentication: OAuth 2.0, JWT

### Cần Bổ Sung
📝 **TODO**: Tạo file chi tiết về công nghệ:
- `docs/01_System_Specification/technology_stack.md`
- Lý do chọn công nghệ
- So sánh các lựa chọn
- Kiến trúc hệ thống (architecture diagram)

---

## Tổng Kết Tiến Độ

### ✅ Đã Hoàn Thành (từ temp.md)

| Mục | Trạng thái | Tài liệu |
|-----|-----------|----------|
| 1. Ngữ cảnh bài toán | ✅ Hoàn thành | system_overview.md, problem_statement.md |
| 2. Mục đích hệ thống | ✅ Hoàn thành | system_overview.md |
| 3. Phạm vi & Bên liên quan | ✅ Hoàn thành | system_scope.md, stakeholders.md |
| Dạng thức công trình | ✅ Hoàn thành | research_output_catalog.md |

### 🚧 Cần Bổ Sung

| Mục | Ưu tiên | Gợi ý tài liệu |
|-----|---------|----------------|
| 4. Công nghệ chi tiết | Cao | technology_stack.md, architecture_diagram |
| Yêu cầu chức năng chi tiết | Cao | functional_requirements.md (từ catalog) |
| Yêu cầu phi chức năng | Cao | performance.md, security.md, usability.md |
| User stories | Trung bình | admin_stories.md, researcher_stories.md |
| Use cases | Trung bình | uc_*.md files |

---

## Tài Liệu Tham Khảo

### File Nguồn
- [`docs/temp/temp.md`](file:///d:/HomeworkProject/DoAnPTHTWeb/DoAnCuoiKy/docs/temp/temp.md) - Nội dung nghiên cứu gốc

### Tài Liệu Đã Tạo (5 files)
1. [`system_overview.md`](file:///d:/HomeworkProject/DoAnPTHTWeb/DoAnCuoiKy/docs/01_System_Specification/system_overview.md)
2. [`system_scope.md`](file:///d:/HomeworkProject/DoAnPTHTWeb/DoAnCuoiKy/docs/01_System_Specification/system_scope.md)
3. [`stakeholders.md`](file:///d:/HomeworkProject/DoAnPTHTWeb/DoAnCuoiKy/docs/01_System_Specification/stakeholders.md)
4. [`problem_statement.md`](file:///d:/HomeworkProject/DoAnPTHTWeb/DoAnCuoiKy/docs/02_System_Clarification/Business_Context/problem_statement.md)
5. [`research_output_catalog.md`](file:///d:/HomeworkProject/DoAnPTHTWeb/DoAnCuoiKy/docs/03_Requirements/Functional/research_output_catalog.md)

---

*Tài liệu tổng hợp này sẽ được cập nhật khi có thêm nghiên cứu.*
