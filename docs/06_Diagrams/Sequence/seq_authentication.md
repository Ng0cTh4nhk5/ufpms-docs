# Biểu đồ Tuần tự: Xác thực Người dùng

> 📊 **ID Biểu đồ**: SEQ-07  
> 🎯 **Ca Sử Dụng**: Xác thực Hệ thống  
> 👤 **Tác nhân**: Tất cả người dùng nội bộ  
> ⚙️ **Chính**: Tích hợp LDAP/AD, tạo token JWT

---

## 📊 Biểu đồ Tuần tự

```mermaid
sequenceDiagram
    actor User as 👤 Người dùng
    participant UI as 🖥️ Giao diện Đăng nhập
    participant API as 🔌 AuthController
    participant AuthService as 🔐 AuthService
    participant LDAP as 📁 Máy chủ LDAP/AD
    participant UserRepo as 💾 UserRepository
    participant DB as 🗄️ CSDL
    participant TokenService as 🎫 JWTService
    
    %% Mở trang đăng nhập
    User->>UI: Điều hướng đến /login
    UI-->>User: Hiển thị biểu mẫu đăng nhập
    
    %% Nhập thông tin xác thực
    User->>UI: Nhập tên đăng nhập + mật khẩu
    User->>UI: Nhấn "Đăng nhập"
    
    activate UI
    UI->>API: POST /api/auth/login
    activate API
    Note over API: Yêu cầu:<br/>{username, password}
    
    %% Xác thực với LDAP
    API->>AuthService: authenticate(username, password)
    activate AuthService
    
    AuthService->>LDAP: LDAP Bind(username, password)
    activate LDAP
    
    alt Thông tin xác thực không hợp lệ
        LDAP-->>AuthService: Xác thực thất bại
        AuthService-->>API: AuthenticationError
        API-->>UI: 401 Unauthorized
        UI-->>User: "Tên đăng nhập hoặc mật khẩu không đúng"
    else Thông tin xác thực hợp lệ
        LDAP-->>AuthService: Xác thực thành công
        deactivate LDAP
        
        %% Lấy hoặc tạo người dùng
        AuthService->>UserRepo: findByUsername(username)
        activate UserRepo
        UserRepo->>DB: SELECT * FROM users<br/>WHERE username = ?
        
        alt Người dùng tồn tại
            DB-->>UserRepo: Bản ghi người dùng
            UserRepo-->>AuthService: Người dùng
        else Người dùng không tìm thấy
            Note over AuthService: Đăng nhập lần đầu<br/>Tự động tạo người dùng
            
            %% Lấy thông tin người dùng từ LDAP
            AuthService->>LDAP: Lấy thuộc tính người dùng
            activate LDAP
            LDAP-->>AuthService: {name, email, department}
            deactivate LDAP
            
            AuthService->>UserRepo: createUser(ldapData)
            UserRepo->>DB: INSERT INTO users<br/>(username, name, email, department)
            DB-->>UserRepo: ID người dùng mới
            UserRepo-->>AuthService: Người dùng mới
        end
        deactivate UserRepo
        
        %% Lấy vai trò người dùng
        AuthService->>UserRepo: getUserRoles(userId)
        activate UserRepo
        UserRepo->>DB: SELECT roles<br/>FROM user_roles<br/>WHERE user_id = ?
        DB-->>UserRepo: Mảng vai trò
        UserRepo-->>AuthService: Vai trò[]
        deactivate UserRepo
        
        %% Tạo token JWT
        AuthService->>TokenService: generateToken(user, roles)
        activate TokenService
        
        Note over TokenService: Payload:<br/>{userId, username,<br/>name, roles,<br/>exp: now + 24h}
        
        TokenService->>TokenService: Ký với khóa bí mật
        TokenService-->>AuthService: Token JWT
        deactivate TokenService
        
        %% Ghi nhật ký đăng nhập
        AuthService->>UserRepo: logLogin(userId, ipAddress)
        UserRepo->>DB: INSERT INTO audit_logs
        
        AuthService-->>API: {token, user}
        deactivate AuthService
        
        API-->>UI: 200 OK + {token, user, roles}
        deactivate API
        
        %% Lưu trữ token
        UI->>UI: Lưu trữ token trong localStorage
        Note over UI: localStorage.setItem(<br/>'authToken', token)
        
        UI-->>User: Chuyển hướng đến bảng điều khiển
        deactivate UI
    end
```

---

## 📋 Luồng Xác thực

### 1. Người dùng Gửi Thông tin Xác thực
- Tên đăng nhập (ví dụ: `nguyen.van.a`)
- Mật khẩu

### 2. Xác thực LDAP
**LDAP Bind** (xác thực thông tin):
```java
ldapTemplate.authenticate(
    "ou=users,dc=university,dc=edu.vn",
    "(uid=" + username + ")",
    password
);
```

Nếu thành công → Lấy thuộc tính người dùng

### 3. Lấy/Tạo Người dùng
**Nếu người dùng tồn tại trong DB**:
- Lấy từ bảng `users`

**Nếu đăng nhập lần đầu**:
- Truy vấn LDAP để lấy thuộc tính:
  - Họ tên
  - Email
  - Bộ môn
  - Khoa
- Tạo bản ghi người dùng trong DB
- Gán vai trò mặc định: `RESEARCHER`

### 4. Lấy Vai trò
Truy vấn bảng `user_roles`:
```sql
SELECT role_name 
FROM user_roles 
WHERE user_id = ?
```

Các vai trò có thể:
- `RESEARCHER`
- `FACULTY_REVIEWER`
- `UNIVERSITY_REVIEWER`
- `SUPERADMIN`

### 5. Tạo Token JWT
**Payload**:
```json
{
  "sub": "nguyen.van.a",      // username
  "userId": 123,
  "name": "Nguyen Van A",
  "email": "nguyen.van.a@university.edu.vn",
  "roles": ["RESEARCHER", "FACULTY_REVIEWER"],
  "iat": 1707612345,          // issued at
  "exp": 1707698745           // expires (24h)
}
```

**Ký với khóa bí mật** → Token JWT

### 6. Trả về Client
Phản hồi:
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "id": 123,
    "username": "nguyen.van.a",
    "name": "Nguyen Van A",
    "email": "nguyen.van.a@university.edu.vn",
    "roles": ["RESEARCHER", "FACULTY_REVIEWER"]
  }
}
```

### 7. Lưu trữ Token
Giao diện lưu trữ token trong `localStorage` hoặc `sessionStorage`

### 8. Các Yêu cầu Tiếp theo
Mỗi cuộc gọi API bao gồm:
```
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

---

## 🔒 Ủy quyền

### Xác minh JWT
Mỗi endpoint được bảo vệ:
```java
@PreAuthorize("hasRole('RESEARCHER')")
public ResponseEntity<?> createPublication(...) {
    // Logic endpoint
}
```

**Middleware** xác minh:
1. Token tồn tại trong header `Authorization`
2. Chữ ký token hợp lệ
3. Token chưa hết hạn
4. Người dùng có vai trò yêu cầu

---

## 🗄️ Bảng Cơ sở Dữ liệu

### Bảng users
```sql
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) UNIQUE NOT NULL,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100),
    department VARCHAR(100),
    faculty_id INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    last_login TIMESTAMP
);
```

### Bảng user_roles
```sql
CREATE TABLE user_roles (
    user_id INT,
    role_name ENUM('RESEARCHER', 'FACULTY_REVIEWER', 'UNIVERSITY_REVIEWER', 'SUPERADMIN'),
    assigned_at TIMESTAMP,
    assigned_by INT,
    PRIMARY KEY (user_id, role_name)
);
```

### Bảng audit_logs (theo dõi đăng nhập)
```sql
INSERT INTO audit_logs (
    user_id, action, ip_address, timestamp
) VALUES (
    123, 'LOGIN', '192.168.1.100', NOW()
);
```

---

## 🚨 Các Kịch Bản Lỗi

### 401 Unauthorized - Thông tin không hợp lệ
```json
{
  "error": "Không được phép",
  "message": "Tên đăng nhập hoặc mật khẩu không hợp lệ"
}
```

### 403 Forbidden - Tài khoản bị vô hiệu hóa
```json
{
  "error": "Bị cấm",
  "message": "Tài khoản của bạn đã bị vô hiệu hóa. Liên hệ quản trị viên."
}
```

### 500 Internal Error - LDAP không khả dụng
```json
{
  "error": "Lỗi Máy chủ Nội bộ",
  "message": "Dịch vụ xác thực tạm thời không khả dụng"
}
```

---

## 🔧 Cấu hình

### Kết nối LDAP
```properties
ldap.url=ldap://ldap.university.edu.vn:389
ldap.base.dn=dc=university,dc=edu,dc=vn
ldap.user.dn=ou= users
ldap.bind.username=cn=admin,dc=university,dc=edu,dc=vn
ldap.bind.password=${LDAP_PASSWORD}
```

### Cài đặt JWT
```properties
jwt.secret=${JWT_SECRET_KEY}
jwt.expiration=86400000  # 24 giờ tính bằng mili giây
jwt.issuer=UFPMS
```

---

## 🔄 Làm mới Token (P1)

**Vấn đề**: Token hết hạn sau 24h  
**Giải pháp**: Endpoint làm mới token

```
POST /api/auth/refresh
Authorization: Bearer {expired_token}

Phản hồi: {new_token}
```

---

## 🔐 Các Thực hành Bảo mật Tốt nhất

1. **Chỉ HTTPS** trong production
2. **Khóa bí mật an toàn**: Mạnh, xoay vòng định kỳ
3. **Hết hạn Token**: 24h (có thể cấu hình)
4. **Giới hạn tốc độ**: Tối đa 5 lần thử đăng nhập mỗi phút
5. **Ghi nhật ký kiểm toán**: Tất cả các lần thử đăng nhập đều được ghi lại
6. **Mật khẩu LDAP**: Không bao giờ lưu trữ trong DB

---

**Liên quan**: FR-ADM-004 (Tích hợp LDAP), NFR-Security  
**Ngày tạo**: 10/02/2026
