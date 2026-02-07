# Cấu Trúc Thư Mục Đồ Án Cuối Kỳ - Đặc Tả Hệ Thống

## 📋 Tổng Quan

Cấu trúc thư mục này được tổ chức theo quy trình phân tích và đặc tả yêu cầu hệ thống chuẩn, từ tổng quát đến chi tiết.

---

## 📂 Cấu Trúc Thư Mục

```
DoAnCuoiKy/
│
├── requirements_checklist.md        # Checklist theo dõi tiến độ
├── README.md                         # File này
│
├── docs/                             # THƯMỤC TÀI LIỆU
│   │
│   ├── 01_System_Specification/      # ĐẶC TẢ HỆ THỐNG
│   │   ├── system_overview.md        # Tổng quan hệ thống
│   │   ├── system_scope.md           # Phạm vi và ranh giới
│   │   ├── constraints.md            # Ràng buộc và giả định
│   │   └── stakeholders.md           # Các bên liên quan
│   │
│   ├── 02_System_Clarification/      # LÀM RÕ HỆ THỐNG
│   │   ├── Business_Context/         # Bối cảnh nghiệp vụ
│   │   │   ├── as_is_process.md      # Quy trình hiện tại
│   │   │   ├── to_be_process.md      # Quy trình tương lai
│   │   │   └── problem_statement.md  # Vấn đề cần giải quyết
│   │   ├── User_Analysis/            # Phân tích người dùng
│   │   │   ├── user_groups.md        # Nhóm người dùng
│   │   │   └── user_needs.md         # Nhu cầu người dùng
│   │   └── Context_Diagrams/         # Sơ đồ ngữ cảnh
│   │       └── context_diagram.drawio # Sơ đồ Context
│   │
│   ├── 03_Requirements/              # YÊU CẦU
│   │   ├── Functional/               # Yêu cầu chức năng
│   │   │   ├── functional_overview.md # Tổng quan chức năng
│   │   │   ├── module_*.md           # Chức năng theo module
│   │   │   └── business_rules.md     # Quy tắc nghiệp vụ
│   │   └── Non_Functional/           # Yêu cầu phi chức năng
│   │       ├── performance.md        # Hiệu năng
│   │       ├── security.md           # Bảo mật
│   │       ├── usability.md          # Tính khả dụng
│   │       ├── scalability.md        # Khả năng mở rộng
│   │       └── compatibility.md      # Tương thích
│   │
│   ├── 04_User_Stories/              # USER STORIES
│   │   ├── user_stories_template.md  # Template mẫu
│   │   ├── By_Role/                  # Phân loại theo vai trò
│   │   │   ├── end_user_stories.md   # Stories người dùng cuối
│   │   │   ├── admin_stories.md      # Stories quản trị viên
│   │   │   └── other_roles_stories.md # Stories vai trò khác
│   │   └── Prioritized/              # Phân loại theo độ ưu tiên
│   │       ├── high_priority.md      # Ưu tiên cao
│   │       ├── medium_priority.md    # Ưu tiên trung bình
│   │       └── low_priority.md       # Ưu tiên thấp
│   │
│   ├── 05_Use_Cases/                 # USE CASES
│   │   ├── use_case_template.md      # Template use case chi tiết
│   │   ├── Diagrams/                 # Sơ đồ use case tổng quan
│   │   │   └── use_case_diagram.drawio # Use Case Diagram chính
│   │   ├── High_Level/               # Use cases cấp cao (Level 0)
│   │   │   ├── uc_list.md            # Danh sách use cases
│   │   │   └── uc_*.md               # Use cases tổng quát
│   │   ├── Medium_Level/             # Use cases mức trung bình
│   │   │   └── uc_*.md               # Use cases với flows
│   │   ├── Detailed_Level/           # Use cases chi tiết
│   │   │   └── uc_*_detail.md        # Đặc tả đầy đủ
│   │   ├── Sequence_Diagrams/        # Sequence diagrams
│   │   │   └── seq_*.drawio          # Sơ đồ tuần tự
│   │   └── Activity_Diagrams/        # Activity diagrams
│   │       └── act_*.drawio          # Sơ đồ hoạt động
│   │
│   ├── 06_Diagrams/                  # SƠ ĐỒ TỔNG HỢP
│   │   ├── Context/                  # Context diagrams
│   │   ├── UseCase/                  # Use case diagrams
│   │   ├── Sequence/                 # Sequence diagrams
│   │   ├── Activity/                 # Activity diagrams  
│   │   ├── DataFlow/                 # Data flow diagrams
│   │   └── ER_Diagrams/              # ER diagrams (nếu cần)
│   │
│   ├── 07_Review_Approval/           # XÁC THỰC & PHÊ DUYỆT
│   │   ├── Feedback/                 # Phản hồi
│   │   │   ├── stakeholder_feedback.md # Phản hồi stakeholders
│   │   │   ├── dev_team_feedback.md  # Phản hồi dev team
│   │   │   └── qa_team_feedback.md   # Phản hồi QA team
│   │   └── Revisions/                # Lịch sử điều chỉnh
│   │       ├── revision_history.md   # Lịch sử thay đổi
│   │       └── approval_records.md   # Hồ sơ phê duyệt
│   │
│   └── 08_Final_Documents/           # TÀI LIỆU CUỐI CÙNG
│       ├── SRS/                      # Software Requirements Spec
│       │   └── srs_document.md       # Tài liệu SRS đầy đủ
│       ├── UseCase_Specs/            # Use Case Specification
│       │   └── use_case_specification.md # Tổng hợp use cases
│       └── Traceability/             # Traceability matrix
│           └── traceability_matrix.xlsx # Ma trận liên kết
│
└── templates/                        # TEMPLATES MẪU
    ├── user_story_template.md        # Template user story
    ├── use_case_template.md          # Template use case
    ├── requirement_template.md       # Template yêu cầu
    └── review_template.md            # Template review
```

---

## 🎯 Hướng Dẫn Sử Dụng

### 1. Bắt Đầu
- Mở `requirements_checklist.md` để xem toàn bộ công việc cần làm
- Đọc kỹ từng phần và đánh dấu tiến độ

### 2. Quy Trình Làm Việc
```
01. System Specification
    ↓
02. System Clarification  
    ↓
03. Requirements (Functional + Non-Functional)
    ↓
04. User Stories
    ↓
05. Use Cases (High → Medium → Detailed)
    ↓
06. Diagrams
    ↓
07. Review & Approval
    ↓
08. Final Documents
```

### 3. Quy Tắc Đặt Tên File
- **Use Cases**: `uc_xxx_[name].md` (ví dụ: `uc_001_login.md`)
- **Diagrams**: `[type]_[name].drawio` (ví dụ: `seq_login.drawio`)
- **Modules**: `module_[name].md` (ví dụ: `module_user_management.md`)

### 4. Tips
- ✅ Sử dụng templates trong folder `templates/` để đảm bảo tính nhất quán
- ✅ Lưu tất cả sơ đồ ở cả `05_Use_Cases/` và `06_Diagrams/` (cross-reference)
- ✅ Cập nhật `requirements_checklist.md` thường xuyên
- ✅ Version control: Commit thường xuyên sau mỗi phần hoàn thành

---

## 📊 Công Cụ Đề Xuất

- **Vẽ sơ đồ**: Draw.io, Lucidchart, PlantUML
- **Tài liệu**: Markdown, Google Docs
- **Traceability Matrix**: Excel, Google Sheets
- **Version Control**: Git

---

## 📝 Ghi Chú

- Tất cả tài liệu nên được viết bằng tiếng Việt để dễ review
- Sử dụng format Markdown (.md) cho tài liệu văn bản
- Sử dụng Draw.io (.drawio) cho các sơ đồ để dễ chỉnh sửa

---

*Cập nhật lần cuối: 07/02/2026*
