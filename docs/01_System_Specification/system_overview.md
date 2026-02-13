# Đặc Tả Hệ Thống: Module Quản Lý Bài Báo Khoa Học

## 1. Tên Hệ Thống

**Hệ thống Quản lý Bài báo Khoa học cho Giảng viên Đại học**  
*(University Faculty Publication Management System - UFPMS)*

---

## 2. Bối Cảnh và Mục Đích

### 2.1. Bối Cảnh Đồ Án

> ⚠️ **Lưu ý về phạm vi**: Đây là module CON trong hệ thống quản lý công trình NCKH tổng thể. Xem [folder 00_Problem_Context](../00_Problem_Context/README.md) để hiểu toàn cảnh bài toán.

**Vấn đề cụ thể đồ án giải quyết:**

Tại các trường đại học Việt Nam, việc quản lý **bài báo khoa học** của giảng viên đang gặp nhiều vấn đề:

❌ **Phân tán dữ liệu:**
- Mỗi giảng viên tự quản lý CV riêng (file Word/PDF)
- Phòng/(Trung tâm) QLKH lưu riêng trong Excel
- Khó tổng hợp, thống kê

❌ **Thiếu tính minh bạch:**
- Sinh viên không biết giảng viên đang nghiên cứu gì
- Khó tìm người hướng dẫn phù hợp với hướng nghiên cứu

❌ **Báo cáo thủ công:**
- Mỗi kỳ phải thu thập lại từ giảng viên
- Nhập liệu nhiều lần cho các báo cáo khác nhau
- Dễ sai sót, trùng lặp

❌ **Khó đánh giá:**
- Không có công cụ phân tích nhanh năng suất nghiên cứu
- Không theo dõi được chỉ số citation, impact factor
- Khó so sánh giữa các khoa/viện

---

### 2.2. Mục Đích Hệ Thống

Xây dựng **module phần mềm quản lý bài báo khoa học** giúp:

✅ **Cho giảng viên:**
- Dễ dàng đăng ký, cập nhật bài báo
- Có profile nghiên cứu cá nhân trực tuyến
- Tự động tích hợp từ ORCID, Google Scholar (nếu có)

✅ **Cho phòng QLKH:**
- Quản lý tập trung tất cả bài báo của trường
- Tạo báo cáo nhanh theo yêu cầu
- Phân tích thống kê đa chiều

✅ **Cho lãnh đạo:**
- Giám sát năng suất nghiên cứu theo thời gian thực
- Đánh giá hiệu quả chính sách khuyến khích
- Hỗ trợ ra quyết định chiến lược

✅ **Cho sinh viên:**
- Tìm hiểu hướng nghiên cứu của giảng viên
- Chọn người hướng dẫn phù hợp
- Khám phá kiến thức khoa học

---

## 3. Phạm Vi Hệ Thống

### 3.1. Trong Phạm Vi (In Scope)

#### A. Loại Công Trình

✅ **CHỈ quản lý Bài báo khoa học** (Journal Articles), bao gồm:
- Bài báo trên tạp chí quốc tế (ISI/Scopus)
- Bài báo trên tạp chí trong nước (có ISSN)
- Bài báo hội thảo quốc tế (có ISBN)

❌ **KHÔNG bao gồm**:
- Sách, giáo trình
- Bằng sáng chế
- Phần mềm, sản phẩm kỹ thuật
- ... (xem đầy đủ 7 nhóm tại [folder 00](../00_Problem_Context/README.md))

---

#### B. Chức Năng Chính

**Module 1: Quản lý Bài báo**
- ✅ Thêm/Sửa/Xóa bài báo
- ✅ Upload file PDF bài báo
- ✅ Phân loại theo: Q1/Q2/Q3/Q4 (Scopus), Impact Factor
- ✅ Gắn tag từ khóa, lĩnh vực nghiên cứu
- ✅ Liên kết đồng tác giả (giảng viên khác trong trường)
- ✅ **Chuyển đổi giờ làm/giờ dạy** (sau khi bài báo được phê duyệt)

**Module 2: Tìm kiếm & Tra cứu**
- ✅ Tìm theo tiêu đề, tác giả, từ khóa
- ✅ Lọc theo loại tạp chí, năm xuất bản, đơn vị
- ✅ Sắp xếp theo Impact Factor, số lượng trích dẫn
- ✅ Xem chi tiết bài báo + tải PDF

**Module 3: Profile Giảng viên**
- ✅ Trang cá nhân công khai
- ✅ Danh sách bài báo đã xuất bản
- ✅ Biểu đồ năng suất nghiên cứu theo năm
- ✅ Lĩnh vực chuyên môn (word cloud từ keywords)

**Module 4: Báo cáo & Thống kê**
- ✅ Báo cáo số lượng bài báo theo đơn vị (Khoa/Viện)
- ✅ Báo cáo theo loại tạp chí (Q1/Q2/Q3/Q4)
- ✅ Xu hướng xuất bản theo năm
- ✅ Top giảng viên có năng suất cao nhất

**Module 5: Quản lý Người dùng & Tài khoản**
- ✅ Phân quyền: SuperAdmin, Giảng viên, Viewer
- ✅ **Quản lý tài khoản phê duyệt theo đơn vị** (Khoa/Phòng ban/Trường)
- ✅ Xác thực qua LDAP/AD (Single Sign-On)
- ✅ Quản lý đơn vị (Khoa/Viện/Bộ môn)
- ✅ Chuyển giao tài khoản khi thay đổi nhân sự

**Module 6: Quy Trình Phê Duyệt (Approval Workflow)** 🆕
- ✅ **Nộp công trình xét duyệt**: Giảng viên chuyển từ Draft → Submitted
- ✅ **Xét duyệt cấp Khoa** (sử dụng **tài khoản phê duyệt của Khoa**):
  - Trưởng đơn vị đăng nhập vào tài khoản phê duyệt của Khoa
  - Xem danh sách công trình chờ duyệt của Khoa mình
  - Phê duyệt (Approve) / Yêu cầu bổ sung (Revision) / Từ chối (Reject)
  - Nhập nhận xét, phản hồi
- ✅ **Phê duyệt cấp Trường** (sử dụng **tài khoản phê duyệt của Trường**):
  - Cán bộ Phòng QLKH đăng nhập vào tài khoản phê duyệt cấp Trường
  - Xem công trình đã được Khoa duyệt
  - Phê duyệt cuối cùng hoặc từ chối
  - **Nhập thủ công số giờ làm/giờ dạy cho bài báo này**
- ✅ **Lịch sử xét duyệt & Audit Trail**:
  - Lưu người duyệt, thời gian, nhận xét
  - **Ghi lại tài khoản nào được sử dụng, IP, thời gian đăng nhập**
  - Audit trail đầy đủ đảm bảo trách nhiệm giải trình
- ✅ **Thông báo (Notification)**:
  - Email/In-app khi có phản hồi
  - Thông báo chuyển trạng thái
- ✅ **Dashboard theo vai trò**:
  - Giảng viên: 
    * Xem trạng thái công trình của mình 
    * **Tổng giờ làm trong năm hiện tại**
    * **Chi tiết giờ làm từ từng bài báo** (bài nào được bao nhiêu giờ)
    * Xuất báo cáo giờ làm cá nhân
  - Tài khoản Khoa: Danh sách chờ duyệt cấp Khoa
  - Tài khoản Trường: Danh sách chờ duyệt cấp Trường + **Nhập giờ làm khi duyệt**
- ✅ **Quản lý tài khoản phê duyệt** (Admin):
  - Tạo tài khoản phê duyệt cho đơn vị mới
  - Reset mật khẩu khi thay đổi nhân sự
  - Xem lịch sử truy cập tài khoản

> 💡 **Lưu ý**: CHỈ công trình đã được **cấp Trường phê duyệt** mới xuất hiện trong Module 2, 3, 4 (tìm kiếm, profile, báo cáo công khai).

---

#### C. Đối Tượng Sử Dụng

| Vai trò | Quyền hạn | Số lượng ước tính |
|---------|-----------|-------------------|
| **SuperAdmin** | Quản trị hệ thống, cấu hình, quản lý tài khoản phê duyệt | 2-5 người |
| **Giảng viên** (Researcher) | Tạo/sửa/nộp công trình; Xem phản hồi; Xem giờ làm đã tính | 300-500 người |
| **Tài khoản Phê duyệt Khoa** | Xét duyệt công trình cấp Khoa (Approve/Revision/Reject) | 10-15 tài khoản (dùng chung bởi Trưởng/Phó khoa) |
| **Tài khoản Phê duyệt Trường** | Phê duyệt cuối cùng + Tính giờ làm (Approve/Reject) | 1 tài khoản (dùng chung bởi CB Phòng QLKH) |
| **Viewer** (Sinh viên, công chúng) | Xem công trình đã công bố, tìm kiếm | Không giới hạn |

---

### 3.2. Ngoài Phạm Vi (Out of Scope)

❌ **Quản lý đề tài nghiên cứu:**
- Đăng ký, thực hiện, nghiệm thu đề tài
- Quản lý kinh phí
- → Đây là hệ thống riêng

❌ **Quản lý giảng dạy:**
- Thời khóa biểu, điểm số
- → Đã có hệ thống LMS/ERP

❌ **Quản lý các loại công trình khác:**
- Sách, sáng chế, phần mềm...
- → Có thể mở rộng trong tương lai

❌ **Peer review system:**
- Không phải hệ thống phản biện bài báo
- Chỉ quản lý bài báo ĐÃ xuất bản

❌ **Tích hợp thanh toán:**
- Không xử lý phí xuất bản (APC)

---

### 3.3. Ranh Giới Dữ Liệu

**Dữ liệu nội bộ (quản lý bởi hệ thống):**
- Thông tin bài báo
- File PDF
- Thống kê truy cập
- Lịch sử chỉnh sửa

**Dữ liệu tích hợp (từ hệ thống khác):**
- Thông tin giảng viên (từ HR system)
- Đơn vị (Khoa/Viện) (từ hệ thống tổ chức)
- ORCID, DOI, Google Scholar (từ internet)

---

### 3.4. Quản Lý Trạng Thái Công Trình (Publication State Machine)

Mỗi công trình khoa học trong hệ thống sẽ trải qua các trạng thái sau:

#### Sơ Đồ Luồng Trạng Thái

```
DRAFT → SUBMITTED → FACULTY_REVIEWING → [REVISION_REQUIRED hoặc FACULTY_APPROVED]
                                              ↓                         ↓
                                           DRAFT (chỉnh sửa)    UNIVERSITY_REVIEWING
                                                                        ↓
                                                         [UNIVERSITY_APPROVED hoặc UNIVERSITY_REJECTED]
                                                                        ↓
                                                                   PUBLISHED
```

#### Chi Tiết Các Trạng Thái

| Trạng thái | Mô tả | Ai thấy được | Ai được thao tác |
|------------|-------|--------------|------------------|
| **DRAFT** | Nháp, giảng viên đang soạn | Chỉ giảng viên | Giảng viên (Edit, Submit) |
| **SUBMITTED** | Đã nộp, chờ Khoa xét | GV, CB Khoa, Admin | CB Khoa (Review) |
| **FACULTY_REVIEWING** | Khoa đang xem xét | GV, CB Khoa, Admin | CB Khoa (Approve/Revision/Reject) |
| **REVISION_REQUIRED** | Khoa yêu cầu bổ sung | GV, CB Khoa, Admin | Giảng viên (Edit, Resubmit) |
| **FACULTY_REJECTED** | Khoa từ chối | GV, CB Khoa, Admin | Giảng viên (View only) |
| **FACULTY_APPROVED** | Khoa đã duyệt, chờ Trường | GV, CB Khoa, CB Trường, Admin | CB Trường (Review) |
| **UNIVERSITY_REVIEWING** | Trường đang xem xét | GV, CB Khoa, CB Trường, Admin | CB Trường (Approve/Reject) |
| **UNIVERSITY_APPROVED** = **PUBLISHED** | Đã công bố chính thức | **Mọi người** (Public) | Không thể sửa |
| **UNIVERSITY_REJECTED** | Trường từ chối | GV, CB Khoa, CB Trường, Admin | Giảng viên (View only) |

#### Quy Tắc Chuyển Trạng Thái

**Từ DRAFT:**
- → SUBMITTED (khi giảng viên nhấn "Nộp xét duyệt")

**Từ SUBMITTED:**
- → FACULTY_REVIEWING (tự động hoặc khi CB Khoa bắt đầu xem)
- → FACULTY_APPROVED (CB Khoa phê duyệt)
- → REVISION_REQUIRED (CB Khoa yêu cầu chỉnh sửa)
- → FACULTY_REJECTED (CB Khoa từ chối)

**Từ REVISION_REQUIRED:**
- → DRAFT (giảng viên chỉnh sửa)
- → SUBMITTED (giảng viên nộp lại)

**Từ FACULTY_APPROVED:**
- → UNIVERSITY_REVIEWING (tự động hoặc khi CB Trường bắt đầu xem)
- → PUBLISHED (CB Trường phê duyệt)
- → UNIVERSITY_REJECTED (CB Trường từ chối)

> ⚠️ **Lưu ý quan trọng**:
> - CHỈ công trình ở trạng thái **PUBLISHED** mới xuất hiện trong:
>   - Module 2: Tìm kiếm công khai
>   - Module 3: Profile giảng viên (phần công khai)
>   - Module 4: Báo cáo thống kê công khai
> - Các trạng thái khác CHỈ hiển thị trong **Dashboard nội bộ** (Module 6)
> - **Khi chuyển sang PUBLISHED, hệ thống tự động tính giờ làm/giờ dạy** dựa trên loại bài báo

---

## 4. Các Bên Liên Quan (Stakeholders)

### 4.1. Stakeholders Chính

| Vai trò | Mô tả | Mong đợi chính |
|---------|-------|----------------|
| **Giảng viên** | Người tạo ra bài báo | Dễ nhập, nộp duyệt đơn giản, nhận phản hồi kịp thời, có profile đẹp, **dashboard xem chi tiết giờ làm từng bài** |
| **Trưởng Đơn vị (sử dụng TK phê duyệt Khoa)** | Xét duyệt công trình cấp Khoa | Dashboard rõ ràng, dễ duyệt hàng loạt, nhập nhận xét nhanh, **chuyển giao tài khoản an toàn** |
| **Cán bộ Trường (sử dụng TK phê duyệt Trường)** | Phê duyệt cuối toàn trường | Xem ý kiến Khoa, lọc theo đơn vị, quyết định nhanh, **nhập giờ làm khi duyệt** |
| **Lãnh đạo trường** | Ra quyết định chiến lược | Dashboard tổng quan, thống kê năng suất, insight xu hướng |
| **Sinh viên/NCS** | Tìm người hướng dẫn | Tìm kiếm dễ dàng, thông tin đầy đủ về công trình đã công bố |

### 4.2. Stakeholders Phụ

- **Phòng Tổ chức - Hành chính**: Cung cấp dữ liệu giảng viên
- **Phòng IT**: Hỗ trợ hạ tầng, bảo mật
- **Bộ GD&ĐT**: Có thể yêu cầu báo cáo định kỳ
- **Cơ quan kiểm định (AUN-QA, ...)**: Đánh giá chất lượng đào tạo

---

## 5. Yêu Cầu Phi Chức Năng

### 5.1. Hiệu Năng

- Thời gian tải trang: < 2 giây
- Tìm kiếm trả về kết quả: < 1 giây (với DB < 10,000 bài báo)
- Hỗ trợ: 100 người dùng đồng thời

### 5.2. Khả Dụng

- Uptime: > 99% (cho phép bảo trì 1 giờ/tuần)
- Backup tự động hàng ngày
- Recovery time: < 4 giờ

### 5.3. Bảo Mật

- HTTPS bắt buộc
- Xác thực qua LDAP/AD (SSO)
- Phân quyền rõ ràng (RBAC)
- Audit log cho mọi thao tác quan trọng

### 5.4. Khả Năng Sử Dụng

- Giao diện tiếng Việt
- Responsive (PC, tablet, mobile)
- Tuân thủ WCAG 2.1 (AA) - Accessibility cơ bản

### 5.5. Khả Năng Bảo Trì

- Code rõ ràng, có documentation
- Unit test coverage > 70%
- Dễ dàng thêm loại công trình mới (mở rộng sau)

---

## 6. Công Nghệ Đề Xuất

> Chi tiết đầy đủ: [technology_stack.md](./technology_stack.md)

**Tóm tắt:**
- Frontend: React + TypeScript + Material-UI
- Backend: Java Spring Boot 3.x
- Database: MySQL 8.0+
- Storage: Hệ thống file cục bộ (Local File System) cho file PDF
- Xác thực: LDAP/AD + JWT

### 6.1. Giải Thích về Storage (Lưu Trữ File)

**Storage** là nơi lưu trữ các file PDF của bài báo khoa học mà giảng viên upload lên hệ thống.

**Các phương án lưu trữ:**

**1. Local File System (Khuyến nghị cho MVP)**
- Lưu file trực tiếp trên server
- Path lưu trong database, file thực tế trong folder `/uploads/publications/`
- **Ưu điểm**: Đơn giản, không phí phát sinh, dễ triển khai
- **Nhược điểm**: Khó scale khi file nhiều, cần backup thủ công

**2. Cloud Storage (Giai đoạn 2)**
- AWS S3, Azure Blob Storage, Google Cloud Storage
- **Ưu điểm**: Tự động backup, dễ mở rộng, có CDN
- **Nhược điểm**: Phí hàng tháng, phụ thuộc Internet

**3. MinIO (S3-compatible, Self-hosted)**
- Giải pháp trung gian: tự host nhưng API giống S3
- **Ưu điểm**: Dễ migration lên AWS S3 sau, không phí cloud
- **Nhược điểm**: Cần server riêng cho storage

**Quyết định cho đồ án:**
- MVP: Sử dụng **Local File System** (đơn giản, đủ dùng)
- Tương lai: Có thể chuyển sang Cloud Storage khi cần scale

---

## 9. Tuân Thủ Chuẩn Quốc Tế (Future-Proofing)

> Xem chi tiết: [Chuẩn mực quốc tế](../00_Problem_Context/international_standards.md)

### 9.1. Metadata và Persistent Identifiers

**Khuyến nghị áp dụng:**

✅ **DOI (Digital Object Identifier)**
- Lưu trữ DOI cho mỗi bài báo (nếu có)
- Validation format: `10.xxxx/xxxxx`
- Tích hợp CrossRef API để tự động lấy metadata

✅ **ORCID (Researcher ID)**
- Lưu ORCID của giảng viên (nếu có)
- Format: `0000-0002-1825-0097`
- Giai đoạn 2: Import publication list từ ORCID tự động

✅ **ISSN (Journal ID)**
- Lưu ISSN của tạp chí
- Format: `0028-0836`

✅ **UUID cho Bài báo**
- Mỗi bài báo có UUID duy nhất
- Đảm bảo tính vĩnh viễn khi hệ thống thay đổi

---

### 9.2. Tuân Thủ FAIR Principles

**FAIR = Findable + Accessible + Interoperable + Reusable**

**Findable (Dễ tìm):**
- ✅ Metadata đầy đủ (tiêu đề, tác giả, từ khóa, tóm tắt)
- ✅ Có search engine optimization (SEO)

**Accessible (Dễ truy cập):**
- ✅ API công khai (cho phép tìm kiếm, xem metadata)
- ✅ Authentication rõ ràng (JWT)

**Interoperable (Tương tác được):
- ✅ RESTful API tuân thủ OpenAPI 3.0
- ✅ Export dạng chuẩn: BibTeX, RIS, JSON

**Reusable (Tái sử dụng được):**
- ✅ License bài báo rõ ràng (CC BY, All Rights Reserved...)
- ✅ Audit trail (lịch sử thay đổi)

---

### 9.3. Khả Năng Mở Rộng (Extensibility)

**Thiết kế database linh hoạt:**

Module hiện tại chỉ quản lý **bài báo**, nhưng structure cần cho phép thêm:
- 🔸 Dataset (dữ liệu nghiên cứu)
- 🔸 Software (phần mềm)
- 🔸 Conference proceedings (kỷ yếu)

**Tham khảo:**
- CERIF ResultPublication structure
- COAR Resource Types vocabulary

```sql
-- Thiết kế mẫu cho tương lai
TABLE research_outputs (
  id UUID PRIMARY KEY,
  type VARCHAR(50), -- 'journal_article', 'dataset', 'software'...
  metadata JSONB,    -- Linh hoạt cho từng loại
  ...
)
```

---

### 9.4. CRediT (Contributor Roles Taxonomy)

**Ghi nhận đóng góp chi tiết:**

Thay vì chỉ "Tác giả chính" và "Đồng tác giả", có thể mở rộng:
- Conceptualization (Hình thành ý tưởng)
- Data curation (Quản lý dữ liệu)
- Formal analysis (Phân tích)
- Writing - original draft (Viết bản thảo)
- Writing - review & editing (Biên tập)

→ Hữu ích cho đánh giá KPI chi tiết

---

## 10. Ràng Buộc và Giả Định

### 10.1. Ràng Buộc Kỹ Thuật

- Phải tương thích với hạ tầng hiện tại của trường (Windows Server, Active Directory)
- Sử dụng công nghệ phổ biến, dễ tìm nhân lực bảo trì

### 10.2. Thời Gian

- MVP trong vòng 3 tháng
- Go-live trước năm học mới

### 7.3. Ngân Sách

- Ưu tiên giải pháp mã nguồn mở
- Chi phí vận hành < 50 triệu/năm

---

## 8. Giả Định

- ✅ Giảng viên có kỹ năng máy tính cơ bản
- ✅ Có kết nối internet ổn định
- ✅ Dữ liệu bài báo do giảng viên tự khai báo (honor system)
- ✅ Phòng QLKH sẽ kiểm tra, phê duyệt định kỳ

---

## 9. Tiêu Chí Thành Công

Sau 6 tháng triển khai:

- ✅ 80% giảng viên đã đăng ký ít nhất 1 bài báo
- ✅ Thời gian tạo báo cáo giảm từ 3 ngày → 30 phút
- ✅ 90% người dùng hài lòng (khảo sát)
- ✅ Không có sự cố bảo mật nghiêm trọng

---

## 10. Kế Hoạch Mở Rộng (Future Scope)

**Giai đoạn 2:**
- ✅ Tích hợp tự động với ORCID, Google Scholar API
- ✅ AI đề xuất đồng nghiệp hợp tác (based on keywords)
- ✅ Thêm loại công trình: Sách, Giáo trình

**Giai đoạn 3:**
- ✅ Mobile app (iOS/Android)
- ✅ Blockchain cho xác thực công trình
- ✅ Kết nối liên trường (University Alliance)

---

*Chi tiết yêu cầu chức năng, user stories, use cases: xem các folder 03-05*
