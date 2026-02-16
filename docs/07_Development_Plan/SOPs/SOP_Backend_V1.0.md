# SOP - Backend Developer
## Version 1.0: Core Publication Management

> 👤 **Vai trò**: Backend Developer  
> 🎯 **Phạm vi**: V1.0 - Phát triển APIs CRUD cho Publications  
> 📅 **Áp dụng cho**: Spring Boot RESTful APIs + Database

---

## 🎯 Mục Tiêu Tổng Quan

Phát triển backend APIs cho V1.0, đảm bảo APIs hoạt động đúng chức năng, an toàn, có performance tốt, và dễ maintain. Backend developer xây dựng nền tảng cho toàn bộ hệ thống.

---

## 📋 Trách Nhiệm Chính

### 1. Phát Triển APIs
- Implement RESTful APIs theo specification
- Xử lý business logic cho Publication module
- Implement xác thực và phân quyền

### 2. Quản Lý Database
- Thiết kế và implement database schema
- Viết queries hiệu quả
- Xử lý migrations

### 3. Testing
- Viết unit tests cho services
- Viết integration tests cho APIs
- Đảm bảo test coverage > 80%

### 4. Tài Liệu
- Document APIs bằng Swagger/OpenAPI
- Viết code comments
- Maintain technical docs

---

## 📐 PHASE 1: DESIGN (Tuần 0-1)

### 1. Thiết Lập Môi Trường

- [ ] **Cài Đặt Công Cụ Phát Triển**
  - [ ] JDK 17+ (hoặc JDK 11+)
  - [ ] IntelliJ IDEA / Eclipse
  - [ ] Maven / Gradle
  - [ ] MySQL / PostgreSQL
  - [ ] Postman / Insomnia (để test APIs)
  - [ ] Git

- [ ] **Setup Spring Boot Project**
  
  **Hướng dẫn:**
  - Sử dụng Spring Initializr (https://start.spring.io/)
  - Chọn dependencies cần thiết:
    - Spring Web (cho REST APIs)
    - Spring Data JPA (cho database)
    - Spring Security (cho authentication)
    - MySQL Driver / PostgreSQL Driver
    - Lombok (giảm boilerplate code)
    - Validation (cho input validation)
    - Springdoc OpenAPI (cho Swagger documentation)

- [ ] **Cấu Trúc Thư Mục Đề Xuất**
  ```
  src/main/java/com/university/ufpms/
  ├── config/           # Configuration classes (Security, CORS, etc.)
  ├── controller/       # REST Controllers
  ├── service/          # Business logic
  ├── repository/       # JPA Repositories
  ├── model/            # Entity classes
  ├── dto/              # Data Transfer Objects
  ├── exception/        # Custom exceptions
  ├── security/         # Security configs (JWT, filters)
  └── util/             # Utility classes
  
  src/main/resources/
  ├── application.properties         # Main config
  ├── application-dev.properties     # Dev environment
  ├── application-prod.properties    # Production environment
  └── db/migration/                  # SQL migration scripts
  ```

---

### 2. Review Database Schema

- [ ] **Các Bảng Cần Implement**

  **Bảng 1: users (Người dùng)**
  ```
  Các cột:
  - id (Primary Key, tự động tăng)
  - username (duy nhất, required)
  - email (duy nhất, required)
  - password (đã mã hóa, required)
  - full_name (required)
  - faculty_id (Foreign Key → faculties)
  - department_id (Foreign Key → departments)
  - role (ENUM: RESEARCHER, FACULTY_REVIEWER, UNIVERSITY_REVIEWER, ADMIN)
  - created_at, updated_at (timestamps)
  
  Indexes:
  - username (unique)
  - email (unique)
  ```

  **Bảng 2: faculties (Khoa)**
  ```
  Các cột:
  - id (Primary Key)
  - name (tên khoa, required)
  - code (mã khoa, unique, required)
  - created_at
  ```

  **Bảng 3: departments (Đơn vị/Bộ môn)**
  ```
  Các cột:
  - id (Primary Key)
  - name (tên đơn vị, required)
  - code (mã đơn vị, unique, required)
  - faculty_id (Foreign Key → faculties)
  - created_at
  ```

  **Bảng 4: publications (Bài báo)**
  ```
  Các cột:
  - id (Primary Key)
  - title (tiêu đề, max 500 ký tự, required)
  - publication_type (ENUM: JOURNAL, CONFERENCE, BOOK_CHAPTER, OTHER)
  - journal_name, conference_name (tên tạp chí/hội nghị)
  - year (năm xuất bản, required)
  - volume, issue, pages, doi (thông tin chi tiết)
  - abstract (tóm tắt, TEXT)
  - keywords (từ khóa, TEXT)
  - pdf_filename, pdf_path (file PDF)
  - status (ENUM: DRAFT, SUBMITTED, FACULTY_REVIEWING, 
             FACULTY_APPROVED, UNIVERSITY_REVIEWING, PUBLISHED, REJECTED)
  - created_by (Foreign Key → users, required)
  - created_at, updated_at, submitted_at, published_at (timestamps)
  
  Indexes:
  - status (để filter)
  - created_by (để query bài báo của user)
  - year (để filter theo năm)
  ```

  **Bảng 5: publication_authors (Đồng tác giả)**
  ```
  Các cột:
  - id (Primary Key)
  - publication_id (Foreign Key → publications, required)
  - user_id (Foreign Key → users, nullable nếu là external author)
  - author_name (tên tác giả, required)
  - author_email (email tác giả)
  - is_corresponding (boolean, tác giả liên hệ?)
  - author_order (thứ tự tác giả: 1 = first author, 2 = second, etc.)
  - created_at
  
  Constraints:
  - Unique (publication_id, author_order) - không trùng thứ tự
  - Cascade delete khi xóa publication
  ```

- [ ] **Tạo Migration Scripts**
  - Sử dụng Flyway hoặc Liquibase để quản lý schema versions
  - Đặt tên file: `V1__create_initial_tables.sql`
  - Chứa: CREATE TABLE statements cho tất cả các bảng trên

---

### 3. Review API Specification

- [ ] **Danh Sách Endpoints Cần Implement**

  **APIs Xác Thực:**
  ```
  POST   /api/auth/login      → Đăng nhập, trả về JWT token
  POST   /api/auth/logout     → Đăng xuất
  GET    /api/auth/me         → Lấy thông tin user hiện tại
  ```

  **APIs Quản Lý Publications:**
  ```
  POST   /api/publications              → Tạo publication mới
  GET    /api/publications              → Lấy danh sách (có filter, pagination)
  GET    /api/publications/{id}         → Lấy chi tiết publication
  PUT    /api/publications/{id}         → Cập nhật publication
  DELETE /api/publications/{id}         → Xóa publication
  POST   /api/publications/{id}/submit  → Nộp để xét duyệt (V2.0)
  ```

  **APIs Upload/Download File:**
  ```
  POST   /api/publications/{id}/upload-pdf    → Upload file PDF
  GET    /api/publications/{id}/download-pdf  → Download file PDF
  ```

  **APIs Đồng Tác Giả:**
  ```
  POST   /api/publications/{id}/authors         → Thêm đồng tác giả
  PUT    /api/publications/{id}/authors/{authorId}  → Cập nhật order
  DELETE /api/publications/{id}/authors/{authorId}  → Xóa đồng tác giả
  ```

  **APIs Dashboard:**
  ```
  GET    /api/dashboard/stats       → Lấy thống kê (total, published, draft, etc.)
  GET    /api/dashboard/work-hours  → Lấy tính toán giờ làm
  ```

---

## 💻 PHASE 2: DEVELOPMENT (Tuần 2-4)

### 4. Module Xác Thực (Authentication)

- [ ] **JWT Authentication Setup**

  **Bước 1: Cấu hình Security**
  ```
  MÃ GIẢ - SecurityConfig:
  
  Hàm: configureSecurityFilterChain()
    - Tắt CSRF (do dùng JWT)
    - Cho phép truy cập public: /api/auth/**
    - Yêu cầu authentication cho: /api/** (còn lại)
    - Cấu hình session: STATELESS (không dùng session)
    - Thêm JWT filter vào trước UsernamePasswordAuthenticationFilter
  ```

  **Bước 2: JWT Utility Class**
  ```
  MÃ GIẢ - JwtUtil:
  
  Hàm: generateToken(username)
    - Tạo JWT token với thông tin: username, expiration time
    - Ký bằng secret key
    - Trả về token string
  
  Hàm: validateToken(token)
    - Verify token signature
    - Kiểm tra expiration
    - Trả về true/false
  
  Hàm: getUsernameFromToken(token)
    - Parse token
    - Trích xuất username
    - Trả về username
  ```

  **Bước 3: AuthController**
  ```
  MÃ GIẢ - AuthController:
  
  API: POST /api/auth/login
  Input: { username, password }
  Xử lý:
    1. Validate username và password
    2. Nếu hợp lệ: Tạo JWT token
    3. Trả về: { token, user: { id, username, email, role } }
    4. Nếu sai: Trả về 401 Unauthorized
  
  API: GET /api/auth/me
  Input: JWT token trong header Authorization
  Xử lý:
    1. Lấy username từ JWT token
    2. Query database lấy user info
    3. Trả về user object
  ```

- [ ] **Unit Tests cho Authentication**
  - Test login với credentials hợp lệ → Trả về JWT token
  - Test login với credentials sai → Trả về 401
  - Test /api/auth/me với valid token → Trả về user info
  - Test /api/auth/me không có token → Trả về 401

---

### 5. Module Publications CRUD

- [ ] **Entity Classes**

  **Publication Entity:**
  ```
  MÃ GIẢ - Publication:
  
  Các thuộc tính:
    - id: Long (Primary Key, auto-generated)
    - title: String (max 500, required)
    - publicationType: Enum (JOURNAL, CONFERENCE, etc.)
    - journalName, conferenceName: String
    - year: Integer (required)
    - volume, issue, pages, doi: String
    - abstractText: Text
    - keywords: Text
    - pdfFilename, pdfPath: String
    - status: Enum (mặc định DRAFT)
    - createdBy: User (Many-to-One relationship)
    - authors: List<PublicationAuthor> (One-to-Many relationship)
    - createdAt, updatedAt: Timestamp (tự động)
  
  Annotations:
    - @Entity, @Table
    - @NotBlank cho required fields
    - @ManyToOne, @OneToMany cho relationships
  ```

- [ ] **Repository**

  **PublicationRepository:**
  ```
  MÃ GIẢ - PublicationRepository extends JpaRepository:
  
  Các query methods:
    - findByCreatedBy(user) → Lấy publications của 1 user
    
    - findByUserAsCreatorOrCoAuthor(user) → 
        Lấy publications mà user là creator HOẶC co-author
        (dùng @Query với JOIN)
    
    - findByFilters(status, year, user, pageable) →
        Lấy publications theo filters + pagination
        (@Query với WHERE conditions động)
  ```

- [ ] **Service Layer**

  **PublicationService:**
  ```
  MÃ GIẢ - PublicationService:
  
  Hàm: createPublication(request)
    1. Lấy currentUser từ SecurityContext
    2. Tạo Publication entity mới
    3. Set các fields từ request
    4. Set createdBy = currentUser
    5. Set status = DRAFT
    6. Lưu vào database
    7. Trả về PublicationDto
  
  Hàm: listPublications(status, year, pageable)
    1. Lấy currentUser
    2. Gọi repository.findByFilters(status, year, currentUser, pageable)
    3. Convert entities sang DTOs
    4. Trả về Page<PublicationDto>
  
  Hàm: getPublication(id)
    1. Tìm publication theo id
    2. Kiểm tra quyền: user phải là creator hoặc co-author
    3. Nếu không có quyền: throw ForbiddenException
    4. Trả về PublicationDto
  
  Hàm: updatePublication(id, request)
    1. Tìm publication và kiểm tra ownership
    2. Kiểm tra: Chỉ cho phép update nếu status = DRAFT
    3. Nếu status != DRAFT: throw BadRequestException
    4. Cập nhật các fields từ request
    5. Lưu vào database
    6. Trả về PublicationDto
  
  Hàm: deletePublication(id)
    1. Tìm publication và kiểm tra ownership
    2. Kiểm tra: Chỉ cho phép delete nếu status = DRAFT
    3. Nếu status != DRAFT: throw BadRequestException
    4. Xóa khỏi database
    5. Xóa file PDF (nếu có)
  ```

- [ ] **Controller**

  **PublicationController:**
  ```
  MÃ GIẢ - PublicationController:
  
  API: POST /api/publications
  Input: CreatePublicationRequest (JSON)
  Xử lý:
    1. Validate input (@Valid annotation)
    2. Gọi service.createPublication(request)
    3. Trả về 201 Created với PublicationDto
  
  API: GET /api/publications?status=DRAFT&year=2024&page=0&size=10
  Input: Query params (optional)
  Xử lý:
    1. Parse query params
    2. Gọi service.listPublications(status, year, pageable)
    3. Trả về 200 OK với Page<PublicationDto>
  
  API: GET /api/publications/{id}
  Input: id trong path
  Xử lý:
    1. Gọi service.getPublication(id)
    2. Trả về 200 OK với PublicationDto
    3. Nếu không tìm thấy: 404 Not Found
  
  API: PUT /api/publications/{id}
  Input: UpdatePublicationRequest (JSON)
  Xử lý:
    1. Validate input
    2. Gọi service.updatePublication(id, request)
    3. Trả về 200 OK với PublicationDto
    4. Nếu status != DRAFT: 400 Bad Request
  
  API: DELETE /api/publications/{id}
  Xử lý:
    1. Gọi service.deletePublication(id)
    2. Trả về 204 No Content
    3. Nếu status != DRAFT: 400 Bad Request
  ```

- [ ] **Unit Tests**
  ```
  Tests cần viết:
  - createPublication_success: Tạo publication thành công
  - createPublication_missingRequiredField: Thiếu field bắt buộc → 400
  - updatePublication_draftStatus: Cập nhật DRAFT → success
  - updatePublication_submittedStatus: Cập nhật SUBMITTED → 400 exception
  - deletePublication_draftStatus: Xóa DRAFT → success
  - deletePublication_submittedStatus: Xóa SUBMITTED → 400 exception
  - listPublications_filterByStatus: Filter theo status hoạt động
  - listPublications_pagination: Pagination hoạt động đúng
  ```

---

### 6. Module Upload/Download File

- [ ] **FileStorageService**

  ```
  MÃ GIẢ - FileStorageService:
  
  Config: uploadDir = từ application.properties (ví dụ: /var/uploads/)
  
  Hàm: storePdfFile(file, publicationId)
    1. Validate file:
       - Kiểm tra file type = application/pdf
       - Kiểm tra size < 20MB
       - Nếu không hợp lệ: throw BadRequestException
    
    2. Generate filename an toàn:
       - Format: "publication_{publicationId}_{timestamp}.pdf"
       - Ví dụ: "publication_123_1708066800000.pdf"
    
    3. Save file:
       - Tạo đường dẫn đầy đủ: uploadDir + filename
       - Copy file input stream vào đường dẫn
       - Xử lý IOException
    
    4. Trả về: filepath đã lưu
  
  Hàm: loadPdfFile(filepath)
    1. Tạo Resource từ filepath
    2. Kiểm tra file tồn tại
    3. Nếu không tồn tại: throw FileNotFoundException
    4. Trả về Resource (để download)
  
  Hàm: validatePdfFile(file)
    - Kiểm tra: file.getSize() <= 20 * 1024 * 1024 (20MB)
    - Kiểm tra: contentType = "application/pdf"
    - Throw exception nếu vi phạm
  ```

- [ ] **FileController**

  ```
  MÃ GIẢ - FileController:
  
  API: POST /api/publications/{publicationId}/upload-pdf
  Input: MultipartFile (form-data)
  Xử lý:
    1. Gọi fileStorageService.storePdfFile(file, publicationId)
    2. Cập nhật publication: set pdfFilename, pdfPath
    3. Trả về: { filename, filepath, size }
  
  API: GET /api/publications/{publicationId}/download-pdf
  Xử lý:
    1. Lấy publication từ database
    2. Lấy pdfPath từ publication
    3. Gọi fileStorageService.loadPdfFile(pdfPath)
    4. Set response headers:
       - Content-Type: application/pdf
       - Content-Disposition: attachment; filename="..."
    5. Trả về file content
  ```

---

### 7. Module Đồng Tác Giả

- [ ] **PublicationAuthorService**

  ```
  MÃ GIẢ - PublicationAuthorService:
  
  Hàm: addCoAuthor(publicationId, addAuthorRequest)
    1. Tìm publication và kiểm tra ownership
    2. Tạo PublicationAuthor entity mới
    3. Set publication_id, author_name, author_email
    4. Tính author_order: max(current order) + 1
    5. Lưu vào database
    6. Trả về PublicationAuthorDto
  
  Hàm: removeCoAuthor(publicationId, authorId)
    1. Tìm publication author và kiểm tra ownership
    2. Lưu lại author_order của author bị xóa
    3. Xóa author khỏi database
    4. Re-order các authors còn lại:
       - Giảm order của authors có order > deleted_order
  
  Hàm: updateAuthorOrder(publicationId, authorId, newOrder)
    1. Tìm publication author
    2. Lấy old_order hiện tại
    3. Cập nhật order = new_order
    4. Điều chỉnh order của authors khác để tránh trùng
  ```

---

### 8. Module Dashboard

- [ ] **DashboardService**

  ```
  MÃ GIẢ - DashboardService:
  
  Hàm: getStats()
    1. Lấy currentUser
    2. Query database:
       - totalPublications = COUNT publications WHERE created_by = currentUser
       - publishedCount = COUNT WHERE created_by = currentUser AND status = PUBLISHED
       - draftCount = COUNT WHERE created_by = currentUser AND status = DRAFT
    3. Tính totalWorkHours:
       - Lấy tất cả publications của user
       - Tính hours theo publication_type:
         * JOURNAL → 40 giờ
         * CONFERENCE → 20 giờ
         * BOOK_CHAPTER → 60 giờ
         * OTHER → 10 giờ
       - Sum tất cả
    4. Trả về DashboardStatsDto
  
  Hàm: getWorkHours(startDate, endDate)
    1. Lấy currentUser
    2. Query publications trong khoảng [startDate, endDate]
    3. Nhóm theo publication_type
    4. Tính work hours cho từng type
    5. Trả về WorkHoursDto: { hoursByType, totalHours }
  ```

---

### 9. API Documentation (Swagger)

- [ ] **Setup Springdoc OpenAPI**

  **Bước 1: Thêm dependency**
  - Maven: springdoc-openapi-ui
  - Version: 1.7.0 hoặc mới hơn

  **Bước 2: Thêm annotations vào Controllers**
  ```
  MÃ GIẢ - Annotations:
  
  Class level:
    @Tag(name = "Publications", description = "APIs quản lý bài báo")
  
  Method level:
    @Operation(summary = "Tạo bài báo mới", description = "Tạo publication với status DRAFT")
    @ApiResponses({
      @ApiResponse(code=201, description="Tạo thành công"),
      @ApiResponse(code=400, description="Dữ liệu không hợp lệ"),
      @ApiResponse(code=401, description="Chưa đăng nhập")
    })
  ```

  **Bước 3: Truy cập Swagger UI**
  - URL: http://localhost:8080/swagger-ui.html
  - Kiểm tra tất cả APIs đã được document

---

### 10. Xử Lý Lỗi Toàn Cục

- [ ] **GlobalExceptionHandler**

```
MÃ GIẢ - GlobalExceptionHandler:

@ExceptionHandler(NotFoundException.class)
Hàm: handleNotFound(exception)
  - Tạo ErrorResponse: { status: 404, message: exception.message, timestamp }
  - Trả về 404 NOT_FOUND

@ExceptionHandler(BadRequestException.class)
Hàm: handleBadRequest(exception)
  - Tạo ErrorResponse: { status: 400, message, timestamp }
  - Trả về 400 BAD_REQUEST

@ExceptionHandler(ForbiddenException.class)
Hàm: handleForbidden(exception)
  - Tạo ErrorResponse: { status: 403, message, timestamp }
  - Trả về 403 FORBIDDEN

@ExceptionHandler(MethodArgumentNotValidException.class)
Hàm: handleValidation(exception)
  - Thu thập tất cả field errors
  - Tạo ValidationErrorResponse: 
    { status: 400, message: "Validation failed", 
      errors: { "title": "Title is required", ... } }
  - Trả về 400 BAD_REQUEST
```

---

## ✅ PHASE 3: VERIFICATION (Tuần 5)

### 11. Integration Testing

- [ ] **API Integration Tests**

  ```
  MÃ GIẢ - PublicationIntegrationTest:
  
  Setup:
    - Tạo user test, login, lấy JWT token
    - Tạo sample data trong database
  
  Test: createPublication_success
    1. Gửi POST /api/publications với data hợp lệ
    2. Header: Authorization: Bearer {token}
    3. Verify: Response 201 Created
    4. Verify: Response body có id, status=DRAFT
  
  Test: createPublication_missingRequiredField
    1. Gửi POST với title bị thiếu
    2. Verify: Response 400 Bad Request
    3. Verify: Error message chứa "Title is required"
  
  Test: listPublications_withFilters
    1. Gửi GET /api/publications?status=DRAFT&year=2024&page=0&size=10
    2. Verify: Response 200 OK
    3. Verify: Response body là Page object với content array
    4. Verify: Filters được áp dụng đúng
  
  Test: updatePublication_notOwner
    1. Login user A, tạo publication
    2. Login user B
    3. Gửi PUT /api/publications/{id} của user A
    4. Verify: Response 403 Forbidden
  
  Test: deletePublication_submittedStatus
    1. Tạo publication, submit (status = SUBMITTED)
    2. Gửi DELETE /api/publications/{id}
    3. Verify: Response 400 Bad Request
  ```

---

### 12. Performance Testing

- [ ] **Query Optimization**
  ```
  Kiểm tra:
  - N+1 query problem: 
    * Khi load publications, eager load authors nếu cần
    * Dùng @EntityGraph hoặc JOIN FETCH
  
  - Database indexes:
    * Đã thêm index cho: status, created_by, year
    * Verify bằng EXPLAIN query
  
  - Pagination:
    * Tất cả list queries phải có pagination
    * Default size = 10, max size = 100
  ```

- [ ] **Load Testing (Optional cho V1.0)**
  - Công cụ: JMeter / Gatling
  - Scenario: 100 concurrent users tạo publications
  - Target: Response time < 500ms (95th percentile)

---

### 13. Code Quality Review

- [ ] **Checklist Code Review**
  - [ ] Tất cả methods có error handling hợp lý
  - [ ] Tất cả DTOs có validation annotations (@NotBlank, @Size, etc.)
  - [ ] Tất cả queries có indexes phù hợp
  - [ ] Không có hardcoded values (dùng application.properties)
  - [ ] Tất cả public methods có Javadoc comments
  - [ ] Không có code smells (long methods > 50 lines, God classes, etc.)
  - [ ] Sensitive data (password) đã được mã hóa
  - [ ] SQL injection đã được prevent (dùng Parameterized queries)

- [ ] **SonarQube Analysis (Nếu có)**
  - Code coverage > 80%
  - 0 critical bugs
  - 0 security vulnerabilities

---

## 📊 Deliverables (Sản Phẩm Bàn Giao)

### Backend Artifacts:

1. **Spring Boot Application**
   - File JAR có thể chạy được
   - Docker image (optional)

2. **Database**
   - Migration scripts (Flyway/Liquibase)
   - Sample data SQL scripts (cho demo)

3. **API Documentation**
   - Swagger UI accessible tại `/swagger-ui.html`
   - Postman collection (exported JSON file)

4. **Test Suite**
   - Unit tests (coverage > 80%)
   - Integration tests
   - Test reports

5. **Deployment Guide**
   - Hướng dẫn chạy locally
   - Danh sách environment variables cần thiết
   - Hướng dẫn setup database

---

## ✅ Tiêu Chí Thành Công

Backend developer làm tốt khi:

✅ Tất cả APIs implement theo spec và hoạt động đúng  
✅ Unit test coverage > 80%  
✅ Integration tests pass 100%  
✅ Không có critical/high bugs từ QA  
✅ API documentation đầy đủ (Swagger)  
✅ Code review approved bởi Tech Lead  
✅ Performance chấp nhận được (< 500ms response time cho hầu hết APIs)

---

**Prepared by**: Backend Team  
**Version**: 1.0  
**Last Updated**: 16/02/2026
