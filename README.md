# Hệ Thống Quản Lý Bài Báo Khoa Học - Đồ Án Cuối Kỳ

## 📋 Tổng Quan

**Tên dự án**: University Faculty Publication Management System (UFPMS)  
**Phạm vi**: Module quản lý bài báo khoa học cho giảng viên trường Đại học  
**Phiên bản tài liệu**: v2.0

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
│   ├── 00_Problem_Context/          # 🆕 BỐI CẢNH VẤN ĐỀ
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
│   ├── 02_System_Clarification/     # LÀM RÕ HỆ THỐNG
│   │   ├── README.md
│   │   ├── Business_Context/
│   │   │   ├── as_is_process.md
│   │   │   ├── to_be_process.md
│   │   │   └── problem_statement.md
│   │   ├── User_Analysis/
│   │   │   ├── user_groups.md
│   │   │   └── user_needs.md
│   │   └── Context_Diagrams/
│   │       └── context_diagram.drawio
│   │
│   ├── 03_Requirements/             # YÊU CẦU
│   │   ├── README.md
│   │   ├── Functional/
│   │   │   ├── functional_overview.md
│   │   │   ├── module_*.md
│   │   │   └── business_rules.md
│   │   └── Non_Functional/
│   │       ├── performance.md
│   │       ├── security.md
│   │       ├── usability.md
│   │       ├── scalability.md
│   │       └── compatibility.md
│   │
│   ├── 04_User_Stories/             # USER STORIES
│   │   ├── README.md
│   │   ├── user_stories_template.md
│   │   ├── By_Role/
│   │   │   ├── researcher_stories.md
│   │   │   ├── faculty_reviewer_stories.md
│   │   │   ├── university_reviewer_stories.md
│   │   │   ├── admin_stories.md
│   │   │   └── viewer_stories.md
│   │   └── Prioritized/
│   │       ├── high_priority.md
│   │       ├── medium_priority.md
│   │       └── low_priority.md
│   │
│   ├── 05_Use_Cases/                # USE CASES
│   │   ├── README.md
│   │   ├── use_case_template.md
│   │   ├── Diagrams/
│   │   │   └── use_case_diagram.drawio
│   │   ├── High_Level/
│   │   │   ├── uc_list.md
│   │   │   └── uc_*.md
│   │   ├── Medium_Level/
│   │   │   └── uc_*.md
│   │   ├── Detailed_Level/
│   │   │   └── uc_*_detail.md
│   │   ├── Sequence_Diagrams/
│   │   │   └── seq_*.drawio
│   │   └── Activity_Diagrams/
│   │       └── act_*.drawio
│   │
│   ├── 06_Diagrams/                 # SƠ ĐỒ TỔNG HỢP
│   │   ├── Context/
│   │   ├── UseCase/
│   │   ├── Sequence/
│   │   ├── Activity/
│   │   ├── DataFlow/
│   │   └── ER_Diagrams/
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
│   ├── 08_Final_Documents/          # TÀI LIỆU CUỐI CÙNG
│   │   ├── SRS/
│   │   │   └── srs_document.md
│   │   ├── UseCase_Specs/
│   │   │   └── use_case_specification.md
│   │   └── Traceability/
│   │       └── traceability_matrix.xlsx
│   │
│   └── temp/                         # 🆕 TÀI LIỆU TẠM, PHÁc THẢO
│       ├── phacthao.md
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
| **01_System_Specification** | ✅ **95%** | Tech stack + Approval Workflow hoàn tất, stakeholders cần bổ sung |
| **02_System_clarification** | 🔄 **20%** | Đang triển khai |
| **03_Requirements** | 🔄 **10%** | Chuẩn bị |
| **04_User_Stories** | ⏳ **0%** | Chưa bắt đầu |
| **05_Use_Cases** | ⏳ **0%** | Chưa bắt đầu |
| **06_Diagrams** | ⏳ **0%** | Chưa bắt đầu |
| **07_Review_Approval** | ⏳ **0%** | Chưa bắt đầu |
| **08_Final_Documents** | ⏳ **0%** | Chưa bắt đầu |

**Tổng tiến độ**: ~25% ⏳

---

## 🎯 Quy Trình Làm Việc

```
00. Problem Context (✅ Hoàn tất)
    ↓
01. System Specification (✅ 95% - Gần hoàn tất)
    ↓
02. System Clarification (🔄 Đang làm)
    ↓
03. Requirements (Functional + Non-Functional)
    ↓
04. User Stories (5 roles)
    ↓
05. Use Cases (High → Medium → Detailed)
    ↓
06. Diagrams
    ↓
07. Review & Approval
    ↓
08. Final Documents (SRS)
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

### Ngắn Hạn (1-2 tuần)

- [x] Hoàn thiện `00_Problem_Context` 
- [x] Hoàn thiện `01_System_Specification` (còn 5% stakeholders)
- [ ] Hoàn thiện `02_System_Clarification`
  - [ ] As-Is process diagram
  - [ ] To-Be process diagram
  - [ ] Context diagram

### Trung Hạn (3-4 tuần)

- [ ] Viết đầy đủ Requirements (Functional + Non-Functional)
- [ ] Tạo User Stories cho 5 roles
- [ ] Vẽ Use Case Diagrams

### Dài Hạn (5-8 tuần)

- [ ] Chi tiết hóa Use Cases
- [ ] Vẽ Sequence Diagrams, Activity Diagrams
- [ ] Tạo Traceability Matrix
- [ ] Hoàn thiện SRS Document

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

**Version**: v2.0  
**Last Updated**: 10/02/2026 21:03  
**Status**: 🔄 Đang phát triển (Development)

**Changelog**:
- v2.0 (10/02/2026): Tích hợp Approval Workflow + Technology Stack finalized
- v1.0 (07/02/2026): Initial structure

---

*Để biết chi tiết tiến độ từng phần, xem [`requirements_checklist.md`](./requirements_checklist.md)*
