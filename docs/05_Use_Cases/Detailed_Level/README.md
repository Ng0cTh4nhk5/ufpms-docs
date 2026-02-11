# Detailed-Level Use Cases - README

> 📁 **Cấp Độ**: Detailed-Level Use Cases (Use Case Chi Tiết)  
> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục đích**: Đặc tả chi tiết cho 20 use cases P0 quan trọng nhất

---

## 📊 Tổng Quan

Detailed-level use cases cung cấp đặc tả đầy đủ cho các P0 (Phải Có) use cases quan trọng nhất, bao gồm:
- Điều kiện tiên quyết & Điều kiện hậu quyết chi tiết
- Luồng chính với các bước cụ thể
- **Luồng thay thế (Alternative Flows)**: Các kịch bản khác nhau
- **Luồng ngoại lệ (Exception Flows)**: Xử lý lỗi
- Quy tắc nghiệp vụ đầy đủ

> [!NOTE]
> **Tại sao chỉ 20 use cases?**
> Đặc tả chi tiết rất tốn công tạo. Chúng tôi tập trung vào 20 use cases P0 QUAN TRỌNG NHẤT cho MVP. Các use cases P1/P2 có đặc tả cấp trung (medium-level specs) là đủ.

---

## 📋 20 Use Cases Chi Tiết (Detailed-Level)

### Module 1: Quản Lý Bài Báo (5 specs)

| ID UC | Tên | Tập Tin |
|-------|------|------|
| UC-D1-01 | Tạo Bài Báo | uc_d1_01_create_publication.md |
| UC-D1-02 | Sửa Bài Báo | uc_d1_02_edit_publication.md |
| UC-D1-03 | Tải Lên PDF | uc_d1_03_upload_pdf.md |
| UC-D1-04 | Xem Danh Sách Bài Báo | uc_d1_04_view_publication_list.md |
| UC-D1-05 | Xóa Bài Báo | uc_d1_05_delete_publication.md |

### Module 2: Quy Trình Xét Duyệt (7 specs)

| ID UC | Tên | Tập Tin |
|-------|------|------|
| UC-D2-01 | Gửi Xét Duyệt | uc_d2_01_submit_for_review.md |
| UC-D2-02 | Khoa Phê Duyệt | uc_d2_02_faculty_approve.md |
| UC-D2-03 | Khoa Yêu Cầu Chỉnh Sửa | uc_d2_03_faculty_request_revision.md |
| UC-D2-04 | Khoa Từ Chối | uc_d2_04_faculty_reject.md |
| UC-D2-05 | Trường Phê Duyệt & Xuất Bản | uc_d2_05_university_approve_publish.md |
| UC-D2-06 | Theo Dõi Trạng Thái Xét Duyệt | uc_d2_06_track_review_status.md |
| UC-D2-07 | Thông Báo Email | uc_d2_07_email_notifications.md |

### Module 3: Tìm Kiếm & Duyệt (3 specs)

| ID UC | Tên | Tập Tin |
|-------|------|------|
| UC-D3-01 | Tìm Kiếm Cơ Bản | uc_d3_01_basic_search.md |
| UC-D3-02 | Tìm Kiếm Nâng Cao | uc_d3_02_advanced_search.md |
| UC-D3-03 | Lọc Kết Quả | uc_d3_03_filter_results.md |

### Module 6: Quản Trị Hệ Thống & Người Dùng (5 specs)

| ID UC | Tên | Tập Tin |
|-------|------|------|
| UC-D6-01 | Tạo Người Dùng | uc_d6_01_create_user.md |
| UC-D6-02 | Gán Vai Trò | uc_d6_02_assign_roles.md |
| UC-D6-03 | Cấu Hình LDAP | uc_d6_03_configure_ldap.md |
| UC-D6-04 | Xem Nhật Ký Kiểm Toán | uc_d6_04_view_audit_logs.md |
| UC-D6-05 | Sao Lưu Hệ Thống | uc_d6_05_backup_system.md |

---

## 📖 Định Dạng Đặc Tả Chi Tiết

Mỗi đặc tả chi tiết bao gồm:

```markdown
# UC-DX-XX: [Tên Use Case]

## Tổng Quan
[Tóm tắt, độ ưu tiên, tác nhân, tài liệu liên quan]

## Điều Kiện Tiên Quyết
[Yêu cầu chi tiết về trạng thái hệ thống và người dùng]

## Luồng Chính
1. [Bước 1 với hành vi hệ thống]
2. [Bước 2 với các xác thực]
...

## Luồng Thay Thế (Alternative Flows)

### Alt-1: [Tên Kịch Bản]
**Khi**: [Điều kiện]
**Thì**: [Đường dẫn khác]

### Alt-2: [Kịch Bản Khác]
...

## Luồng Ngoại Lệ (Exception Flows)

### Exc-1: [Kịch Bản Lỗi]
**Khi**: [Điều kiện lỗi]
**Hệ thống**: [Xử lý lỗi]

## Điều Kiện Hậu Quyết
**Thành Công**: [Trạng thái sau khi thành công]
**Thất Bại**: [Trạng thái sau khi thất bại]

## Quy Tắc Nghiệp Vụ
- BR-XXX-001: [Quy tắc chi tiết]
...

## Mockup Giao Diện (nếu có)
[Sơ đồ hoặc ảnh chụp màn hình]

## Biểu Đồ Tuần Tự (nếu phức tạp)
[Biểu đồ tuần tự Mermaid]
```

---

## 🎯 Lợi Ích Của Đặc Tả Chi Tiết

1. **Cho Lập Trình Viên**: Hướng dẫn cài đặt rõ ràng
2. **Cho Tester**: Các kịch bản kiểm thử và trường hợp biên
3. **Cho Designer**: Yêu cầu về luồng giao diện người dùng
4. **Cho Tài Liệu**: Nội dung hướng dẫn sử dụng

---

## 🚧 Trạng Thái

> [!IMPORTANT]
> **Đặc tả chi tiết sẽ được tạo trong Giai Đoạn 2 (Phase 2)**
> 
> Do thời gian hạn chế, chúng tôi đã tạo:
> - ✅ Main README và cấu trúc thư mục
> - ✅ 6 High-Level UCs (hoàn thành)
> - ✅ 54 Medium-Level UCs (hoàn thành) 
> - 📝 20 Detailed-Level UCs (đã có template và cấu trúc, nội dung sẽ được tạo khi triển khai MVP)
>
> Đặc tả cấp trung (Medium-level specs) đã đủ chi tiết để bắt đầu phát triển. Đặc tả chi tiết sẽ được tạo song song với quá trình cài đặt.

---

**Tài liệu liên quan**:
- [Use Cases Cấp Trung (Medium-Level)](../Medium_Level/)
- [Use Cases Cấp Cao (High-Level)](../High_Level/)
- [Biểu Đồ Tuần Tự (Sequence Diagrams)](../Sequence_Diagrams/) (để tạo trong Phase 2)
- [Biểu Đồ Hoạt Động (Activity Diagrams)](../Activity_Diagrams/) (để tạo trong Phase 2)
