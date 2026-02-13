# Bảng Thuật Ngữ - UFPMS (Glossary)

> 📚 **Mục đích**: Định nghĩa rõ ràng các thuật ngữ quan trọng trong hệ thống UFPMS  
> 🎯 **Tránh nhầm lẫn**: Phân biệt giữa Account, Role, và Permission

---

## 1. Phân Biệt: Tài Khoản, Vai Trò, Quyền Hạn

### 🔐 Tài Khoản (Account)

**Định nghĩa**: Username/password dùng để đăng nhập vào hệ thống.

**Đặc điểm**:
- Mỗi tài khoản có username và password riêng
- **ĐẶC BIỆT**: Trong hệ thống UFPMS, có 2 loại tài khoản phê duyệt DÙNG CHUNG theo đơn vị

**Các loại tài khoản**:

| Loại | Ví dụ Username | Người dùng | Mô tả |
|------|----------------|-----------|-------|
| **Tài khoản cá nhân** | `nguyen.van.a` | 1 người | Giảng viên, Admin |
| **Tài khoản Phê duyệt Khoa** | `faculty_khoa_cntt`<br>`faculty_khoa_kinh_te` | Nhiều người (Trưởng khoa, Phó khoa) | **Dùng chung** cho cả Khoa |
| **Tài khoản Phê duyệt Trường** | `university_reviewer` | Nhiều người (CB Phòng QLKH) | **Dùng chung** cho toàn Trường |

---

### 👤 Vai Trò (Role)

**Định nghĩa**: Nhóm quyền hạn được gán cho tài khoản, quyết định tài khoản có thể làm gì trong hệ thống.

**5 vai trò chính trong UFPMS**:

| Vai trò | Mô tả | Được gán cho |
|---------|-------|--------------|
| **Researcher** | Giảng viên tạo và quản lý bài báo | Tài khoản cá nhân giảng viên |
| **Faculty Reviewer** | Người xét duyệt cấp Khoa | **Tài khoản Phê duyệt Khoa** (dùng chung) |
| **University Reviewer** | Người phê duyệt cấp Trường | **Tài khoản Phê duyệt Trường** (dùng chung) |
| **SuperAdmin** | Quản trị viên hệ thống | Tài khoản admin cá nhân |
| **Public Visitor** | Khách truy cập công khai | Không cần đăng nhập |

---

### 🔑 Quyền Hạn (Permission)

**Định nghĩa**: Hành động cụ thể mà 1 vai trò được phép thực hiện.

**Ví dụ quyền hạn**:
- `publication.create` - Tạo bài báo mới
- `publication.submit` - Nộp xét duyệt
- `approval.faculty_review` - Xét duyệt cấp Khoa
- `approval.university_review` - Phê duyệt cấp Trường
- `user.manage` - Quản lý người dùng

---

## 2. Mối Quan Hệ: Account → Role → Permission

```
📌 Tài khoản (Account)
    ↓
👤 Vai trò (Role)
    ↓
🔑 Quyền hạn (Permissions)
```

### Ví Dụ Cụ Thể:

#### Ví dụ 1: Giảng viên Nguyễn Văn A
```
Tài khoản:  nguyen.van.a
    ↓
Vai trò:    Researcher
    ↓
Quyền hạn:  - publication.create
            - publication.edit (chỉ bài của mình)
            - publication.submit
            - publication.view_own_status
```

#### Ví dụ 2: Tài khoản Phê duyệt Khoa CNTT
```
Tài khoản:  faculty_khoa_cntt  (DÙNG CHUNG)
    ↓
Vai trò:    Faculty Reviewer
    ↓
Quyền hạn:  - approval.faculty_review
            - approval.faculty_approve
            - approval.faculty_reject
            - approval.request_revision
            - reporting.view_faculty_level
```

**Lưu ý**: 
- **Trưởng khoa hiện tại** đăng nhập bằng `faculty_khoa_cntt`
- Khi **thay đổi Trưởng khoa** → Người mới đăng nhập vào **CÙNG tài khoản** này (chỉ đổi mật khẩu)

#### Ví dụ 3: Tài khoản Phê duyệt Trường
```
Tài khoản:  university_reviewer  (DÙNG CHUNG)
    ↓
Vai trò:    University Reviewer
    ↓
Quyền hạn:  - approval.university_review
            - approval.university_approve
            - approval.university_reject
            - approval.assign_work_hours
            - reporting.view_university_level
```

---

## 3. Cơ Chế Account-Based Approval (Phê Duyệt Theo Tài Khoản)

### ⚙️ Cách Hoạt Động

**Truyền thống** (role-based per person):
```
❌ Trưởng khoa A → Có role "Faculty Reviewer"
❌ Khi thay người → Admin phải:
   1. Gỡ role của người cũ
   2. Gán role cho người mới
   → Phức tạp, dễ quên
```

**UFPMS** (account-based per unit):
```
✅ Tài khoản "faculty_khoa_cntt" → Có role "Faculty Reviewer"
✅ Khi thay người:
   1. Người cũ chuyển giao username/password
   2. Người mới đổi mật khẩu mới
   → Đơn giản, không cần Admin
```

### 🔄 Quy Trình Chuyển Giao

**Khi thay đổi Trưởng khoa:**

1. **Trưởng khoa cũ**: 
   - Chuyển giao thông tin đăng nhập cho Trưởng khoa mới
   - Hoặc liên hệ Admin để reset mật khẩu

2. **Trưởng khoa mới**:
   - Đăng nhập vào tài khoản `faculty_khoa_cntt`
   - Đổi mật khẩu mới
   - Tiếp tục sử dụng (không cần Admin can thiệp)

3. **Hệ thống**:
   - Ghi log: "User X đã đăng nhập vào tài khoản faculty_khoa_cntt lúc [timestamp]"
   - Audit trail đầy đủ: Ai đã duyệt bài nào, khi nào

---

## 4. Thuật Ngữ Nghiệp Vụ (Business Terms)

### 📄 Publication (Bài báo)

| Thuật ngữ | Định nghĩa |
|-----------|-----------|
| **Publication** | Bài báo khoa học đã xuất bản |
| **Journal Article** | Bài báo trên tạp chí |
| **DOI** | Digital Object Identifier - Mã định danh số |
| **ISSN** | International Standard Serial Number - Mã tạp chí |
| **ORCID** | Open Researcher and Contributor ID - Mã nhà nghiên cứu |
| **Impact Factor** | Chỉ số ảnh hưởng của tạp chí |
| **Q1/Q2/Q3/Q4** | Quartile ranking theo Scopus |

### 🔄 Workflow (Quy trình)

| Thuật ngữ | Định nghĩa |
|-----------|-----------|
| **Approval Workflow** | Quy trình phê duyệt 2 cấp (Khoa → Trường) |
| **State Machine** | Máy trạng thái (9 trạng thái) |
| **Audit Trail** | Nhật ký kiểm toán (ghi lại mọi thay đổi) |
| **SLA** | Service Level Agreement - Thời gian xử lý mục tiêu |
| **Revision** | Yêu cầu chỉnh sửa |

### 📊 Reporting (Báo cáo)

| Thuật ngữ | Định nghĩa |
|-----------|-----------|
| **Dashboard** | Bảng điều khiển (giao diện tổng quan) |
| **Work Hours** | Giờ làm/giờ dạy được chuyển đổi từ bài báo |
| **Metrics** | Chỉ số đo lường |
| **KPI** | Key Performance Indicator - Chỉ số hiệu suất chính |

---

## 5. Trạng Thái Công Trình (Publication States)

| Trạng thái | Tiếng Anh | Mô tả | Ai thấy được |
|------------|-----------|-------|--------------|
| **DRAFT** | Nháp | Đang soạn thảo | Chỉ người tạo và Admin |
| **SUBMITTED** | Đã nộp | Chờ Khoa xét duyệt | GV + CB Khoa + Admin |
| **FACULTY_REVIEWING** | Khoa đang xét | Khoa đang xem xét | GV + CB Khoa + Admin |
| **FACULTY_APPROVED** | Khoa đã duyệt | Chờ Trường phê duyệt | GV + CB Khoa + CB Trường + Admin |
| **REVISION_REQUIRED** | Yêu cầu sửa | Cần chỉnh sửa theo yêu cầu | GV + CB Khoa + Admin |
| **FACULTY_REJECTED** | Khoa từ chối | Không được phê duyệt | GV + CB Khoa + Admin |
| **UNIVERSITY_REVIEWING** | Trường đang xét | Trường đang xem xét | GV + CB Khoa + CB Trường + Admin |
| **PUBLISHED** | Đã công bố | Hiển thị công khai | **MỌI NGƯỜI** (Public) |
| **UNIVERSITY_REJECTED** | Trường từ chối | Bị từ chối cấp Trường | GV + CB Khoa + CB Trường + Admin |

---

## 6. Modules (Phân Hệ)

| Module | Tên Tiếng Việt | Mô tả Ngắn |
|--------|----------------|-----------|
| **Module 1** | Quản lý Bài báo | CRUD bài báo, upload PDF |
| **Module 2** | Quy trình Phê duyệt | Workflow 2 cấp, state machine |
| **Module 3** | Tìm kiếm & Duyệt | Tìm kiếm công khai, filter |
| **Module 4** | Hồ sơ Giảng viên | Profile công khai, dashboard cá nhân |
| **Module 5** | Báo cáo & Phân tích | Dashboard, export Excel/PDF |
| **Module 6** | Quản trị | User management, role assignment |

---

## 7. Lưu Ý Quan Trọng ⚠️

### Khi đọc tài liệu:

1. **"Faculty Reviewer"** = **VAI TRÒ** (role)
   - Đây là role trong hệ thống RBAC
   - Quyết định quyền hạn là gì

2. **"Tài khoản Phê duyệt Khoa"** = **TÀI KHOẢN** (account)
   - Đây là username/password cụ thể
   - Một tài khoản được gán 1 role

3. **Một cá nhân CÓ THỂ**:
   - Đăng nhập vào "Tài khoản Phê duyệt Khoa"
   - → Hệ thống nhận diện: "Người này đang dùng role Faculty Reviewer"
   - → Cấp quyền: Xét duyệt cấp Khoa

### Trong code implementation:

```typescript
// ✅ ĐÚNG: Phân biệt rõ
interface User {
  id: UUID;
  username: string;      // Ví dụ: "faculty_khoa_cntt"
  email: string;
  role: Role;            // Ví dụ: Role.FACULTY_REVIEWER
}

enum Role {
  RESEARCHER = 'researcher',
  FACULTY_REVIEWER = 'faculty_reviewer',
  UNIVERSITY_REVIEWER = 'university_reviewer',
  SUPER_ADMIN = 'super_admin',
  PUBLIC_VISITOR = 'public_visitor'
}
```

---

## 8. Tham Khảo

- [System Overview](./system_overview.md#module-6-quy-trình-phê-duyệt-approval-workflow)
- [Stakeholders](./stakeholders.md#22-trưởng-đơn-vị--người-phê-duyệt-unit-leaders--approvers)
- [Requirements - Approval Workflow](../03_Requirements/Functional/module_approval_workflow.md)

---

*Tài liệu này giúp làm rõ terminology và tránh nhầm lẫn khi đọc/viết tài liệu hệ thống UFPMS.*
