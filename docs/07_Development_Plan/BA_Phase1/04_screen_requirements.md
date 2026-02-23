# BA Deliverable 4: Screen Requirements

> 📋 **Phiên bản**: V1.0  
> 👤 **Vai trò**: Business Analyst  
> 📅 **Ngày tạo**: 20/02/2026  
> 🎯 **Phạm vi**: 6 Màn hình chính - Core Publication Management

---

## Tổng Quan - 6 Màn Hình Chính

| Screen ID | Tên Màn Hình | Route | Related Stories |
|---|---|---|---|
| SCR-001 | Đăng Nhập (Login) | /login | - |
| SCR-002 | Dashboard | /dashboard | US-RES-024 |
| SCR-003 | Danh Sách Bài Báo | /publications | US-RES-005 |
| SCR-004 | Tạo Bài Báo | /publications/new | US-RES-001, US-RES-006 |
| SCR-005 | Chỉnh Sửa Bài Báo | /publications/{id}/edit | US-RES-003, US-RES-006 |
| SCR-006 | Chi Tiết Bài Báo | /publications/{id} | US-RES-002, US-RES-008, US-RES-009 |

---

## SCR-001: Màn Hình Đăng Nhập

### Layout
```
┌─────────────────────────────────────────┐
│                                         │
│              [LOGO]                     │
│          UFPMS - Hệ thống               │
│       Quản Lý Bài Báo Khoa Học         │
│                                         │
│   ┌─────────────────────────────────┐   │
│   │  Tên đăng nhập *               │   │
│   │  [_________________________]   │   │
│   │                                │   │
│   │  Mật khẩu *                    │   │
│   │  [_________________________]   │   │
│   │                                │   │
│   │  [      Đăng Nhập      ]       │   │
│   │                                │   │
│   │  ⚠ [Thông báo lỗi nếu có]     │   │
│   └─────────────────────────────────┘   │
│                                         │
└─────────────────────────────────────────┘
```

### UI Elements

| Element | ID | Type | Trạng thái |
|---|---|---|---|
| Logo | - | Image | Static |
| Tiêu đề | title-ufpms | Text | Static |
| Username input | input-username | Text Input | Required |
| Password input | input-password | Password Input | Required, masked |
| Nút Đăng nhập | btn-login | Button | Primary color |
| Error message | alert-login-error | Alert | Ẩn mặc định, hiện khi lỗi |

### Behaviors

| Trigger | Hành vi |
|---|---|
| Form rỗng → Click Login | Nút Login bị disabled (hoặc validate trước khi submit) |
| Nhấn Enter trong field | Submit form |
| Login thành công | Redirect đến /dashboard |
| Login thất bại | Hiện error: "Tên đăng nhập hoặc mật khẩu không đúng" |
| Đã đăng nhập, vào /login | Redirect về /dashboard |

---

## SCR-002: Dashboard

### Layout
```
┌─────────────────────────────────────────────────────────┐
│ [Logo] UFPMS    Bài báo   Dashboard    [Tên user ▼]     │ ← Header/Nav
├─────────────────────────────────────────────────────────┤
│  Chào mừng trở lại, [Tên Người Dùng]!                  │
│                                                          │
│  ┌──────────────┐ ┌──────────────┐ ┌──────────────┐    │
│  │ Tổng bài báo │ │ Đã duyệt    │ │ Nháp         │    │ ← Stats cards
│  │     [N]      │ │     [N]      │ │     [N]      │    │
│  └──────────────┘ └──────────────┘ └──────────────┘    │
│  ┌──────────────┐                                        │
│  │ Giờ làm năm  │                                        │
│  │ hiện tại [N]h│                                        │
│  └──────────────┘                                        │
│                                                          │
│  📄 Bài báo gần đây                                     │
│  ┌─────────────────────────────────────────────────┐   │
│  │ Tiêu đề            │ Trạng thái │ Cập nhật      │   │
│  │ ─────────────────  │ ─────────  │ ─────────     │   │
│  │ [Title 1]          │ [DRAFT]   │ 20/02/2026    │   │
│  │ [Title 2]          │ [SUBMITTED]│ 19/02/2026    │   │
│  │ ...                │ ...        │ ...           │   │
│  └─────────────────────────────────────────────────┘   │
│                                                          │
│                          ⊕ [Tạo bài báo mới]            │ ← FAB button
└─────────────────────────────────────────────────────────┘
```

### UI Elements

| Element | ID | Content |
|---|---|---|
| Total Publications card | card-total | Tổng số publications của user |
| Published/Approved card | card-published | Số publications đã được PUBLISHED |
| Draft card | card-draft | Số publications DRAFT |
| Work Hours card | card-work-hours | Tổng giờ năm hiện tại (chỉ PUBLISHED) |
| Recent publications table | table-recent | 5 publications gần nhất |
| Create New FAB | btn-create-fab | Nút nổi (floating action button) |

### Behaviors

| Trigger | Hành vi |
|---|---|
| Page load | Auto-fetch statistics từ API |
| Click row trong table | Navigate đến /publications/{id} |
| Click FAB "Tạo mới" | Navigate đến /publications/new |
| Click "Giờ làm" card | Navigate đến /work-hours |

---

## SCR-003: Danh Sách Bài Báo

### Layout
```
┌─────────────────────────────────────────────────────────┐
│ [Nav]                                                   │
├─────────────────────────────────────────────────────────┤
│  Bài Báo Của Tôi                [+ Tạo bài báo mới]    │
│                                                          │
│  [Lọc: Trạng thái ▼]  [Năm: ____]  [🔍 Tìm kiếm...]   │
│                                                          │
│  ┌─────────────────────────────────────────────────┐   │
│  │ Tiêu đề │ Loại │ Năm │ Trạng thái │ Cập nhật │ ⚙ │   │
│  ├─────────────────────────────────────────────────┤   │
│  │ [Title] │JOURN.│2024 │[DRAFT tag] │20/02/2026 │👁✏🗑│   │
│  │ [Title] │CONF. │2023 │[SUBMIT tag]│19/02/2026 │👁   │   │
│  │ ...                                             │   │
│  └─────────────────────────────────────────────────┘   │
│                                                          │
│  Trang 1/3   [◀]  1  2  3  [▶]   Tổng: 25 bài báo     │
│                                                          │
│  [Không có kết quả: "Chưa có bài báo. Tạo ngay?"]      │
└─────────────────────────────────────────────────────────┘
```

### UI Elements

| Element | ID | Mô tả |
|---|---|---|
| Status filter | select-status | Dropdown: Tất cả / DRAFT / SUBMITTED / REVISION_REQUIRED / APPROVED / PUBLISHED |
| Year filter | input-year | Number input, clear button |
| Search box | input-search | Placeholder "Tìm kiếm theo tiêu đề..." |
| Data table | table-publications | Sortable columns |
| View icon | btn-view-{id} | Luôn hiển thị |
| Edit icon | btn-edit-{id} | Chỉ hiển thị cho DRAFT, REVISION_REQUIRED |
| Delete icon | btn-delete-{id} | Chỉ hiển thị cho DRAFT |
| Pagination | pagination-control | Page numbers + Prev/Next |
| Empty state | empty-state | Hiển thị khi không có data |

### Status Badge Colors

| Status | Màu | Label |
|---|---|---|
| DRAFT | ⚪ Xám | Nháp |
| SUBMITTED | 🔵 Xanh dương | Đã nộp |
| REVISION_REQUIRED | 🟠 Cam | Cần chỉnh sửa |
| APPROVED | 🟢 Xanh lá | Đã duyệt |
| PUBLISHED | 🟣 Tím | Đã công bố |

### Behaviors

| Trigger | Hành vi |
|---|---|
| Thay đổi Status filter | Re-fetch với filter mới (immediate) |
| Nhập Year | Re-fetch khi blur hoặc Enter |
| Nhập Search | Re-fetch sau debounce 300ms |
| Click row | Navigate đến /publications/{id} |
| Click Edit icon | Navigate đến /publications/{id}/edit |
| Click Delete icon | Hiện Confirm Dialog |
| Click Tạo mới button | Navigate đến /publications/new |

---

## SCR-004 & SCR-005: Tạo / Chỉnh Sửa Bài Báo

*(Cùng layout, khác title và hành vi)*

### Layout
```
┌─────────────────────────────────────────────────────────┐
│ [Nav]                                                   │
├─────────────────────────────────────────────────────────┤
│  ← Quay lại    Tạo Bài Báo Mới / Chỉnh Sửa Bài Báo     │
│                                                          │
│  ┌────────────────────┬────────────────────────────────┐ │
│  │Loại bài báo *      │Năm công bố *                   │ │
│  │[Journal ▼        ] │[2024             ]             │ │
│  ├────────────────────┴────────────────────────────────┤ │
│  │Tiêu đề *                                            │ │
│  │[_________________________________________________ ]│ │
│  ├────────────────────┬────────────────────────────────┤ │
│  │Tên tạp chí/hội nghị│DOI                             │ │
│  │[_________________ ]│[10.xxxx/xxxxxx                ]│ │
│  ├────────────────────┬────────────────────────────────┤ │
│  │Volume              │Issue          │Pages           │ │
│  │[_______________]   │[___________]  │[_____________] │ │
│  ├────────────────────┴────────────────────────────────┤ │
│  │Abstract                                              │ │
│  │[                                                  ] │ │
│  │[                                                  ] │ │
│  ├─────────────────────────────────────────────────────┤ │
│  │Từ khóa (phân cách bằng dấu phẩy)                   │ │
│  │[machine learning, NLP, deep learning              ] │ │
│  └─────────────────────────────────────────────────────┘ │
│                                                          │
│  👥 Đồng Tác Giả                                         │
│  ┌─────────────────────────────────────────────────┐   │
│  │ 1. [Tên bạn] (Tác giả chính) [Tác giả liên hệ ✓]│   │
│  │ 2. [Đồng tác giả 2]  [X]                        │   │
│  │ [+ Thêm đồng tác giả: Tìm theo tên...]          │   │
│  └─────────────────────────────────────────────────┘   │
│                                                          │
│  📎 File PDF                                             │
│  ┌─────────────────────────────────────────────────┐   │
│  │ [Chọn file PDF] (tối đa 20MB)                   │   │
│  │ [Tên file hiện tại: paper.pdf] (nếu có)         │   │
│  └─────────────────────────────────────────────────┘   │
│                                                          │
│  [🗑 Xóa bài báo]  (Edit only, DRAFT only, đỏ, ở trái)│
│                         [Hủy]  [Lưu Nháp]              │
└─────────────────────────────────────────────────────────┘
```

### UI Elements

| Element | ID | Required | Mô tả |
|---|---|---|---|
| Publication Type | select-pub-type | ✅ | Dropdown: JOURNAL, CONFERENCE, BOOK_CHAPTER, OTHER |
| Year | input-year | ✅ | Number input, min=1900, max=current year |
| Title | input-title | ✅ | Text input, maxlength=500 |
| Journal Name | input-journal | ❌ | Text input |
| DOI | input-doi | ❌ | Text input, pattern validation |
| Volume | input-volume | ❌ | Text input |
| Issue | input-issue | ❌ | Text input |
| Pages | input-pages | ❌ | Text input (format: 1-10) |
| Abstract | textarea-abstract | ❌ | Textarea, auto-resize |
| Keywords | input-keywords | ❌ | Tag input, comma-separated |
| Co-authors section | section-coauthors | - | Search + list |
| Co-author search | input-coauthor-search | - | Autocomplete |
| PDF upload | input-pdf | ❌ | File input, accept=".pdf" |
| Delete button | btn-delete | - | Chỉ Edit mode, DRAFT only |
| Cancel button | btn-cancel | - | Quay về List |
| Save button | btn-save | - | Primary button |

### Validation Messages

| Field | Rule | Error Message |
|---|---|---|
| Title | Required | "Tiêu đề là bắt buộc" |
| Title | Max 500 chars | "Tiêu đề không được vượt quá 500 ký tự" |
| Year | Required | "Năm công bố là bắt buộc" |
| Year | Range 1900-now | "Năm phải từ 1900 đến [năm hiện tại]" |
| Publication Type | Required | "Vui lòng chọn loại bài báo" |
| DOI | Format | "Định dạng DOI không hợp lệ (ví dụ: 10.1000/xyz123)" |

### Behaviors

| Trigger | Hành vi |
|---|---|
| Rời khỏi field (blur) | Validate field đó, hiện error nếu sai |
| Click "Lưu Nháp" | Validate toàn form → nếu OK: submit API |
| Submit thành công | Toast success, redirect /publications/{id} |
| Submit thất bại | Toast error với message từ server |
| Click "Hủy" | Confirmation dialog "Các thay đổi sẽ bị mất?" → Nếu OK: về /publications |
| Click "Xóa" (Edit only) | Confirm dialog → Nếu OK: gọi DELETE API → về /publications |
| Nhập đồng tác giả | Debounce 300ms → Gọi search API → Hiện dropdown |
| Chọn file PDF | Validate size và type trước khi submit |

---

## SCR-006: Chi Tiết Bài Báo

### Layout
```
┌─────────────────────────────────────────────────────────────┐
│ [Nav]                                                       │
├─────────────────────────────────────────────────────────────┤
│  ← Quay lại    Chi Tiết Bài Báo         [DRAFT ●]          │
├────────────────────────────┬────────────────────────────────┤
│                            │                                │
│   PDF VIEWER (60%)         │   METADATA PANEL (40%)         │
│                            │                                │
│   ┌──────────────────────┐│   📌 Loại: JOURNAL             │
│   │                      ││   📅 Năm: 2024                 │
│   │   [PDF hiển thị]     ││   📰 Tạp chí: IEEE Access      │
│   │   (iframe)           ││   🔢 DOI: 10.xxxx/xxxx [↗]    │
│   │                      ││   📄 Trang: 1-15               │
│   │                      ││                                │
│   │                      ││   👥 Tác Giả                   │
│   │                      ││   1. Nguyễn Văn A (Tác giả LC) │
│   │                      ││   2. Trần Thị B                │
│   │                      ││                                │
│   └──────────────────────┘│   📝 Tóm Tắt                  │
│                            │   [Nội dung abstract...]      │
│   Nếu không có PDF:        │                                │
│   ┌──────────────────────┐│   🏷 Từ Khóa                  │
│   │  📎 Chưa có tệp PDF  ││   [ML] [NLP] [Deep Learning]  │
│   │  [↑ Tải lên PDF]     ││                                │
│   └──────────────────────┘│   📁 File: paper.pdf (2.3MB)  │
│                            │   Tải lên: 20/02/2026         │
│                            │                                │
│                            │   ────────────────────────    │
│                            │   [✏ Chỉnh sửa] [⬇ Tải PDF] │
│                            │   [🗑 Xóa] (nếu DRAFT)       │
│                            │                               │
└────────────────────────────┴───────────────────────────────┘
```

### UI Elements

| Element | ID | Hiển thị khi |
|---|---|---|
| PDF Viewer (iframe) | pdf-viewer | Có PDF file |
| Upload PDF placeholder | placeholder-no-pdf | Không có PDF + là owner |
| Publication metadata | section-metadata | Luôn hiển thị |
| Status badge | badge-status | Luôn hiển thị, màu theo status |
| DOI link | link-doi | DOI có giá trị |
| Co-authors list | list-coauthors | Luôn hiển thị (kể cả khi chưa có co-author) |
| Abstract | text-abstract | Luôn hiển thị |
| Keywords tags | tags-keywords | Có keywords |
| File info | section-fileinfo | Có PDF |
| Edit button | btn-edit | owner + status ∈ {DRAFT, REVISION_REQUIRED} |
| Delete button | btn-delete | owner + status = DRAFT |
| Download PDF button | btn-download | Có PDF |

### Behaviors

| Trigger | Hành vi |
|---|---|
| Page load | Fetch publication data, render PDF viewer nếu có PDF |
| Click Edit | Navigate /publications/{id}/edit |
| Click Download | Trigger browser download, ghi audit log |
| Click Delete | Confirm dialog → DELETE API → về /publications |
| Click Upload PDF (trong placeholder) | Trigger file picker |
| DOI link click | Mở tab mới: https://doi.org/{DOI} |
| Abstract dài > 500 chars | Hiện "Xem thêm" toggle |

---

## Navigation Flow tổng quát

```
/login
    │
    └→ /dashboard ──→ /publications (list)
                 │              │
                 └→ /work-hours └→ /publications/new (create)
                                │
                                ├→ /publications/{id} (detail)
                                │           │
                                │           └→ /publications/{id}/edit
                                │
                                └→ /publications/{id}/edit (via edit icon)
```

---

**Prepared by**: Business Analysis Team  
**Version**: 1.0  
**Date**: 20/02/2026
