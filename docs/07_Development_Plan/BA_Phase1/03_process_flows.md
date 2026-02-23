# BA Deliverable 3: Process Flow Diagrams

> 📋 **Phiên bản**: V1.0  
> 👤 **Vai trò**: Business Analyst  
> 📅 **Ngày tạo**: 20/02/2026  
> 🎯 **Phạm vi**: Core Publication Management Workflows

---

## Tổng Quan

Tài liệu này mô tả các **process flows chính** của hệ thống UFPMS V1.0. Mỗi flow thể hiện các bước xử lý từ góc nhìn người dùng, bao gồm cả các nhánh lỗi và edge cases.

---

## Flow 1: Đăng Nhập (Login)

```
[Bắt đầu]
    │
    ▼
[User truy cập ứng dụng]
    │
    ▼
[Hiển thị trang Login]
    │
    ▼
[User nhập Username + Password]
    │
    ▼
[User nhấn "Đăng nhập"]
    │
    ▼
◇ [Thông tin hợp lệ?]
    │                    │
   Không                 Có
    │                    │
    ▼                    ▼
[Hiện lỗi:         [Tạo JWT Token]
"Sai thông              │
tin đăng               ▼
nhập"]         [Lưu token vào
    │           localStorage]
    │                   │
    └──────────────►[Redirect đến Dashboard]
                        │
                    [Kết thúc]
```

---

## Flow 2: Tạo Bài Báo Mới (Create Publication)

```
[Bắt đầu - User đã đăng nhập]
    │
    ▼
[User click "Tạo bài báo mới"]
    │
    ▼
[Hiển thị Form Tạo Bài Báo (trống)]
    │
    ▼
[User điền thông tin: Title, Type, Year, ...]
    │
    ▼
[User click "Lưu nháp"]
    │
    ▼
◇ [Validation frontend OK?]
    │                    │
   Không                 Có
    │                    │
    ▼                    ▼
[Hiện lỗi         [Gửi POST request
inline cho          đến API]
từng field]              │
    │                    ▼
    │           ◇ [API trả về OK?]
    │                │           │
    │              Không         Có
    │                │           │
    │                ▼           ▼
    │           [Hiện toast:   [Lưu vào DB:
    │            "Có lỗi xảy    publication
    │             ra. Thử lại"]  status=DRAFT]
    │                               │
    │                               ▼
    │                   [Redirect đến Detail page]
    │                               │
    └───────────────────────────────┘
                                [Kết thúc]
```

---

## Flow 3: Upload File PDF

```
[Bắt đầu - User trên Detail page]
    │
    ▼
◇ [User là owner?]
    │              │
   Không           Có
    │              │
    ▼              ▼
[Ẩn nút       [Hiển thị nút
"Upload PDF"]  "Upload PDF"]
    │              │
[Kết thúc]         ▼
               [User click "Upload PDF"]
                   │
                   ▼
               [Mở file picker (.pdf only)]
                   │
                   ▼
               ◇ [User chọn file?]
                   │              │
                  Không           Có
                   │              │
                   ▼              ▼
               [Đóng picker]  ◇ [File hợp lệ?]
               [Không đổi gì]    (PDF + ≤20MB)
                                  │           │
                                 Không        Có
                                  │           │
                                  ▼           ▼
                             [Hiện lỗi:   [Upload lên server]
                              "Chỉ PDF"    (progress bar)
                              "File ≤20MB"]     │
                                               ▼
                                     ◇ [Upload thành công?]
                                          │           │
                                         Không        Có
                                          │           │
                                          ▼           ▼
                                    [Toast error:  [Lưu path vào DB]
                                     "Upload thất      │
                                      bại. Thử lại"]   ▼
                                                   [Hiển thị PDF preview]
                                                        │
                                                        ▼
                                                   [Toast: "Upload thành công"]
                                                        │
                                                   [Kết thúc]
```

---

## Flow 4: Sửa Bài Báo (Edit Publication)

```
[Bắt đầu - User trên List hoặc Detail page]
    │
    ▼
◇ [Publication thuộc user? VÀ status DRAFT/REVISION_REQUIRED?]
    │                              │
   Không                           Có
    │                              │
    ▼                              ▼
[Edit button ẩn/disabled]    [Hiển thị Edit button]
[Kết thúc]                        │
                                   ▼
                         [User click Edit]
                                   │
                                   ▼
                         [Hiển thị Form Edit đã pre-filled]
                                   │
                                   ▼
                         [User sửa các trường cần thiết]
                                   │
                                   ▼
                         [User click "Lưu"]
                                   │
                                   ▼
                    ◇ [Validation frontend OK?]
                         │                  │
                        Không               Có
                         │                  │
                         ▼                  ▼
                    [Hiện lỗi inline]   [PUT request đến API]
                                            │
                                            ▼
                                 ◇ [API trả về OK?]
                                      │         │
                                     Không       Có
                                      │         │
                                      ▼         ▼
                               [Toast error] [Cập nhật DB]
                                             [Ghi Audit Log]
                                                  │
                                                  ▼
                                       [Redirect về Detail page]
                                                  │
                                       [Toast: "Lưu thành công"]
                                                  │
                                             [Kết thúc]
```

---

## Flow 5: Xóa Bài Báo DRAFT (Delete Publication)

```
[Bắt đầu - User trên List hoặc Detail page]
    │
    ▼
◇ [owner? VÀ status = DRAFT?]
    │              │
   Không           Có
    │              │
    ▼              ▼
[Delete button]   [Hiển thị delete button]
[không hiển thị]       │
[Kết thúc]             ▼
                  [User click Delete]
                        │
                        ▼
                  [Hiện Confirm Dialog:
                   "Bạn chắc chắn muốn xóa?
                    Hành động không thể hoàn tác."]
                        │
                        ▼
              ◇ [User nhấn?]
                  │            │
                "Hủy"       "Xác nhận"
                  │            │
                  ▼            ▼
             [Đóng dialog] [DELETE request API]
             [Không đổi gì]     │
                                ▼
                     ◇ [API OK?]
                         │        │
                        Không      Có
                         │        │
                         ▼        ▼
                    [Toast error] [Soft delete DB: set deleted_at]
                                  [Xóa PDF vật lý (nếu có)]
                                  [Ghi Audit Log]
                                        │
                                        ▼
                                  [Redirect về List]
                                  [Toast: "Đã xóa thành công"]
                                        │
                                  [Kết thúc]
```

---

## Flow 6: Thêm Đồng Tác Giả (Add Co-Author)

```
[Bắt đầu - User trong Create/Edit form]
    │
    ▼
[User gõ tên vào Co-Author search box]
    │
    ▼
[Debounce 300ms → Gọi API search users]
    │
    ▼
◇ [Có kết quả?]
    │              │
   Không           Có
    │              │
    ▼              ▼
[Hiện option:  [Hiện dropdown:
"Thêm tác giả   danh sách users]
ngoài hệ thống"]     │
    │                 ▼
    ▼           [User chọn user]
[User nhập          │
 tên + email]       └──────────┐
    │                          │
    └─────────────────────────►▼
                         ◇ [User đã có trong list?]
                              │              │
                             Có             Không
                              │              │
                              ▼              ▼
                         [Warning:       [Thêm vào list
                          "Đã có"]        co-authors]
                                          [Assign sequence]
                                               │
                                               ▼
                                    [Hiển thị trong danh sách]
                                    [User có thể:
                                     - Kéo để sắp xếp
                                     - Click X để xóa
                                     - Check Corresponding Author]
                                               │
                                          [Kết thúc]
```

---

## Flow 7: Xem Dashboard Giờ Làm

```
[Bắt đầu - User đã đăng nhập]
    │
    ▼
[User click "Dashboard Giờ Làm"]
    │
    ▼
[Gọi API: GET /work-hours?year=[năm hiện tại]]
    │
    ▼
◇ [API trả về dữ liệu?]
    │                  │
   Không               Có
    │                  │
    ▼                  ▼
[Hiện loading]  [Render Dashboard:
[→ Error state]  - Summary card: "Năm YYYY: Xh"
                 - Year filter dropdown
                 - Bảng chi tiết publications]
                       │
                       ▼
           ◇ [User thay đổi Year filter?]
                   │             │
                  Không          Có
                   │             │
                   ▼             ▼
             [Hiển thị     [Gọi API với year mới]
              nút Xuất          │
              Excel]            └────────────►[Re-render Dashboard]
                   │
                   ▼
           ◇ [User click "Xuất Excel"?]
                   │         │
                  Không       Có
                   │         │
              [Kết thúc]     ▼
                         [Gọi API: GET /work-hours/export?year=...]
                              │
                              ▼
                         [Server tạo file .xlsx]
                              │
                              ▼
                         [Browser download file]
                              │
                         [Kết thúc]
```

---

## Flow 8: Publication Detail View

```
[Bắt đầu - User click vào publication]
    │
    ▼
[Gọi API: GET /publications/{id}]
    │
    ▼
◇ [User có quyền xem?]
    │              │
   Không           Có
    │              │
    ▼              ▼
[Redirect      [Render Detail page:
 403 page]      Layout 2 cột]
                   │
          ┌────────┴────────┐
          ▼                 ▼
    [Cột trái:        [Cột phải:
     PDF Viewer]       Metadata Panel]
          │                 │
          ▼                 ▼
    ◇ [Có PDF?]      [Hiện: Title, Type,
          │           Year, Authors,
         Có           Abstract, Keywords,
          │           Status badge]
          ▼                 │
    [iframe PDF]            ▼
                     ◇ [User là owner?
                      VÀ status DRAFT?]
                          │      │
                         Có     Không
                          │      │
                          ▼      ▼
                     [Hiện btn  [Hiện btn
                      Edit +     Download only]
                      Delete]
                          │
                     [Kết thúc]
```

---

**Prepared by**: Business Analysis Team  
**Version**: 1.0  
**Date**: 20/02/2026
