# Hệ Thống Quản Lý Bài Báo Khoa Học - Đồ Án Cuối Kỳ

## 📋 Tổng Quan

**Tên dự án**: University Faculty Publication Management System (UFPMS)  
**Phạm vi**: Module quản lý bài báo khoa học cho giảng viên trường Đại học  
**Phiên bản tài liệu**: v4.0

Dự án này xây dựng hệ thống quản lý tập trung các công trình nghiên cứu khoa học của giảng viên, bao gồm:
- **Quy trình phê duyệt 2 cấp** (Khoa → Trường)
- **Portfolio công khai** cho giảng viên
- **Báo cáo và thống kê** tự động
- **Dual-Mode System**: Private (Internal workflow) + Public (Portfolio)

---

## 🎯 Mục Tiêu Dự Án

1. ✅ Quản lý tập trung thay vì Excel phân tán
2. ✅ Quy trình phê duyệt minh bạch, có audit trail
3. ✅ Giảm thời gian tạo báo cáo từ **3 ngày → 30 phút**
4. ✅ Tăng uy tín giảng viên qua profile chuyên nghiệp
5. ✅ 80% giảng viên sử dụng trong 6 tháng

---

## 📂 Cấu Trúc Thư Mục

```
DoAnCuoiKy/
│
├── README.md                         # File này
├── requirements_checklist.md        # Checklist theo dõi tiến độ
│
├── docs/                             # THƯ MỤC TÀI LIỆU
│   │
│   ├── 00_Problem_Context/          # ✅ BỐI CẢNH VẤN ĐỀ (HOÀN TẤT)
│   │   ├── README.md                # Tổng quan big picture
│   │   ├── research_output_catalog.md # 7 nhóm công trình NCKH
│   │   ├── legal_framework.md       # Khung pháp lý quốc gia
│   │   └── international_standards.md # Tiêu chuẩn quốc tế
│   │
│   ├── 01_System_Specification/     # ✅ ĐẶC TẢ HỆ THỐNG (HOÀN TẤT)
│   │   ├── README.md                # Tổng hợp + hướng dẫn
│   │   ├── system_overview.md       # 6 modules + State Machine
│   │   ├── system_scope.md          # Phạm vi + Approval Workflow
│   │   ├── stakeholders.md          # 5 roles + Stakeholder analysis
│   │   ├── constraints.md           # Ràng buộc + Workflow assumptions
│   │   └── technology_stack.md      # Spring Boot + MySQL + Storage
│   │
│   ├── 02_System_Clarification/     # ✅ LÀM RÕ HỆ THỐNG (HOÀN TẤT)
│   │   ├── README.md
│   │   ├── Business_Context/
│   │   │   ├── README.md
│   │   │   ├── problem_statement.md    # NEW: Định nghĩa vấn đề
│   │   │   ├── as_is_process.md
│   │   │   └── to_be_process.md
│   │   ├── User_Analysis/
│   │   │   ├── README.md
│   │   │   ├── user_groups.md
│   │   │   └── user_needs.md
│   │   └── Context_Diagrams/
│   │       └── README.md               # Context diagrams
│   │
│   ├── 03_Requirements/             # ✅ YÊU CẦU (HOÀN TẤT)
│   │   ├── README.md                # 65 FRs + 25 NFRs
│   │   ├── Functional/
│   │   │   ├── functional_overview.md
│   │   │   ├── module_01_publication.md (15 FRs)
│   │   │   ├── module_02_approval.md (20 FRs)
│   │   │   ├── module_03_search.md (10 FRs)
│   │   │   ├── module_04_profile.md (7 FRs)
│   │   │   ├── module_05_reporting.md (10 FRs)
│   │   │   ├── module_06_admin.md (8 FRs)
│   │   │   └── business_rules.md
│   │   └── Non_Functional/
│   │       ├── performance.md (5 NFRs)
│   │       ├── security.md (7 NFRs)
│   │       ├── usability.md (5 NFRs)
│   │       ├── scalability.md (4 NFRs)
│   │       └── compatibility.md (4 NFRs)
│   │
│   ├── 04_User_Stories/             # ✅ USER STORIES (HOÀN TẤT)
│   │   ├── README.md                # 65 user stories
│   │   ├── user_stories_template.md
│   │   ├── By_Role/
│   │   │   ├── researcher_stories.md (28 stories)
│   │   │   ├── faculty_reviewer_stories.md (11 stories)
│   │   │   ├── university_reviewer_stories.md (8 stories)
│   │   │   ├── admin_stories.md (13 stories)
│   │   │   └── viewer_stories.md (5 stories)
│   │   └── Prioritized/
│   │       ├── high_priority.md (P0: 25 stories)
│   │       ├── medium_priority.md (P1: 25 stories)
│   │       └── low_priority.md (P2: 15 stories)
│   │
│   ├── 05_Use_Cases/                # ✅ USE CASES (HOÀN TẤT)
│   │   ├── README.md                # 80 use cases
│   │   ├── use_case_template.md
│   │   ├── High_Level/
│   │   │   └── 6 high-level use cases
│   │   ├── Medium_Level/
│   │   │   └── 54 medium-level use cases (6 modules)
│   │   └── Detailed_Level/
│   │       └── 20 detailed P0 use cases
│   │
│   ├── 06_Diagrams/                 # ✅ SƠ ĐỒ TỔNG HỢP (HOÀN TẤT)
│   │   ├── README.md                # Navigation guide
│   │   ├── UseCase/                 # 7 use case diagrams
│   │   │   ├── README.md
│   │   │   ├── overall_system.md
│   │   │   └── module_01-06_*.md
│   │   ├── Sequence/                # 7 sequence diagrams (P0)
│   │   │   ├── README.md
│   │   │   ├── seq_create_publication.md
│   │   │   ├── seq_submit_for_review.md
│   │   │   ├── seq_faculty_review.md
│   │   │   ├── seq_university_approval.md
│   │   │   ├── seq_revision_request.md
│   │   │   ├── seq_search_publications.md
│   │   │   └── seq_authentication.md
│   │   ├── Activity/                # 4 activity diagrams
│   │   │   ├── README.md
│   │   │   ├── act_approval_workflow.md
│   │   │   ├── act_publication_creation.md
│   │   │   ├── act_search_filter.md
│   │   │   └── act_report_generation.md
│   │   ├── ER_Diagrams/             # Database schema
│   │   │   ├── README.md
│   │   │   ├── complete_erd.md (10 tables)
│   │   │   └── entity_specifications.md
│   │   ├── Context/                 # System context
│   │   │   ├── README.md
│   │   │   ├── system_context.md
│   │   │   └── external_integrations.md
│   │   └── DataFlow/                # Data flow diagrams
│   │       ├── README.md
│   │       ├── dfd_level_0.md
│   │       ├── dfd_level_1.md
│   │       └── dfd_level_2_approval.md
│   │
│   ├── 07_Development_Plan/         # ✅ KẾ HOẠCH PHÁT TRIỂN (HOÀN TẤT)
│   │   ├── incremental_development_plan.md  # MVP → v1.0 → v1.1 plan
│   │   ├── initial_setup_guide.md           # Hướng dẫn setup môi trường
│   │   ├── team_workflow_v1.0.md            # Quy trình làm việc nhóm
│   │   └── SOPs/                            # 8 SOPs
│   │       ├── README.md
│   │       ├── sop-system-specification.md  # SOP phân tích đặc tả
│   │       ├── SOP_PM_V1.0.md               # Project Manager
│   │       ├── SOP_BA_V1.0.md               # Business Analyst
│   │       ├── SOP_TechLead_V1.0.md         # Tech Lead
│   │       ├── SOP_Backend_V1.0.md          # Backend Developer
│   │       ├── SOP_Frontend_V1.0.md         # Frontend Developer
│   │       ├── SOP_UIUX_V1.0.md             # UI/UX Designer
│   │       └── SOP_QA_V1.0.md               # QA Engineer
│   │
│   ├── 07_Review_Approval/          # XÁC THỰC & PHÊ DUYỆT
│   │   ├── Feedback/
│   │   │   ├── stakeholder_feedback.md
│   │   │   ├── dev_team_feedback.md
│   │   │   └── qa_team_feedback.md
│   │   └── Revisions/
│   │       ├── revision_history.md
│   │       └── approval_records.md
│   │
│   ├── 08_Final_Documents/          # 🔄 TÀI LIỆU CUỐI CÙNG (ĐANG TIẾN HÀNH)
│   │   ├── EXECUTIVE_SUMMARY.md             # ✅ Báo cáo Executive Summary
│   │   ├── SDD_Software_Design_Document.md  # ✅ Tài liệu thiết kế phần mềm
│   │   ├── SRS/                             # ⏳ Software Requirements Spec
│   │   ├── UseCase_Specs/                   # ⏳ Use Case Specification
│   │   └── Traceability/                    # ⏳ Traceability Matrix
│   │
│   └── temp/                         # TÀI LIỆU TẠM, PHÁC THẢO
│       ├── phacthao.md
│       ├── presentation_script.md
│       ├── review_01_system_specification.md
│       ├── research_keywords.md
│       └── ... (các file tạm khác)
│
└── templates/                        # TEMPLATES MẪU
    ├── user_story_template.md
    ├── use_case_template.md
    ├── requirement_template.md
    └── review_template.md
```

---

## ✅ Tiến Độ Hiện Tại

| Folder | Trạng thái | Ghi chú |
|--------|-----------|---------|
| **00_Problem_Context** | ✅ **100%** | Big picture, 7 nhóm công trình, pháp lý |
| **01_System_Specification** | ✅ **100%** | Tech stack + Approval Workflow + Stakeholders |
| **02_System_Clarification** | ✅ **100%** | Problem statement, As-Is/To-Be, User analysis |
| **03_Requirements** | ✅ **100%** | 65 FRs + 25 NFRs, P0/P1/P2 prioritization |
| **04_User_Stories** | ✅ **100%** | 65 stories by Role + Priority |
| **05_Use_Cases** | ✅ **100%** | 80 use cases (6 high-level, 54 medium, 20 detailed) |
| **06_Diagrams** | ✅ **100%** | 25 diagrams (Use Case, Sequence, Activity, ER, Context, DFD) |
| **07_Development_Plan** | ✅ **100%** | Incremental plan, Team workflow, Initial setup, 8 SOPs |
| **07_Review_Approval** | ⏳ **0%** | Chưa bắt đầu |
| **08_Final_Documents** | 🔄 **20%** | Executive Summary, SDD hoàn thành, SRS/Traceability đang tiến hành |

**Tổng tiến độ**: ~92% 🚀 (8/10 folders hoàn thành, 1 đang tiến hành)

---

## 🎯 Quy Trình Làm Việc

```
00. Problem Context (✅ Hoàn tất)
    ↓
01. System Specification (✅ Hoàn tất)
    ↓
02. System Clarification (✅ Hoàn tất - Problem + As-Is/To-Be + User Analysis)
    ↓
03. Requirements (✅ Hoàn tất - 65 FRs + 25 NFRs)
    ↓
04. User Stories (✅ Hoàn tất - 65 stories)
    ↓
05. Use Cases (✅ Hoàn tất - 80 use cases)
    ↓
06. Diagrams (✅ Hoàn tất - 25 diagrams)
    ↓
07. Development Plan (✅ Hoàn tất - Incremental plan + Team workflow + 8 SOPs)
    ↓
07. Review & Approval (⏳ Tiếp theo)
    ↓
08. Final Documents/SRS (🔄 Đang tiến hành - SDD hoàn thành)
```

---

## 🔑 Quyết Định Kỹ Thuật Chính

### Technology Stack

| Thành phần | Công nghệ | Lý do |
|------------|-----------|-------|
| **Backend** | Java Spring Boot 3.x | Phổ biến VN, ecosystem mạnh, dễ tuyển người |
| **Database** | MySQL 8.0+ | Free, ACID, community support tốt |
| **Frontend** | React 18 + TypeScript | Ecosystem lớn, dễ tìm developer |
| **Storage** | Local File System (MVP) | Đơn giản, đủ dùng, không phí phát sinh |
| **Auth** | LDAP/AD + JWT | SSO, tích hợp sẵn |

### Architecture

- **Pattern**: N-tier (Presentation → Business Logic → Data Access)
- **API**: RESTful API (stateless)
- **Dual-Mode**: 
  - Private (Internal): Workflow phê duyệt
  - Public (Portfolio): CHỈ công trình đã phê duyệt

---

## 🌟 Đặc Điểm Nổi Bật

### 1. Quy Trình Phê Duyệt 2 Cấp

```
Giảng viên nộp → Khoa xét duyệt → Trường phê duyệt → Công bố
                      ↓                    ↓
              [Yêu cầu sửa]         [Từ chối/Approve]
```

**9 trạng thái**: DRAFT → SUBMITTED → FACULTY_REVIEWING → FACULTY_APPROVED → UNIVERSITY_REVIEWING → PUBLISHED

### 2. State Machine với Audit Trail

- Lưu lịch sử mọi thay đổi trạng thái
- Người duyệt, thời gian, nhận xét
- Không thể xóa/sửa lịch sử

### 3. Dual-Mode System

- **Private Mode**: Workflow nội bộ (GV, CB Khoa, CB Trường, Admin)
- **Public Mode**: Portfolio công khai (Viewer, Sinh viên, Cộng đồng)

### 4. Phân Quyền Chi Tiết (5 Roles)

1. **SuperAdmin**: Quản trị hệ thống
2. **Researcher** (Giảng viên): Nộp công trình, xem feedback
3. **Faculty Reviewer** (CB Khoa): Xét duyệt cấp Khoa
4. **University Reviewer** (CB Trường): Phê duyệt cuối
5. **Viewer**: Xem công trình đã công bố

---

## 📖 Hướng Dẫn Sử Dụng

### 1. Bắt Đầu

1. Đọc [`requirements_checklist.md`](./requirements_checklist.md) để nắm toàn bộ công việc
2. Đọc [`docs/00_Problem_Context/README.md`](./docs/00_Problem_Context/README.md) để hiểu big picture
3. Đọc [`docs/01_System_Specification/README.md`](./docs/01_System_Specification/README.md) để hiểu scope

### 2. Quy Tắc Đặt Tên File

- **Use Cases**: `uc_xxx_[name].md` (ví dụ: `uc_001_login.md`)
- **Diagrams**: `[type]_[name].drawio` (ví dụ: `seq_login.drawio`)
- **Modules**: `module_[name].md` (ví dụ: `module_publication_management.md`)

### 3. Workflow Git

```bash
# Sau mỗi phần hoàn thành
git add .
git commit -m "Hoàn thành [tên phần]"
git push origin main
```

### 4. Tips

- ✅ Sử dụng templates trong `templates/` để đảm bảo tính nhất quán
- ✅ Tham khảo international standards trong `00_Problem_Context/`
- ✅ Cập nhật `requirements_checklist.md` thường xuyên
- ✅ Lưu phác thảo tạm trong `docs/temp/` trước khi finalize

---

## 📊 Công Cụ Đề Xuất

| Mục đích | Công cụ |
|----------|---------|
| **Vẽ sơ đồ** | Draw.io, Lucidchart, PlantUML |
| **Tài liệu** | Markdown (VS Code), Notion |
| **Traceability Matrix** | Excel, Google Sheets |
| **Version Control** | Git + GitHub |
| **Project Management** | Trello, Notion, GitHub Projects |

---

## 🚀 Các Bước Tiếp Theo

### ✅ Đã Hoàn Thành

- [x] Hoàn thiện `00_Problem_Context` (100%)
- [x] Hoàn thiện `01_System_Specification` (100%)
- [x] Hoàn thiện `02_System_Clarification` (100% - Problem statement, As-Is/To-Be, User analysis)
- [x] Viết đầy đủ `03_Requirements` (65 FRs + 25 NFRs)
- [x] Tạo `04_User_Stories` cho 5 roles (65 stories)
- [x] Chi tiết hóa `05_Use_Cases` (80 use cases)
- [x] Vẽ `06_Diagrams` (25 diagrams: Use Case, Sequence, Activity, ER, Context, DFD)
- [x] Lập `07_Development_Plan` (Incremental plan + Team workflow + Initial setup + 8 SOPs)
- [x] Tạo `SDD_Software_Design_Document.md` trong `08_Final_Documents`

### 🔄 Đang Tiến Hành

- [ ] `08_Final_Documents` - SRS document & Traceability Matrix

### ⏳ Tiếp Theo

- [ ] `07_Review_Approval` - Stakeholder feedback & revisions
- [ ] Validation & testing planning



---

## 📝 Ghi Chú Quan Trọng

### Phạm Vi Đã Thu Hẹp

> ⚠️ **Lưu ý**: Dự án CHỈ quản lý **BÀI BÁO KHOA HỌC**, không phải 7 nhóm công trình như trong `00_Problem_Context`. 
> 
> Đây là quyết định **scope reduction** để đảm bảo MVP hoàn thành đúng hạn 3 tháng.

### Technology Choice Rationale

> ✅ **Java Spring Boot + MySQL** được chọn vì:
> - Phổ biến nhất tại VN (dễ tuyển người)
> - Documentation và community support mạnh
> - Ecosystem JVM ổn định
> - Không phí license

### Approval Workflow Design

> 💡 **Dual-Mode System** được thiết kế để:
> - **Internal**: Kiểm soát chất lượng qua workflow 2 cấp
> - **Public**: Chỉ công bố những công trình đã được phê duyệt
> - Tách biệt rõ ràng giữa quản trị nội bộ và portfolio công khai

---

## 📚 Tài Liệu Tham Khảo

- [ISO/IEC/IEEE 29148:2018](./docs/00_Problem_Context/international_standards.md) - Systems and software engineering
- [Research Information Management Standards](./docs/00_Problem_Context/international_standards.md#rim-standards)
- [Vietnam Legal Framework](./docs/00_Problem_Context/legal_framework.md) - Khung pháp lý quốc gia

---

## 👥 Team \u0026 Contact

**Sinh viên thực hiện**: [Tên của bạn]  
**Lớp**: [Mã lớp]  
**Giảng viên hướng dẫn**: [Tên giảng viên]  

---

## 📄 License \u0026 Version

**Version**: v4.0  
**Last Updated**: 18/02/2026  
**Status**: 🚀 Gần hoàn thành (92% - Documentation & Planning Phase)

**Changelog**:
- v4.0 (18/02/2026): ✅ Hoàn thành 07_Development_Plan (Incremental plan, Team workflow, 8 SOPs); ✅ SDD trong 08_Final_Documents
- v3.1 (11/02/2026): ✅ Hoàn thành 02_System_Clarification (Problem statement, As-Is/To-Be process, User analysis)
- v3.0 (11/02/2026): ✅ Hoàn thành Requirements, User Stories, Use Cases, và Diagrams (25 files)
- v2.0 (10/02/2026): Tích hợp Approval Workflow + Technology Stack finalized
- v1.0 (07/02/2026): Initial structure

---

*Để biết chi tiết tiến độ từng phần, xem [`requirements_checklist.md`](./requirements_checklist.md)*
