---
description: SOP cho Liệt kê - Phân tích Đặc tả & Thiết kế Hệ thống Phần mềm
---

# SOP: Liệt kê - Phân tích Đặc tả & Thiết kế Hệ thống Phần mềm

> **Mục đích**: Quy trình chuẩn hóa để thu thập, phân tích và tài liệu hóa đặc tả hệ thống phần mềm từ bối cảnh đến thiết kế chi tiết.
> 
> **Áp dụng cho**: Đồ án phần mềm, dự án phát triển hệ thống, tài liệu kỹ thuật
> 
> **Phiên bản**: 1.0 (Ngày: 12/02/2026)

---

## 📋 Tổng Quan Quy Trình

### Quy trình 9 Bước

```
[00] Bối Cảnh Bài Toán
   ↓
[01] Đặc Tả Hệ Thống
   ↓
[02] Làm Rõ Hệ Thống
   ↓
[03] Yêu Cầu Chi Tiết
   ↓
[04] User Stories
   ↓
[05] Use Cases
   ↓
[06] Biểu Đồ Thiết Kế
   ↓
[07] Review & Approval
   ↓
[08] Tài Liệu Cuối Cùng
```

**Đầu vào**: Ý tưởng/yêu cầu nghiệp vụ ban đầu

**Đầu ra**: Bộ tài liệu hoàn chỉnh sẵn sàng cho thiết kế kỹ thuật và phát triển

---

## 🎯 BƯỚC 00: Phân Tích Bối Cảnh Bài Toán

### Mục Đích
Hiểu toàn cảnh vấn đề trước khi thu hẹp phạm vi đồ án.

### Thư Mục
```
docs/00_Problem_Context/
├── README.md
├── research_output_catalog.md (nếu có danh mục liên quan)
├── legal_framework.md (khung pháp lý liên quan)
├── stakeholders_full.md (tất cả bên liên quan)
└── problem_context.md (phân tích vấn đề chi tiết)
```

### Các Công Việc

#### 1. Xác Định Toàn Cảnh (Big Picture)
- [ ] Mô tả vấn đề tổng quát (domain industry, lĩnh vực)
- [ ] Liệt kê tất cả loại đối tượng/tính năng có thể có
- [ ] Phân tích các bên liên quan ở cấp độ cao nhất
- [ ] Tìm hiểu khung pháp lý/tiêu chuẩn ngành (nếu có)

**Ví dụ**: 
- Domain: Quản lý nghiên cứu khoa học
- Toàn cảnh: 7 nhóm công trình, 28 loại khác nhau
- Stakeholders: Bộ, Ngành, Địa phương, Cơ sở

#### 2. Phân Tích Tình Trạng Hiện Tại (As-Is)
- [ ] ❌ Vấn đề gì đang tồn tại?
- [ ] ❌ Điểm nghẽn, khó khăn nào?
- [ ] ❌ Chi phí (thời gian, tiền bạc, nguồn lực)?

#### 3. Xác Định Phạm Vi Đồ Án
- [ ] Thu hẹp từ toàn cảnh → phạm vi khả thi
- [ ] Lý do chọn phạm vi này (tầm quan trọng, tính khả thi, dữ liệu sẵn có)
- [ ] Giá trị đóng góp của module nhỏ trong hệ thống lớn

**Template Thu Hẹp Phạm Vi**:
```
TOÀN CẢNH:
- Đối tượng: [Tất cả loại đối tượng có thể]
- Người dùng: [Tất cả nhóm người dùng tiềm năng]
- Quy mô: [Quốc gia/Quốc tế/Ngành]

PHẠM VI ĐỒ ÁN:
✅ Đối tượng: CHỈ [loại cụ thể]
✅ Người dùng: CHỈ [nhóm cụ thể]
✅ Cơ quan: CHỉ [tổ chức cụ thể]
✅ Chức năng: [Scope cốt lõi]
```

### Sản Phẩm Đầu Ra
- [x] `README.md` - Tổng quan folder
- [x] Tài liệu phân tích bối cảnh (3-4 files)
- [x] Biểu đồ minh họa quan hệ toàn cảnh ↔ đồ án

---

## 🎯 BƯỚC 01: Đặc Tả Hệ Thống (System Specification)

### Mục Đích
Định nghĩa "WHAT" (làm gì) với phạm vi đã thu hẹp, chưa nói đến "HOW" (làm thế nào).

### Thư Mục
```
docs/01_System_Specification/
├── README.md
├── system_overview.md
├── system_scope.md
├── stakeholders.md
├── constraints.md
└── technology_stack.md
```

### Các Công Việc

#### 1. System Overview (Tổng Quan Hệ Thống)
- [ ] Tên hệ thống (viết tắt + đầy đủ)
- [ ] Vấn đề giải quyết (Problem Statement)
- [ ] Mục đích và mục tiêu (Purpose & Goals)
- [ ] Các module chính (6-8 modules)
- [ ] Tiêu chí thành công (Success Metrics)

**Template Module**:
```
Module [X]: [Tên Module]
- Mô tả: [1-2 câu]
- Người dùng chính: [Vai trò]
- Tính năng cốt lõi: [3-5 items]
```

#### 2. System Scope (Phạm Vi & Ranh Giới)
- [ ] ✅ TRONG phạm vi: Liệt kê cụ thể
- [ ] ❌ NGOÀI phạm vi: Liệt kê rõ ràng
- [ ] Ranh giới dữ liệu (owned vs integrated)
- [ ] Ranh giới người dùng (primary vs secondary)
- [ ] Ranh giới thời gian (MVP → Phase 2 → Phase 3)

#### 3. Stakeholders (Các Bên Liên Quan)
- [ ] **Primary**: Người dùng trực tiếp (ước tính số lượng)
- [ ] **Secondary**: Người dùng gián tiếp
- [ ] **External**: Đối tác, cơ quan bên ngoài
- [ ] Vai trò hệ thống (Roles): 4-6 roles
- [ ] Ma trận phân tích: Mức quan tâm × Mức ảnh hưởng
- [ ] Kế hoạch giao tiếp với từng nhóm

#### 4. Constraints (Ràng Buộc & Giả Định)

**Ràng buộc**:
- [ ] Pháp lý: Luật, nghị định, thông tư liên quan
- [ ] Kỹ thuật: Tương thích, hiệu năng, công nghệ hiện có
- [ ] Tài nguyên: Ngân sách, nhân lực, thời gian
- [ ] Dữ liệu: Import dữ liệu cũ, kích thước file
- [ ] Trình duyệt/Thiết bị: Hỗ trợ nền tảng nào

**Giả định**:
- [ ] Về người dùng (kỹ năng, thiết bị)
- [ ] Về dữ liệu (chất lượng, tính trung thực)
- [ ] Về tổ chức (cam kết, hỗ trợ)
- [ ] Về hạ tầng (Internet, AD/LDAP, backup)

**Rủi ro**:
- [ ] Liệt kê rủi ro cho mỗi giả định

#### 5. Technology Stack (Công Nghệ & Kiến Trúc)

**Quyết định chính**:
- [ ] Frontend: Framework + Library + UI Kit
- [ ] Backend: Framework + Language
- [ ] Database: RDBMS
- [ ] Storage: File system strategy
- [ ] Authentication: Method

**Lý do chọn** (cho mỗi quyết định):
- [ ] Phổ biến tại thị trường
- [ ] Ecosystem mạnh
- [ ] Dễ tuyển nhân lực
- [ ] Chi phí thấp
- [ ] Documentation đầy đủ

**Phương án thay thế**:
- [ ] Liệt kê 2-3 phương án khác với ưu/nhược điểm

### Sản Phẩm Đầu Ra
- [x] 5 tài liệu đặc tả (.md files)
- [x] README tổng hợp
- [x] Biểu đồ mối quan hệ giữa các tài liệu

---

## 🎯 BƯỚC 02: Làm Rõ Hệ Thống (System Clarification)

### Mục Đích
Hiểu sâu hơn về nghiệp vụ, người dùng, và quy trình.

### Thư Mục
```
docs/02_System_Clarification/
├── README.md
├── Business_Context/
│   ├── as_is_process.md
│   ├── to_be_process.md
│   └── process_comparison.md
├── User_Analysis/
│   ├── user_groups.md
│   ├── user_needs.md
│   └── user_personas.md
└── Context_Diagrams/
    ├── system_context.md
    └── data_flow_context.md
```

### Các Công Việc

#### 1. Business Context (Bối Cảnh Nghiệp Vụ)

**As-Is Process** (Quy trình hiện tại):
- [ ] Vẽ flowchart quy trình cũ
- [ ] Xác định điểm nghẽn, vấn đề
- [ ] Đo lường: Thời gian, chi phí, tỉ lệ lỗi

**To-Be Process** (Quy trình tương lai):
- [ ] Vẽ flowchart quy trình mới với hệ thống
- [ ] Highlight những thay đổi chính
- [ ] Dự đoán cải thiện: % giảm thời gian, chi phí

**Process Comparison**:
- [ ] Bảng so sánh As-Is vs To-Be
- [ ] Key Performance Indicators (KPIs)

#### 2. User Analysis (Phân Tích Người Dùng)

**User Groups**:
- [ ] Liệt kê 4-6 nhóm người dùng
- [ ] Mỗi nhóm: Tên, Mô tả, Số lượng, Mục tiêu

**User Needs**:
- [ ] Mỗi nhóm có 5-10 nhu cầu cụ thể
- [ ] Độ ưu tiên: Must Have / Should Have / Nice to Have

**User Personas**:
- [ ] 2-3 personas đại diện
- [ ] Mỗi persona: Tên, Tuổi, Vai trò, Mục tiêu, Pain Points, Tech Savviness

#### 3. Context Diagrams

**System Context Diagram**:
- [ ] Hệ thống ở trung tâm
- [ ] External actors (người dùng, hệ thống bên ngoài)
- [ ] Data flows giữa actors và hệ thống

**Data Flow Context**:
- [ ] Level 0 DFD (tổng quan)
- [ ] Xác định: Data sources, Data sinks, Processes, Data stores

### Sản Phẩm Đầu Ra
- [x] 3 nhóm tài liệu (Business, User, Context)
- [x] Biểu đồ quy trình (Mermaid/PlantUML)
- [x] User personas

---

## 🎯 BƯỚC 03: Yêu Cầu Chi Tiết (Requirements)

### Mục Đích
Chuyển đổi nhu cầu người dùng thành yêu cầu hệ thống cụ thể, đo lường được.

### Thư Mục
```
docs/03_Requirements/
├── README.md
├── Functional/
│   ├── README.md
│   ├── functional_overview.md
│   ├── module_01_[tên].md (10-20 FRs)
│   ├── module_02_[tên].md
│   ├── ...
│   └── business_rules.md
└── Non_Functional/
    ├── README.md
    ├── performance.md
    ├── security.md
    ├── usability.md
    ├── scalability.md
    └── compatibility.md
```

### Các Công Việc

#### 1. Functional Requirements (Yêu cầu Chức Năng)

**Cho mỗi Module**:
- [ ] Liệt kê 5-20 yêu cầu chức năng cụ thể
- [ ] Mỗi FR có:
  - ID: `FR-[MODULE]-[NUMBER]`
  - Tên: [Tên ngắn gọn]
  - Độ ưu tiên: P0 (Must) / P1 (Should) / P2 (Nice to Have)
  - Mô tả: [1-2 câu]
  - Acceptance Criteria: GIVEN-WHEN-THEN format

**Template FR**:
```
### FR-[MOD]-[NUM]: [Tên Yêu Cầu]

**Độ ưu tiên**: P[0/1/2]
**Module**: [Module X]

**Mô tả**:
[Mô tả 1-2 câu về yêu cầu]

**Tiêu chí Chấp nhận (Acceptance Criteria)**:
GIVEN (KHI) [điều kiện tiên quyết]
WHEN (VÀ) [hành động người dùng]
THEN (THÌ) [kết quả mong đợi]
AND (VÀ) [kết quả bổ sung]
```

**Business Rules**:
- [ ] Tổng hợp các quy tắc nghiệp vụ quan trọng
- [ ] Ví dụ: Quy tắc hiển thị, quyền sở hữu, validation

**Tổng Số FR Gợi Ý**:
- Module CRUD: 10-15 FRs
- Module Workflow: 15-25 FRs
- Module Search: 5-10 FRs
- Module Report: 5-10 FRs
- Module Admin: 8-15 FRs

#### 2. Non-Functional Requirements (Yêu cầu Phi Chức Năng)

**Performance (Hiệu Năng)**:
- [ ] Response time: Tải trang < Xs, API < Ys
- [ ] Throughput: X transactions/second
- [ ] Concurrent users: Số người dùng đồng thời

**Security (Bảo Mật)**:
- [ ] Authentication method (LDAP, OAuth, etc.)
- [ ] Authorization (RBAC, ABAC)
- [ ] Data encryption (at rest, in transit)
- [ ] Audit logging

**Usability (Khả Dụng)**:
- [ ] Form completion time < X phút
- [ ] Responsive design (mobile, tablet, desktop)
- [ ] Accessibility standards (WCAG AA)
- [ ] Multi-language support (nếu có)

**Scalability (Khả Năng Mở Rộng)**:
- [ ] Data volume (số lượng records)
- [ ] User growth (số người dùng trong 1-3 năm)
- [ ] Stateless architecture

**Compatibility (Tương Thích)**:
- [ ] Browsers: Chrome X+, Firefox X+, Edge X+, Safari X+
- [ ] Database: MySQL/PostgreSQL version
- [ ] OS: Windows/Linux/macOS

#### 3. Dependencies & Integrations
- [ ] Hệ thống bên ngoài cần tích hợp
- [ ] APIs cần sử dụng
- [ ] Độ ưu tiên cho mỗi integration (P0/P1/P2)

### Sản Phẩm Đầu Ra
- [x] 60-80 Functional Requirements (6 modules)
- [x] 20-30 Non-Functional Requirements (5 categories)
- [x] Business rules document
- [x] Traceability map (User Needs → FRs)

---

## 🎯 BƯỚC 04: User Stories

### Mục Đích
Chuyển đổi yêu cầu thành stories theo góc nhìn người dùng cuối.

### Thư Mục
```
docs/04_User_Stories/
├── README.md
├── By_Role/
│   ├── [role1]_stories.md
│   ├── [role2]_stories.md
│   ├── ...
└── Prioritized/
    ├── p0_must_have.md
    ├── p1_should_have.md
    └── p2_nice_to_have.md
```

### Các Công Việc

#### 1. Xác Định User Roles
- [ ] Liệt kê 4-6 vai trò người dùng chính
- [ ] Mỗi role: Tên, Mục tiêu, Modules sử dụng

#### 2. Viết User Stories Theo Role

**Template**:
```
### US-[ROLE]-[NUM]: [Tên Story]

**Độ ưu tiên**: P[0/1/2]
**Yêu cầu liên quan**: FR-[MOD]-[NUM]

**Story**:
As a [vai trò],
I want [tính năng],
So that [lợi ích].

**Acceptance Criteria**:
GIVEN [điều kiện tiên quyết]
WHEN [hành động]
THEN [kết quả mong đợi]
AND [kết quả bổ sung]
```

**Số lượng Stories**:
- Primary users: 20-30 stories mỗi role
- Secondary users: 8-15 stories mỗi role
- Admin: 8-12 stories

#### 3. Phân Loại Theo Priority
- [ ] Tổng hợp tất cả stories vào 3 files theo P0/P1/P2
- [ ] P0: 40-50 stories (MVP)
- [ ] P1: 20-30 stories (Phase 1.5)
- [ ] P2: 10-20 stories (Phase 2)

#### 4. Traceability Matrix
- [ ] Bảng: User Story ↔ FR ↔ Module

### Sản Phẩm Đầu Ra
- [x] 60-80 User Stories
- [x] Tài liệu theo Role (4-6 files)
- [x] Tài liệu theo Priority (3 files)
- [x] Traceability matrix

---

## 🎯 BƯỚC 05: Use Cases

### Mục Đích
Mô tả chi tiết tương tác giữa actors và hệ thống để đạt mục tiêu.

### Thư Mục
```
docs/05_Use_Cases/
├── README.md
├── High_Level/
│   ├── README.md
│   └── uc_hl_0X_[module].md (1 file/module)
├── Medium_Level/
│   ├── README.md
│   └── module_0X_[name].md (6 files, ~9 UCs/file)
├── Detailed_Level/
│   ├── README.md
│   └── uc_dX_XX_[name].md (20 files cho P0)
└── Diagrams/
    ├── README.md
    └── overall_system_diagram.md
```

### Các Công Việc

#### 1. High-Level Use Cases (6 Use Cases)
- [ ] 1 use case cho mỗi module
- [ ] ID: `UC-HL-0X`
- [ ] Mô tả tổng quan, actors, sub-use cases

#### 2. Medium-Level Use Cases (40-60 Use Cases)
- [ ] Chia nhỏ mỗi high-level thành 7-10 medium-level
- [ ] ID: `UC-MX-XXX` (X = module number)

**Template**:
```
### UC-MX-XXX: [Tên Use Case]

**ID**: UC-MX-XXX
**Độ Ưu Tiên**: P[0/1/2]
**Tác Nhân**: [Actors]
**User Stories Liên Quan**: US-XXX-XXX
**Yêu Cầu Chức Năng**: FR-XXX-XXX

**Mục Tiêu**:
[Mô tả ngắn gọn]

**Điều Kiện Tiên Quyết**:
- [Điều kiện 1]
- [Điều kiện 2]

**Luồng Chính**:
1. Actor thực hiện [hành động]
2. Hệ thống [phản hồi]
3. ...

**Điều Kiện Hậu Quyết**:
- Thành công: [Trạng thái]
- Thất bại: [Trạng thái]

**Quy Tắc Nghiệp Vụ**:
- [Rule 1]
- [Rule 2]
```

#### 3. Detailed-Level Use Cases (15-25 Use Cases)
- [ ] Chỉ cho các use cases P0 quan trọng nhất
- [ ] Bổ sung: Luồng thay thế, Luồng ngoại lệ

**Template Bổ Sung**:
```
### Luồng Thay Thế
**Alt 1: [Tình huống]**
- Tại bước [X]: Nếu [điều kiện]
- Thì: [Hành động thay thế]
- Quay lại: Bước [Y]

### Luồng Ngoại Lệ
**Exc 1: [Lỗi]**
- Tại bước [X]: Nếu [lỗi xảy ra]
- Hệ thống: [Xử lý lỗi]
- Kết thúc / Quay lại: [Bước nào]
```

#### 4. Use Case Diagrams
- [ ] Overall system diagram (tất cả actors và modules)
- [ ] Module-specific diagrams (chi tiết từng module)

**Công cụ**: Mermaid, PlantUML, hoặc draw.io

### Sản Phẩm Đầu Ra
- [x] 6 High-Level UCs
- [x] 40-60 Medium-Level UCs
- [x] 15-25 Detailed-Level UCs
- [x] 3-7 Use Case Diagrams
- [x] Traceability: UC ↔ User Story ↔ FR

---

## 🎯 BƯỚC 06: Biểu Đồ Thiết Kế (Design Diagrams)

### Mục Đích
Mô hình hóa hệ thống qua các góc nhìn khác nhau (dữ liệu, luồng, hoạt động, tuần tự).

### Thư Mục
```
docs/06_Diagrams/
├── README.md
├── Context/
│   └── system_context.md
├── UseCase/
│   └── [module]_usecase.md
├── Sequence/
│   ├── README.md
│   └── seq_[feature].md (10-20 diagrams)
├── Activity/
│   ├── README.md
│   └── act_[process].md (5-10 diagrams)
├── DataFlow/
│   ├── README.md
│   └── dfd_level[X].md
└── ER_Diagrams/
    ├── README.md
    ├── erd_conceptual.md
    ├── erd_logical.md
    └── erd_physical.md
```

### Các Công Việc

#### 1. Context Diagram
- [ ] System context (đã có ở Bước 02)

#### 2. Use Case Diagrams
- [ ] Overall + per-module diagrams (đã có ở Bước 05)

#### 3. Sequence Diagrams (10-20 diagrams)
- [ ] Chọn các luồng quan trọng từ Detailed Use Cases
- [ ] Mô tả interaction giữa actors, UI, controllers, services, database
- [ ] Mỗi diagram: ~5-15 bước

**Danh sách gợi ý**:
- Login flow
- Create entity
- Update entity
- Approval workflow (multi-level)
- Search & filter
- Report generation

#### 4. Activity Diagrams (5-10 diagrams)
- [ ] Cho các quy trình phức tạp (workflows, decision trees)
- [ ] Hiển thị: Start → Activities → Decision Points → End

**Danh sách gợi ý**:
- Approval workflow
- Data validation process
- Import/Export flow

#### 5. Data Flow Diagrams (DFD)
- [ ] Level 0: Context DFD
- [ ] Level 1: Major processes (6 modules)
- [ ] Level 2: Detailed processes (cho 2-3 modules phức tạp)

#### 6. Entity-Relationship Diagrams (ERD)
- [ ] **Conceptual ERD**: Entities và relationships (high-level)
- [ ] **Logical ERD**: Attributes, primary keys, foreign keys
- [ ] **Physical ERD** (optional): SQL-specific (data types, indexes)

**Số lượng entities gợi ý**: 8-15 entities chính

**Quy tắc**:
- Mỗi entity có: Tên, Attributes, Primary Key
- Relationships: 1-1, 1-N, M-N (với cardinality rõ ràng)

### Sản Phẩm Đầu Ra
- [x] 2-3 Context Diagrams
- [x] 5-7 Use Case Diagrams
- [x] 10-20 Sequence Diagrams
- [x] 5-10 Activity Diagrams
- [x] 3-5 Data Flow Diagrams
- [x] 1-3 ERD Diagrams

---

## 🎯 BƯỚC 07: Review & Approval

### Mục Đích
Đảm bảo chất lượng và sự đồng thuận từ stakeholders.

### Thư Mục
```
docs/08_Review_Approval/
├── README.md
├── review_checklist.md
├── stakeholder_feedback.md
└── approval_log.md
```

### Các Công Việc

#### 1. Internal Review (Tự kiểm tra)
- [ ] Xem lại tất cả tài liệu theo checklist
- [ ] Kiểm tra tính nhất quán giữa các bước
- [ ] Traceability matrix đầy đủ
- [ ] Spelling, grammar, formatting

**Checklist**:
```
- [ ] Mọi FR đều có User Story tương ứng
- [ ] Mọi User Story đều có Use Case tương ứng
- [ ] Mọi Use Case P0 đều có Sequence Diagram
- [ ] ERD bao phủ tất cả entities được nhắc đến trong FRs
- [ ] Không có mâu thuẫn giữa các tài liệu
- [ ] Tất cả IDs (FR-XXX, US-XXX, UC-XXX) đều unique
```

#### 2. Peer Review (Nếu làm nhóm)
- [ ] Assign reviewers cho từng phần
- [ ] Feedback format: File → Section → Comment → Suggestion
- [ ] Address feedback và update docs

#### 3. Stakeholder Review (Phê duyệt)
- [ ] Chuẩn bị presentation (30-45 phút)
- [ ] Highlight: Problem, Solution, Scope, Modules, MVP
- [ ] Collect feedback
- [ ] Update docs theo feedback

#### 4. Final Approval
- [ ] Sign-off từ stakeholders
- [ ] Version control: Tag release (v1.0)

### Sản Phẩm Đầu Ra
- [x] Review checklist (completed)
- [x] Feedback document
- [x] Approval log (ai approve khi nào)

---

## 🎯 BƯỚC 08: Tài Liệu Cuối Cùng (Final Documents)

### Mục Đích
Tổng hợp và xuất bản tài liệu hoàn chỉnh.

### Thư Mục
```
docs/09_Final_Documents/
├── README.md
├── executive_summary.md (2-3 trang)
├── complete_specification.pdf (compile tất cả)
└── presentation_slides.pdf
```

### Các Công Việc

#### 1. Executive Summary
- [ ] 2-3 trang tóm tắt toàn bộ dự án
- [ ] Bao gồm:
  - Problem statement
  - Proposed solution
  - Key features (6 modules)
  - Success metrics
  - Timeline & Budget

#### 2. Complete Specification Document
- [ ] Compile tất cả tài liệu từ Bước 00-06
- [ ] Table of contents với page numbers
- [ ] Appendices (glossary, references)
- [ ] Export PDF

**Cấu trúc**:
```
1. Executive Summary
2. Problem Context (Bước 00)
3. System Specification (Bước 01)
4. System Clarification (Bước 02)
5. Requirements (Bước 03)
6. User Stories (Bước 04)
7. Use Cases (Bước 05)
8. Design Diagrams (Bước 06)
9. Appendices
```

#### 3. Presentation Slides
- [ ] 20-30 slides
- [ ] Cover major points from each step
- [ ] Heavy on visuals (diagrams, tables)

### Sản Phẩm Đầu Ra
- [x] Executive Summary (2-3 pages)
- [x] Complete Specification PDF (80-150 pages)
- [x] Presentation Slides (20-30 slides)

**Thời gian**: 2-3 ngày

---

## 📊 Bản Đồ Truy Xuất Toàn Bộ (End-to-End Traceability)

```
User Needs (Bước 02)
   ↓
Functional Requirements (Bước 03)
   ↓
User Stories (Bước 04)
   ↓
Use Cases (Bước 05)
   ↓
Design Diagrams (Bước 06)
   ↓
Implementation (Ngoài SOP này)
```

**Ví dụ Traceability**:
```
Need: "Giảng viên cần quản lý bài báo dễ dàng"
  → FR-PUB-001: Tạo bài báo mới
    → US-RES-001: Giảng viên muốn tạo bài báo
      → UC-M1-001: Create Publication
        → Sequence Diagram: seq_create_publication
          → ERD: Publication entity
            → Code: PublicationController.create()
```

---

## ✅ Checklist Tổng Thể

### Sau khi hoàn thành SOP:

**Bước 00: Bối Cảnh**
- [ ] Toàn cảnh và phạm vi đã rõ ràng
- [ ] Stakeholders đã được xác định

**Bước 01: Đặc Tả**
- [ ] 5 tài liệu cốt lõi đã hoàn thiện
- [ ] Technology stack được chọn và biện minh

**Bước 02: Làm Rõ**
- [ ] As-Is và To-Be process đã mô tả
- [ ] User personas đã tạo

**Bước 03: Yêu Cầu**
- [ ] 60-80 FRs đã liệt kê với acceptance criteria
- [ ] 20-30 NFRs đã định nghĩa với metrics

**Bước 04: User Stories**
- [ ] 60-80 stories đã viết
- [ ] Phân loại theo role và priority

**Bước 05: Use Cases**
- [ ] 6 High-level, 40-60 Medium-level UCs
- [ ] 15-25 Detailed UCs cho P0

**Bước 06: Biểu Đồ**
- [ ] Sequence, Activity, DFD, ERD đã vẽ
- [ ] Minimum 30-50 diagrams tổng cộng

**Bước 07: Review**
- [ ] Internal review hoàn tất
- [ ] Stakeholder approval đã có

**Bước 08: Tổng Hợp**
- [ ] Executive summary hoàn thiện
- [ ] Complete PDF compiled
- [ ] Presentation slides sẵn sàng

---

## 🛠️ Công Cụ Khuyên Dùng

### Soạn Thảo Văn Bản
- **Markdown Editors**: VS Code, Typora, Obsidian
- **Documentation**: MkDocs, Docusaurus

### Vẽ Biểu Đồ
- **Text-based**: Mermaid, PlantUML (recommend for version control)
- **GUI**: draw.io, Lucidchart, Excalidraw
- **ERD**: dbdiagram.io, ERD Plus

### Quản Lý Dự Án
- **Traceability**: Excel, Google Sheets, Jira
- **Version Control**: Git + GitHub/GitLab

### Export PDF
- **Markdown to PDF**: Pandoc, MkDocs PDF Export
- **Presentation**: Marp, reveal.js

---

## 📝 Mẫu README Cho Mỗi Bước

```markdown
# [Tên Folder] - README

> 📁 **Folder**: `0X_[TenFolder]`  
> 📅 **Cập nhật**: [Ngày]  
> 🎯 **Mục đích**: [Mô tả ngắn gọn]

---

## 📁 Cấu Trúc Folder

[Liệt kê cây thư mục]

---

## 🎯 Tổng Quan

[Giải thích mục đích folder này]

---

## 📊 Tổng Số [Artifacts]

[Bảng thống kê]

---

## 📖 Hướng Dẫn Đọc

### Dành cho [Nhóm 1]
- File 1
- File 2

### Dành cho [Nhóm 2]
- File 3
- File 4

---

## 🔗 Mối Quan Hệ

[Biểu đồ Mermaid hoặc mô tả]

---

## ✅ Checklist Hoàn Thiện

- [ ] Item 1
- [ ] Item 2

---

## 🚀 Bước Tiếp Theo

[Link đến folder tiếp theo]

---

*Hoàn thành: [Ngày]*
```

---

## 🎓 Lưu Ý Quan Trọng

### 1. Tính Nhất Quán (Consistency)
- Sử dụng cùng một convention đặt tên (ID, files)
- Cùng template cho cùng loại tài liệu
- Cross-reference giữa các docs (FR-XXX, US-XXX, UC-XXX)

### 2. Tính Truy Xuất (Traceability)
- Mọi artifact phải link được đến source
- Duy trì traceability matrix
- Update matrix khi có thay đổi

### 3. Tính Lặp Lại (Iterative)
- Không cần hoàn hảo từ lần đầu
- Review và cập nhật liên tục
- Version control mọi thứ

### 4. Collaboration
- Sử dụng Git cho version control
- Clear commit messages
- Code review cho documentation

### 5. Audience Awareness
- Viết cho đúng audience (technical vs non-technical)
- Sử dụng visuals cho stakeholders
- Chi tiết kỹ thuật cho developers

---

## 📚 Tài Liệu Tham Khảo

### Standards & Best Practices
- IEEE 830: Software Requirements Specification
- ISO/IEC 25010: Systems and software Quality Requirements
- SWEBOK: Software Engineering Body of Knowledge
- UML 2.5 Specification

### Templates & Examples
- [Tham khảo đồ án UFPMS](../docs/)
- Volere Requirements Template
- Agile Alliance User Story Template

---

## 📞 Hỗ Trợ & Câu Hỏi

Nếu có câu hỏi hoặc cần làm rõ quy trình, vui lòng:
- Review lại tài liệu ví dụ trong `../docs/`
- Check issue tracker (nếu dùng GitHub)
- Liên hệ người tạo SOP

---

**Phiên bản**: 1.0  
**Ngày tạo**: 12/02/2026  
**Tác giả**: [Dựa trên phương pháp đồ án UFPMS]  
**Cập nhật lần cuối**: 12/02/2026

---

**Chúc bạn thành công với dự án của mình! 🚀**
