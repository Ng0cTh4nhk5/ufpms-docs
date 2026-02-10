# P0 User Stories - Must Have (MVP)

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục đích**: User stories bắt buộc cho MVP  
> ⚠️ **Priority**: P0 - Must Have

---

## Tổng Quan

**Total P0 Stories**: 40  

---

## Phân Bổ Theo Role

| Role | P0 Stories |
|------|-----------|
| Researcher | 18 |
| Faculty Reviewer | 6 |
| University Reviewer | 6 |
| SuperAdmin | 8 |
| Public Visitor | 2 |

---

## Researcher (18 Stories)

### Publication Management
- **US-RES-001**: Tạo Bài Báo Mới (FR-PUB-001)
- **US-RES-002**: Upload File PDF (FR-PUB-002)
- **US-RES-003**: Sửa Bài Báo Nháp (FR-PUB-004)
- **US-RES-004**: Xóa Bài Báo Nháp (FR-PUB-005)
- **US-RES-005**: Xem Danh Sách Bài Báo (FR-PUB-006)
- **US-RES-008**: Xem Chi Tiết Bài Báo (FR-PUB-010)
- **US-RES-009**: Download File PDF (FR-PUB-011)

### Approval Workflow
- **US-RES-010**: Nộp Xét Duyệt (FR-APR-001)
- **US-RES-011**: Xem Trạng Thái Xét Duyệt (FR-APR-002)
- **US-RES-012**: Chỉnh Sửa Theo Yêu Cầu (FR-APR-003)

**Total**: 10 P0 stories

---

## Faculty Reviewer (6 Stories)

### Approval Workflow
- **US-FCR-001**: Xem Dashboard Chờ Duyệt Khoa (FR-APR-005)
- **US-FCR-002**: Phê Duyệt Bài Báo (FR-APR-006)
- **US-FCR-003**: Yêu Cầu Bổ Sung (FR-APR-007)
- **US-FCR-004**: Từ Chối Bài Báo (FR-APR-008)
- **US-FCR-005**: Xem Lịch Sử Xét Duyệt (FR-APR-015)
- **US-FCR-006**: Nhận Thông Báo Email (FR-APR-016)

---

## University Reviewer (6 Stories)

### Approval Workflow
- **US-UNR-001**: Xem Dashboard Chờ Duyệt Trường (FR-APR-010)
- **US-UNR-002**: Xem Ý Kiến Cấp Khoa (FR-APR-011)
- **US-UNR-003**: Phê Duyệt và Công Bố (FR-APR-012)
- **US-UNR-004**: Từ Chối Cấp Trường (FR-APR-013)
- **US-UNR-005**: Xem Audit Trail (FR-APR-015)
- **US-UNR-006**: Nhận Thông Báo Email (FR-APR-016)

---

## SuperAdmin (8 Stories)

### Admin & User Management
- **US-ADM-001**: Quản Lý Người Dùng (CRUD) (FR-ADM-001)
- **US-ADM-002**: Gán Vai Trò Người Dùng (FR-ADM-002)
- **US-ADM-003**: Quản Lý Khoa/Đơn Vị (FR-ADM-003)
- **US-ADM-004**: Cấu Hình LDAP/AD (FR-ADM-004)
- **US-ADM-005**: Cấu Hình Email (FR-ADM-005)
- **US-ADM-006**: Xem Audit Logs (FR-ADM-006)
- **US-ADM-007**: Backup và Restore (FR-ADM-007)
- **US-ADM-010**: Thao Tác Hàng Loạt (FR-ADM-010)

---

## Public Visitor (2 Stories)

### Search & Browse
- **US-VIW-005**: Phân Trang Kết Quả (FR-SEA-005)
- **US-VIW-006**: Xem Chi Tiết Công Trình (FR-SEA-006)

---

## MVP Implementation Priority

### Sprint 1: Core Publication Management + Workflow
**Duration**: 2-3 weeks

**Features**:
- Publication CRUD (US-RES-001 to US-RES-009)
- Submit for review (US-RES-010, US-RES-011, US-RES-012)

**Deliverables**:
- Researchers can create, edit, delete publications
- Researchers can submit publications
- Basic draft workflow

---

### Sprint 2: Faculty Review Workflow
**Duration**: 2 weeks

**Features**:
- Faculty reviewer dashboard (US-FCR-001)
- Approve/Reject/Request Revision (US-FCR-002, US-FCR-003, US-FCR-004)
- Email notifications (US-FCR-006)
- Audit trail (US-FCR-005)

**Deliverables**:
- Faculty reviewers can review publications
- 2-level approval workflow functioning

---

### Sprint 3: University Review + Admin
**Duration**: 2 weeks

**Features**:
- University reviewer dashboard (US-UNR-001 to US-UNR-006)
- Admin user management (US-ADM-001 to US-ADM-007, US-ADM-010)

**Deliverables**:
- Complete approval workflow
- System administration functional
- LDAP authentication working

---

### Sprint 4: Public Access
**Duration**: 1 week

**Features**:
- Public search with pagination (US-VIW-005, US-VIW-006)

**Deliverables**:
- Public can view published publications
- Basic search functionality

---

## Acceptance Criteria Summary

### Definition of Done for P0 Stories

✅ **Code Complete**:
- Unit tests pass
- Integration tests pass
- Code reviewed and merged

✅ **Functional**:
- Acceptance criteria met
- Manual testing complete
- Edge cases handled

✅ **Non-Functional**:
- Performance targets met (page load < 2s)
- Security requirements met (LDAP auth, RBAC)
- Audit logging in place

✅ **Documentation**:
- API documentation updated
- User documentation created
- Deployment guide updated

---

## Dependencies

### External Systems (Must Have)
- ✅ LDAP/AD server for authentication
- ✅ Email server (SMTP) for notifications
- ✅ MySQL 8.0+ database

### Technical Stack (P0)
- ✅ Backend: Java Spring Boot 3.x
- ✅ Frontend: React 18 + TypeScript
- ✅ Database: MySQL 8.0+
- ✅ Authentication: LDAP/AD + JWT

---

## Risks & Mitigation

| Risk | Impact | Mitigation |
|------|--------|-----------|
| LDAP integration delay | High | Use mock authentication for development |
| Email server unavailable | Medium | Queue emails, retry mechanism |
| File storage issues | Medium | Implement local storage first, cloud later |
| State machine complexity | High | Thorough unit testing, state validation |

---

**Tài liệu liên quan**:
- [All User Stories by Role](../By_Role/)
- [Functional Requirements](../../03_Requirements/Functional/)
- [P1 Should Have Stories](./p1_should_have.md)
