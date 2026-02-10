# Module 1: Publication Management - Yêu Cầu Chức Năng

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Module**: Quản lý Bài báo Khoa học  
> 👥 **Users**: Researcher, SuperAdmin

---

## 1. Tổng Quan Module

**Mục đích**: Quản lý bài báo khoa học (CRUD + metadata)

**Scope**:
- ✅ CRUD bài báo
- ✅ Upload file PDF
- ✅ Quản lý metadata
- ✅ Liên kết đồng tác giả
- ❌ KHÔNG bao gồm: Quy trình phê duyệt (Module 2)

---

## 2. Functional Requirements

### FR-PUB-001: Tạo Bài Báo Mới
**Priority**: 🔴 P0 - Must Have

**Description**:  
Giảng viên có thể tạo bài báo mới với các thông tin bắt buộc và tùy chọn.

**User Story**: US-RES-001

**Acceptance Criteria**:
```
GIVEN giảng viên đã đăng nhập
WHEN nhấn "Thêm bài báo mới"
THEN hiển thị form với các trường:
  - Bắt buộc: Tiêu đề, Tác giả, Năm xuất bản, Loại tạp chí
  - Tùy chọn: DOI, ISSN, Abstract, Keywords, File PDF
```

**Business Rules**:
- Trạng thái mặc định: DRAFT
- Chỉ tác giả chính (owner) mới có quyền sửa/xóa

**Technical Notes**:
- Form validation real-time
- Auto-save every 30s (nháp)

---

### FR-PUB-002: Upload File PDF
**Priority**: 🔴 P0 - Must Have

**Description**:  
Giảng viên có thể upload file PDF bài báo full-text.

**Acceptance Criteria**:
```
GIVEN đang tạo/sửa bài báo
WHEN chọn file PDF (< 10MB)
THEN
  - Upload file lên server
  - Lưu path vào database
  - Hiển thị preview thumbnail
  - Cho phép download lại
```

**Validation Rules**:
- File type: PDF only (`.pdf`)
- File size: Max 10MB
- File name: Sanitize để tránh SQL injection

---

### FR-PUB-003: Auto-Fetch Metadata từ DOI
**Priority**: 🟢 P2 - Nice to Have (Phase 2)

**Description**:  
Khi nhập DOI, tự động lấy metadata từ DOI Resolver.

**Acceptance Criteria**:
```
GIVEN giảng viên nhập DOI hợp lệ (10.xxxx/xxxxx)
WHEN nhấn "Lấy thông tin từ DOI"
THEN
  - Gọi CrossRef API
  - Auto-fill: Title, Authors, Journal, Year, ISSN
  - Cho phép chỉnh sửa thủ công
```

**Dependencies**:
- CrossRef API hoặc DOI.org API

---

### FR-PUB-004: Sửa Bài Báo
**Priority**: 🔴 P0 - Must Have

**Description**:  
Giảng viên có thể sửa bài báo của mình.

**Acceptance Criteria**:
```
GIVEN bài báo ở trạng thái DRAFT hoặc REVISION_REQUIRED
AND user là owner
WHEN sửa thông tin và Save
THEN
  - Cập nhật database
  - Lưu audit log (ai sửa, khi nào)
  - Hiển thị thông báo "Đã lưu"
```

**Business Rules**:
- CHỈ sửa được khi: DRAFT hoặc REVISION_REQUIRED
- KHÔNG sửa được khi: SUBMITTED, REVIEWING, PUBLISHED

---

### FR-PUB-005: Xóa Bài Báo
**Priority**: 🔴 P0 - Must Have

**Description**:  
Giảng viên có thể xóa bài báo nháp của mình.

**Acceptance Criteria**:
```
GIVEN bài báo ở trạng thái DRAFT
AND user là owner
WHEN nhấn "Xóa" và confirm
THEN
  - Soft delete (set deleted_at timestamp)
  - Xóa file PDF khỏi storage
  - Redirect về danh sách
```

**Business Rules**:
- CHỈ xóa được khi: DRAFT
- KHÔNG xóa được: Đã nộp hoặc đã duyệt

---

### FR-PUB-006: Xem Danh Sách Bài Báo Của Mình
**Priority**: 🔴 P0 - Must Have

**Description**:  
Giảng viên xem danh sách bài báo của mình, phân loại theo trạng thái.

**Acceptance Criteria**:
```
GIVEN giảng viên đã đăng nhập
WHEN vào "My Publications"
THEN hiển thị danh sách với:
  - Filter: All / Draft / Submitted / Approved / Rejected
  - Sort: Newest first
  - Thông tin: Title, Status, Updated date, Actions
```

---

### FR-PUB-007: Thêm Đồng Tác Giả (Co-authors)
**Priority**: 🟡 P1 - Should Have

**Description**:  
Liên kết bài báo với đồng tác giả (giảng viên khác trong trường).

**Acceptance Criteria**:
```
GIVEN đang tạo/sửa bài báo
WHEN nhập tên giảng viên
THEN
  - Autocomplete từ danh sách GV trong hệ thống
  - Thêm vào danh sách co-authors
  - Có thể xóa khỏi danh sách
```

**Business Rules**:
- Tác giả chính (owner) không thể bị xóa
- Đồng tác giả không có quyền sửa/xóa bài báo

---

### FR-PUB-008: Gắn Tags/Keywords
**Priority**: 🟡 P1 - Should Have

**Description**:  
Gắn từ khóa cho bài báo để hỗ trợ tìm kiếm và phân loại.

**Acceptance Criteria**:
```
GIVEN đang tạo/sửa bài báo
WHEN nhập keywords (phân tách bằng dấu phẩy)
THEN
  - Lưu dưới dạng array
  - Hiển thị dạng tags
  - Cho phép xóa từng tag
```

---

### FR-PUB-009: Phân Loại Theo Quartile (Q1/Q2/Q3/Q4)
**Priority**: 🟡 P1 - Should Have

**Description**:  
Tự động phân loại tạp chí theo Quartile (Scopus).

**Acceptance Criteria**:
```
GIVEN nhập ISSN của tạp chí
WHEN lưu bài báo
THEN
  - Tra cứu Scopus ranking (nếu có API)
  - Gắn nhãn Q1/Q2/Q3/Q4
  - Hiển thị badge
```

**Dependencies**:
- Scopus API (hoặc danh sách cứng từ Excel)

---

### FR-PUB-010: Xem Chi Tiết Bài Báo
**Priority**: 🔴 P0 - Must Have

**Description**:  
Xem đầy đủ thông tin bài báo.

**Acceptance Criteria**:
```
GIVEN có quyền xem bài báo (owner hoặc admin hoặc reviewer)
WHEN nhấn "View Details"
THEN hiển thị:
  - Tất cả metadata
  - Trạng thái hiện tại
  - Lịch sử xét duyệt (nếu có)
  - File PDF (nếu đã upload)
  - Link DOI (nếu có)
```

---

### FR-PUB-011: Download File PDF
**Priority**: 🔴 P0 - Must Have

**Description**:  
Download file PDF đã upload.

**Acceptance Criteria**:
```
GIVEN bài báo có file PDF
AND user có quyền xem (owner / admin / reviewer / hoặc PUBLISHED)
WHEN nhấn "Download PDF"
THEN
  - Tải file về máy
  - Log audit trail (ai tải, khi nào)
```

**Security**:
- CHỈ cho tải nếu có quyền
- PDF không public link (cần authentication)

---

### FR-PUB-012: Validate DOI Format
**Priority**: 🟡 P1 - Should Have

**Description**:  
Kiểm tra format DOI hợp lệ.

**Business Rule**:
```
DOI format: 10.xxxx/xxxxx
Regex: ^10\.\d{4,9}/[-._;()/:A-Z0-9]+$
```

**Acceptance Criteria**:
```
GIVEN giảng viên nhập DOI
WHEN blur khỏi field
THEN
  - Validate format
  - Hiển thị lỗi nếu sai
  - Link đến https://doi.org/[DOI] nếu đúng
```

---

### FR-PUB-013: Validate ISSN Format
**Priority**: 🟡 P1 - Should Have

**Description**:  
Kiểm tra format ISSN hợp lệ.

**Business Rule**:
```
ISSN format: xxxx-xxxx
Regex: ^\d{4}-\d{3}[0-9X]$
```

---

### FR-PUB-014: Duplicate Detection (Co-authors)
**Priority**: 🟡 P1 - Should Have

**Description**:  
Cảnh báo khi có nhiều giảng viên khai báo cùng 1 bài.

**Acceptance Criteria**:
```
GIVEN bài báo có DOI
WHEN lưu bài báo
THEN
  - Kiểm tra DOI đã tồn tại chưa
  - Nếu có: Hiển thị cảnh báo "Bài này đã được [Tên GV] khai báo"
  - Gợi ý: "Thêm làm đồng tác giả?"
```

---

### FR-PUB-015: Import từ ORCID
**Priority**: 🟢 P2 - Nice to Have (Phase 2)

**Description**:  
Import danh sách bài báo từ ORCID tự động.

**Acceptance Criteria**:
```
GIVEN giảng viên có ORCID
WHEN nhấn "Import from ORCID"
THEN
  - Gọi ORCID API
  - Hiển thị danh sách bài báo
  - Cho phép chọn bài nào muốn thêm
  - Auto-fill metadata
```

---

## 3. Data Model (Publication Entity)

```typescript
interface Publication {
  // Primary Key
  id: UUID;
  
  // Metadata
  title: string; // Bắt buộc
  abstract?: string; // Tùy chọn
  authors: Author[]; // Bắt buộc, ít nhất 1
  correspondingAuthor: User; // Owner
  
  // Journal Info
  journalName: string; // Bắt buộc
  journalISSN?: string;
  journalQuartile?: 'Q1' | 'Q2' | 'Q3' | 'Q4';
  impactFactor?: number;
  
  // Publication Info
  publicationYear: number; // Bắt buộc
  publicationDate?: Date;
  volume?: string;
  issue?: string;
  pages?: string;
  doi?: string;
  url?: string;
  
  // Classification
  publicationType: 'journal' | 'conference';
  keywords?: string[];
  researchField?: string;
  
  // File
  pdfPath?: string;
  pdfSize?: number;
  
  // State
  status: PublicationStatus;
  
  // Audit
  createdAt: Date;
  updatedAt: Date;
  createdBy: UUID;
  updatedBy: UUID;
  deletedAt?: Date; // Soft delete
}

enum PublicationStatus {
  DRAFT,
  SUBMITTED,
  FACULTY_REVIEWING,
  REVISION_REQUIRED,
  FACULTY_APPROVED,
  FACULTY_REJECTED,
  UNIVERSITY_REVIEWING,
  PUBLISHED,
  UNIVERSITY_REJECTED
}
```

---

## 4. API Endpoints (Sample)

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| POST | `/api/publications` | Tạo bài báo mới | Researcher |
| GET | `/api/publications` | Danh sách của mình | Researcher |
| GET | `/api/publications/:id` | Chi tiết bài báo | Owner/Admin/Reviewer |
| PUT | `/api/publications/:id` | Cập nhật bài báo | Owner (if DRAFT) |
| DELETE | `/api/publications/:id` | Xóa bài báo | Owner (if DRAFT) |
| POST | `/api/publications/:id/upload-pdf` | Upload PDF | Owner |
| GET | `/api/publications/:id/download-pdf` | Download PDF | Authorized |

---

## 5. Traceability

| FR ID | User Need | User Story | Test Case |
|-------|-----------|------------|-----------|
| FR-PUB-001 | Nhập bài báo nhanh | US-RES-001 | TC-PUB-001 |
| FR-PUB-002 | Upload PDF | US-RES-002 | TC-PUB-002 |
| FR-PUB-004 | Sửa bài báo | US-RES-003 | TC-PUB-004 |
| FR-PUB-005 | Xóa bài báo | US-RES-004 | TC-PUB-005 |

---

**Tài liệu liên quan**:
- [Module 2: Approval Workflow](./module_approval_workflow.md)
- [User Needs - Researcher](../../02_System_Clarification/User_Analysis/user_needs.md#1-researcher)
- [Business Rules](./business_rules.md)
