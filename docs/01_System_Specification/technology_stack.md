# Technology Stack và Quyết Định Kỹ Thuật

## 1. Tổng Quan

Tài liệu này mô tả chi tiết các quyết định về công nghệ cho hệ thống quản lý công trình NCKH, bao gồm lý do lựa chọn, ưu nhược điểm, và các phương án thay thế.

---

## 2. Nguyên Tắc Chọn Công Nghệ

### 2.1. Tiêu Chí Ưu Tiên

1. ✅ **Độ phổ biến trong môi trường VN** - Dễ tìm nhân lực bảo trì
2. ✅ **Tính ổn định** - Công nghệ đã được chứng minh, ít thay đổi đột ngột
3. ✅ **Hỗ trợ cộng đồng mạnh** - Dễ tìm tài liệu, giải quyết vấn đề
4. ✅ **Chi phí hợp lý** - Ưu tiên mã nguồn mở, tránh vendor lock-in
5. ✅ **Khả năng mở rộng** - Hỗ trợ tăng trưởng số lượng người dùng

---

## 3. Frontend Stack

### 3.1. Core Technologies

| Công nghệ | Phiên bản | Lý do chọn | Phương án thay thế |
|-----------|-----------|------------|--------------------|
| **React.js** | 18.x | - Ecosystem lớn nhất<br>- Dễ tuyển developer<br>- Component reusable | Vue.js 3.x, Angular 15+ |
| **TypeScript** | 5.x | - Type safety<br>- Autocomplete tốt<br>- Giảm bug runtime | JavaScript (ES6+) |
| **Material-UI (MUI)** | 5.x | - Component library đầy đủ<br>- Design system professional<br>- Accessibility tốt | Ant Design, Chakra UI |
| **Redux Toolkit** | 1.9+ | - State management dễ dùng<br>- DevTools mạnh<br>- RTK Query cho API calls | Zustand, Recoil, Context API |

### 3.2. UI/UX Libraries

```
- React Router v6 - Routing
- React Hook Form - Form validation
- Axios - HTTP client
- Day.js - Date manipulation (nhẹ hơn Moment.js)
- Chart.js hoặc Recharts - Data visualization
- React PDF - Xem file PDF
```

### 3.3. Build Tools

```
- Vite - Build tool (nhanh hơn Create React App)
- ESLint + Prettier - Code quality
- Husky + lint-staged - Pre-commit hooks
```

---

## 4. Backend Stack

### 4.1. Khuyến Nghị: Java Spring Boot

**Lý do chọn:**
- ✅ **Phổ biến nhất tại Việt Nam** - Đặc biệt trong giáo dục và doanh nghiệp
- ✅ **Ecosystem JVM mạnh mẽ** - Hàng triệu thư viện, framework phong phú
- ✅ **Dễ tuyển nhân lực** - Java là ngôn ngữ được dạy nhiều nhất ở VN
- ✅ **Ổn định, tin cậy** - Sử dụng rộng rãi trong enterprise applications
- ✅ **Tích hợp tốt** - Dễ kết nối với LDAP/AD, MySQL, và các hệ thống cũ
- ✅ **Community support mạnh** - Documentation phong phú, dễ tìm giải pháp

**Stack cụ thể:**
```
- Spring Boot 3.x (Java 17+)
- Spring Data JPA - ORM
- Spring Security - Authentication/Authorization
- Spring Web - RESTful API
- Lombok - Reduce boilerplate code
- MapStruct - Object mapping
- Liquibase/Flyway - Database migration
- Springdoc OpenAPI - API documentation (Swagger)
- SLF4J + Logback - Logging
```

**Kiến trúc:**
```
- Layered Architecture (Controller → Service → Repository)
- Clean Architecture (tùy chọn nâng cao)
- Repository Pattern + Service Layer
- DTO Pattern (Data Transfer Objects)
```

---

### 4.2. Phương Án Thay Thế: ASP.NET Core (C#)

**Khi nào chọn:**
- Đội ngũ có kinh nghiệm .NET mạnh
- Môi trường Microsoft (Windows Server, Azure)

**Stack:**
```
- ASP.NET Core 8.0 (LTS)
- Entity Framework Core 8.0 - ORM
- Swashbuckle - Swagger/OpenAPI documentation
- Serilog - Logging structured
- Hangfire - Background jobs (nếu cần)
```

---

### 4.3. Phương Án Thay Thế: Node.js

**Khi nào chọn:**
- Đội full-stack JavaScript (frontend + backend cùng ngôn ngữ)
- Cần real-time features nhiều

**Stack:**
```
- Node.js 20.x.x LTS
- NestJS - Framework enterprise-grade
- TypeORM hoặc Prisma - ORM
- Passport.js - Authentication
- Bull - Job queue
```

---

## 5. Database

### 5.1. Khuyến Nghị: MySQL

**Lý do chọn:**
```
✅ Phổ biến nhất thế giới - Dễ tìm tài liệu, tutorial
✅ Mã nguồn mở, không phí license
✅ ACID compliance đầy đủ (từ phiên bản 8.0+)
✅ Hiệu năng cao cho read-heavy workload
✅ Dễ setup và bảo trì
✅ Tích hợp tốt với Spring Boot (Spring Data JPA)
✅ Community support mạnh tại Việt Nam
✅ JSON support (JSON datatype từ MySQL 5.7+)
```

**Phiên bản:** MySQL 8.0+ (LTS)

**Tính năng quan trọng sử dụng:**
```sql
- InnoDB engine -- ACID transactions
- Full-text search -- Tìm kiếm tiếng Việt
- JSON datatype -- Lưu metadata linh hoạt
- Indexes (B-Tree, Full-text) -- Tối ưu query
```

---

### 5.2. Phương Án Thay Thế

| Database | Khi nào chọn | Ưu điểm | Nhược điểm |
|----------|--------------|---------|------------|
| **PostgreSQL 14+** | Cần JSON/NoSQL features mạnh | Extension ecosystem, advanced features | Ít phổ biến hơn MySQL ở VN |
| **SQL Server** | Môi trường Microsoft | Tích hợp tốt .NET | Phí license đắt |
| **MariaDB** | Muốn fork MySQL mới hơn | Mã nguồn mở, performance tốt | Ecosystem nhỏ hơn MySQL |

---

### 5.3. File Storage

**Storage** là nơi lưu trữ file PDF của bài báo khoa học do giảng viên upload.

#### Khuyến nghị: Local File System (MVP)

**Cách hoạt động:**
```
1. Upload file PDF lên server
2. Lưu vào folder: /uploads/publications/{year}/{month}/{uuid}.pdf
3. Lưu path vào database (bảng publications)
4. Khi download: đọc file từ path và trả về
```

**Ưu điểm:**
- ✅ Đơn giản, dễ implement
- ✅ Không phí phát sinh
- ✅ Đủ dùng cho < 10,000 files
- ✅ Không phụ thuộc dịch vụ bên ngoài

**Nhược điểm:**
- ❌ Khó scale khi file nhiều (> 100GB)
- ❌ Cần backup thủ công
- ❌ Không có CDN (tải chậm nếu xa server)

**Implementation với Spring Boot:**
```java
@Value("${upload.path}")
private String uploadPath;

public String saveFile(MultipartFile file) {
    String fileName = UUID.randomUUID() + ".pdf";
    Path path = Paths.get(uploadPath, fileName);
    Files.copy(file.getInputStream(), path);
    return fileName; // Lưu vào DB
}
```

---

#### Phương án thay thế

**1. Cloud Storage (AWS S3, Azure Blob, Google Cloud Storage)**
- **Khi nào dùng**: Production, cần scale lớn
- **Ưu điểm**: Auto backup, CDN, không lo dung lượng
- **Nhược điểm**: Phí hàng tháng (~$10-50/tháng cho 1TB)

**2. MinIO (Self-hosted S3-compatible)**
- **Khi nào dùng**: Muốn API giống S3 nhưng tự host
- **Ưu điểm**: Dễ migrate lên AWS S3 sau, miễn phí
- **Nhược điểm**: Cần server riêng, phức tạp hơn file system

**3. Database BLOB (Không khuyến nghị)**
- Lưu file PDF trực tiếp vào database
- **Tại sao không nên**: Database phình to, query chậm

---

### 5.4. Search Engine (Tùy Chọn)

**MySQL Full-text Search (Khuyến nghị cho MVP)**

Cân nhắc sử dụng:
- ✅ Đủ dùng cho < 50,000 bài báo
- ✅ Đã built-in trong MySQL, không cần cài thêm
- ✅ Hỗ trợ tiếng Việt có dấu

**Elasticsearch 8.x (Giai đoạn 2)**

Nâng cấp khi:
- Số lượng công trình > 50,000
- Cần search phức tạp (fuzzy, synonym, autocomplete)
- Cần search realtime với độ trễ thấp

---

## 6. Authentication & Authorization

### 6.1. Strategy

```
Ưu tiên 1: LDAP/Active Directory (SSO nội bộ)
Ưu tiên 2: JWT (JSON Web Token) cho API
Ưu tiên 3: OAuth 2.0 (kết nối hệ thống bên ngoài)
```

### 6.2. Implementation

**ASP.NET Core:**
```csharp
- ASP.NET Core Identity - User management
- Microsoft.AspNetCore.Authentication.JwtBearer
- Microsoft.AspNetCore.Authentication.OpenIdConnect
```

**RBAC (Role-Based Access Control):**
```
Roles:
- SuperAdmin (quản trị hệ thống)
- Admin (cán bộ QLKH)
- Researcher (nhà nghiên cứu)
- Viewer (sinh viên, độc giả)

Permissions: Gán theo chức năng (Create, Read, Update, Delete, Approve...)
```

---

## 7. Security Stack

### 7.1. Bảo Mật Tầng Transport

```
- HTTPS (SSL/TLS 1.3) - Bắt buộc toàn bộ
- HSTS (HTTP Strict Transport Security)
- Certificate: Let's Encrypt (miễn phí) hoặc DigiCert
```

### 7.2. Bảo Mật Dữ Liệu

```
- Mã hóa at-rest: AES-256
- Hash password: bcrypt / Argon2
- Sensitive data: Encrypt trước khi lưu DB
```

### 7.3. Bảo Mật API

```
- Rate Limiting (100 requests/minute/IP)
- CORS policy rõ ràng
- Input validation (Fluent Validation)
- Output encoding (chống XSS)
- CSRF protection
```

### 7.4. Antivirus

**ClamAV** - Scan file upload

```
- Scan ngay khi upload
- Quarantine file nghi ngờ
- Log tất cả file bị reject
```

---

## 8. DevOps & Infrastructure

### 8.1. Containerization

**Docker**
```dockerfile
Frontend: nginx + React build
Backend: ASP.NET Core runtime
Database: postgres:14-alpine
Cache: redis:7-alpine (nếu cần)
```

**Docker Compose** cho development environment

---

### 8.2. CI/CD

**GitHub Actions** (nếu dùng GitHub)

```yaml
Pipeline:
1. Code push → Trigger build
2. Run linters (ESLint, Prettier)
3. Run unit tests
4. Build Docker images
5. Push to registry (Docker Hub / ACR)
6. Deploy to staging (auto)
7. Deploy to production (manual approve)
```

**Phương án thay thế:**
- GitLab CI/CD
- Azure DevOps
- Jenkins

---

### 8.3. Monitoring & Logging

**Stack khuyến nghị:**
```
- Prometheus - Metrics collection
- Grafana - Visualization
- Loki - Log aggregation (alternative: ELK stack)
- Serilog - Structured logging (.NET)
```

**Metrics cần theo dõi:**
- API response time (p50, p95, p99)
- Error rate
- Database connection pool
- Memory/CPU usage
- Disk space

---

## 9. Tích Hợp Hệ Thống Bên Ngoài

### 9.1. Cơ Sở Dữ Liệu Quốc Gia KH&CN

**Protocol:** REST API hoặc SOAP (tùy Bộ KH&CN cung cấp)

**Thư viện:**
- ASP.NET: HttpClient + Polly (retry policy)
- Java: RestTemplate hoặc WebClient
- Node.js: Axios

**Xử lý lỗi:**
- Retry 3 lần với exponential backoff
- Lưu queue nếu API down → sync sau
- Logging đầy đủ request/response

---

### 9.2. Cổng Dịch Vụ Công

**VNeID / Smart CA Integration**

**Thư viện:**
- SAML 2.0 authentication
- Tham khảo SDK do Bộ TT&TT cung cấp

---

### 9.3. ORCID, Crossref, Google Scholar

**RESTful API calls**
```
- Rate limiting tuân thủ API provider
- Cache results để giảm calls
- Async processing (background jobs)
```

---

## 10. Development Tools

### 10.1. IDE

**Backend (.NET):**
- Visual Studio 2022 Community (free)
- Rider (JetBrains - paid, nhưng tốt hơn)
- VS Code + C# extension

**Frontend:**
- VS Code + ESLint, Prettier, Volar

---

### 10.2. Database Tools

- pgAdmin 4 - PostgreSQL GUI
- DBeaver - Multi-database support
- TablePlus - Modern, elegant UI

---

### 10.3. API Testing

- Postman - Manual testing
- Swagger UI - Auto-generated từ code
- k6 hoặc JMeter - Load testing

---

## 11. Ma Trận So Sánh Backend Frameworks

| Tiêu chí | ASP.NET Core | Spring Boot | Node.js (NestJS) |
|----------|--------------|-------------|------------------|
| **Hiệu năng** | ⭐⭐⭐⭐⭐ (Tốt nhất) | ⭐⭐⭐⭐ | ⭐⭐⭐ |
| **Type Safety** | ⭐⭐⭐⭐⭐ (C# static) | ⭐⭐⭐⭐⭐ (Java static) | ⭐⭐⭐⭐ (TypeScript) |
| **Ecosystem** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Learning Curve** | ⭐⭐⭐ (Trung bình) | ⭐⭐⭐ | ⭐⭐⭐⭐ (Dễ hơn) |
| **Nhân lực VN** | ⭐⭐⭐⭐ (Dễ tìm) | ⭐⭐⭐⭐⭐ (Rất dễ) | ⭐⭐⭐⭐ |
| **Chi phí** | ⭐⭐⭐⭐⭐ (Free) | ⭐⭐⭐⭐⭐ (Free) | ⭐⭐⭐⭐⭐ (Free) |
| **Enterprise Ready** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ |

**Kết luận:**  
✅ **ASP.NET Core** nếu môi trường Microsoft, team .NET  
✅ **Spring Boot** nếu team Java, cần ecosystem JVM mạnh  
✅ **NestJS** nếu team full-stack JS, ưu tiên rapid development  

---

## 12. Quyết Định Cuối Cùng (Khuyến Nghị)

### MVP (Minimum Viable Product)

```
Frontend:  React 18 + TypeScript + MUI + Redux Toolkit
Backend:   Java Spring Boot 3.x + Spring Data JPA
Database:  MySQL 8.0+
Storage:   Local File System (với cấu trúc rõ ràng)
Auth:      JWT + LDAP/AD integration (Spring Security)
Deploy:    Docker + Docker Compose
```

**Lý do lựa chọn Stack này:**
- ✅ **Java** phổ biến nhất tại VN, dễ tuyển người
- ✅ **Spring Boot** có ecosystem mạnh, documentation đầy đủ
- ✅ **MySQL** dễ setup, free, phổ biến
- ✅ **Local Storage** đơn giản, đủ dùng cho giai đoạn đầu
- ✅ Toàn bộ stack đều mã nguồn mở, không phí license

### Giai Đoạn 2 (Scale)

```
+ Kubernetes orchestration
+ Redis caching (Spring Cache)
+ Elasticsearch full-text search
+ Cloud Storage (AWS S3 hoặc MinIO)
+ CDN cho static assets
+ Load balancer (Nginx / HAProxy)
```

---

*Tài liệu này nên được review lại mỗi 6 tháng để cập nhật phiên bản mới của các công nghệ.*
