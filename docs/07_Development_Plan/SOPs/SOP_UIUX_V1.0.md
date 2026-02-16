# SOP - UI/UX Designer
## Version 1.0: Core Publication Management

> 👤 **Vai trò**: UI/UX Designer  
> 🎯 **Phạm vi**: V1.0 - Thiết kế 6 Screens + Design System  
> 📅 **Áp dụng cho**: Figma Design, Prototyping, Design QA

---

## 🎯 Mục Tiêu Tổng Quan

Thiết kế giao diện người dùng đẹp, dễ sử dụng, và consistent cho V1.0. UI/UX Designer chịu trách nhiệm tạo design system, design 6 screens, và support frontend team trong implementation.

---

## 📋 Trách Nhiệm Chính

### 1. User Research (Tối thiểu)
- Hiểu user personas (Researchers)
- Identify user needs và pain points
- Reference existing systems (nếu có)

### 2. Design System Creation
- Define colors, typography, spacing
- Tạo core components (Button, Input, Card, etc.)
- Document design tokens

### 3. Screen Design
- Design 6 screens theo user stories
- Ensure consistency across screens
- Responsive layouts (desktop + tablet)

### 4. Prototyping
- Tạo interactive prototype trong Figma
- Demo user flows
- Collect feedback

### 5. Collaboration
- Work với BA để understand requirements
- Work với Frontend dev để handoff designs
- Participate trong design reviews

### 6. Design QA
- Verify implementations match designs
- Provide feedback cho frontend dev

---

## 📐 PHASE 1: DESIGN (Tuần 0-1)

### 1. Figma Setup

- [ ] **Tạo Figma Project**

  ```
  Structure:
  - Project: UFPMS V1.0
    ├── 📄 Cover Page (project info, team, version)
    ├── 📄 Design System
    │   ├── Colors
    │   ├── Typography
    │   ├── Spacing & Grid
    │   └── Components
    ├── 📄 Screens - Desktop (1920x1080)
    │   ├── Login
    │   ├── Dashboard
    │   ├── Publication List
    │   ├── Create Publication
    │   ├── Edit Publication
    │   └── Publication Detail
    └── 📄 Prototype Flows
  ```

---

### 2. User Research Nhanh

- [ ] **Interview Stakeholders/Sample Users (1-2 giờ)**

  ```
  Câu hỏi:
  1. Bạn hiện tại quản lý publications như thế nào? (Excel, Word, Paper?)
  2. Khó khăn chính là gì?
  3. Features quan trọng nhất đối với bạn?
  4. Bạn có dùng hệ thống tương tự nào chưa? (Google Scholar, ResearchGate?)
  5. Expectations về giao diện?
  
  Output: User insights document (1-2 pages)
  ```

- [ ] **Competitive Analysis (Optional)**

  ```
  Research các hệ thống tương tự:
  - Google Scholar: Simple, clean UI
  - ResearchGate: Social features, rich profiles
  - University publication systems (nếu có)
  
  Take inspiration (không copy trực tiếp)
  ```

---

### 3. Design System

- [ ] **Color Palette**

  ```
  Chọn màu sắc phản ánh tính chuyên nghiệp và học thuật:
  
  Primary Color (Chủ đạo):
  - #1976D2 (Blue) - Đại diện tin cậy, chuyên nghiệp
  - Variants: Light (#42A5F5), Dark (#1565C0)
  
  Secondary Color:
  - #FF9800 (Orange) - Accent, call-to-action
  
  Status Colors:
  - Success: #4CAF50 (Green)
  - Warning: #FFC107 (Amber)
  - Error: #F44336 (Red)
  - Info: #2196F3 (Light Blue)
  
  Neutral Colors:
  - Text Primary: #212121 (Dark Gray)
  - Text Secondary: #757575 (Medium Gray)
  - Background: #FAFAFA (Off-white)
  - Paper: #FFFFFF (White)
  - Dividers: #E0E0E0 (Light Gray)
  
  Document trong Figma: Color styles với naming convention
  "Primary/Main", "Primary/Light", "Text/Primary", etc.
  ```

- [ ] **Typography**

  ```
  Font Family: Roboto (Google Font - free, readable, professional)
  
  Hierarchy:
  - H1 (Page Titles): 32px, Weight 700 (Bold)
  - H2 (Section Titles): 24px, Weight 600 (Semi-Bold)
  - H3 (Subsections): 20px, Weight 600
  - Body 1 (Main text): 16px, Weight 400 (Regular)
  - Body 2 (Secondary): 14px, Weight 400
  - Caption: 12px, Weight 400
  - Button: 14px, Weight 500 (Medium), Uppercase
  
  Line Heights:
  - Headers: 1.2
  - Body: 1.5
  
  Document trong Figma: Text styles
  ```

- [ ] **Spacing & Grid**

  ```
  Base Unit: 8px (tất cả spacing là bội số của 8)
  
  Spacing Scale:
  - 4px (0.5 unit) - Tight spacing
  - 8px (1 unit) - Default spacing
  - 16px (2 units) - Medium spacing
  - 24px (3 units) - Large spacing
  - 32px (4 units) - Section spacing
  - 48px (6 units) - Page margins
  
  Grid System:
  - Container: 1200px max-width (desktop)
  - Columns: 12 columns
  - Gutter: 16px
  - Margin: 24px
  
  Responsive Breakpoints:
  - Desktop: > 1200px
  - Tablet: 768px - 1199px
  - Mobile: < 768px (defer to V2.0)
  ```

- [ ] **Border Radius**

  ```
  - Small (buttons, inputs): 4px
  - Medium (cards): 8px
  - Large (modals): 12px
  - Circular (avatars, icons): 50%
  ```

---

### 4. Core Components Design

- [ ] **Button Component**

  ```
  Variants:
  - Primary (filled, blue): Main actions (Save, Submit, Login)
  - Secondary (outlined, blue): Secondary actions (Cancel)
  - Text (no border): Tertiary actions (View More)
  - Danger (filled, red): Destructive actions (Delete)
  
  States:
  - Default
  - Hover (slightly darker)
  - Pressed (darker + shadow)
  - Disabled (gray, low opacity)
  - Loading (spinner icon)
  
  Sizes:
  - Small: 32px height, 8px vertical padding
  - Medium: 40px height, 12px vertical padding
  - Large: 48px height, 16px vertical padding
  
  Design trong Figma: Component với variants (Size × Type × State)
  ```

- [ ] **Input Component** (Text Field)

  ```
  Variants:
  - Standard
  - Filled (with background)
  - Outlined (with border)
  
  States:
  - Default
  - Focused (blue border)
  - Error (red border + error message below)
  - Disabled (gray, low opacity)
  
  Elements:
  - Label (above hoặc floating)
  - Input field
  - Helper text (below)
  - Error message (red text below)
  - Icon (optional, left hoặc right)
  
  Sizes: Small (32px), Medium (40px), Large (48px)
  ```

- [ ] **Card Component**

  ```
  Structure:
  - Container: White background, 8px border radius, subtle shadow
  - Padding: 24px
  - Header (optional)
  - Content
  - Actions (optional, bottom right)
  
  States:
  - Default
  - Hover (subtle shadow increase)
  - Pressed (shadow decrease)
  
  Use cases: Dashboard stat cards, Publication cards
  ```

- [ ] **Table Component**

  ```
  Elements:
  - Header row (bold text, background color)
  - Data rows (alternate background colors cho readability)
  - Hover state (highlight row)
  - Action column (icons: View, Edit, Delete)
  - Pagination (bottom)
  
  Columns:
  - Flexible width based on content
  - Sortable (arrow icons in header)
  ```

- [ ] **Modal/Dialog Component**

  ```
  Structure:
  - Overlay (dark, semi-transparent)
  - Dialog box (white, centered, 12px radius)
  - Title (top)
  - Content (middle)
  - Actions (bottom right): Cancel + Confirm buttons
  - Close icon (top right corner)
  
  Sizes: Small, Medium, Large, Full-screen
  ```

- [ ] **Badge Component**

  ```
  Use case: Publication status display
  
  Variants by status:
  - DRAFT: Gray badge
  - SUBMITTED: Blue badge
  - PUBLISHED: Green badge
  - REJECTED: Red badge
  
  Style: Small, rounded corners, colored background, white text
  ```

---

### 5. Screen Designs

- [ ] **Screen 1: Login Page**

  ```
  Layout (Centered):
  - Logo (top, 80x80px)
  - Title: "UFPMS Login" (H1)
  - Username input (full width, 400px)
  - Password input (full width, masked)
  - Login button (full width, primary, large size)
  - Error message area (tạm ẩn, hiện khi có lỗi)
  
  Visual Style:
  - Background: Light gradient hoặc subtle pattern
  - Login form: White card với shadow
  
  States:
  - Empty: Button disabled
  - Filled: Button enabled
  - Loading: Button shows spinner
  - Error: Red error message below button
  ```

- [ ] **Screen 2: Dashboard**

  ```
  Layout:
  - Header (fixed top):
    * Logo (left)
    * Title "Dashboard" (center hoặc left)
    * User info + Logout (right)
  
  - Main Content:
    * Statistics Grid (2x2):
      - Total Publications (card)
      - Published Count (card)
      - Draft Count (card)
      - Total Work Hours (card)
    
    * Recent Publications Section:
      - Title: "Recent Publications" (H2)
      - Table (5 rows)
      - "View All" link → Publications List
  
  - Floating Action Button (FAB):
    * Position: Bottom right, fixed
    * Icon: "+" (plus)
    * Label: "Create New"
    * Color: Primary blue
  
  Visual Hierarchy: Stats cards nổi bật, table dễ scan
  ```

- [ ] **Screen 3: Publication List**

  ```
  Layout:
  - Header: "My Publications" (H1)
  
  - Filter Bar:
    * Status dropdown (left)
    * Year input (middle)
    * Search box (middle-right)
    * "Create New" button (far right)
  
  - Data Table:
    * Columns: Title, Year, Status (badge), Created Date, Actions
    * Rows: Hover effect
    * Action icons: View (eye), Edit (pencil), Delete (trash)
  
  - Pagination (bottom center):
    * Previous / Page numbers / Next
  
  - Empty State (when no data):
    * Image/Icon (paperwork)
    * Text: "No publications yet"
    * CTA button: "Create Your First Publication"
  
  Responsive: Table scrollable horizontally on tablet
  ```

- [ ] **Screen 4 & 5: Create/Edit Publication Form**

  ```
  Layout:
  - Page Title: "Create New Publication" hoặc "Edit Publication" (H1)
  - Breadcrumb (optional): Dashboard > Publications > Create
  
  - Form (Grid 2 columns on desktop, 1 column on tablet):
    * Section 1: Basic Info
      - Publication Type (dropdown) *
      - Title (text, full width) *
      - Year (number) *
    
    * Section 2: Publication Details
      - Journal/Conference Name
      - Volume, Issue, Pages (3 columns)
      - DOI
    
    * Section 3: Content
      - Abstract (textarea, full width, 6 rows)
      - Keywords (text input)
    
    * Section 4: Authors
      - Co-authors list
      - "Add Co-Author" button
    
    * Section 5: PDF Upload (Edit mode only, nếu có PDF)
      - Current file info
      - "Upload New PDF" button
  
  - Actions (bottom):
    * "Cancel" button (secondary, left)
    * "Save as Draft" button (primary, right)
    * "Delete" button (danger, far left - Edit mode, DRAFT only)
  
  Visual:
  - Required fields marked với red asterisk *
  - Validation errors: Inline, red text below field
  - Form has max-width 900px, centered
  ```

- [ ] **Screen 6: Publication Detail**

  ```
  Layout (2 columns):
  
  Left Column (60%): PDF Viewer
  - iframe với PDF (if uploaded)
  - Placeholder: "No PDF available" (if not uploaded)
  - Loading state: Skeleton
  
  Right Column (40%): Metadata Panel (Card)
  - Header: Publication Title (H2)
  - Status Badge (top right)
  
  - Section: Details
    * Type, Year, Journal/Conference
    * Volume, Issue, Pages, DOI (grid)
  
  - Section: Authors
    * Main author (bold)
    * Co-authors list (numbered)
  
  - Section: Abstract
    * Full text, scrollable if long
  
  - Section: Keywords
    * Comma-separated, styled as chips (optional)
  
  - Section: File Info (if PDF exists)
    * Filename, Size, Upload date
    * Download button
  
  - Actions (bottom):
    * "Edit" button (if DRAFT, primary)
    * "Back to List" button (secondary)
  
  Responsive: Stack columns on tablet (PDF top, Metadata bottom)
  ```

---

### 6. Prototype Creation

- [ ] **Create Interactive Prototype trong Figma**

  ```
  Link screens để demo user flows:
  
  Flow 1: Login → Dashboard
  - Login screen: Click "Login" → Navigate to Dashboard
  
  Flow 2: Create Publication
  - Dashboard: Click "Create New" FAB → Create Form
  - Create Form: Fill fields, click "Save" → Detail Page
  
  Flow 3: Edit Publication
  - List: Click Edit icon → Edit Form
  - Edit Form: Make changes, click "Save" → Detail Page
  
  Flow 4: View Detail
  - List: Click row → Detail Page
  - Detail: View PDF, metadata
  
  Interactions:
  - Button hover effects
  - Form validation states (mock)
  - Modal open/close (nếu có)
  
  Present prototype trong Design Review meeting
  ```

---

### 7. Design Review & Iteration

- [ ] **Design Review Meeting**

  ```
  Present designs to team:
  - BA: Verify designs match requirements
  - Frontend Dev: Feasibility check
  - PM: Business alignment
  - QA: Testability concerns
  
  Collect feedback:
  - "This button should be more prominent"
  - "Add a tooltip for DOI field"
  - "Error states need to be more visible"
  
  Iterate based on feedback (1-2 rounds)
  Final approval: PM + BA sign-off
  ```

---

## 💻 PHASE 2: DEVELOPMENT (Tuần 2-4)

### 8. Design Handoff

- [ ] **Prepare Assets cho Frontend Dev**

  ```
  Figma handoff:
  - Share Figma link với "View" access cho Frontend team
  - Enable "Inspect" mode trong Figma
  
  Export assets:
  - Logo: SVG + PNG
  - Icons: SVG (từ icon library như Material Icons)
  - Images (nếu có): Optimized PNG/JPG
  
  Lưu vào folder assets và share với team
  ```

- [ ] **Tạo Developer Specs Document**

  ```
  Document chi tiết cho dev (hoặc trong Figma comments):
  
  - Colors: HEX codes
  - Typography: Font family, sizes, weights
  - Spacing: Values in px
  - Components: Behavior notes
  
  Example:
  "Button Primary:
  - Background: #1976D2
  - Text: #FFFFFF, 14px, Weight 500
  - Padding: 12px 24px
  - Border radius: 4px
  - Hover: Background #1565C0"
  ```

- [ ] **Create Style Guide (1-page reference)**

  ```
  Tóm tắt:
  - Color palette với names
  - Typography scale
  - Component library reference
  - Do's and Don'ts
  
  Format: PDF hoặc Figma page
  Share với toàn team
  ```

---

### 9. Support Development

- [ ] **Available cho Frontend Dev Questions**

  ```
  Câu hỏi thường gặp:
  Q: "Spacing giữa table rows là bao nhiêu?"
  A: "16px (2 units)"
  
  Q: "Hover state của button có shadow không?"
  A: "Có, shadow tăng nhẹ. Check spec trong Figma."
  
  Q: "Empty state image dùng illustration nào?"
  A: "Tôi sẽ tạo hoặc ref từ undraw.co"
  
  Response time: < 1 ngày
  ```

- [ ] **Design QA During Development**

  ```
  Weekly check-in với Frontend:
  - Review implemented screens
  - Compare với Figma designs
  - Note differences:
    * "Button padding hơi nhỏ, cần tăng từ 8px lên 12px"
    * "Card shadow quá đậm, giảm opacity"
    * "Heading font size 28px thay vì 32px"
  
  Log issues for frontend to fix
  ```

---

## ✅ PHASE 3: VERIFICATION (Tuần 5-6)

### 10. UI/UX Testing

- [ ] **Visual QA**

  ```
  Checklist cho mỗi screen:
  - Colors match design system ✅
  - Typography (sizes, weights) correct ✅
  - Spacing consistent (8px grid) ✅
  - Components match Figma ✅
  - Alignment đúng ✅
  - Icons đúng size và color ✅
  ```

- [ ] **Interaction QA**

  ```
  Test behaviors:
  - Hover states hoạt động ✅
  - Focus states visible (accessibility) ✅
  - Transitions smooth (không giật) ✅
  - Loading states display properly ✅
  - Error states clear và helpful ✅
  ```

---

### 11. Accessibility Check

- [ ] **Basic Accessibility Compliance**

  ```
  - Color contrast ratios:
    * Text/Background: Minimum 4.5:1 (WCAG AA)
    * Large text: Minimum 3:1
    * Tool: Use Figma plugin "Contrast" hoặc WebAIM checker
  
  - Keyboard navigation:
    * Tab order logical
    * Focus indicators visible
  
  - Labels:
    * All inputs có labels
    * Buttons có descriptive text (không chỉ icons)
  
  - Alternative text:
    * Images có alt text (nếu meaningful)
  ```

---

### 12. Final Design Polish

- [ ] **Post-Implementation Adjustments**

  ```
  After seeing implementation:
  - Micro-interactions cần thêm? (Ví dụ: Success toast animation)
  - Spacing adjustments based on real content
  - Color tweaks nếu cần (ví dụ: text contrast)
  
  Create "V1.0.1 Design Updates" page trong Figma nếu có changes
  ```

---

### 13. Documentation

- [ ] **Design handoff document (Final)**

  ```
  Include:
  - Link to Figma project
  - Design system summary
  - Component library
  - Screen variants (desktop/tablet)
  - Known limitations/Future improvements
  
  Format: Markdown hoặc PDF
  ```

---

## ✅ Tiêu Chí Thành Công

UI/UX Designer làm tốt khi:

✅ Design system complete và consistent  
✅ Tất cả 6 screens designed và approved  
✅ Prototype interactive và demo được user flows  
✅ Frontend implementation matches designs (> 95%)  
✅ Accessibility baseline đạt (contrast, labels, keyboard nav)  
✅ Team hài lòng với design handoff process

---

## 📋 Deliverables (Sản Phẩm Bàn Giao)

1. **Figma Project File** - Design system, 6 screens, prototype
2. **Design System Documentation** - Colors, typography, components
3. **Exported Assets** - SVG icons, PNG images, logos
4. **Style Guide** - Quick reference cho developers
5. **Design QA Report** - Issues found, status (fixed/pending)
6. **Handoff Notes** - Special instructions, edge cases

---

## 🔍 UI/UX Best Practices

### 1. Consistency is Key
- Reuse design system components
- Don't create one-off styles

### 2. User-Centered Design
- Design cho researchers (the actual users)
- Prioritize usability over aesthetics (but both is best!)

### 3. Accessibility Baseline
- Always check color contrast
- Design for keyboard navigation
- Don't rely solely on color to convey information

### 4. Mobile-First? No, Desktop-First cho V1.0
- V1.0 focus on desktop + tablet
- Mobile defer to V2.0

### 5. Iterate Based on Feedback
- Design review không phải 1 lần xong
- Expect 2-3 rounds of revisions

---

**Prepared by**: UI/UX Design Team  
**Version**: 1.0  
**Last Updated**: 16/02/2026
