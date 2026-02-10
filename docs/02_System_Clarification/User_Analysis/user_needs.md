# Nhu Cầu Người Dùng - UFPMS

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục đích**: Tổng hợp nhu cầu chi tiết của 5 nhóm người dùng

---

## 1. Researcher (Giảng Viên) - 300-500 người

### 1.1. Functional Needs (Nhu Cầu Chức Năng)

| Nhu cầu | Mô tả | Mức độ ưu tiên |
|---------|-------|----------------|
| **Quản lý bài báo dễ dàng** | Thêm/Sửa/Xóa bài báo nhanh chóng | 🔴 P0 - Bắt buộc |
| **Upload file PDF** | Lưu trữ bài báo full-text | 🔴 P0 - Bắt buộc |
| **Nộp xét duyệt** | Gửi công trình để Khoa/Trường phê duyệt | 🔴 P0 - Bắt buộc |
| **Theo dõi trạng thái** | Biết bài báo đang ở đâu trong quy trình | 🔴 P0 - Bắt buộc |
| **Nhận feedback** | Xem nhận xét từ CB Khoa/Trường | 🔴 P0 - Bắt buộc |
| **Profile công khai** | Trang cá nhân chuyên nghiệp | 🟡 P1 - Quan trọng |
| **Auto-import từ ORCID** | Tự động lấy danh sách bài báo | 🟢 P2 - Tương lai |
| **Thống kê cá nhân** | Biểu đồ năng suất, H-index | 🟡 P1 - Quan trọng |

---

### 1.2. Non-Functional Needs (Nhu Cầu Phi Chức Năng)

| Nhu cầu | Yêu cầu cụ thể |
|---------|----------------|
| **Dễ sử dụng** | Form nhập liệu < 5 phút/bài báo |
| **Thời gian phản hồi** | Tải trang < 2 giây |
| **Khả dụng** | Truy cập 24/7, uptime \u003e 99% |
| **Mobile-friendly** | Xem được trên điện thoại |
| **Ngôn ngữ** | Tiếng Việt (UI + thông báo) |
| **Thông báo** | Email tự động khi có phản hồi |

---

### 1.3. Pain Points Cần Giải Quyết

❌ **Hiện tại**: Phải nhập lại danh sách bài báo mỗi 6 tháng  
✅ **Giải pháp**: Nhập 1 lần, lưu vĩnh viễn

❌ **Hiện tại**: Không biết công trình có được ghi nhận không  
✅ **Giải pháp**: Workflow phê duyệt minh bạch, có timeline

❌ **Hiện tại**: Không có profile công khai  
✅ **Giải pháp**: Profile tự động từ dữ liệu đã nhập

---

## 2. Faculty Reviewer (Cán Bộ Khoa) - 10-20 người

### 2.1. Functional Needs

| Nhu cầu | Mô tả | Mức độ ưu tiên |
|---------|-------|----------------|
| **Dashboard chờ duyệt** | Xem tất cả công trình của Khoa | 🔴 P0 - Bắt buộc |
| **Lọc và sắp xếp** | Filter theo trạng thái, giảng viên, loại tạp chí | 🔴 P0 - Bắt buộc |
| **Xem chi tiết công trình** | Metadata đầy đủ + PDF | 🔴 P0 - Bắt buộc |
| **Approve/Revision/Reject** | 3 actions chính | 🔴 P0 - Bắt buộc |
| **Nhập nhận xét** | Comment box cho feedback | 🔴 P0 - Bắt buộc |
| **Bulk approve** | Duyệt nhiều bài cùng lúc | 🟡 P1 - Quan trọng |
| **Lịch sử xét duyệt** | Xem lại bài đã duyệt | 🟡 P1 - Quan trọng |
| **Báo cáo Khoa** | Thống kê công trình của Khoa | 🟡 P1 - Quan trọng |

---

### 2.2. Non-Functional Needs

| Nhu cầu | Yêu cầu cụ thể |
|---------|----------------|
| **Hiệu quả** | Duyệt 1 bài trong 5-10 phút |
| **Thông báo** | Email khi có công trình mới |
| **Bảo mật** | CHỈ xem công trình của Khoa mình |
| **Audit trail** | Hệ thống lưu ai duyệt gì, khi nào |

---

### 2.3. Pain Points Cần Giải Quyết

❌ **Hiện tại**: Không có công cụ xét duyệt, phải email qua lại  
✅ **Giải pháp**: Dashboard tập trung, workflow rõ ràng

❌ **Hiện tại**: Không biết bài nào đã duyệt, bài nào chưa  
✅ **Giải pháp**: Lịch sử đầy đủ, trạng thái rõ ràng

❌ **Hiện tại**: Nhiều bài chờ duyệt, không biết ưu tiên  
✅ **Giải pháp**: Highlight bài quá hạn, filter mạnh mẽ

---

## 3. University Reviewer (Cán Bộ Trường) - 2-5 người

### 3.1. Functional Needs

| Nhu cầu | Mô tả | Mức độ ưu tiên |
|---------|-------|----------------|
| **Dashboard toàn trường** | Xem công trình đã được Khoa duyệt | 🔴 P0 - Bắt buộc |
| **Xem ý kiến Khoa** | Context để quyết định | 🔴 P0 - Bắt buộc |
| **Approve/Reject** | Phê duyệt cuối cùng | 🔴 P0 - Bắt buộc |
| **Báo cáo toàn trường** | Thống kê theo Khoa, theo năm | 🔴 P0 - Bắt buộc |
| **Export báo cáo** | Excel, PDF cho lãnh đạo, Bộ | 🔴 P0 - Bắt buộc |
| **Dashboard analytics** | Xu hướng, top giảng viên | 🟡 P1 - Quan trọng |

---

### 3.2. Non-Functional Needs

| Nhu cầu | Yêu cầu cụ thể |
|---------|----------------|
| **Tốc độ báo cáo** | Export báo cáo trong vài phút (vs 2-3 ngày hiện tại) |
| **Độ chính xác** | Không trùng lặp, tự động loại bỏ duplicates |
| **Bảo mật** | Audit logs đầy đủ |

---

### 3.3. Pain Points Cần Giải Quyết

❌ **Hiện tại**: Mất 2-3 ngày tạo 1 báo cáo  
✅ **Giải pháp**: Báo cáo tự động, export 1-click

❌ **Hiện tại**: Dữ liệu trùng lặp ~15-20%  
✅ **Giải pháp**: Hệ thống tự động detect và gộp

❌ **Hiện tại**: Không có dashboard thời gian thực  
✅ **Giải pháp**: Dashboard analytics với biểu đồ động

---

## 4. Viewer (Sinh Viên, Công Chúng) - Không giới hạn

### 4.1. Functional Needs

| Nhu cầu | Mô tả | Mức độ ưu tiên |
|---------|-------|----------------|
| **Tìm kiếm bài báo** | Full-text search, filter | 🔴 P0 - Bắt buộc |
| **Tìm giảng viên theo lĩnh vực** | Filter theo từ khóa | 🔴 P0 - Bắt buộc |
| **Xem profile giảng viên** | Danh sách bài báo, biểu đồ | 🔴 P0 - Bắt buộc |
| **Tải PDF (nếu public)** | Access full-text | 🟡 P1 - Quan trọng |
| **Link đến DOI** | Xem paper gốc | 🟡 P1 - Quan trọng |

---

### 4.2. Non-Functional Needs

| Nhu cầu | Yêu cầu cụ thể |
|---------|----------------|
| **Không cần đăng nhập** | Public access |
| **SEO tốt** | Xuất hiện trên Google |
| **Mobile-friendly** | Responsive design |
| **Tốc độ** | Tìm kiếm < 1 giây |

---

### 4.3. Pain Points Cần Giải Quyết

❌ **Hiện tại**: Không biết thầy/cô nào chuyên về gì  
✅ **Giải pháp**: Tìm kiếm theo từ khóa, lĩnh vực

❌ **Hiện tại**: Thông tin giảng viên lỗi thời  
✅ **Giải pháp**: Profile tự động cập nhật

---

## 5. SuperAdmin - 2-5 người

### 5.1. Functional Needs

| Nhu cầu | Mô tả | Mức độ ưu tiên |
|---------|-------|----------------|
| **User management** | CRUD tài khoản, phân quyền | 🔴 P0 - Bắt buộc |
| **Quản lý đơn vị** | CRUD Khoa/Viện/Bộ môn | 🔴 P0 - Bắt buộc |
| **System config** | LDAP, email templates | 🔴 P0 - Bắt buộc |
| **Monitoring** | Dashboard hệ thống | 🔴 P0 - Bắt buộc |
| **Audit logs** | Xem lịch sử thao tác | 🔴 P0 - Bắt buộc |
| **Backup/Restore** | Quản lý backup | 🔴 P0 - Bắt buộc |
| **Import dữ liệu cũ** | Import từ Excel | 🟡 P1 - Quan trọng |

---

### 5.2. Non-Functional Needs

| Nhu cầu | Yêu cầu cụ thể |
|---------|----------------|
| **Dễ vận hành** | Documentation đầy đủ |
| **Monitoring** | Alert khi có lỗi |
| **Recovery** | RTO < 4 giờ |

---

## 6. Ma Trận Nhu Cầu Chung (Cross-Cutting Concerns)

### 6.1. Tất Cả Người Dùng

| Nhu cầu | Yêu cầu |
|---------|---------|
| **Bảo mật** | HTTPS, LDAP/AD, phân quyền rõ ràng |
| **Hiệu năng** | Tải trang < 2 giây |
| **Khả dụng** | Uptime \u003e 99% |
| **Hỗ trợ** | Help docs, FAQ |

---

### 6.2. Internal Users (Researcher, Reviewers, Admin)

| Nhu cầu | Yêu cầu |
|---------|---------|
| **Single Sign-On** | Đăng nhập qua LDAP/AD |
| **Email notification** | Thông báo tự động |
| **Audit trail** | Lưu lịch sử thao tác |
| **Dashboard** | Theo dõi công việc |

---

### 6.3. Public Users (Viewer)

| Nhu cầu | Yêu cầu |
|---------|---------|
| **Không cần đăng nhập** | Public access |
| **SEO** | Google indexing |
| **Responsive** | Mobile-friendly |

---

## 7. Prioritization (Ưu Tiên Phát Triển)

### MVP (3 tháng đầu)

🔴 **P0 - Bắt buộc**:
- ✅ Quản lý bài báo (CRUD)
- ✅ Quy trình phê duyệt 2 cấp
- ✅ Dashboard theo vai trò
- ✅ Báo cáo cơ bản
- ✅ User management

---

### Phase 2 (Tháng 4-6)

🟡 **P1 - Quan trọng**:
- ✅ Profile công khai
- ✅ Public search
- ✅ Bulk operations
- ✅ Advanced analytics
- ✅ Export báo cáo (Excel/PDF)

---

### Phase 3 (Tương lai)

🟢 **P2 - Nice to have**:
- ✅ ORCID auto-import
- ✅ Google Scholar sync
- ✅ AI gợi ý đồng nghiệp
- ✅ Mobile app

---

## 8. Validation Checklist

### 8.1. Câu Hỏi Kiểm Tra

✅ **Researcher có dùng không?**
- Có dễ nhập bài báo không? → Form < 5 phút
- Có theo dõi được trạng thái không? → Timeline rõ ràng
- Có nhận được feedback không? → Email tự động

✅ **Reviewer có hiệu quả không?**
- Có duyệt nhanh không? → Dashboard tập trung
- Có lọc, sắp xếp được không? → Filter mạnh mẽ
- Có lịch sử đầy đủ không? → Audit trail

✅ **Lãnh đạo có hài lòng không?**
- Có báo cáo nhanh không? → Export 1-click
- Có dashboard thời gian thực không? → Analytics

✅ **Sinh viên có tìm được không?**
- Có tìm kiếm dễ không? → Full-text search
- Có thông tin mới nhất không? → Auto-update profile

---

## 9. Kết Luận

### 9.1. Top 3 Nhu Cầu Quan Trọng Nhất

1. **Quy trình phê duyệt minh bạch** (cho Researcher, Reviewer)
2. **Báo cáo tự động nhanh** (cho University Reviewer, Lãnh đạo)
3. **Profile công khai** (cho Researcher, Viewer)

---

### 9.2. Success Metrics

| Chỉ số | Baseline (As-Is) | Target (To-Be) |
|--------|------------------|----------------|
| **Thời gian nhập 1 bài báo** | 15-30 phút | < 5 phút |
| **Thời gian tạo báo cáo** | 2-3 ngày | < 5 phút |
| **Tỉ lệ giảng viên sử dụng** | ~60% (bị động) | \u003e 80% (chủ động) |
| **Độ hài lòng người dùng** | N/A | \u003e 85% |

---

**Tài liệu liên quan**:
- [User Groups](./user_groups.md) - Phân tích chi tiết 5 nhóm
- [Stakeholders](../../01_System_Specification/stakeholders.md) - Ma trận stakeholder
- [Requirements](../../03_Requirements/) - Chuyển hóa thành yêu cầu chức năng
