# Detailed-Level Use Cases - README

> 📁 **Level**: Detailed-Level Use Cases  
> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Mục đích**: Specifications chi tiết cho 20 use cases P0 quan trọng nhất

---

## 📊 Tổng Quan

Detailed-level use cases cung cấp specifications đầy đủ cho các P0 (Must Have) use cases quan trọng nhất, bao gồm:
- Preconditions & Postconditions chi tiết
- Main Flow với các bước cụ thể
- **Alternative Flows**: Các kịch bản khác nhau
- **Exception Flows**: Xử lý lỗi
- Business Rules đầy đủ

> [!NOTE]
> **Tại sao chỉ 20 use cases?**
> Detailed specs rất chi tiết và tốn công tạo. Chúng tôi tập trung vào 20 use cases P0 CRITICAL nhất cho MVP. Các use cases P1/P2 có medium-level specs là đủ.

---

## 📋 20 Detailed-Level Use Cases

### Module 1: Publication Management (5 specs)

| UC ID | Name | File |
|-------|------|------|
| UC-D1-01 | Create Publication | uc_d1_01_create_publication.md |
| UC-D1-02 | Edit Publication | uc_d1_02_edit_publication.md |
| UC-D1-03 | Upload PDF | uc_d1_03_upload_pdf.md |
| UC-D1-04 | View Publication List | uc_d1_04_view_publication_list.md |
| UC-D1-05 | Delete Publication | uc_d1_05_delete_publication.md |

### Module 2: Approval Workflow (7 specs)

| UC ID | Name | File |
|-------|------|------|
| UC-D2-01 | Submit for Review | uc_d2_01_submit_for_review.md |
| UC-D2-02 | Faculty Approve | uc_d2_02_faculty_approve.md |
| UC-D2-03 | Faculty Request Revision | uc_d2_03_faculty_request_revision.md |
| UC-D2-04 | Faculty Reject | uc_d2_04_faculty_reject.md |
| UC-D2-05 | University Approve & Publish | uc_d2_05_university_approve_publish.md |
| UC-D2-06 | Track Review Status | uc_d2_06_track_review_status.md |
| UC-D2-07 | Email Notifications | uc_d2_07_email_notifications.md |

### Module 3: Search & Browse (3 specs)

| UC ID | Name | File |
|-------|------|------|
| UC-D3-01 | Basic Search | uc_d3_01_basic_search.md |
| UC-D3-02 | Advanced Search | uc_d3_02_advanced_search.md |
| UC-D3-03 | Filter Results | uc_d3_03_filter_results.md |

### Module 6: Admin & User Management (5 specs)

| UC ID | Name | File |
|-------|------|------|
| UC-D6-01 | Create User | uc_d6_01_create_user.md |
| UC-D6-02 | Assign Roles | uc_d6_02_assign_roles.md |
| UC-D6-03 | Configure LDAP | uc_d6_03_configure_ldap.md |
| UC-D6-04 | View Audit Logs | uc_d6_04_view_audit_logs.md |
| UC-D6-05 | Backup System | uc_d6_05_backup_system.md |

---

## 📖 Detailed Spec Format

Mỗi detailed spec bao gồm:

```markdown
# UC-DX-XX: [Use Case Name]

## Overview
[Summary, priority, actors, related artifacts]

## Preconditions
[Detailed system and user state requirements]

## Main Flow
1. [Step 1 with system behavior]
2. [Step 2 with validations]
...

## Alternative Flows

### Alt-1: [Scenario Name]
**When**: [Condition]
**Then**: [Different path]

### Alt-2: [Another Scenario]
...

## Exception Flows

### Exc-1: [Error Scenario]
**When**: [Error condition]
**System**: [Error handling]

## Postconditions
**Success**: [State after success]
**Failure**: [State after failure]

## Business Rules
- BR-XXX-001: [Detailed rule]
...

## UI Mockup (if applicable)
[Diagram or screenshot]

## Sequence Diagram (if complex)
[Mermaid sequence diagram]
```

---

## 🎯 Lợi Ích Của Detailed Specs

1. **For Developers**: Clear implementation guide
2. **For Testers**: Test scenarios and edge cases
3. **For Designers**: UI flow requirements
4. **For Documentation**: User manual content

---

## 🚧 Trạng Thái

> [!IMPORTANT]
> **Detailed specs sẽ được tạo trong Phase 2**
> 
> Do thời gian hạn chế, chúng tôi đã tạo:
> - ✅ Main README và structure
> - ✅ 6 High-Level UCs (complete)
> - ✅ 54 Medium-Level UCs (complete) 
> - 📝 20 Detailed-Level UCs (template và structure đã có, content sẽ được tạo khi implement MVP)
>
> Medium-level specs đã đủ chi tiết để bắt đầu development. Detailed specs sẽ được tạo song song với implementation.

---

**Tài liệu liên quan**:
- [Medium-Level Use Cases](../Medium_Level/)
- [High-Level Use Cases](../High_Level/)
- [Sequence Diagrams](../Sequence_Diagrams/) (để tạo trong Phase 2)
- [Activity Diagrams](../Activity_Diagrams/) (để tạo trong Phase 2)
