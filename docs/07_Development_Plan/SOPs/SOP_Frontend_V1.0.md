# SOP - Frontend Developer
## Version 1.0: Core Publication Management

> 👤 **Vai trò**: Frontend Developer  
> 🎯 **Phạm vi**: V1.0 - Phát triển giao diện CRUD cho Publications  
> 📅 **Áp dụng cho**: React + TypeScript + MUI

---

## 🎯 Mục Tiêu Tổng Quan

Phát triển giao diện người dùng (UI) cho V1.0 theo designs từ UI/UX team, đảm bảo UI responsive, performant, và có UX mượt mà. Frontend developer chịu trách nhiệm implement 6 screens và tích hợp với backend APIs.

---

## 📋 Trách Nhiệm Chính

### 1. Triển Khai UI
- Implement 6 screens theo Figma designs
- Đảm bảo pixel-perfect implementation
- Responsive layouts (desktop + tablet)

### 2. Tích Hợp API
- Integrate với backend RESTful APIs
- Xử lý loading states, error states, empty states
- Implement data validation

### 3. Quản Lý State
- Quản lý application state (Redux / Context API / Zustand)
- Xử lý authentication state
- Cache data phù hợp

### 4. Testing
- Viết unit tests cho components
- Viết integration tests cho user flows
- Đảm bảo test coverage > 70%

---

## 📐 PHASE 1: DESIGN

### 1. Thiết Lập Môi Trường Phát Triển

- [ ] **Cài Đặt Công Cụ**
  - [ ] Node.js 18+ (LTS version)
  - [ ] VS Code (hoặc IDE yêu thích)
  - [ ] VS Code Extensions khuyến nghị:
    - ESLint (kiểm tra code quality)
    - Prettier (format code)
    - TypeScript and JavaScript (language support)
    - ES7+ React/Redux/React-Native snippets
  - [ ] Git

- [ ] **Setup React Project**

  **Bước 1: Tạo project bằng Vite (khuyến nghị vì build nhanh)**
  ```bash
  npm create vite@latest ufpms-frontend -- --template react-ts
  cd ufpms-frontend
  npm install
  ```

  **Bước 2: Cài đặt dependencies**
  ```bash
  # UI Framework
  npm install @mui/material @emotion/react @emotion/styled
  
  # Routing
  npm install react-router-dom
  
  # HTTP Client
  npm install axios
  
  # Form handling
  npm install react-hook-form yup @hookform/resolvers
  
  # Data fetching (optional: giúp quản lý API calls tốt hơn)
  npm install @tanstack/react-query
  
  # State management (chọn 1 trong 2)
  npm install zustand   # Nhẹ, đơn giản
  # HOẶC
  npm install @reduxjs/toolkit react-redux  # Đầy đủ tính năng hơn
  
  # Dev dependencies
  npm install -D @types/react @types/react-dom
  npm install -D @testing-library/react @testing-library/jest-dom vitest
  ```

- [ ] **Cấu Trúc Thư Mục Đề Xuất**
  ```
  src/
  ├── components/          # Reusable components
  │   ├── common/          # Button, Input, Card, Modal, etc.
  │   ├── layout/          # Header, Sidebar, Footer
  │   └── publication/     # Publication-specific components
  ├── pages/               # Page components (6 screens)
  │   ├── Login.tsx
  │   ├── Dashboard.tsx
  │   ├── PublicationList.tsx
  │   ├── CreatePublication.tsx
  │   ├── EditPublication.tsx
  │   └── PublicationDetail.tsx
  ├── services/            # API service layer
  │   ├── api.ts           # Axios instance config
  │   ├── authService.ts
  │   └── publicationService.ts
  ├── hooks/               # Custom React hooks
  ├── store/               # State management (Zustand/Redux)
  ├── types/               # TypeScript types, interfaces
  ├── utils/               # Utility functions
  ├── routes/              # Routing configuration
  ├── theme/               # MUI theme customization
  └── App.tsx              # Main app component
  ```

---

### 2. Review Figma Designs

- [ ] **Truy Cập Figma Project**
  - Xin quyền view/comment từ UI/UX designer
  - Review tất cả 6 screens
  - Ghi chú:
    - Color values (HEX codes)
    - Spacing values (padding, margins)
    - Font sizes, font weights
    - Component states (hover, focus, error, disabled)

- [ ] **Export Assets**
  - Download icons (format SVG)
  - Download logos (SVG + PNG nếu cần)
  - Download hình ảnh (nếu có)
  - Lưu vào thư mục `src/assets/`

- [ ] **Clarify với UI/UX Designer**
  - Hỏi về behaviors không rõ:
    - "Khi user click vào đây thì chuyện gì xảy ra?"
    - "Animation này hoạt động như thế nào?"
    - "Validation rules cho field này là gì?"
  - Document câu trả lời để reference sau

---

## 💻 PHASE 2: DEVELOPMENT

### 3. Thiết Lập Foundation

- [ ] **Tạo MUI Theme**

  **Tạo file: src/theme/theme.ts**
  ```
  MÃ GIẢ - Theme Configuration:
  
  Tạo theme với các giá trị từ Figma:
    Palette (màu sắc):
      - primary.main: #1976D2 (từ Figma)
      - secondary.main: #FF9800
      - error.main: #F44336
      - success.main: #4CAF50
      - background.default: #FAFAFA
      - background.paper: #FFFFFF
    
    Typography (chữ):
      - fontFamily: "Roboto", "Helvetica", "Arial", sans-serif
      - h1: { fontSize: '2rem', fontWeight: 700 }
      - h2: { fontSize: '1.5rem', fontWeight: 600 }
      - body1: { fontSize: '1rem' }
    
    Spacing: 8 (base unit = 8px)
    
    Shape:
      - borderRadius: 8
  
  Export theme để sử dụng trong App
  ```

- [ ] **Setup Axios Instance**

  **Tạo file: src/services/api.ts**
  ```
  MÃ GIẢ - Axios Configuration:
  
  Tạo axios instance:
    - baseURL: từ environment variable hoặc 'http://localhost:8080/api'
    - timeout: 10000 (10 giây)
  
  Request interceptor:
    Hàm: thêm JWT token vào mọi request
      1. Lấy token từ localStorage
      2. Nếu có token: Thêm vào header Authorization: "Bearer {token}"
      3. Return config
  
  Response interceptor:
    Hàm: xử lý lỗi global
      1. Nếu response thành công: Return response
      2. Nếu lỗi 401 (Unauthorized):
         - Xóa token khỏi localStorage
         - Redirect về trang login
      3. Return error để component xử lý tiếp
  
  Export axios instance
  ```

- [ ] **TypeScript Types**

  **Tạo file: src/types/publication.ts**
  ```
  MÃ GIẢ - Type Definitions:
  
  Enum PublicationType:
    - JOURNAL
    - CONFERENCE
    - BOOK_CHAPTER
    - OTHER
  
  Enum PublicationStatus:
    - DRAFT
    - SUBMITTED
    - FACULTY_REVIEWING
    - PUBLISHED
    - REJECTED
  
  Interface Publication:
    - id: number
    - title: string
    - publicationType: PublicationType
    - journalName?: string (optional)
    - year: number
    - ... (các fields khác)
    - status: PublicationStatus
    - createdAt: string (ISO date)
    - updatedAt: string
  
  Interface CreatePublicationRequest:
    - title: string
    - publicationType: PublicationType
    - year: number
    - ... (các fields cần thiết để tạo publication)
  
  Export các types
  ```

---

### 4. Common Components

- [ ] **Button Component**

  ```
  MÃ GIẢ - src/components/common/Button.tsx:
  
  Extend MUI Button với customizations:
    - textTransform: 'none' (không uppercase text)
    - borderRadius: từ theme
    - padding: 8px 16px
  
  Props: kế thừa tất cả ButtonProps từ MUI
  ```

- [ ] **Input Component**

  ```
  MÃ GIẢ - src/components/common/Input.tsx:
  
  Wrap MUI TextField với defaults:
    - fullWidth: true
    - variant: "outlined"
  
  Props: kế thừa TextFieldProps từ MUI
  ```

- [ ] **Card Component**

  ```
  MÃ GIẢ - src/components/common/Card.tsx:
  
  Wrap MUI Card với styling:
    - borderRadius từ theme
    - boxShadow: '0 2px 4px rgba(0,0,0,0.1)'
    - padding: 24px (trong CardContent)
  ```

---

### 5. Screen 1: Login Page

- [ ] **Auth Service**

  ```
  MÃ GIẢ - src/services/authService.ts:
  
  Interface LoginRequest: { username, password }
  Interface LoginResponse: { token, user: {...} }
  
  Hàm: login(request)
    1. Gửi POST /api/auth/login với request body
    2. Nhận response: { token, user }
    3. Return response
  
  Hàm: getCurrentUser()
    1. Gửi GET /api/auth/me
    2. Return user info
  ```

- [ ] **Login Page Component**

  ```
  MÃ GIẢ - src/pages/Login.tsx:
  
  State:
    - loading: boolean (đang login hay không)
    - error: string | null (lỗi nếu có)
  
  Form handling: dùng react-hook-form
    - Fields: username, password
    - Validation: required cho cả 2 fields
  
  Hàm: onSubmit(data)
    1. Set loading = true, error = null
    2. Gọi authService.login(data)
    3. Nếu thành công:
       - Lưu token vào localStorage
       - Lưu user info vào localStorage
       - Navigate đến /dashboard
    4. Nếu thất bại:
       - Set error message
    5. Set loading = false
  
  UI Layout:
    - Centered box với width 400px
    - Logo và tiêu đề ở trên
    - Form với username, password inputs
    - Login button (disabled khi loading)
    - Error alert nếu có lỗi
  ```

---

### 6. Screen 2: Dashboard

- [ ] **Dashboard Service**

  ```
  MÃ GIẢ - src/services/dashboardService.ts:
  
  Interface DashboardStats:
    - totalPublications: number
    - publishedCount: number
    - draftCount: number
    - totalWorkHours: number
  
  Hàm: getStats()
    - Gửi GET /api/dashboard/stats
    - Return DashboardStats
  ```

- [ ] **Dashboard Page**

  ```
  MÃ GIẢ - src/pages/Dashboard.tsx:
  
  Data fetching: dùng React Query hoặc useEffect + useState
    - Gọi dashboardService.getStats()
    - Loading state: hiện skeleton/spinner
    - Error state: hiện error message
  
  UI Layout:
    - Header: "Dashboard" title
    - Grid 2x2 cho 4 statistics cards:
      * Card 1: Total Publications
      * Card 2: Published Count (màu xanh)
      * Card 3: Draft Count (màu vàng)
      * Card 4: Total Work Hours (màu xanh dương)
    - Recent Publications section:
      * Title: "Recent Publications"
      * Table với 5 publications gần nhất
      * Link "View All" → navigate đến /publications
    - Floating Action Button: "Create New" (góc dưới phải)
  ```

---

### 7. Screen 3: Publication List

- [ ] **Publication Service**

  ```
  MÃ GIẢ - src/services/publicationService.ts:
  
  Hàm: list(params)
    - Params: { status?, year?, page?, size? }
    - Gửi GET /api/publications với query params
    - Return: { content: Publication[], totalPages: number }
  
  Hàm: get(id)
    - Gửi GET /api/publications/{id}
    - Return: Publication
  
  Hàm: create(data)
    - Gửi POST /api/publications với data
    - Return: Publication đã tạo
  
  Hàm: update(id, data)
    - Gửi PUT /api/publications/{id}
    - Return: Publication đã cập nhật
  
  Hàm: delete(id)
    - Gửi DELETE /api/publications/{id}
    - Return: void
  ```

- [ ] **Publication List Page**

  ```
  MÃ GIẢ - src/pages/PublicationList.tsx:
  
  State:
    - page: number (trang hiện tại)
    - filters: { status, year }
  
  Data fetching:
    - Gọi publicationService.list({ ...filters, page, size: 10 })
    - Auto refresh khi page hoặc filters thay đổi
  
  UI Layout:
    - Page title: "My Publications"
    - Filter bar:
      * Status dropdown: All, DRAFT, SUBMITTED, PUBLISHED
      * Year input
      * Search box (future: search by title)
    - "Create New" button (góc phải)
    - Data table:
      * Columns: Title, Year, Status (badge), Created Date, Actions
      * Actions: View, Edit, Delete icons
      * Click vào row → navigate đến detail
    - Pagination controls (bottom)
    - Empty state: "No publications yet. Create your first one!"
  ```

---

### 8. Screen 4 & 5: Create/Edit Publication Form

- [ ] **Publication Form Component (Reusable)**

  ```
  MÃ GIẢ - src/components/publication/PublicationForm.tsx:
  
  Props:
    - initialData?: Publication (cho Edit form)
    - onSubmit: (data) => void
    - isLoading?: boolean
  
  Form handling: react-hook-form + yup validation
    - Validation schema:
      * title: required, max 500 chars
      * publicationType: required
      * year: required, min 1900, max current year
      * doi: optional, format validation
      * ... (other fields)
  
  UI Layout (Grid 2 columns):
    Section 1: Basic Information
      - Publication Type (dropdown)
      - Title (full width)
      - Year (number input)
    
    Section 2: Publication Details
      - Journal/Conference Name
      - Volume, Issue, Pages
      - DOI (với hint format)
    
    Section 3: Content
      - Abstract (textarea, full width)
      - Keywords (text input, hint: "Separate by commas")
    
    Section 4: File Upload (tích hợp sau, V1.0 có thể tách riêng)
    
    Section 5: Co-Authors (tích hợp sau)
    
    Actions:
      - Save as Draft button
      - Cancel button
      - Delete button (chỉ trong Edit form, chỉ cho DRAFT)
  
  Xử lý submit:
    1. Validate form
    2. Nếu hợp lệ: Gọi onSubmit(data)
    3. Parent component xử lý API call
  ```

- [ ] **Create Publication Page**

  ```
  MÃ GIẢ - src/pages/CreatePublication.tsx:
  
  State:
    - isSubmitting: boolean
  
  Hàm: handleSubmit(data)
    1. Set isSubmitting = true
    2. Gọi publicationService.create(data)
    3. Nếu thành công:
       - Show success toast
       - Navigate về /publications hoặc /dashboard
    4. Nếu thất bại:
       - Show error toast/alert
    5. Set isSubmitting = false
  
  UI:
    - Page title: "Create New Publication"
    - PublicationForm component với:
      * initialData: undefined (empty form)
      * onSubmit: handleSubmit
      * isLoading: isSubmitting
  ```

- [ ] **Edit Publication Page**

  ```
  MÃ GIẢ - src/pages/EditPublication.tsx:
  
  State:
    - publication: Publication | null
    - isLoading: boolean (loading publication data)
    - isSubmitting: boolean
  
  useEffect: Load publication data
    1. Lấy id từ URL params
    2. Gọi publicationService.get(id)
    3. Set publication state
  
  Hàm: handleUpdate(data)
    1. Gọi publicationService.update(id, data)
    2. Nếu thành công: Show toast, navigate back
    3. Nếu thất bại: Show error
  
  Hàm: handleDelete()
    1. Confirm dialog: "Are you sure you want to delete?"
    2. Nếu confirm:
       - Gọi publicationService.delete(id)
       - Navigate về /publications
  
  UI:
    - Page title: "Edit Publication"
    - PublicationForm với:
      * initialData: publication (pre-filled)
      * onSubmit: handleUpdate
    - Delete button (chỉ hiện nếu status = DRAFT)
  ```

---

### 9. Screen 6: Publication Detail

- [ ] **Publication Detail Page**

  ```
  MÃ GIẢ - src/pages/PublicationDetail.tsx:
  
  State:
    - publication: Publication | null
    - isLoading: boolean
  
  useEffect: Load publication
    1. Lấy id từ URL params
    2. Gọi publicationService.get(id)
    3. Set publication state
  
  UI Layout (Grid 2 columns):
    Left column (60%): PDF Viewer
      - iframe hiển thị PDF (src = /api/publications/{id}/download-pdf)
      - Fallback message nếu không load được: "Cannot display PDF. Click to download."
      - Loading state: Skeleton loader
    
    Right column (40%): Metadata Panel
      Section: Publication Info
        - Type, Year, Journal/Conference, Volume, Issue, Pages, DOI
      
      Section: Authors
        - Main author (bold)
        - Co-authors list
      
      Section: Content
        - Abstract
        - Keywords
      
      Section: Status
        - Status badge
        - Created date, Updated date
      
      Section: File
        - Filename, Size, Upload date
        - Download button
    
    Top actions:
      - Edit button (nếu status = DRAFT)
      - Download PDF button
      - Back button
  ```

---

## ✅ PHASE 3: VERIFICATION

### 10. Component Testing

- [ ] **Unit Tests**

  ```
  MÃ GIẢ - Component Tests:
  
  Test: Button component
    - Renders với text
    - Calls onClick handler khi clicked
    - Disabled khi disabled prop = true
  
  Test: Input component
    - Renders với label
    - Shows error message khi có error
    - Calls onChange handler
  
  Test: PublicationForm
    - Validates required fields
    - Shows error messages
    - Calls onSubmit với correct data
    - Disables submit button khi isLoading
  ```

---

### 11. UI/UX Polish

- [ ] **States Cần Implement**
  - **Loading states**: Hiện spinners/skeletons trong khi fetch data
  - **Empty states**: Hiện messages thân thiện khi không có data
  - **Error handling**: Hiện error messages user-friendly
  - **Success feedback**: Toast notifications cho actions thành công

- [ ] **Accessibility**
  - **Keyboard navigation**: Tab order hợp lý
  - **Focus indicators**: Visible khi tab qua elements
  - **Labels**: Tất cả inputs có labels
  - **ARIA attributes**: Cho screen readers

- [ ] **Responsive Design**
  - **Desktop**: Test trên 1920x1080, 1366x768
  - **Tablet**: Test trên 1024x768, iPad landscape
  - **Breakpoints**: Adjust layouts cho các kích thước khác nhau

---

## ✅ Tiêu Chí Thành Công

Frontend developer làm tốt khi:

✅ Tất cả 6 screens implement và match Figma designs  
✅ APIs integration thành công, data flows đúng  
✅ Responsive trên desktop + tablet  
✅ Không có console errors trong browser  
✅ Test coverage > 70%  
✅ UI/UX designer approval  
✅ Accessibility baseline đạt (keyboard nav, contrast, labels)

---

**Prepared by**: Frontend Team  
**Version**: 1.0  
**Last Updated**: 16/02/2026
