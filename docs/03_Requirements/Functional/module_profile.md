# Module 4: Researcher Profile - Yêu Cầu Chức Năng

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Module**: Profile Công khai Giảng viên  
> 👥 **Users**: Researcher (edit), Tất cả (view)

---

## 1. Functional Requirements

### FR-PRO-001: Profile Công khai
**Priority**: 🟡 P1 - Should Have

**Acceptance Criteria**:
```
GIVEN giảng viên có ít nhất 1 publication PUBLISHED
WHEN truy cập /profile/:username
THEN hiển thị:
  - Ảnh đại diện
  - Tên, Chức danh, Khoa
  - Contact (email, ORCID)
  - Bio/Research interests
  - Danh sách bài báo (PUBLISHED only)
  - Biểu đồ năng suất theo năm
  - Word cloud từ keywords
```

---

### FR-PRO-002: Edit Profile
**Priority**: 🟡 P1 - Should Have

**Editable fields**:
- Profile photo
- Bio (max 500 chars)
- Research interests
- ORCID
- Google Scholar link
- Personal website

---

### FR-PRO-003: Publication List on Profile
**Priority**: 🟡 P1 - Should Have

**Features**:
- Sort by year (newest first)
- Filter by type (Journal/Conference)
- Show: Title, Journal, Year, DOI link
- Click to view details

---

### FR-PRO-004: Analytics Chart
**Priority**: 🟢 P2 - Nice to Have

**Charts**:
- Publications per year (bar chart)
- Publications by journal type (pie chart)
- Most productive years

---

### FR-PRO-005: Research Field Word Cloud
**Priority**: 🟢 P2 - Nice to Have

**Generate từ**:
- Keywords của tất cả publications
- Frequent words in Abstract
- Font size based on frequency

---

### FR-PRO-006: Public URL
**Priority**: 🟡 P1 - Should Have

**URL format**:
```
https://ufpms.university.edu.vn/profile/[username]
```

**SEO**:
- Meta tags with researcher name
- Open Graph for social sharing

---

## 2. Non-Functional Requirements

**Performance**:
- Profile load time < 2s
- Cache heavily (update khi có public ation mới)

---

**Tài liệu liên quan**:
- [Module 3: Search](./module_search.md)
