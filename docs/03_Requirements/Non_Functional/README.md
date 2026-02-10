# Non-Functional Requirements - README

> 📁 **Folder**: `03_Requirements/Non_Functional`  
> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục đích**: Tổng hợp yêu cầu phi chức năng

---

## 📚 Tài Liệu Trong Folder

1. **[performance.md](./performance.md)** - Hiệu năng (response time, throughput, caching)
2. **[security.md](./security.md)** - Bảo mật (auth, authorization, HTTPS, audit)
3. **[usability.md](./usability.md)** - Khả năng sử dụng (UI/UX, accessibility, help)
4. **[scalability.md](./scalability.md)** - Khả năng mở rộng (data volume, scaling strategy)
5. **[compatibility.md](./compatibility.md)** - Tương thích (browsers, OS, integrations)

---

## 📊 Summary

| Category | Key Requirements |
|----------|-----------------|
| **Performance** | Page load < 2s, Search < 1s, Report < 5 phút |
| **Security** | LDAP/AD SSO, HTTPS, RBAC, Audit logs |
| **Usability** | Form < 5 phút, Responsive, Tiếng Việt, WCAG AA |
| **Scalability** | 20K publications, 1K users, Redis cache, Stateless |
| **Compatibility** | Chrome 90+, MySQL 8.0+, PDF only |

---

**Tài liệu liên quan**:
- [Functional Requirements](../Functional/)
- [User Needs](../../02_System_Clarification/User_Analysis/user_needs.md)
