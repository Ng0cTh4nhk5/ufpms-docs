# User Stories - README

> 📁 **Folder**: `04_User_Stories`  
> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục đích**: Chuyển đổi 65 functional requirements thành user stories theo vai trò và độ ưu tiên

---

## 📁 Cấu Trúc Folder

```
04_User_Stories/
├── README.md (file này)
├── By_Role/
│   ├── researcher_stories.md
│   ├── faculty_reviewer_stories.md
│   ├── university_reviewer_stories.md
│   ├── admin_stories.md
│   └── public_visitor_stories.md
└── Prioritized/
    ├── p0_must_have.md
    ├── p1_should_have.md
    └── p2_nice_to_have.md
```

---

## 🎯 Tổng Quan

User stories là cách diễn đạt yêu cầu hệ thống từ góc nhìn người dùng cuối, theo cấu trúc:

```
Là một [vai trò],
Tôi muốn [tính năng],
Để [lợi ích/giá trị]
```

---

## 👥 User Roles

### 1. Giảng viên (Researcher)
**Mục tiêu**: Quản lý bài báo khoa học và theo dõi tiến độ phê duyệt

**Modules Chính (Primary Modules)**:
- Module 1: Quản lý Bài báo (Publication Management)
- Module 2: Quy trình Xét duyệt (Approval Workflow) (nộp, chỉnh sửa, theo dõi trạng thái)
- Module 4: Hồ sơ Giảng viên (Researcher Profile)

---

### 2. Cán bộ Khoa (Faculty Reviewer)
**Mục tiêu**: Xét duyệt bài báo cấp Khoa

**Modules Chính (Primary Modules)**:
- Module 2: Quy trình Xét duyệt (Approval Workflow) (duyệt cấp khoa)
- Module 5: Báo cáo & Phân tích (Reporting & Analytics) (báo cáo khoa)

---

### 3. Cán bộ Trường (University Reviewer)
**Mục tiêu**: Phê duyệt cuối cùng và công bố, quản lý báo cáo toàn trường

**Modules Chính (Primary Modules)**:
- Module 2: Quy trình Xét duyệt (Approval Workflow) (duyệt cấp trường)
- Module 5: Báo cáo & Phân tích (Reporting & Analytics) (báo cáo toàn trường)

---

### 4. Quản trị viên (SuperAdmin)
**Mục tiêu**: Quản trị hệ thống, người dùng, cấu hình

**Modules Chính (Primary Modules)**:
- Module 6: Quản trị & Quản lý Người dùng (Admin & User Management)

---

### 5. Khách truy cập (Public Visitor)
**Mục tiêu**: Tìm kiếm và xem thông tin công trình công bố, profile giảng viên

**Modules Chính (Primary Modules)**:
- Module 3: Tìm kiếm & Duyệt (Search & Browse)
- Module 4: Hồ sơ Giảng viên (Researcher Profile) (chỉ xem)

---

## 📊 Tổng Số User Stories

| Role | Tổng số Stories | P0 | P1 | P2 |
|------|--------------|----|----|-----|
| **Giảng viên (Researcher)** | 28 | 18 | 7 | 3 |
| **Cán bộ Khoa (Faculty Reviewer)** | 9 | 6 | 2 | 1 |
| **Cán bộ Trường (University Reviewer)** | 10 | 6 | 3 | 1 |
| **Quản trị viên (SuperAdmin)** | 10 | 8 | 2 | 0 |
| **Khách (Public Visitor)** | 8 | 2 | 4 | 2 |
| **TỔNG** | **65** | **40** | **18** | **7** |

---

## 🗺️ Cấu trúc User Story (User Story Format)

### Mẫu (Template)

```
US-[ROLE]-[NUMBER]: [Tên Story]
Độ ưu tiên: P[0/1/2]
Yêu cầu liên quan: FR-[MODULE]-[NUMBER]

Là một [xu vai trò],
Tôi muốn [tính năng],
Để [lợi ích].

Tiêu chí Chấp nhận (Acceptance Criteria):
KHI (GIVEN) [điều kiện tiên quyết]
VÀ (WHEN) [hành động]
THÌ (THEN) [kết quả mong đợi]
```

### Ví dụ (Example)

```
US-RES-001: Tạo Bài Báo Mới
Priority: P0 - Must Have
Related FR: FR-PUB-001

As a researcher (Là một giảng viên),
I want to create a new publication entry with required metadata (Tôi muốn tạo mới một bài báo với các thông tin bắt buộc),
So that I can submit it for review and eventual publication (Để tôi có thể gửi nó đi xét duyệt và công bố sau này).

Acceptance Criteria:
GIVEN I am logged in as a researcher (KHI tôi đã đăng nhập với vai trò giảng viên)
WHEN I click "Add New Publication" (VÀ tôi nhấn nút "Thêm bài báo mới")
THEN I see a form with required fields (Title, Authors, Year, Journal Type) (THÌ tôi thấy một biểu mẫu với các trường bắt buộc: Tiêu đề, Tác giả, Năm, Loại tạp chí)
AND optional fields (DOI, ISSN, Abstract, Keywords, PDF) (VÀ các trường tùy chọn: DOI, ISSN, Tóm tắt, Từ khóa, File PDF)
AND the publication status is set to DRAFT by default (VÀ trạng thái bài báo được đặt mặc định là DRAFT - Nháp)
```

---

## 🔗 Bản đồ Truy xuất (Traceability Map)

| User Story | Vai trò | Độ ưu tiên | Yêu cầu Chức năng | Module |
|-----------|------|----------|----------------|--------|
| US-RES-001 | Researcher | P0 | FR-PUB-001 | 1 - Publication Management |
| US-RES-002 | Researcher | P0 | FR-PUB-002 | 1 - Publication Management |
| US-RES-010 | Researcher | P0 | FR-APR-001 | 2 - Approval Workflow |
| US-FCR-001 | Faculty Reviewer | P0 | FR-APR-006 | 2 - Approval Workflow |
| US-UNR-001 | University Reviewer | P0 | FR-APR-012 | 2 - Approval Workflow |
| US-ADM-001 | SuperAdmin | P0 | FR-ADM-001 | 6 - Admin & User Mgmt |
| US-VIW-001 | Public Visitor | P1 | FR-SEA-001 | 3 - Search & Browse |
| ... | ... | ... | ... | ... |

> **Chi tiết**: Xem các file trong thư mục `By_Role/` và `Prioritized/`

---

## 📖 Hướng Dẫn Sử Dụng

### Cho Product Owner
1. **[P0 Must Have](./Prioritized/p0_must_have.md)** - Phạm vi MVP, 40 stories bắt buộc
2. **[P1 Should Have](./Prioritized/p1_should_have.md)** - Quan trọng, nên có trong MVP
3. **[P2 Nice to Have](./Prioritized/p2_nice_to_have.md)** - Giai đoạn 2 (Phase 2)

### Cho Developers
1. **[Researcher Stories](./By_Role/researcher_stories.md)** - 28 stories cho Quản lý bài báo + Xét duyệt
2. **[Faculty Reviewer Stories](./By_Role/faculty_reviewer_stories.md)** - 9 stories cho Duyệt cấp Khoa
3. **[University Reviewer Stories](./By_Role/university_reviewer_stories.md)** - 10 stories cho Duyệt cấp Trường
4. **[Admin Stories](./By_Role/admin_stories.md)** - 10 stories cho Quản trị hệ thống
5. **[Public Visitor Stories](./By_Role/public_visitor_stories.md)** - 8 stories cho Tìm kiếm + Hồ sơ

### Cho Scrum Team
- Sprint 1: P0 stories cho Module 1 + 2 (CRUD cốt lõi + quy trình)
- Sprint 2: P0 stories cho Module 6 (admin)
- Sprint 3: P1 stories cho Module 3 + 4 + 5
- Sprint 4: P2 stories (cải tiến tùy chọn)

---

## 🚀 Các bước tiếp theo (Next Steps)

Sau khi User Stories đã được review:

### 📁 05_Use_Cases
- Chuyển user stories thành use case diagrams
- Detailed use case specifications
- Actor interaction flows

### 📁 06_Diagrams
- Sequence diagrams cho key flows
- Activity diagrams cho approval workflow
- ERD cho database design

---

**Tài liệu liên quan**:
- [Requirements](../03_Requirements/)
- [Functional Requirements](../03_Requirements/Functional/)
- [User Needs](../02_System_Clarification/User_Analysis/user_needs.md)
- [To-Be Process](../02_System_Clarification/Business_Context/to_be_process.md)

---

*Hoàn thành: 10/02/2026 23:15*
