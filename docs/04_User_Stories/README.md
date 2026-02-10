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

User stories là cách diễn đạt yêu cầu hệ thống từ góc nhìn người dùng cuối, theo format:

```
As a [role],
I want [feature],
So that [benefit/value]
```

---

## 👥 User Roles

### 1. Researcher (Giảng viên)
**Mục tiêu**: Quản lý bài báo khoa học và theo dõi tiến độ phê duyệt

**Primary Modules**:
- Module 1: Publication Management
- Module 2: Approval Workflow (submit, revision, track status)
- Module 4: Researcher Profile

---

### 2. Faculty Reviewer (Cán bộ Khoa)
**Mục tiêu**: Xét duyệt bài báo cấp Khoa

**Primary Modules**:
- Module 2: Approval Workflow (faculty review)
- Module 5: Reporting & Analytics (faculty reports)

---

### 3. University Reviewer (Cán bộ Trường)
**Mục tiêu**: Phê duyệt cuối cùng và công bố, quản lý báo cáo toàn trường

**Primary Modules**:
- Module 2: Approval Workflow (university review)
- Module 5: Reporting & Analytics (university-wide reports)

---

### 4. SuperAdmin
**Mục tiêu**: Quản trị hệ thống, người dùng, cấu hình

**Primary Modules**:
- Module 6: Admin & User Management

---

### 5. Public Visitor (Khách truy cập)
**Mục tiêu**: Tìm kiếm và xem thông tin công trình công bố, profile giảng viên

**Primary Modules**:
- Module 3: Search & Browse
- Module 4: Researcher Profile (view only)

---

## 📊 Tổng Số User Stories

| Role | Total Stories | P0 | P1 | P2 |
|------|--------------|----|----|-----|
| **Researcher** | 28 | 18 | 7 | 3 |
| **Faculty Reviewer** | 9 | 6 | 2 | 1 |
| **University Reviewer** | 10 | 6 | 3 | 1 |
| **SuperAdmin** | 10 | 8 | 2 | 0 |
| **Public Visitor** | 8 | 2 | 4 | 2 |
| **TỔNG** | **65** | **40** | **18** | **7** |

---

## 🗺️ User Story Format

### Template

```
US-[ROLE]-[NUMBER]: [Story Title]
Priority: P[0/1/2]
Related FR: FR-[MODULE]-[NUMBER]

As a [role],
I want [feature],
So that [benefit].

Acceptance Criteria:
GIVEN [precondition]
WHEN [action]
THEN [expected outcome]
```

### Example

```
US-RES-001: Tạo Bài Báo Mới
Priority: P0 - Must Have
Related FR: FR-PUB-001

As a researcher,
I want to create a new publication entry with required metadata,
So that I can submit it for review and eventual publication.

Acceptance Criteria:
GIVEN I am logged in as a researcher
WHEN I click "Add New Publication"
THEN I see a form with required fields (Title, Authors, Year, Journal Type)
AND optional fields (DOI, ISSN, Abstract, Keywords, PDF)
AND the publication status is set to DRAFT by default
```

---

## 🔗 Traceability Map

| User Story | Role | Priority | Functional Req | Module |
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
1. **[P0 Must Have](./Prioritized/p0_must_have.md)** - MVP scope, 40 stories bắt buộc
2. **[P1 Should Have](./Prioritized/p1_should_have.md)** - Quan trọng, nên có trong MVP
3. **[P2 Nice to Have](./Prioritized/p2_nice_to_have.md)** - Phase 2

### Cho Developers
1. **[Researcher Stories](./By_Role/researcher_stories.md)** - 28 stories cho Publication + Approval
2. **[Faculty Reviewer Stories](./By_Role/faculty_reviewer_stories.md)** - 9 stories cho Faculty review
3. **[University Reviewer Stories](./By_Role/university_reviewer_stories.md)** - 10 stories cho University review
4. **[Admin Stories](./By_Role/admin_stories.md)** - 10 stories cho quản trị hệ thống
5. **[Public Visitor Stories](./By_Role/public_visitor_stories.md)** - 8 stories cho search + profile

### Cho Scrum Team
- Sprint 1: P0 stories for Module 1 + 2 (core CRUD + workflow)
- Sprint 2: P0 stories for Module 6 (admin)
- Sprint 3: P1 stories for Module 3 + 4 + 5
- Sprint 4: P2 stories (optional enhancement)

---

## 🚀 Next Steps

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
