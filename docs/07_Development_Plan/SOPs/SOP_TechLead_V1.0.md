# SOP - Tech Lead
## Version 1.0: Core Publication Management

> 👤 **Vai trò**: Tech Lead  
> 🎯 **Phạm vi**: V1.0 - Kiến trúc kỹ thuật & Hướng dẫn Team  
> 📅 **Áp dụng cho**: Overall Technical Leadership

---

## 🎯 Mục Tiêu Tổng Quan

Dẫn dắt team về mặt kỹ thuật, đảm bảo kiến trúc hệ thống đúng đắn, code quality cao, và team development process hiệu quả. Tech Lead là cầu nối giữa technical execution và business requirements.

---

## 📋 Trách Nhiệm Chính

### 1. Kiến Trúc Kỹ Thuật
- Thiết kế overall system architecture
- Quyết định technology stack
- Đảm bảo scalability và maintainability

### 2. Lãnh Đạo Kỹ Thuật Team
- Hướng dẫn backend và frontend teams
- Code review và technical mentoring
- Giải quyết technical blockers

### 3. Đảm Bảo Chất Lượng
- Định nghĩa coding standards
- Đảm bảo test coverage targets met
- Review performance và security

### 4. Cộng Tác
- Làm việc với PM về khả thi và timeline
- Làm việc với BA về clarifications kỹ thuật
- Làm việc với QA về test strategy

---

## 📐 PHASE 1: DESIGN (Tuần 0-1)

### 1. Thiết Kế Kiến Trúc High-Level

- [ ] **System Architecture Diagram**

  ```
  Sơ đồ kiến trúc 3 tầng:
  
  PRESENTATION LAYER (Tầng Giao Diện):
  - React SPA (TypeScript + MUI)
  - Components: Login, Dashboard, Publication CRUD Pages
  - State Management: Zustand / Redux
  - API Client: Axios
  
  ↕ HTTPS/REST APIs
  
  APPLICATION LAYER (Tầng Ứng Dụng):
  - Spring Boot REST API (Java 17)
  - Controllers: Auth, Publication, File
  - Services: Business logic
  - Repositories: JPA/Hibernate
  
  ↕ JDBC
  
  DATA LAYER (Tầng Dữ Liệu):
  - MySQL Database
    * Tables: users, publications, faculties, departments, publication_authors
  - File System
    * PDF uploads: /var/uploads/
  ```

- [ ] **Quyết Định Technology Stack**

  **Backend:**
  ```
  - Language: Java 17
  - Framework: Spring Boot 3.x
  - ORM: Spring Data JPA (Hibernate)
  - Security: Spring Security + JWT
  - Database: MySQL 8.0
  - Build Tool: Maven
  - Documentation: Springdoc OpenAPI (Swagger)
  
  Lý do chọn:
  - Java: Ngôn ngữ phổ biến, enterprise-ready
  - Spring Boot: Framework mature, cộng đồng lớn, nhiều tính năng
  - MySQL: RDBMS reliable, performance tốt
  ```

  **Frontend:**
  ```
  - Language: TypeScript (type safety)
  - Framework: React 18 (component-based, large ecosystem)
  - UI Library: Material-UI (MUI) - ready-to-use components
  - State Management: Zustand (nhẹ) hoặc Redux Toolkit (đầy đủ)
  - Routing: React Router v6
  - HTTP Client: Axios
  - Form Handling: React Hook Form + Yup
  - Build Tool: Vite (fast dev server)
  ```

  **DevOps:**
  ```
  - Version Control: Git (GitHub / GitLab)
  - CI/CD: GitHub Actions / GitLab CI
  - Deployment: Docker containers (optional cho V1.0)
  ```

  **Testing:**
  ```
  - Backend: JUnit 5, Mockito, MockMvc
  - Frontend: Vitest, React Testing Library
  - API Testing: Postman
  ```

---

### 2. Review Database Schema

- [ ] **Tables và Relationships**

  ```
  Sơ đồ quan hệ các bảng:
  
  users ──────────┐
    ↓             ↓
  publications  publication_authors
    ↑             ↑
    └─────────────┘
  
  faculties ──→ departments
      ↑             ↑
      └─────────────┘
         users
  
  Chi tiết:
  - users: Thông tin người dùng (username, email, password, role, faculty, department)
  - publications: Bài báo (title, type, year, status, PDF path, created_by)
  - publication_authors: Đồng tác giả (publication_id, user_id, author_name, order)
  - faculties: Khoa (name, code)
  - departments: Đơn vị/Bộ môn (name, code, faculty_id)
  ```

- [ ] **Quyết Định Thiết Kế**
  ```
  - Primary Keys: Auto-increment INT (đơn giản, dễ reference)
  - Soft delete hay Hard delete? → Hard delete cho V1.0 (đơn giản hóa)
  - Status field: ENUM (performance tốt hơn VARCHAR)
  - File storage: File system (V1.0), S3 (V2.0+)
  - Timestamps: Auto-managed bởi JPA (@CreatedDate, @LastModifiedDate)
  ```

- [ ] **Indexing Strategy**
  ```
Indexes cần thiết:
  - publications(status) - filter by status thường xuyên
  - publications(created_by) - query publications của user
  - publications(year) - filter by year
  - publication_authors(publication_id) - JOIN frequently
  - users(username), users(email) - login lookup
  ```

---

### 3. Review API Design

- [ ] **RESTful API Conventions**

  ```
  Nguyên tắc đặt tên:
  - Resource names: Plural nouns (/publications, /users)
  - Use kebab-case: /publication-authors
  - Avoid verbs in URLs: ✅ POST /publications vs ❌ POST /createPublication
  
  HTTP Methods:
  - GET: Retrieve resource(s)
  - POST: Create new resource
  - PUT: Update entire resource
  - DELETE: Delete resource
  
  HTTP Status Codes:
  - 200 OK: Successful GET, PUT
  - 201 Created: Successful POST
  - 204 No Content: Successful DELETE
  - 400 Bad Request: Validation error
  - 401 Unauthorized: Not authenticated
  - 403 Forbidden: Not authorized
  - 404 Not Found: Resource not found
  - 500 Internal Server Error: Server error
  ```

- [ ] **Error Response Format Chuẩn**
  ```
  Định dạng JSON cho errors:
  {
    "status": 400,
    "message": "Validation failed",
    "timestamp": "2024-02-16T10:00:00Z",
    "errors": {
      "title": "Title is required",
      "year": "Year must be between 1900 and 2026"
    }
  }
  ```

---

### 4. Thiết Kế Security

- [ ] **Authentication Strategy**

  ```
  V1.0: JWT-based authentication
  
  Luồng hoạt động:
  1. User gửi username/password đến /api/auth/login
  2. Backend verify credentials
  3. Nếu hợp lệ: Tạo JWT token (expires 24h)
  4. Return token cho client
  5. Client lưu token trong localStorage
  6. Mọi API requests kèm header: Authorization: Bearer {token}
  7. Backend verify token mỗi request
  
  V2.0+: LDAP integration với university directory
  ```

- [ ] **Authorization Strategy**

  ```
  V1.0: Simple role-based + ownership check
  
  Roles:
  - RESEARCHER: Quản lý own publications
  - FACULTY_REVIEWER: Review publications (V3.0)
  - UNIVERSITY_REVIEWER: Final review (V4.0)
  - ADMIN: Full access (V5.0)
  
  Ownership check:
  - User chỉ có thể edit/delete publications mình tạo
  - Status check: Chỉ edit/delete được DRAFT publications
  ```

- [ ] **Data Validation & Security**
  ```
  - Backend: Bean Validation (@NotBlank, @Size, @Min, @Max, etc.)
  - Frontend: Yup schemas
  - Principle: Never trust client input
  
  - File upload security:
    * Type validation: Chỉ PDF
    * Size limit: 20MB
    * Virus scanning: Recommended cho V2.0
    * Filename sanitization: Remove special chars, prevent path traversal
  
  - SQL Injection prevention: Parameterized queries (JPA tự động)
  - XSS prevention: Sanitize user input, escape output
  ```

---

### 5. Development Standards

- [ ] **Coding Standards Document**

  **Java (Backend):**
  ```
  - Naming conventions:
    * Classes: PascalCase (PublicationService)
    * Methods: camelCase (createPublication)
    * Constants: UPPER_SNAKE_CASE (MAX_FILE_SIZE)
  
  - Package structure:
    * com.university.ufpms.controller
    * com.university.ufpms.service
    * com.university.ufpms.repository
  
  - Code quality:
    * Max line length: 120 characters
    * Javadoc required cho public methods
    * No commented-out code
    * Use meaningful variable names
  ```

  **TypeScript (Frontend):**
  ```
  - Naming conventions:
    * Components: PascalCase (PublicationList.tsx)
    * Files: PascalCase cho components, camelCase cho utils
    * Variables/functions: camelCase
    * Constants: UPPER_SNAKE_CASE
  
  - Code style:
    * Use functional components (not class components)
    * Use TypeScript strict mode
    * Prefer const over let, avoid var
    * Use arrow functions
  ```

  **Git Commit Messages:**
  ```
  Format: [TYPE] Short description
  
  Types:
  - [FEAT] New feature
  - [FIX] Bug fix
  - [REFACTOR] Code refactoring
  - [TEST] Add/update tests
  - [DOCS] Documentation
  - [CHORE] Maintenance (build, dependencies, etc.)
  
  Examples:
  - [FEAT] Add publication CRUD APIs
  - [FIX] Fix validation error for publication title
  - [REFACTOR] Extract file upload logic to service
  ```

- [ ] **Branch Strategy**

  ```
  GitFlow lite:
  - main: Production-ready code
  - develop: Integration branch
  - feature/US-RES-001-create-publication: Feature branches
  - bugfix/BUG-001-fix-title-validation: Bug fix branches
  
  Pull Request Process:
  1. Create feature branch from develop
  2. Implement feature + tests
  3. Create PR to develop
  4. Code review by Tech Lead (mandatory)
  5. CI passes (build, tests, linting)
  6. Merge to develop
  7. Delete feature branch
  ```

- [ ] **Code Review Checklist**
  ```
  Reviewer phải check:
  - Code follows style guide ✅
  - Tests included (unit + integration) ✅
  - No hardcoded values (use config) ✅
  - Error handling proper ✅
  - No console.log (backend) / System.out.println (frontend) ✅
  - Performance OK (no N+1 queries, etc.) ✅
  - Security OK (no SQL injection, XSS, etc.) ✅
  - Naming clear and meaningful ✅
  ```

---

## 💻 PHASE 2: DEVELOPMENT (Tuần 2-4)

### 6. Setup CI/CD Pipeline

- [ ] **CI Pipeline (GitHub Actions / GitLab CI)**

  **Backend Pipeline Pseudo-Config:**
  ```
  Tên: Backend CI
  
  Trigger: On push và pull request
  
  Jobs:
    Build & Test:
      - Checkout code
      - Setup JDK 17
      - Run: mvn clean install
      - Run: mvn test
      - Check test coverage (JaCoCo)
      - Upload test reports
      
    Linter:
      - Run: mvn checkstyle:check
      
    Security Scan (optional):
      - Run: mvn dependency-check:check
  ```

  **Frontend Pipeline Pseudo-Config:**
  ```
  Tên: Frontend CI
  
  Trigger: On push và pull request
  
  Jobs:
    Build & Test:
      - Checkout code
      - Setup Node.js 18
      - Run: npm ci (install dependencies)
      - Run: npm run lint
      - Run: npm run test
      - Run: npm run build
      - Upload build artifacts
  ```

---

### 7. Daily Technical Leadership

- [ ] **Morning Routine**
  ```
  - Review tất cả open Pull Requests
  - Provide feedback trong vòng 4 giờ
  - Approve PRs đạt checklist + CI green
  - Check CI/CD pipelines - có failures không?
  ```

- [ ] **Mid-day**
  ```
  - Attend Daily Standup
  - Listen cho technical blockers
  - Provide guidance on the spot
  - Escalate nếu cần (PM, Management)
  ```

- [ ] **Afternoon**
  ```
  - Availability window: 2-3 giờ cho team questions
  - Pair programming với team members (nếu cần)
  - Architecture decisions
  - Research new approaches
  ```

- [ ] **Code Quality Monitoring**
  ```
  - Weekly: Run SonarQube scan (nếu có)
  - Track metrics:
    * Code coverage (target > 80%)
    * Code smells count
    * Security vulnerabilities
    * Technical debt
  ```

---

### 8. Technical Debt Management

- [ ] **Maintain Tech Debt Log**

  ```
  Format:
  ID | Description | Priority | Effort | Impact | Plan
  
  Examples:
  TD-001 | Refactor FileStorageService to strategy pattern | Low | M | Low | V2.0
  TD-002 | Add database connection pooling config | Med | L | Med | V1.1
  TD-003 | Implement API rate limiting | High | M | High | V1.1
  
  Rule: Allocate 20% sprint capacity cho tech debt
  ```

---

### 9. Performance Optimization

- [ ] **Backend Performance**
  ```
  Kiểm soát:
  - Query optimization:
    * Avoid N+1 queries → use JOIN FETCH
    * Add indexes cho frequently queried fields
    * Use pagination cho list endpoints
  
  - API response time:
    * Target: < 500ms (P95)
    * Monitor bằng logging/APM tools
  
  - Caching (V2.0):
    * Cache GET /api/publications/{id}
    * Cache dashboard stats
  ```

- [ ] **Frontend Performance**
  ```
  Optimization tactics:
  - Code splitting: Lazy load routes
  - Bundle size: Keep < 500KB initial load
  - Image optimization: Compress images
  - React optimization:
    * Use React.memo cho expensive components
    * Avoid unnecessary re-renders
    * Use virtualization cho long lists (react-window)
  ```

---

## ✅ PHASE 3: VERIFICATION (Tuần 5)

### 10. Pre-Release Checklist

- [ ] **Code Quality**
  ```
  - All PRs merged to develop ✅
  - Code coverage > 80% (backend + frontend) ✅
  - 0 critical bugs from SonarQube ✅
  - 0 high-severity security vulnerabilities ✅
  ```

- [ ] **Testing**
  ```
  - All unit tests pass ✅
  - All integration tests pass ✅
  - QA sign-off received ✅
  - UAT passed by PM ✅
  ```

- [ ] **Documentation**
  ```
  - API documentation complete (Swagger) ✅
  - README updated (how to run locally) ✅
  - Architecture diagram documented ✅
  - Database schema documented ✅
  - Deployment guide ready ✅
  ```

- [ ] **Security**
  ```
  - JWT authentication working ✅
  - Authorization checks in place ✅
  - Input validation on all endpoints ✅
  - File upload validation working ✅
  - HTTPS configured (production) ✅
  ```

- [ ] **Performance**
  ```
  - API response time < 500ms (P95) ✅
  - Frontend initial load < 3 seconds ✅
  - Database queries optimized ✅
  - No memory leaks ✅
  ```

---

### 11. Production Deployment

- [ ] **Deployment Checklist**

  ```
  Pre-Deployment:
  - Merge develop → main
  - Tag release: v1.0.0
  - Backup production database (nếu upgra

de)
  
  Deployment Steps:
  - Deploy backend (Spring Boot JAR)
  - Run database migrations
  - Deploy frontend (build + upload to server/CDN)
  - Update environment variables
  - Restart services
  
  Post-Deployment:
  - Smoke test: Login, create publication, upload PDF
  - Check application logs (no errors)
  - Monitor for 1 hour
  - Announce deployment to team
  ```

- [ ] **Rollback Plan**
  ```
  Nếu deployment fails:
  1. Revert code về previous version
  2. Restore database backup (nếu cần)
  3. Notify team
  4. Post-mortem: Analyze what went wrong
  ```

---

### 12. Post-Release Monitoring

- [ ] **Week 1 Post-Release**
  ```
  Actions:
  - Monitor application logs daily
  - Track error rates (should be < 1%)
  - Track API response times
  - Check database performance
  - Collect user feedback
  ```

- [ ] **Production Issues**
  ```
  - Log all bugs reported by users
  - Priority:
    * P0 → Hotfix immediately
    * P1/P2 → Plan for V1.1
    * P3 → Backlog
  ```

---

## 🔍 Tech Lead Best Practices

### 1. Dẫn Dắt Bằng Gương
- Viết code chất lượng cao
- Follow own standards
- Review PRs đầu tiên

### 2. Trao Quyền Cho Team
- Đừng micromanage
- Trust developers để make decisions
- Provide guidance, not solutions

### 3. Cân Bằng Speed vs. Quality
- Đừng hy sinh quality vì speed
- Nhưng cũng đừng over-engineer
- V1.0 không cần perfect, nhưng phải work

### 4. Document Decisions
- Document why decisions were made
- Example: "Tại sao chọn JWT thay vì session-based auth?"
- Team members tương lai sẽ cảm ơn

### 5. Continuous Learning
- Stay updated với latest technologies
- Encourage team học new things
- Allocate time cho R&D

---

## ✅ Tiêu Chí Thành Công

Tech Lead làm tốt khi:

✅ Architecture solid, scalable, và maintainable  
✅ Team follows coding standards consistently  
✅ Code quality cao (coverage > 80%, no critical bugs)  
✅ PRs reviewed promptly (< 4 hours)  
✅ Technical blockers resolved nhanh  
✅ V1.0 deployed successfully to production  
✅ Team hài lòng với technical leadership (from retrospective)  
✅ Clear technical roadmap cho V2.0

---

## 📋 Deliverables (Sản Phẩm Bàn Giao)

1. **Architecture Design Document** - System architecture, tech stack, database schema
2. **API Specification** - OpenAPI/Swagger, Postman collection
3. **Coding Standards Document** - Backend + Frontend standards, Git workflow
4. **Technical Debt Log** - Known issues, prioritized backlog
5. **Deployment Guide** - Production deployment, environment setup, rollback procedures
6. **Post-Release Report** - Lessons learned, improvements cho V2.0

---

**Prepared by**: Tech Lead  
**Version**: 1.0  
**Last Updated**: 16/02/2026
