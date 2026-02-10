# Phạm Vi và Ranh Giới Module Bài Báo Khoa Học

## 1. Tổng Quan

Tài liệu này định nghĩa rõ ràng **phạm vi IN/OUT** của module quản lý bài báo khoa học, để tránh hiểu nhầm và scope creep.

---

## 2. Vị Trí trong Hệ Sinh Thái Lớn Hơn

```
┌──────────────────────────────────────────────────────────┐
│ Hệ thống Toàn Diện: Quản lý TOÀN BỘ Công trình NCKH    │
│ (7 nhóm, 28 loại - Xem folder 00_Problem_Context)       │
│                                                          │
│  ┌────────────────────────────────────────────────┐    │
│  │ ✅ MODULE ĐỒ ÁN: Bài báo Khoa học              │    │
│  │    - Chỉ 1 loại trong nhóm Publications        │    │
│  │    - Phạm vi: 1 trường Đại học                 │    │
│  └────────────────────────────────────────────────┘    │
│                                                          │
│  ❌ Các module KHÔNG làm (giai đoạn này):              │
│     - Sách, Giáo trình                                  │
│     - Bằng sáng chế, SHTT                              │
│     - Phần mềm, Sản phẩm kỹ thuật                      │
│     - Tiêu chuẩn, Quy chuẩn                            │
│     - Bản vẽ thiết kế                                   │
│     - ...                                               │
└──────────────────────────────────────────────────────────┘
```

---

## 3. Phạm Vi Chức Năng (Functional Scope)

### 3.1. ✅ TRONG PHẠM VI

#### **Quản lý Bài báo Khoa học**

**Loại bài báo được quản lý:**
- Bài báo tạp chí quốc tế (ISI/Scopus/Web of Science)
- Bài báo tạp chí trong nước (có ISSN)
- Bài báo hội thảo quốc tế (conference paper có ISBN)

**Metadata bắt buộc:**
- Tiêu đề (Tiếng Việt + Tiếng Anh)
- Danh sách tác giả (có thứ tự)
- Tạp chí/Hội nghị
- ISSN/ISBN
- DOI (nếu có)
- Năm xuất bản, số, trang
- Loại tạp chí (Q1/Q2/Q3/Q4 hoặc ISI/Scopus/Other)
- Impact Factor (nếu có)
- Số lượng trích dẫn (nếu có)
- File PDF toàn văn
- Từ khóa (keywords)
- Tóm tắt (abstract)

**Chức năng CRUD:**
- ✅ Thêm bài báo mới (Create)
- ✅ Xem chi tiết (Read)
- ✅ Sửa thông tin (Update)
- ✅ Xóa bài báo (Delete - soft delete)
- ✅ Upload/Download file PDF
- ✅ Liên kết đồng tác giả (trong cùng trường)

---

#### **Tìm kiếm & Lọc**

✅ **Tìm kiếm theo:**
- Tiêu đề (full-text search)
- Tác giả
- Từ khóa
- Tạp chí/Hội nghị
- DOI/ISSN

✅ **Lọc theo:**
- Năm xuất bản (từ - đến)
- Loại tạp chí (Q1/Q2/Q3/Q4)
- Đơn vị (Khoa/Viện)
- Tác giả chính/Đồng tác giả

✅ **Sắp xếp:**
- Mới nhất → cũ nhất
- Impact Factor cao → thấp
- Số trích dẫn nhiều → ít
- A-Z theo tiêu đề

---

#### **Profile Giảng viên**

✅ **Trang cá nhân công khai:**
- Thông tin cơ bản (Tên, đơn vị, email, ORCID)
- Danh sách tất cả bài báo
- Biểu đồ số lượng bài báo theo năm
- Biểu đồ phân bố theo loại tạp chí
- Word cloud từ keywords (lĩnh vực nghiên cứu)
- Tổng số trích dẫn, h-index (nếu có nguồn)

✅ **URL thân thiện:**
- `domain.edu.vn/profile/nguyen-van-a`

---

#### **Báo cáo & Thống kê**

✅ **Báo cáo admin:**
- Số lượng bài báo theo đơn vị (Khoa/Viện)
- Số lượng theo loại tạp chí (Q1/Q2/Q3/Q4)
- Xu hướng xuất bản theo năm (line chart)
- Top 10 giảng viên năng suất cao nhất
- Top 10 bài báo được trích dẫn nhiều nhất
- So sánh giữa các Khoa/Viện (bar chart)

✅ **Export:**
- Excel (.xlsx)
- PDF
- CSV (cho phân tích thêm)

---

#### **Quản lý Người dùng & Phân quyền**

✅ **5 vai trò:**

| Vai trò | Quyền hạn |
|---------|-----------|
| **SuperAdmin** | - Quản trị hệ thống<br>- Cấu hình, quản lý người dùng<br>- Xem toàn bộ báo cáo |
| **Researcher** (Giảng viên) | - Tạo/sửa/nộp công trình<br>- Xem phản hồi xét duyệt<br>- Chỉnh sửa theo yêu cầu<br>- Xem profile của mình |
| **Faculty Reviewer** (CB Khoa) | - Xét duyệt công trình cấp Khoa<br>- Phê duyệt/Yêu cầu bổ sung/Từ chối<br>- Nhập nhận xét |
| **University Reviewer** (CB Trường) | - Phê duyệt cuối cấp Trường<br>- Approve/Reject<br>- Xem ý kiến cấp Khoa |
| **Viewer** (Công chúng) | - Tìm kiếm, xem công trình ĐÃ CÔNG BỐ<br>- Xem profile giảng viên<br>- Tải file PDF (nếu công khai) |

✅ **Xác thực:**
- LDAP/Active Directory (Single Sign-On)
- JWT token cho API

---

#### **Quy Trình Phê Duyệt (Approval Workflow)** 🆕

✅ **Quản lý trạng thái công trình:**
- DRAFT → SUBMITTED → FACULTY_REVIEWING → FACULTY_APPROVED → UNIVERSITY_REVIEWING → PUBLISHED
- Hỗ trợ REVISION_REQUIRED (yêu cầu bổ sung), REJECTED (từ chối)

✅ **Workflow 2 cấp:**
- **Cấp 1 - Khoa**: Xét duyệt sơ bộ, yêu cầu chỉnh sửa, từ chối
- **Cấp 2 - Trường**: Phê duyệt chính thức để công bố

✅ **Feedback và Revision:**
- CB Khoa/Trường nhập nhận xét, phản hồi
- Giảng viên xem feedback, chỉnh sửa theo yêu cầu
- Nộp lại sau khi chỉnh sửa

✅ **Lịch sử xét duyệt (Audit Trail):**
- Lưu người duyệt, thời gian, nhận xét
- Theo dõi mọi thay đổi trạng thái
- Không thể xóa/sửa lịch sử

✅ **Dashboard theo vai trò:**
- **Giảng viên**: Danh sách công trình của mình + trạng thái hiện tại
- **CB Khoa**: Danh sách công trình chờ duyệt cấp Khoa (của Khoa mình)
- **CB Trường**: Danh sách công trình đã Khoa duyệt, chờ Trường phê duyệt

✅ **Notification System:**
- Email/In-app notification khi có phản hồi
- Thông báo khi trạng thái thay đổi
- Nhắc nhở khi công trình chờ duyệt quá lâu

> 💡 **Dual-Mode System (Hệ thống 2 chế độ):**
> - **Private Mode (Internal)**: Workflow phê duyệt nội bộ - Chỉ người liên quan thấy
> - **Public Mode (Portfolio)**: CHỈ công trình ở trạng thái **PUBLISHED** mới xuất hiện trong Module 2, 3, 4 (tìm kiếm công khai, profile, báo cáo)

---

### 3.2. ❌ NGOÀI PHẠM VI

#### **Các loại công trình KHÁC:**

❌ Sách chuyên khảo, giáo trình, sách tham khảo  
❌ Bằng sáng chế, giải pháp hữu ích  
❌ Phần mềm, cơ sở dữ liệu  
❌ Thiết bị, máy móc kỹ thuật  
❌ Tiêu chuẩn quốc gia, quy chuẩn  
❌ Bản vẽ thiết kế, quy hoạch  
❌ Tác phẩm nghệ thuật  

→ **Lý do**: Mỗi loại có metadata và quy trình quản lý khác nhau đáng kể

---

#### **Quản lý Đề tài NCKH:**

❌ Đăng ký đề tài mới  
❌ Theo dõi tiến độ thực hiện  
❌ Quản lý kinh phí  
❌ Nghiệm thu đề tài  
❌ Thanh lý hợp đồng  

→ **Lý do**: Đây là hệ thống riêng biệt với quy trình phức tạp (xem pháp lý tại folder 00)

---

#### **Quản lý Dạy học:**

❌ Thời khóa biểu, lịch giảng  
❌ Quản lý điểm số sinh viên  
❌ Đánh giá giảng viên bởi sinh viên  

→ **Lý do**: Đã có hệ thống LMS/ERP riêng

---

#### **Peer Review System:**

❌ Hệ thống phản biện bài báo  
❌ Quản lý vòng review  
❌ Quyết định chấp nhận/từ chối  

→ **Lý do**: Module này chỉ quản lý bài báo ĐÃ XUẤT BẢN

---

#### **Thanh toán:**

❌ Xử lý phí xuất bản (APC - Article Processing Charge)  
❌ Thanh toán online  
❌ Quản lý hóa đơn  

→ **Lý do**: Nằm ngoài phạm vi quản lý công trình

---

#### **Chức năng Nâng cao (giai đoạn sau):**

❌ Tích hợp tự động với ORCID, Google Scholar API  
❌ AI đề xuất reviewer  
❌ Plagiarism check  
❌ Tự động trích xuất metadata từ PDF  
❌ Recommendation engine (đề xuất bài báo liên quan)  
❌ Collaboration network visualization  

→ **Lý do**: MVP cần tập trung vào core features trước

---

## 4. Ranh Giới Dữ Liệu (Data Boundary)

### 4.1. ✅ Dữ liệu NỘI BỘ (Owned by System)

**Hệ thống sở hữu và quản lý:**
- Thông tin bài báo (metadata)
- File PDF toàn văn
- Lịch sử chỉnh sửa (audit log)
- Thống kê truy cập
- Đơn vị (Khoa/Viện/Bộ môn)

---

### 4.2. 🔗 Dữ liệu TÍCH HỢP (External Source)

**Lấy từ hệ thống khác (read-only):**
- Thông tin giảng viên (Tên, email, đơn vị) → từ HR system
- LDAP/AD accounts → từ IT system

**Tích hợp tùy chọn (giai đoạn sau):**
- ORCID profile
- Google Scholar metrics
- Crossref (xác minh DOI)

---

### 4.3. ❌ Dữ liệu KHÔNG QUẢN LÝ

- Dữ liệu tài chính, lương
- Dữ liệu sinh viên (điểm, học phí)
- Dữ liệu đề tài (kinh phí, tiến độ)
- Dữ liệu tài sản, thiết bị

---

## 5. Ranh Giới Người Dùng (User Boundary)

### 5.1. ✅ Primary Users (Người dùng chính)

- **Giảng viên** - Người tạo và quản lý bài báo
- **Cán bộ QLKH** - Admin, phê duyệt, báo cáo
- **Lãnh đạo** - Xem dashboard, báo cáo

---

### 5.2. ✅ Secondary Users (Người dùng phụ)

- **Sinh viên** - Tìm kiếm, xem profile giảng viên
- **Cộng đồng** - Xem bài báo công khai (read-only)

---

### 5.3. ❌ Non-Users (KHÔNG phải người dùng)

- Cán bộ tài chính (họ chỉ quan tâm kinh phí đề tài)
- Cán bộ đào tạo (họ dùng hệ thống LMS)
- Sinh viên quản lý điểm (họ dùng hệ thống ERP)

---

## 6. Ranh Giới Tích Hợp (Integration Boundary)

### 6.1. ✅ Tích hợp BẮT BUỘC

- **LDAP/Active Directory** - Xác thực người dùng
- **HR System** - Lấy thông tin giảng viên (nếu có API)

---

### 6.2. 🔗 Tích hợp TÙY CHỌN (Nice-to-have)

- **ORCID API** - Import bài báo tự động
- **Google Scholar API** - Lấy citation count
- **Crossref API** - Xác minh DOI
- **Email Server (SMTP)** - Gửi thông báo

---

### 6.3. ❌ KHÔNG tích hợp

- ❌ Hệ thống quản lý tài chính
- ❌ Hệ thống quản lý đào tạo (LMS)
- ❌ Hệ thống quản lý đề tài (nếu có)
- ❌ CSDL quốc gia KH&CN (nằm ngoài phạm vi trường ĐH)

---

## 7. Ranh Giới Thời Gian (Time Boundary)

### 7.1. ✅ Giai đoạn 1 (MVP - 3 tháng)

- CRUD bài báo
- Tìm kiếm cơ bản
- Profile giảng viên
- Báo cáo đơn giản
- Quản lý người dùng

---

### 7.2. 🔜 Giai đoạn 2 (6 tháng sau MVP)

- Tích hợp ORCID, Google Scholar
- Báo cáo nâng cao
- Dashboard interactice
- Mobile responsive cải tiến

---

### 7.3. 🔮 Giai đoạn 3 (Tương lai xa)

- AI recommendation
- Collaboration network
- Mobile app (iOS/Android)
- Thêm loại công trình khác (Sách, Sáng chế...)

---

## 8. Ranh Giới Công Nghệ (Technology Boundary)

### 8.1. ✅ Nền tảng

- **Web Application** (Browser-based)
- Responsive design (PC, tablet, mobile browser)

---

### 8.2. ❌ KHÔNG phát triển

- ❌ Native mobile app (iOS/Android) - giai đoạn đầu
- ❌ Desktop app (Windows/macOS)
- ❌ Plugin cho Word/Excel

---

## 9. Ma Trận Scope Summary

| Khía cạnh | Trong scope ✅ | Ngoài scope ❌ |
|-----------|---------------|----------------|
| **Loại công trình** | Bài báo khoa học | 6 nhóm công trình còn lại |
| **Chức năng** | CRUD, Tìm kiếm, Báo cáo | Quản lý đề tài, Peer review |
| **Người dùng** | Giảng viên, Admin, Viewer | Cán bộ tài chính, Sinh viên quản lý điểm |
| **Dữ liệu** | Metadata bài báo, PDF | Dữ liệu tài chính, điểm số |
| **Tích hợp** | LDAP/AD | ERP tài chính, LMS |
| **Nền tảng** | Web app | Native mobile app |
| **Thời gian** | MVP 3 tháng | AI features (giai đoạn 3) |

---

## 10. Change Request Process

Nếu có yêu cầu **nằm ngoài scope** này:

1. ✅ Ghi nhận vào backlog
2. ✅ Đánh giá mức độ ưu tiên
3. ✅ Ước lượng effort
4. ✅ Quyết định: MVP / Phase 2 / Phase 3 / Reject
5. ✅ Cập nhật tài liệu scope

---

*Tài liệu này là "hợp đồng" giữa đội phát triển và stakeholders về những gì sẽ/không làm.*
