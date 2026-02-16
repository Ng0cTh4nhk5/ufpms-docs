# Hướng Dẫn Setup Ban Đầu - UFPMS V1.0

> 📅 **Ngày tạo**: 16/02/2026  
> 🎯 **Mục đích**: Hướng dẫn setup môi trường và công cụ cho team V1.0  
> ⏱️ **Timeline**: Week 1 (Design Phase)

---

## 📋 Tổng Quan

Document này hướng dẫn setup ban đầu cho **tất cả 7 vai trò** trong team để bắt đầu phát triển UFPMS Version 1.0.

---

## 🗂️ Chiến Lược Repository

### Quyết Định: **3 Repositories Riêng Biệt**

```
ufpms-backend/          ← Repository 1: Spring Boot APIs
ufpms-frontend/         ← Repository 2: React Application  
ufpms-docs/             ← Repository 3: Documentation (Optional)
```

**Lý do:**
- ✅ Deploy độc lập
- ✅ CI/CD pipelines khác nhau
- ✅ Team làm việc song song không conflict
- ✅ Version control rõ ràng
- ✅ Dễ scale sau này

---

## 👤 ROLE 1: PRODUCT MANAGER

### Checklist Setup (30 phút)

- [ ] **1.1 Tạo GitHub Repositories**
  ```bash
  # Trên GitHub.com:
  1. Click "New Repository"
  2. Tạo "ufpms-backend" (Private)
  3. Tạo "ufpms-frontend" (Private)
  4. Tạo "ufpms-docs" (Private) - Optional
  
  # Add team members với quyền:
  - Tech Lead: Admin
  - Developers, BA, UI/UX, QA: Write
  ```

- [ ] **1.2 Setup Project Management Tool**
  ```
  Chọn 1 trong 2:
  
  Option A: Jira
  - Tạo project "UFPMS V1.0"
  - Create board (Scrum/Kanban)
  - Add 9 user stories (US-RES-001 đến US-RES-024)
  
  Option B: Trello
  - Tạo board "UFPMS V1.0"
  - Lists: Backlog, To Do, In Progress, Review, Done
  - Add cards cho 9 user stories
  ```

- [ ] **1.3 Setup Communication Channel**
  ```
  Slack/Teams:
  - Tạo channel: #ufpms-v1-general
  - Tạo channel: #ufpms-v1-dev (technical discussions)
  - Tạo channel: #ufpms-v1-qa (bug reports)
  
  Schedule:
  - Daily Standup: 9:00 AM (Google Calendar recurring)
  ```

- [ ] **1.4 Push Documentation**
  ```bash
  # Clone ufpms-docs repo
  git clone <ufpms-docs-url>
  cd ufpms-docs
  
  # Copy tất cả docs hiện tại
  cp -r /path/to/current/docs/* .
  
  # Commit
  git add .
  git commit -m "docs: initial documentation for V1.0"
  git push origin main
  ```

---

## 👤 ROLE 2: TECH LEAD

### Checklist Setup (2 giờ)

- [ ] **2.1 Setup Branch Protection Rules**
  ```
  Cho cả backend và frontend repos:
  
  GitHub Settings → Branches → Add rule:
  - Branch name pattern: main
  - ✅ Require pull request reviews (1 approval)
  - ✅ Require status checks to pass
  - ✅ Include administrators (uncheck nếu cần emergency fix)
  
  Repeat cho "develop" branch
  ```

- [ ] **2.2 Tạo Coding Standards Document**
  
  File: `docs/CODING_STANDARDS.md` (trong cả 2 repos)
  
  ```markdown
  # Coding Standards - UFPMS V1.0
  
  ## Backend (Java/Spring Boot)
  
  ### Naming Conventions
  - Classes: PascalCase (PublicationService, UserController)
  - Methods: camelCase (createPublication, findById)
  - Constants: UPPER_SNAKE_CASE (MAX_FILE_SIZE, JWT_EXPIRATION)
  - Packages: lowercase (vn.edu.ufpms.controller)
  
  ### Package Structure

  ``plaintext
  src/main/java/vn/edu/ufpms/
  ├── controller/      # REST endpoints
  ├── service/         # Business logic
  ├── repository/      # Data access
  ├── model/           # Entity classes
  ├── dto/             # Data Transfer Objects
  ├── config/          # Configuration classes
  ├── security/        # Security configs
  └── exception/       # Custom exceptions
  ``
  
  ### Code Review Checklist
  - [ ] No hardcoded values
  - [ ] Proper error handling
  - [ ] Unit tests included (coverage > 80%)
  - [ ] No SQL injection risks
  - [ ] Follows naming conventions
  - [ ] JavaDoc for public methods
  
  ## Frontend (TypeScript/React)
  
  ### Naming Conventions
  - Components: PascalCase (PublicationList, LoginPage)
  - Hooks: camelCase with "use" prefix (useAuth, useFetch)
  - Utils: camelCase (formatDate, validateEmail)
  - Constants: UPPER_SNAKE_CASE
  
  ### Folder Structure

  ``plaintext
  src/
  ├── components/      # Reusable components
  ├── pages/           # Page components
  ├── services/        # API calls
  ├── hooks/           # Custom hooks
  ├── store/           # State management
  ├── types/           # TypeScript types
  ├── utils/           # Helper functions
  └── assets/          # Images, fonts
  ``
  
  ### Code Review Checklist
  - [ ] TypeScript types defined
  - [ ] No "any" types
  - [ ] Props documented
  - [ ] Tests included (coverage > 70%)
  - [ ] Accessibility attributes (aria-label, alt)
  - [ ] Error boundaries
  ``

- [ ] **2.3 Setup CI/CD Skeleton**
  
  File: `.github/workflows/ci.yml` (backend)
  
  ```yaml
  name: Backend CI
  
  on:
    push:
      branches: [ develop, main ]
    pull_request:
      branches: [ develop, main ]
  
  jobs:
    build:
      runs-on: ubuntu-latest
      
      steps:
      - uses: actions/checkout@v3
      
      - name: Set up JDK 17
        uses: actions/setup-java@v3
        with:
          java-version: '17'
          distribution: 'temurin'
      
      - name: Build with Maven
        run: mvn clean install
      
      - name: Run tests
        run: mvn test
  ```
  
  File: `.github/workflows/ci.yml` (frontend)
  
  ```yaml
  name: Frontend CI
  
  on:
    push:
      branches: [ develop, main ]
    pull_request:
      branches: [ develop, main ]
  
  jobs:
    build:
      runs-on: ubuntu-latest
      
      steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      
      - name: Install dependencies
        run: npm ci
      
      - name: Run tests
        run: npm test
      
      - name: Build
        run: npm run build
  ```

- [ ] **2.4 Tạo Git Workflow Guide**
  
  File: `docs/GIT_WORKFLOW.md`
  
  ```markdown
  # Git Workflow - UFPMS V1.0
  
  ## Branch Strategy (GitFlow Lite)
  
  ``plaintext
  main (production)
    ↑
  develop (staging)
    ↑
  feature/US-RES-001-create-publication
  feature/US-RES-002-upload-pdf
  bugfix/BUG-001-validation-error
  ``
  
  ## Workflow
  
  1. **Create feature branch**
     ```bash
     git checkout develop
     git pull origin develop
     git checkout -b feature/US-RES-001-create-publication
     ``
  
  2. **Make changes & commit**
     ```bash
     git add .
     git commit -m "feat: implement create publication API"
     ``
  
  3. **Push & create PR**
     ```bash
     git push origin feature/US-RES-001-create-publication
     # Create PR on GitHub: feature/* → develop
     ``
  
  4. **Code review → Merge → Delete branch**
  
  ## Commit Message Convention
  
  Format: `<type>: <description>`
  
  Types:
  - `feat`: New feature (feat: add publication CRUD)
  - `fix`: Bug fix (fix: resolve validation error)
  - `docs`: Documentation (docs: update API spec)
  - `test`: Tests (test: add unit tests for service)
  - `refactor`: Code refactoring
  - `chore`: Chores (chore: update dependencies)
  
  Examples:
  ``plaintext
  feat: implement JWT authentication
  fix: resolve file upload size validation
  docs: add API documentation for publications
  test: add integration tests for publication controller
  ``
  ```

---

## 👤 ROLE 3: BUSINESS ANALYST

### Checklist Setup (1 giờ)

- [ ] **3.1 Clone ufpms-docs Repository**
  ```bash
  git clone <ufpms-docs-url>
  cd ufpms-docs
  ```

- [ ] **3.2 Push Business Rules Document**
  ```bash
  # Copy BRD vào docs/
  cp /path/to/business_rules_v1.0.md docs/07_Development_Plan/
  
  git add .
  git commit -m "docs: add business rules document for V1.0"
  git push origin main
  ```

- [ ] **3.3 Push Process Flow Diagrams**
  ```bash
  # Tạo folder
  mkdir -p docs/07_Development_Plan/diagrams
  
  # Copy diagrams
  cp /path/to/flowcharts/*.png docs/07_Development_Plan/diagrams/
  
  git add .
  git commit -m "docs: add process flow diagrams"
  git push origin main
  ```

- [ ] **3.4 Review Requirements với Team**
  ```
  Schedule meeting (30 phút) với:
  - UI/UX Designer: Clarify screen requirements
  - QA: Clarify test scenarios
  - Developers: Clarify business rules
  ```

---

## 👤 ROLE 4: UI/UX DESIGNER

### Checklist Setup (1 giờ)

- [ ] **4.1 Setup Figma Project**
  ```
  1. Tạo Figma project: "UFPMS V1.0"
  2. Import design system template (nếu có)
  3. Create pages:
     - Design System
     - Login Page
     - Dashboard
     - Publication List
     - Create/Edit Publication Form
     - Publication Detail
  ```

- [ ] **4.2 Share Figma Access**
  ```
  Invite team members:
  - Frontend Developer: Can edit
  - Others: Can view
  
  Share link trong Slack channel
  ```

- [ ] **4.3 Export Design Assets**
  ```bash
  # Tạo shared folder (Google Drive/OneDrive)
  UFPMS_V1.0_Assets/
  ├── icons/
  ├── images/
  ├── logos/
  └── fonts/
  
  # Share link với Frontend Developer
  ```

- [ ] **4.4 Install Design Tools**
  ```
  - Figma Desktop App
  - Adobe XD (optional)
  - Sketch (optional)
  ```

---

## 👤 ROLE 5: BACKEND DEVELOPER

### Checklist Setup (3 giờ)

- [ ] **5.1 Install Development Tools**
  ```bash
  Required:
  ✅ Java 17 (OpenJDK hoặc Oracle JDK)
  ✅ Maven 3.8+
  ✅ IntelliJ IDEA / Eclipse / VS Code
  ✅ MySQL 8.0
  ✅ Git
  ✅ Postman
  
  Verify:
  java -version    # Should show Java 17
  mvn -version     # Should show Maven 3.8+
  mysql --version  # Should show MySQL 8.0+
  ```

- [ ] **5.2 Clone Backend Repository**
  ```bash
  git clone <ufpms-backend-url>
  cd ufpms-backend
  git checkout -b develop
  git push -u origin develop
  ```

- [ ] **5.3 Create Spring Boot Project (Week 3, Day 1)**
  
  **Option A: Spring Initializr (Recommended)**
  ```
  1. Visit https://start.spring.io/
  
  2. Config:
     Project: Maven
     Language: Java
     Spring Boot: 3.2.x (latest stable)
     
     Group: vn.edu.ufpms
     Artifact: ufpms-backend
     Name: UFPMS Backend
     Package name: vn.edu.ufpms
     Packaging: Jar
     Java: 17
  
  3. Dependencies:
     - Spring Web
     - Spring Data JPA
     - Spring Security
     - MySQL Driver
     - Lombok
     - Validation
     - Spring Boot DevTools
     
     # Add manually sau:
     - springdoc-openapi (Swagger)
  
  4. Generate → Download → Extract vào ufpms-backend/
  ```

- [ ] **5.4 Setup Database**
  ```sql
  # Login vào MySQL
  mysql -u root -p
  
  # Create database
  CREATE DATABASE ufpms_v1 CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
  
  # Create user (optional, cho security)
  CREATE USER 'ufpms_user'@'localhost' IDENTIFIED BY 'ufpms_password';
  GRANT ALL PRIVILEGES ON ufpms_v1.* TO 'ufpms_user'@'localhost';
  FLUSH PRIVILEGES;
  
  # Verify
  SHOW DATABASES;
  USE ufpms_v1;
  ```

- [ ] **5.5 Configure application.properties**
  
  File: `src/main/resources/application.properties`
  
  ```properties
  # Server
  server.port=8080
  
  # Database
  spring.datasource.url=jdbc:mysql://localhost:3306/ufpms_v1?useSSL=false&serverTimezone=UTC
  spring.datasource.username=root
  spring.datasource.password=yourpassword
  spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
  
  # JPA/Hibernate
  spring.jpa.hibernate.ddl-auto=update
  spring.jpa.show-sql=true
  spring.jpa.properties.hibernate.format_sql=true
  spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect
  
  # JWT (placeholder)
  jwt.secret=your-secret-key-minimum-256-bits-long-for-HS256
  jwt.expiration=86400000
  
  # File Upload
  spring.servlet.multipart.max-file-size=20MB
  spring.servlet.multipart.max-request-size=20MB
  upload.path=./uploads/
  
  # Swagger
  springdoc.api-docs.path=/api-docs
  springdoc.swagger-ui.path=/swagger-ui.html
  ```

- [ ] **5.6 Add Swagger Dependency**
  
  File: `pom.xml`
  
  ```xml
  <dependency>
      <groupId>org.springdoc</groupId>
      <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
      <version>2.3.0</version>
  </dependency>
  ```

- [ ] **5.7 Create Initial Package Structure**
  ```bash
  mkdir -p src/main/java/vn/edu/ufpms/{controller,service,repository,model,dto,config,security,exception}
  mkdir -p src/test/java/vn/edu/ufpms/{controller,service,repository}
  ```

- [ ] **5.8 Test Application Startup**
  ```bash
  # Build
  mvn clean install
  
  # Run
  mvn spring-boot:run
  
  # Verify:
  # Browser: http://localhost:8080
  # Should see Swagger UI: http://localhost:8080/swagger-ui.html
  ```

- [ ] **5.9 Push Initial Setup**
  ```bash
  git add .
  git commit -m "chore: initial Spring Boot project setup"
  git push origin develop
  ```

---

## 👤 ROLE 6: FRONTEND DEVELOPER

### Checklist Setup (2 giờ)

- [ ] **6.1 Install Development Tools**
  ```bash
  Required:
  ✅ Node.js 18+ (LTS)
  ✅ npm 9+ hoặc yarn
  ✅ VS Code
  ✅ Git
  
  Verify:
  node -v    # Should show v18+
  npm -v     # Should show v9+
  ```

- [ ] **6.2 Clone Frontend Repository**
  ```bash
  git clone <ufpms-frontend-url>
  cd ufpms-frontend
  git checkout -b develop
  git push -u origin develop
  ```

- [ ] **6.3 Create Vite Project (Week 3, Day 1)**
  ```bash
  # Create project
  npm create vite@latest . -- --template react-ts
  
  # Install dependencies
  npm install
  ```

- [ ] **6.4 Install Required Libraries**
  ```bash
  # UI Framework
  npm install @mui/material @emotion/react @emotion/styled
  npm install @mui/icons-material
  
  # Routing
  npm install react-router-dom
  
  # HTTP Client
  npm install axios
  
  # Form Management
  npm install react-hook-form yup @hookform/resolvers
  
  # State Management (choose one)
  npm install zustand
  # OR
  npm install @reduxjs/toolkit react-redux
  
  # Dev Dependencies
  npm install -D @types/node
  ```

- [ ] **6.5 Create Folder Structure**
  ```bash
  mkdir -p src/{components,pages,services,hooks,store,types,utils,assets}
  
  # Create subfolders
  mkdir -p src/components/{common,layout}
  mkdir -p src/pages/{auth,dashboard,publications}
  mkdir -p src/services/api
  ```

- [ ] **6.6 Setup Base Configuration**
  
  File: `tsconfig.json` (update paths)
  
  ```json
  {
    "compilerOptions": {
      "target": "ES2020",
      "useDefineForClassFields": true,
      "lib": ["ES2020", "DOM", "DOM.Iterable"],
      "module": "ESNext",
      "skipLibCheck": true,
      
      "moduleResolution": "bundler",
      "allowImportingTsExtensions": true,
      "resolveJsonModule": true,
      "isolatedModules": true,
      "noEmit": true,
      "jsx": "react-jsx",
      
      "strict": true,
      "noUnusedLocals": true,
      "noUnusedParameters": true,
      "noFallthroughCasesInSwitch": true,
      
      "baseUrl": ".",
      "paths": {
        "@/*": ["./src/*"]
      }
    },
    "include": ["src"],
    "references": [{ "path": "./tsconfig.node.json" }]
  }
  ```
  
  File: `vite.config.ts` (add alias)
  
  ```typescript
  import { defineConfig } from 'vite'
  import react from '@vitejs/plugin-react'
  import path from 'path'
  
  export default defineConfig({
    plugins: [react()],
    resolve: {
      alias: {
        '@': path.resolve(__dirname, './src'),
      },
    },
    server: {
      port: 3000,
      proxy: {
        '/api': {
          target: 'http://localhost:8080',
          changeOrigin: true,
        },
      },
    },
  })
  ```

- [ ] **6.7 Create Axios Instance**
  
  File: `src/services/api/axiosInstance.ts`
  
  ```typescript
  import axios from 'axios';
  
  const axiosInstance = axios.create({
    baseURL: import.meta.env.VITE_API_BASE_URL || 'http://localhost:8080/api',
    timeout: 10000,
    headers: {
      'Content-Type': 'application/json',
    },
  });
  
  // Request interceptor (add JWT token)
  axiosInstance.interceptors.request.use(
    (config) => {
      const token = localStorage.getItem('access_token');
      if (token) {
        config.headers.Authorization = `Bearer ${token}`;
      }
      return config;
    },
    (error) => Promise.reject(error)
  );
  
  // Response interceptor (handle errors)
  axiosInstance.interceptors.response.use(
    (response) => response,
    (error) => {
      if (error.response?.status === 401) {
        // Redirect to login
        localStorage.removeItem('access_token');
        window.location.href = '/login';
      }
      return Promise.reject(error);
    }
  );
  
  export default axiosInstance;
  ```

- [ ] **6.8 Create Environment File**
  
  File: `.env.development`
  
  ```env
  VITE_API_BASE_URL=http://localhost:8080/api
  ```

- [ ] **6.9 Test Application Startup**
  ```bash
  npm run dev
  
  # Verify:
  # Browser: http://localhost:3000
  ```

- [ ] **6.10 Push Initial Setup**
  ```bash
  git add .
  git commit -m "chore: initial Vite + React + TypeScript setup"
  git push origin develop
  ```

---

## 👤 ROLE 7: QA/TESTER

### Checklist Setup (1 giờ)

- [ ] **7.1 Install Testing Tools**
  ```
  Required:
  ✅ Postman (or Insomnia)
  ✅ Chrome Browser + DevTools
  ✅ Git
  
  Optional:
  ✅ JMeter (performance testing)
  ✅ Selenium IDE (automation)
  ```

- [ ] **7.2 Setup Postman Workspace**
  ```
  1. Create Workspace: "UFPMS V1.0"
  2. Create Collections:
     - Authentication APIs
     - Publication APIs
     - File Upload APIs
     - Dashboard APIs
  
  3. Setup Environment:
     Name: UFPMS Dev
     Variables:
     - base_url: http://localhost:8080/api
     - token: (will be set after login)
  ```

- [ ] **7.3 Clone Docs Repository**
  ```bash
  git clone <ufpms-docs-url>
  cd ufpms-docs
  ```

- [ ] **7.4 Push Test Plan**
  ```bash
  # Copy test plan
  cp /path/to/test_plan_v1.0.md docs/07_Development_Plan/
  
  # Create test cases folder
  mkdir -p docs/07_Development_Plan/test_cases
  
  git add .
  git commit -m "docs: add test plan and test cases for V1.0"
  git push origin main
  ```

- [ ] **7.5 Prepare Test Data**
  ```
  Create folder: test_data/
  
  Files:
  - valid_publication.json (sample publication data)
  - valid_5mb.pdf (test PDF file)
  - large_25mb.pdf (test file size limit)
  - corrupted.pdf (test error handling)
  - invalid.docx (test file type validation)
  ```

---

## 🛠️ Common Tools for Everyone

### Git Configuration

```bash
# Set name and email
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Set default branch name
git config --global init.defaultBranch main

# Set editor
git config --global core.editor "code --wait"

# Verify
git config --list
```

### VS Code Extensions (Recommended)

```
All:
- GitLens
- GitHub Pull Requests

Backend Developers:
- Extension Pack for Java
- Spring Boot Extension Pack
- Database Client (for MySQL)

Frontend Developers:
- ES7+ React/Redux snippets
- Auto Rename Tag
- Prettier - Code formatter
- ESLint
```

---

## ✅ Week 1 (Design Phase) - Final Checklist

```markdown
### By End of Week 1, These Should Be DONE:

**Infrastructure:**
- [ ] 3 GitHub repos created and accessible to all
- [ ] Branch protection rules setup
- [ ] Jira/Trello board created với 9 user stories

**Documentation:**
- [ ] Business Rules Document pushed
- [ ] Process Flow Diagrams pushed
- [ ] Coding Standards documented
- [ ] Git Workflow documented
- [ ] Test Plan pushed

**Design:**
- [ ] Figma project created với 6 screens
- [ ] Design system defined
- [ ] Figma access shared với team

**Communication:**
- [ ] Slack channels created
- [ ] Daily standup scheduled (9:00 AM)
- [ ] Design Review meeting scheduled (end of week 2)

**Environment (Week 3 readiness):**
- [ ] Backend: Java, Maven, MySQL installed
- [ ] Frontend: Node.js, npm installed
- [ ] QA: Postman installed
- [ ] All: Git configured
```

---

## 📞 Support & Questions

**Blockers?**
- Tag `@Tech Lead` trong Slack #ufpms-v1-dev
- Or raise trong Daily Standup

**Documentation unclear?**
- Tag `@BA` trong Slack #ufpms-v1-general

**Design questions?**
- Tag `@UI/UX` trong Slack #ufpms-v1-general

---

## 🚀 Next Steps

**Week 2:**
- BA: Finalize Business Rules Document
- UI/UX: Complete all 6 screen designs
- TL: Finalize API specification
- QA: Complete test cases (~55 cases)
- **End of Week 2: Design Review Meeting**

**Week 3 (Development Starts):**
- Backend: Begin Authentication Module
- Frontend: Begin Login Page + Dashboard
- QA: Begin API testing với Postman

---

**Last Updated**: 16/02/2026  
**Maintainer**: Tech Lead & PM
