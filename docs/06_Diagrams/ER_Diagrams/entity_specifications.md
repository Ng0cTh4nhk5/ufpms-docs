# Entity Specifications

> 📊 **Database**: MySQL 8.0+  
> 🎯 **Purpose**: Chi tiết specifications cho từng entity  
> 📅 **Created**: 11/02/2026

---

## 📋 Table of Contents

1. [users](#users)
2. [publications](#publications)
3. [publication_authors](#publication_authors)
4. [review_history](#review_history)
5. [review_comments](#review_comments)
6. [user_roles](#user_roles)
7. [departments](#departments)
8. [faculties](#faculties)
9. [publication_types](#publication_types)
10. [roles](#roles)

---

## 1. users

### Purpose
Store all system users (researchers, reviewers, admins)

### Columns

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| `id` | INT | PK, AUTO_INCREMENT | Unique user ID |
| `username` | VARCHAR(50) | UNIQUE, NOT NULL | LDAP username |
| `name` | VARCHAR(100) | NOT NULL | Full name |
| `email` | VARCHAR(100) | | Email address |
| `department_id` | INT | FK → departments.id | User's department |
| `created_at` | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Account creation |
| `last_login` | TIMESTAMP | NULL | Last login time |
| `is_active` | BOOLEAN | DEFAULT TRUE | Account status |

### Indexes
```sql
CREATE UNIQUE INDEX idx_username ON users(username);
CREATE INDEX idx_department ON users(department_id);
CREATE INDEX idx_active ON users(is_active);
```

### Sample Data
```sql
INSERT INTO users (username, name, email, department_id) VALUES
('nguyen.van.a', 'Nguyễn Văn A', 'nguyen.van.a@university.edu.vn', 1),
('tran.thi.b', 'Trần ThịB', 'tran.thi.b@university.edu.vn', 2);
```

### Business Rules
- Username từ LDAP (không lưu password)
- `is_active = false` → User không thể login
- Soft delete: set `is_active = false` thay vì DELETE

---

## 2. publications

### Purpose
Store research publications

### Columns

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| `id` | INT | PK, AUTO_INCREMENT | Unique publication ID |
| `title` | VARCHAR(500) | NOT NULL | Publication title |
| `publication_type` | VARCHAR(50) | NOT NULL | JOURNAL, CONFERENCE, etc. |
| `year` | INT | NOT NULL | Publication year |
| `journal` | VARCHAR(200) | | Journal/Conference name |
| `doi` | VARCHAR(100) | UNIQUE, NULL | Digital Object Identifier |
| `issn` | VARCHAR(20) | | ISSN number |
| `abstract` | TEXT | | Abstract |
| `keywords` | VARCHAR(500) | | Comma-separated keywords |
| `pdf_path` | VARCHAR(255) | | File path to PDF |
| `status` | ENUM | NOT NULL | Workflow status |
| `owner_id` | INT | FK → users.id, NOT NULL | Creator |
| `submitted_at` | TIMESTAMP | NULL | Submission timestamp |
| `published_at` | TIMESTAMP | NULL | Publication timestamp |
| `created_at` | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Created |
| `updated_at` | TIMESTAMP | ON UPDATE CURRENT_TIMESTAMP | Last updated |
| `deleted_at` | TIMESTAMP | NULL | Soft delete |

### Status ENUM Values
```sql
ENUM('DRAFT', 'SUBMITTED', 'FACULTY_REVIEWING', 'FACULTY_APPROVED', 
     'UNIVERSITY_REVIEWING', 'PUBLISHED', 'REVISION_REQUIRED', 
     'REJECTED', 'WITHDRAWN')
```

### Indexes
```sql
CREATE UNIQUE INDEX idx_doi ON publications(doi);
CREATE INDEX idx_status_year ON publications(status, year);
CREATE INDEX idx_owner ON publications(owner_id);
CREATE INDEX idx_type ON publications(publication_type);
CREATE FULLTEXT INDEX idx_search ON publications(title, abstract, keywords);
```

### Sample Data
```sql
INSERT INTO publications (title, publication_type, year, journal, doi, status, owner_id) VALUES
('Machine Learning for Healthcare', 'JOURNAL', 2024, 'IEEE Transactions', '10.1234/example', 'PUBLISHED', 1);
```

### Business Rules
- `doi` must be unique if provided
- `status = PUBLISHED` → `published_at` must be set
- `deleted_at != NULL` → Soft deleted, không visible

---

## 3. publication_authors

### Purpose
N:M junction table between publications and users (authors)

### Columns

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| `publication_id` | INT | FK → publications.id | Publication reference |
| `user_id` | INT | FK → users.id | Author (user) |
| `author_order` | INT | NOT NULL | Author order (1, 2, 3...) |
| `role` | VARCHAR(50) | DEFAULT 'AUTHOR' | Author role |
| `is_corresponding` | BOOLEAN | DEFAULT FALSE | Corresponding author flag |

### Primary Key
```sql
PRIMARY KEY (publication_id, user_id)
```

### Indexes
```sql
CREATE INDEX idx_user ON publication_authors(user_id);
CREATE INDEX idx_pub ON publication_authors(publication_id);
```

### Sample Data
```sql
INSERT INTO publication_authors (publication_id, user_id, author_order, is_corresponding) VALUES
(1, 1, 1, TRUE),
(1, 2, 2, FALSE);
```

### Business Rules
- `author_order` must be unique per publication
- At least 1 author per publication
- Owner (creator) usually first author

---

## 4. review_history

### Purpose
Audit trail for approval workflow

### Columns

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| `id` | INT | PK, AUTO_INCREMENT | Unique history ID |
| `publication_id` | INT | FK → publications.id, NOT NULL | Publication |
| `from_status` | VARCHAR(50) | NOT NULL | Previous status |
| `to_status` | VARCHAR(50) | NOT NULL | New status |
| `actor_id` | INT | FK → users.id, NOT NULL | Who made the change |
| `action` | VARCHAR(50) | NOT NULL | Action type |
| `comments` | TEXT | | Optional comments |
| `created_at` | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | When |

### Action Values
```
'SUBMIT', 'APPROVE', 'REJECT', 'REQUEST_REVISION', 
'PUBLISH', 'WITHDRAW', 'SEND_BACK'
```

### Indexes
```sql
CREATE INDEX idx_publication ON review_history(publication_id);
CREATE INDEX idx_actor ON review_history(actor_id);
CREATE INDEX idx_created ON review_history(created_at);
```

### Sample Data
```sql
INSERT INTO review_history (publication_id, from_status, to_status, actor_id, action) VALUES
(1, 'DRAFT', 'SUBMITTED', 1, 'SUBMIT'),
(1, 'FACULTY_REVIEWING', 'FACULTY_APPROVED', 2, 'APPROVE');
```

### Business Rules
- Immutable (no UPDATE or DELETE)
- One record per state transition
- Used for audit logs và timeline

---

## 5. review_comments

### Purpose
Comments from reviewers

### Columns

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| `id` | INT | PK, AUTO_INCREMENT | Unique comment ID |
| `publication_id` | INT | FK → publications.id, NOT NULL | Publication |
| `reviewer_id` | INT | FK → users.id, NOT NULL | Reviewer |
| `comment_type` | VARCHAR(50) | NOT NULL | Type |
| `comment_text` | TEXT | NOT NULL | Comment content |
| `created_at` | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | When |

### Comment Type Values
```
'APPROVAL_COMMENT', 'REVISION_REQUEST', 'REJECTION_REASON', 'GENERAL_FEEDBACK'
```

### Indexes
```sql
CREATE INDEX idx_publication ON review_comments(publication_id);
CREATE INDEX idx_reviewer ON review_comments(reviewer_id);
```

### Sample Data
```sql
INSERT INTO review_comments (publication_id, reviewer_id, comment_type, comment_text) VALUES
(1, 2, 'REVISION_REQUEST', 'Please add more details to the methodology section.');
```

### Business Rules
- Visible to: owner, reviewers, admins
- Not editable after creation
- Required for REVISION_REQUIRED và REJECTED actions

---

## 6. user_roles

### Purpose
Assign roles to users

### Columns

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| `user_id` | INT | FK → users.id | User |
| `role_name` | VARCHAR(50) | FK → roles.name | Role |
| `assigned_by` | INT | FK → users.id | Who assigned |
| `assigned_at` | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | When |

### Primary Key
```sql
PRIMARY KEY (user_id, role_name)
```

### Sample Data
```sql
INSERT INTO user_roles (user_id, role_name, assigned_by) VALUES
(1, 'RESEARCHER', 1),
(2, 'FACULTY_REVIEWER', 1);
```

### Business Rules
- One user có multiple roles
- Default role: RESEARCHER (auto-assigned at first login)
- Only SuperAdmin can assign/remove roles

---

## 7. departments

### Purpose
Academic departments

### Columns

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| `id` | INT | PK, AUTO_INCREMENT | Unique department ID |
| `name` |VARCHAR(100) | NOT NULL | Department name |
| `faculty_id` | INT | FK → faculties.id | Parent faculty |

### Sample Data
```sql
INSERT INTO departments (name, faculty_id) VALUES
('Khoa Công Nghệ Thông Tin', 1),
('Khoa Điện - Điện Tử', 1);
```

---

## 8. faculties

### Purpose
Academic faculties

### Columns

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| `id` | INT | PK, AUTO_INCREMENT | Unique faculty ID |
| `name` | VARCHAR(100) | NOT NULL | Faculty name |
| `code` | VARCHAR(20) | UNIQUE, NOT NULL | Faculty code |

### Sample Data
```sql
INSERT INTO faculties (name, code) VALUES
('Khoa Kỹ Thuật và Công Nghệ', 'KTKH'),
('Khoa Kinh Tế', 'KTE');
```

---

## 9. publication_types

### Purpose
Lookup table for publication types

### Columns

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| `code` | VARCHAR(50) | PK | Type code |
| `name` | VARCHAR(100) | NOT NULL | Display name |

### Sample Data
```sql
INSERT INTO publication_types (code, name) VALUES
('JOURNAL', 'Journal Article'),
('CONFERENCE', 'Conference Paper'),
('BOOK_CHAPTER', 'Book Chapter');
```

---

## 10. roles

### Purpose
System roles definition

### Columns

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| `name` | VARCHAR(50) | PK | Role name |
| `description` | VARCHAR(255) | | Role description |

### Sample Data
```sql
INSERT INTO roles (name, description) VALUES
('RESEARCHER', 'Can create and manage own publications'),
('FACULTY_REVIEWER', 'Can review publications at faculty level'),
('UNIVERSITY_REVIEWER', 'Can approve publications at university level'),
('SUPERADMIN', 'Full system access');
```

---

**Related**: complete_erd.md  
**Created**: 11/02/2026
