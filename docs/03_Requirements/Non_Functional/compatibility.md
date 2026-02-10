# Yêu Cầu Tương Thích - Compatibility Requirements

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Danh mục**: Non-Functional Requirements

---

## 1. Browser Compatibility

### NFR-COM-001: Supported Browsers
**Desktop**:
- ✅ Google Chrome 90+ (Primary)
- ✅ Mozilla Firefox 88+
- ✅ Microsoft Edge 90+
- ✅ Safari 14+ (macOS)

**Mobile**:
- ✅ Chrome Mobile (Android)
- ✅ Safari Mobile (iOS 13+)

**NOT supported**:
- ❌ Internet Explorer (any version)

**Testing**: BrowserStack hoặc manual testing

---

## 2. Operating System Compatibility

### NFR-COM-010: Server OS
**Supported**:
- ✅ Windows Server 2019+
- ✅ Linux (Ubuntu 20.04+, CentOS 8+)

**Preferred**: Linux (better performance)

---

### NFR-COM-011: Client OS
**End users** (any modern OS):
- Windows 10/11
- macOS 10.15+
- Linux (Ubuntu, Fedora...)
- iOS, Android

---

## 3. Device Compatibility

### NFR-COM-020: Screen Sizes
**Desktop**:
- 1920x1080 (Full HD)
- 1366x768 (Laptop common)
- 2560x1440 (2K)

**Tablet**:
- 768x1024 (iPad)
- 800x1280 (Android tablet)

**Mobile**:
- 375x667 (iPhone 8)
- 414x896 (iPhone 11)
- 360x640 (Android)

**Approach**: Responsive design (mobile-first)

---

## 4. Database Compatibility

### NFR-COM-030: MySQL Versions
**Supported**:
- MySQL 8.0+ (Preferred)
- MySQL 5.7 (Legacy support)
- MariaDB 10.5+ (Compatible)

**NOT supported**:
- MySQL < 5.7

---

## 5. Integration Compatibility

### NFR-COM-040: LDAP/AD Versions
**Supported**:
- Active Directory (Windows Server 2016+)
- OpenLDAP 2.4+

**Protocol**: LDAPv3

---

### NFR-COM-041: Email Servers
**SMTP compatibility**:
- Microsoft Exchange Server
- Postfix, Sendmail
- Gmail SMTP
- Any SMTP-compliant server

---

### NFR-COM-042: API Integrations
**Third-party APIs**:
- ORCID API (REST)
- CrossRef API (REST)
- DOI.org resolver (HTTP)

**Versioning**: Client adapts to API changes

---

## 6. File Format Compatibility

### NFR-COM-050: File Upload
**Accepted**:
- ✅ PDF only (`.pdf`)

**PDF versions**: 1.4 trở lên

---

### NFR-COM-051: Export Formats
**Reports**:
- Excel (.xlsx) - Excel 2007+
- PDF (PDF/A for archival)
- CSV (UTF-8)

**Citations**:
- BibTeX
- RIS
- JSON

---

## 7. Network Compatibility

### NFR-COM-060: Protocols
**Supported**:
- HTTPS (TLS 1.2+)
- WebSocket (for realtime - optional)
- SMTP (email)
- LDAP (authentication)

---

### NFR-COM-061: Firewall Requirements
**Inbound ports**:
- 443 (HTTPS)
- 80 (HTTP redirect to HTTPS)

**Outbound ports**:
- 443 (HTTPS for APIs)
- 25/587 (SMTP)
- 389/636 (LDAP/LDAPS)

---

## 8. Encoding & Localization

### NFR-COM-070: Character Encoding
**Standard**: UTF-8 (tất cả layers)

**Support**:
- Tiếng Việt (có dấu)
- English
- Special characters (trong citations)

---

### NFR-COM-071: Date/Time Format
**Display**: dd/MM/yyyy HH:mm (Việt Nam)

**Storage**: ISO 8601 (yyyy-MM-dd'T'HH:mm:ss'Z')

**Timezone**: UTC trong DB, convert to ICT (+7) khi hiển thị

---

## 9. Backward Compatibility

### NFR-COM-080: API Versioning
**Guarantee**: API v1 hỗ trợ ít nhất 1 năm sau khi ra v2

**Deprecation notice**: 6 tháng trước

---

### NFR-COM-081: Database Migrations
**Requirement**: Zero-downtime migrations

**Strategy**:
- Additive changes (add columns, not remove)
- Backward-compatible schema changes

---

## 10. Third-Party Library Compatibility

### NFR-COM-090: Dependency Versions
**Backend** (Java):
- Spring Boot 3.x
- JDK 17+

**Frontend** (JavaScript):
- React 18+
- Node.js 18+ (for build)

**Upgrade policy**: Follow LTS releases

---

**Tài liệu liên quan**:
- [Technology Stack](../../01_System_Specification/technology_stack.md)
- [Constraints](../../01_System_Specification/constraints.md)
