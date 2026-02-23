# BA Deliverable 2: Business Rules Document (BRD)

> 📋 **Phiên bản**: V1.0  
> 👤 **Vai trò**: Business Analyst  
> 📅 **Ngày tạo**: 20/02/2026  
> 🎯 **Phạm vi**: Core Publication Management - V1.0

---

## Tổng Quan

Tài liệu này tổng hợp **tất cả business rules** áp dụng cho V1.0 của UFPMS. Đây là nguồn tham chiếu duy nhất (Single Source of Truth) cho Dev và QA về logic nghiệp vụ.

---

## Module 1: Publication Rules

### 1.1 Validation Rules (Kiểm tra đầu vào)

| Rule ID | Field | Mô tả | Error Message (VI) |
|---|---|---|---|
| BR-001 | Title | Bắt buộc, tối đa 500 ký tự | "Tiêu đề là bắt buộc" / "Tiêu đề không được vượt quá 500 ký tự" |
| BR-002 | Year | Bắt buộc, số nguyên trong khoảng [1900, năm hiện tại] | "Năm là bắt buộc" / "Năm phải từ 1900 đến [năm hiện tại]" |
| BR-003 | Publication Type | Bắt buộc, chỉ nhận: JOURNAL \| CONFERENCE \| BOOK_CHAPTER \| OTHER | "Vui lòng chọn loại bài báo" |
| BR-004 | DOI | Tùy chọn. Nếu nhập phải đúng format `10.XXXX/...` (regex: `^10\.\d{4,}/.*$`) | "Định dạng DOI không hợp lệ (ví dụ: 10.1000/xyz123)" |
| BR-005 | Abstract | Tùy chọn, không giới hạn ký tự (textarea) | - |
| BR-006 | Keywords | Tùy chọn, ngăn cách bằng dấu phẩy | - |
| BR-007 | Journal/Conference Name | Tùy chọn với TYPE=JOURNAL/CONFERENCE (recommended); bắt buộc = false cho V1.0 | - |

### 1.2 Status Rules (Quy tắc trạng thái)

| Rule ID | Mô tả |
|---|---|
| BR-008 | Status mặc định khi tạo mới = `DRAFT` |
| BR-009 | Chỉ `DRAFT` và `REVISION_REQUIRED` có thể Edit (update metadata) |
| BR-010 | Chỉ `DRAFT` có thể Delete |
| BR-011 | Status không thể thay đổi trực tiếp qua form thông thường; chỉ thay đổi qua các actions: Submit, Approve, Reject, Publish |
| BR-012 | Status transitions hợp lệ: `DRAFT` → `SUBMITTED` → `APPROVED` → `PUBLISHED`; `SUBMITTED` → `REVISION_REQUIRED` → `SUBMITTED` |

**Status Transition Diagram:**
```
DRAFT ──[Submit]──→ SUBMITTED ──[Approve]──→ APPROVED ──[Publish]──→ PUBLISHED
  ↑                     │
  │              [Request Revision]
  │                     ↓
  └──────────── REVISION_REQUIRED
```

### 1.3 Authorization Rules (Quy tắc phân quyền)

| Rule ID | Action | Quyền |
|---|---|---|
| BR-013 | Xem publication | Owner + Co-authors + Admin + Reviewer (khi assigned) |
| BR-014 | Edit publication | Owner only + Status ∈ {DRAFT, REVISION_REQUIRED} |
| BR-015 | Delete publication | Owner only + Status = DRAFT |
| BR-016 | Upload PDF | Owner only |
| BR-017 | Download PDF (private) | Owner + Co-authors + Admin + Reviewer |
| BR-018 | Download PDF (PUBLISHED) | Tất cả user đã đăng nhập |

---

## Module 2: File Upload Rules

| Rule ID | Mô tả |
|---|---|
| BR-019 | Chỉ chấp nhận file PDF: extension `.pdf` VÀ MIME type `application/pdf` |
| BR-020 | Kích thước file tối đa: **20MB** |
| BR-021 | Filename trên server được rename bằng UUID để tránh trùng lặp |
| BR-022 | Upload mới sẽ **replace** file cũ (xóa file vật lý cũ + cập nhật path trong DB) |
| BR-023 | Nếu PDF file bị xóa > 10MB trên storage, inline viewer không hoạt động → hiển thị download link thay thế |

---

## Module 3: Co-Author Rules

| Rule ID | Mô tả |
|---|---|
| BR-024 | Co-authors được lưu kèm `sequence` (thứ tự tác giả: 1, 2, 3, ...) |
| BR-025 | Creator của publication tự động là **Author #1** (sequence=1), không thể remove |
| BR-026 | Internal co-author: search trong Users table theo `name` hoặc `email` |
| BR-027 | External co-author: nhập thủ công `name` (bắt buộc) + `email` (tùy chọn); không có user account link |
| BR-028 | Mỗi publication có **tối đa 1** Corresponding Author (flag `is_corresponding`) |
| BR-029 | Nếu không chỉ định Corresponding Author → mặc định là creator |
| BR-030 | Không giới hạn số co-authors trong V1.0 |

---

## Module 4: Dashboard & Work Hours Rules

| Rule ID | Mô tả | Chi Tiết |
|---|---|---|
| BR-031 | Giờ quy đổi theo loại bài báo | JOURNAL = **40h**, CONFERENCE = **20h**, BOOK_CHAPTER = **60h**, OTHER = **10h** |
| BR-032 | Chỉ tính publications với status = `PUBLISHED` | DRAFT/SUBMITTED không được tính |
| BR-033 | Filter theo năm = năm của `approved_date` (ngày được approve) | Không dùng `created_at` hay `year` của publication |
| BR-034 | Default filter khi vào dashboard = **Năm hiện tại** | |
| BR-035 | Export Excel bao gồm tất cả publications theo filter đang áp dụng | Columns: Title, Type, Work Hours, Approval Date |

---

## Module 5: Audit Log Rules

| Rule ID | Action cần ghi log | Data cần capture |
|---|---|---|
| BR-036 | Tạo publication | user_id, publication_id, action=CREATE, timestamp |
| BR-037 | Sửa publication | user_id, publication_id, action=UPDATE, changed_fields, timestamp |
| BR-038 | Xóa publication | user_id, publication_id, action=DELETE, timestamp |
| BR-039 | Upload PDF | user_id, publication_id, action=UPLOAD_PDF, filename, timestamp |
| BR-040 | Download PDF | user_id, publication_id, action=DOWNLOAD_PDF, timestamp |
| BR-041 | Submit publication | user_id, publication_id, action=SUBMIT, timestamp |

---

## Module 6: General Validation Rules

| Rule ID | Mô tả |
|---|---|
| BR-042 | Tất cả text input phải được sanitize (HTML escape) trước khi lưu vào DB để tránh XSS |
| BR-043 | Year phải là số nguyên (integer), không chấp nhận số thập phân |
| BR-044 | Email format (nếu nhập): phải đúng standard email regex |
| BR-045 | Mọi API request phải qua Authentication middleware → 401 nếu không có token hợp lệ |
| BR-046 | Mọi thao tác với publication phải qua Authorization check → 403 nếu không có quyền |

---

## Tóm Tắt Nhanh (Quick Reference)

```
┌─────────────────────────────────────────────────────────────┐
│                 UFPMS V1.0 Business Rules                   │
├─────────────────┬───────────────────────────────────────────┤
│ PUBLICATION     │ Title ≤500c | Year [1900,now] | 4 Types   │
│                 │ Default Status = DRAFT                      │
├─────────────────┼───────────────────────────────────────────┤
│ CAN EDIT        │ DRAFT, REVISION_REQUIRED (owner only)      │
│ CAN DELETE      │ DRAFT only (owner only)                    │
├─────────────────┼───────────────────────────────────────────┤
│ FILE UPLOAD     │ PDF only | Max 20MB | UUID rename           │
├─────────────────┼───────────────────────────────────────────┤
│ CO-AUTHORS      │ No limit | Creator = Author #1 (cant remove)│
│                 │ 1 Corresponding Author max                  │
├─────────────────┼───────────────────────────────────────────┤
│ WORK HOURS      │ JOURNAL=40h | CONFERENCE=20h               │
│                 │ BOOK_CHAPTER=60h | OTHER=10h               │
│                 │ Only PUBLISHED publications count          │
└─────────────────┴───────────────────────────────────────────┘
```

---

**Prepared by**: Business Analysis Team  
**Version**: 1.0  
**Date**: 20/02/2026  
**Status**: Draft - Chờ review từ Dev Lead và Stakeholder
