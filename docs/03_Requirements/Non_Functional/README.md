# Yêu Cầu Phi Chức Năng - README

> 📁 **Thư mục**: `03_Requirements/Non_Functional`  
> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục đích**: Tổng hợp yêu cầu phi chức năng

---

## 📚 Tài Liệu Trong Thư Mục

1. **[performance.md](./performance.md)** - Hiệu năng (thời gian phản hồi, thông lượng, bộ nhớ đệm)
2. **[security.md](./security.md)** - Bảo mật (xác thực, phân quyền, HTTPS, kiểm toán)
3. **[usability.md](./usability.md)** - Khả năng sử dụng (Giao diện/Trải nghiệm, khả năng truy cập, trợ giúp)
4. **[scalability.md](./scalability.md)** - Khả năng mở rộng (khối lượng dữ liệu, chiến lược mở rộng)
5. **[compatibility.md](./compatibility.md)** - Tương thích (trình duyệt, hệ điều hành, tích hợp)

---

## 📊 Tóm Tắt

| Danh mục | Yêu cầu Chính |
|----------|-----------------|
| **Hiệu năng** | Tải trang < 2s, Tìm kiếm < 1s, Báo cáo < 5 phút |
| **Bảo mật** | Đăng nhập một lần (SSO) LDAP/AD, HTTPS, Phân quyền theo vai trò (RBAC), Nhật ký kiểm toán |
| **Khả năng sử dụng** | Nhập liệu < 5 phút, Responsive (tương thích mọi thiết bị), Tiếng Việt, Chuẩn WCAG AA |
| **Khả năng mở rộng** | 20K bài báo, 1K người dùng, Redis cache, Stateless (phi trạng thái) |
| **Tương thích** | Chrome 90+, MySQL 8.0+, Chỉ hỗ trợ PDF |

---

**Tài liệu liên quan**:
- [Yêu Cầu Chức Năng](../Functional/)
- [Nhu Cầu Người Dùng](../../02_System_Clarification/User_Analysis/user_needs.md)
