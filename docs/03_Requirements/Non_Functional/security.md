# Yêu Cầu Bảo Mật - Security Requirements

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Danh mục**: Non-Functional Requirements

---

## 1. Authentication Requirements

### NFR-SEC-001: LDAP/AD Integration (SSO)
**Requirement**: Tất cả internal users PHẢI đăng nhập qua LDAP/AD

**Implementation**:
- Spring Security + LDAP
- No local password storage
- Session timeout: 8 giờ
- Remember me: 30 ngày (optional)

---

### NFR-SEC-002: JWT Token Security
**Requirements**:
- Algorithm: HS256 hoặc RS256
- Expiry: 24 giờ
- Refresh token: 7 ngày
- Store in HttpOnly cookie (not localStorage)

---

## 2. Authorization Requirements

### NFR-SEC-010: Role-Based Access Control (RBAC)
**Roles**: SuperAdmin, Researcher, Faculty Reviewer, University Reviewer, Viewer

**Enforcement**:
- Backend: Check role trước mọi API call
- Frontend: Hide UI elements based on role
- Database: Row-level security (optional)

---

### NFR-SEC-011: Publication Access Control
**Rules**:
- DRAFT: CHỈ owner + admin
- SUBMITTED/REVIEWING: Owner + reviewer (by faculty) + admin
- PUBLISHED: Everyone

---

## 3. Data Protection

### NFR-SEC-020: HTTPS Mandatory
**Requirement**: Tất cả traffic PHẢI qua HTTPS

- TLS 1.2 minimum (TLS 1.3 preferred)
- Certificate từ Let's Encrypt hoặc commercial CA
- HSTS (HTTP Strict Transport Security)
- Redirect HTTP → HTTPS

---

### NFR-SEC-021: Personal Data Protection
**Compliance**: Nghị định 13/2023/NĐ-CP

**Protected data**:
- Email addresses
- ORCID
- Personal contact info

**Measures**:
- No public display without consent
- Encrypted trong database (optional)
- Audit logs cho mọi access

---

### NFR-SEC-022: File Upload Security
**Validations**:
- File type: CHỈ PDF (check magic bytes, không chỉ extension)
- Virus scan (ClamAV - optional)
- Sanitize filename
- Store outside webroot
- Generate random filename

---

## 4. Input Validation

### NFR-SEC-030: XSS Prevention
**Measures**:
- Sanitize tất cả user input
- Escape output trong HTML
- Content Security Policy (CSP) headers
- Use React (auto-escaping)

---

### NFR-SEC-031: SQL Injection Prevention
**Measures**:
- Prepared statements (JDBC)
- ORM (JPA/Hibernate)
- KHÔNG concatenate SQL strings

---

### NFR-SEC-032: CSRF Protection
**Measures**:
- CSRF tokens (Spring Security default)
- SameSite cookie attribute
- Verify Origin header

---

## 5. API Security

### NFR-SEC-040: API Rate Limiting
**Limits**:
- Public API: 100 requests/hour per IP
- Authenticated API: 1000 requests/hour per user
- Admin API: Unlimited

**Response**: HTTP 429 Too Many Requests

---

### NFR-SEC-041: API Input Validation
**Validations**:
- Max request size: 15MB (cho PDF upload)
- JSON schema validation
- Whitelist allowed fields
- Reject unknown parameters

---

## 6. Audit & Logging

### NFR-SEC-050: Audit Trail
**Log events**:
- User login/logout
- Failed login attempts
- Publication state changes
- User role changes
- File downloads
- Admin operations

**Log fields**:
- User ID, IP address
- Timestamp
- Action type
- Resource ID
- Before/After values (for changes)

---

### NFR-SEC-051: Security Logs
**Log to separate file**:
- Authentication failures
- Authorization failures
- Suspicious activities
- Error 500 (server errors)

**Retention**: 1 năm minimum

---

## 7. Password Policy (nếu có local accounts)

### NFR-SEC-060: Password Requirements
**Note**: Primary auth là LDAP/AD, nhưng nếu có local accounts:

- Min length: 8 characters
- Require: Upper + Lower + Number
- Special characters: Recommended
- No common passwords (check against list)
- Expiry: 90 ngày
- History: Không reuse 5 passwords gần nhất

---

## 8. Session Management

### NFR-SEC-070: Session Security
**Requirements**:
- Session ID: Random, unpredictable
- Rotate session ID after login
- Invalidate on logout
- Session timeout: 8 giờ inactivity
- Concurrent sessions: Allow (same user, different devices)

---

## 9. Vulnerability Management

### NFR-SEC-080: Dependency Scanning
**Tools**: OWASP Dependency-Check, npm audit

**Frequency**: Weekly

**Action**: Patch critical vulnerabilities trong 7 ngày

---

### NFR-SEC-081: Penetration Testing
**Frequency**: Yearly hoặc before major releases

**Scope**: OWASP Top 10

---

## 10. Backup & Recovery Security

### NFR-SEC-090: Backup Encryption
**Requirement**: Tất cả backups PHẢI encrypted

- Encryption: AES-256
- Keys: Securely stored (không trong code)
- Offsite storage: Recommended

---

### NFR-SEC-091: Access to Backups
**Restriction**: CHỈ SuperAdmin + IT team

---

## 11. Error Handling

### NFR-SEC-100: Secure Error Messages
**Requirements**:
- KHÔNG expose stack traces to users
- Generic error messages
- Detailed logs to server only

**Examples**:
- ✅ "Invalid credentials"
- ❌ "User 'admin' not found in database 'ufpms'"

---

## 12. Third-Party Integration Security

### NFR-SEC-110: API Key Management
**For integrations**: ORCID, DOI Resolver, Email

**Requirements**:
- Store trong environment variables (KHÔNG hard-code)
- Rotate keys quarterly
- Use HTTPS only
- Monitor usage

---

## 13. Compliance Checklist

### NFR-SEC-120: Security Compliance
**Standards to follow**:
- ✅ OWASP Top 10 (2021)
- ✅ GDPR principles (if applicable)
- ✅ Nghị định 13/2023/NĐ-CP (Vietnam data protection)

---

**Tài liệu liên quan**:
- [Constraints](../../01_System_Specification/constraints.md)
- [Legal Framework](../../00_Problem_Context/legal_framework.md)
