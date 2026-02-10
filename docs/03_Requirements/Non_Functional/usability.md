# Yêu Cầu Khả Dụng - UsabilityRequirements

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Danh mục**: Non-Functional Requirements

---

## 1. Learnability (Dễ Học)

### NFR-USA-001: Nhập Bài Báo trong < 5 Phút
**Target**: Giảng viên mới có thể nhập bài báo đầu tiên trong < 5 phút

**Measures**:
- Form đơn giản, rõ ràng
- Required fields có đánh dấu *
- Tooltips cho các field phức tạp
- Auto-save every 30s

---

### NFR-USA-002: Onboarding Tutorial
**Requirement**: First-time users thấy tutorial

**Content**:
- Video 2-3 phút (optional)
- Step-by-step guide
- "Skip for now" option

---

## 2. Efficiency (Hiệu Quả)

### NFR-USA-010: Số Click Tối Thiểu
**Targets**:
- Tạo bài báo mới: < 3 clicks
- Nộp xét duyệt: 1 click (từ publication detail)
- Duyệt công trình: 2-3 clicks
- Tạo báo cáo: 3-4 clicks

---

### NFR-USA-011: Keyboard Shortcuts
**Support shortcuts** (optional):
- Ctrl+S: Save
- Ctrl+Enter: Submit form
- Esc: Close dialog

---

## 3. Error Prevention & Recovery

### NFR-USA-020: Validation Real-time
**Requirement**: Validate ngay khi blur khỏi field

**Examples**:
- Email format
- DOI format
- Required fields

---

### NFR-USA-021: Confirmation Dialogs
**Show confirmation cho**:
- Delete publication
- Reject publication
- Submit for review

**Format**: "Are you sure? [Action] cannot be undone."

---

### NFR-USA-022: Auto-save Drafts
**Requirement**: Tự động lưu nháp mỗi 30s

**Indicator**: "Saving..." / "Saved at HH:MM"

---

## 4. Visual Design

### NFR-USA-030: Responsive Design
**Support**:
- Desktop: 1920x1080, 1366x768
- Tablet: 768x1024 (iPad)
- Mobile: 375x667 (iPhone), 360x640 (Android)

**Breakpoints**:
- Mobile: < 768px
- Tablet: 768px - 1024px
- Desktop: > 1024px

---

### NFR-USA-031: Consistent UI
**Design system**:
- Material-UI components
- Consistent colors, fonts, spacing
- Reusable components

---

### NFR-USA-032: Visual Feedback
**Requirements**:
- Loading spinners cho async operations
- Success/Error toasts
- Progress bars cho uploads
- Skeleton screens (loading placeholders)

---

## 5. Accessibility (A11Y)

### NFR-USA-040: WCAG 2.1 Level AA
**Requirements**:
- Color contrast ratio: >= 4.5:1 (text)
- Keyboard navigation: Tất cả functions accessible
- Screen reader: ARIA labels
- Focus indicators: Visible

---

### NFR-USA-041: Alt Text for Images
**Requirement**: Mọi image có alt text

---

## 6. Internationalization (i18n)

### NFR-USA-050: Ngôn Ngữ Tiếng Việt
**Requirement**: UI, error messages, emails đều tiếng Việt

**Encoding**: UTF-8

**Future**: Support English (Phase 2)

---

## 7. Help & Documentation

### NFR-USA-060: Inline Help
**Requirements**:
- Tooltips cho các field
- Help icon (?) bên cạnh complex features
- Link đến documentation

---

### NFR-USA-061: FAQ Section
**Topics**:
- Làm sao để thêm bài báo?
- Làm sao kiểm tra trạng thái xét duyệt?
- Làm sao tạo báo cáo?
- Làm sao upload PDF?

---

## 8. Search & Navigation

### NFR-USA-070: Search Auto-complete
**Requirement**: Gợi ý khi gõ >= 3 ký tự

**Suggest**:
- Publication titles
- Author names
- Keywords

---

### NFR-USA-071: Breadcrumbs
**Show navigation path**:
Example: Home > Publications > Publication Detail

---

## 9. Feedback Mechanisms

### NFR-USA-080: User Feedback Form
**Location**: Footer hoặc Help menu

**Fields**:
- Issue type (Bug, Feature request, Question)
- Description
- Screenshot upload (optional)

---

## 10. Performance Perception

### NFR-USA-090: Progress Indicators
**For long operations**:
- PDF upload: Progress bar
- Report generation: "Processing... 50%"
- Search: Loading spinner

---

## 11. Usability Testing

### NFR-USA-100: User Testing
**Frequency**: Before major releases

**Scenarios**:
1. Researcher: Thêm bài báo mới
2. Faculty Reviewer: Xét duyệt công trình
3. Viewer: Tìm kiếm giảng viên theo lĩnh vực

**Metrics**:
- Task completion rate: > 90%
- Task completion time
- User satisfaction: > 4/5

---

**Tài liệu liên quan**:
- [User Needs](../../02_System_Clarification/User_Analysis/user_needs.md)
- [User Groups](../../02_System_Clarification/User_Analysis/user_groups.md)
