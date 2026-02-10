# Sequence Diagram: User Authentication

> 📊 **Diagram ID**: SEQ-07  
> 🎯 **Use Case**: System Authentication  
> 👤 **Actor**: All internal users  
> ⚙️ **Key**: LDAP/AD integration, JWT token generation

---

## 📊 Sequence Diagram

```mermaid
sequenceDiagram
    actor User as 👤 User
    participant UI as 🖥️ Login UI
    participant API as 🔌 AuthController
    participant AuthService as 🔐 AuthService
    participant LDAP as 📁 LDAP/AD Server
    participant UserRepo as 💾 UserRepository
    participant DB as 🗄️ Database
    participant TokenService as 🎫 JWTService
    
    %% Open login page
    User->>UI: Navigate to /login
    UI-->>User: Show login form
    
    %% Enter credentials
    User->>UI: Enter username + password
    User->>UI: Click "Login"
    
    activate UI
    UI->>API: POST /api/auth/login
    activate API
    Note over API: Request:<br/>{username, password}
    
    %% Authenticate with LDAP
    API->>AuthService: authenticate(username, password)
    activate AuthService
    
    AuthService->>LDAP: LDAP Bind(username, password)
    activate LDAP
    
    alt Invalid credentials
        LDAP-->>AuthService: Authentication failed
        AuthService-->>API: AuthenticationError
        API-->>UI: 401 Unauthorized
        UI-->>User: "Invalid username or password"
    else Valid credentials
        LDAP-->>AuthService: Authentication successful
        deactivate LDAP
        
        %% Get or create user
        AuthService->>UserRepo: findByUsername(username)
        activate UserRepo
        UserRepo->>DB: SELECT * FROM users<br/>WHERE username = ?
        
        alt User exists
            DB-->>UserRepo: User record
            UserRepo-->>AuthService: User
        else User not found
            Note over AuthService: First-time login<br/>Auto-create user
            
            %% Get user info from LDAP
            AuthService->>LDAP: Get user attributes
            activate LDAP
            LDAP-->>AuthService: {name, email, department}
            deactivate LDAP
            
            AuthService->>UserRepo: createUser(ldapData)
            UserRepo->>DB: INSERT INTO users<br/>(username, name, email, department)
            DB-->>UserRepo: New user ID
            UserRepo-->>AuthService: New user
        end
        deactivate UserRepo
        
        %% Get user roles
        AuthService->>UserRepo: getUserRoles(userId)
        activate UserRepo
        UserRepo->>DB: SELECT roles<br/>FROM user_roles<br/>WHERE user_id = ?
        DB-->>UserRepo: Roles array
        UserRepo-->>AuthService: Roles[]
        deactivate UserRepo
        
        %% Generate JWT token
        AuthService->>TokenService: generateToken(user, roles)
        activate TokenService
        
        Note over TokenService: Payload:<br/>{userId, username,<br/>name, roles,<br/>exp: now + 24h}
        
        TokenService->>TokenService: Sign with secret key
        TokenService-->>AuthService: JWT token
        deactivate TokenService
        
        %% Log login
        AuthService->>UserRepo: logLogin(userId, ipAddress)
        UserRepo->>DB: INSERT INTO audit_logs
        
        AuthService-->>API: {token, user}
        deactivate AuthService
        
        API-->>UI: 200 OK + {token, user, roles}
        deactivate API
        
        %% Store token
        UI->>UI: Store token in localStorage
        Note over UI: localStorage.setItem(<br/>'authToken', token)
        
        UI-->>User: Redirect to dashboard
        deactivate UI
    end
```

---

## 📋 Authentication Flow

### 1. User Submits Credentials
- Username (e.g., `nguyen.van.a`)
- Password

### 2. LDAP Authentication
**LDAP Bind** (validate credentials):
```java
ldapTemplate.authenticate(
    "ou=users,dc=university,dc=edu.vn",
    "(uid=" + username + ")",
    password
);
```

If successful → Fetch user attributes

### 3. Get/Create User
**If user exists in DB**:
- Fetch from `users` table

**If first-time login**:
- Query LDAP for attributes:
  - Full name
  - Email
  - Department
  - Faculty
- Create user record in DB
- Assign default role: `RESEARCHER`

### 4. Get Roles
Query `user_roles` table:
```sql
SELECT role_name 
FROM user_roles 
WHERE user_id = ?
```

Possible roles:
- `RESEARCHER`
- `FACULTY_REVIEWER`
- `UNIVERSITY_REVIEWER`
- `SUPERADMIN`

### 5. Generate JWT Token
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

**Sign with secret key** → JWT token

### 6. Return to Client
Response:
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

### 7. Store Token
UI stores token in `localStorage` or `sessionStorage`

### 8. Subsequent Requests
Every API call includes:
```
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

---

## 🔒 Authorization

### JWT Verification
Every protected endpoint:
```java
@PreAuthorize("hasRole('RESEARCHER')")
public ResponseEntity<?> createPublication(...) {
    // Endpoint logic
}
```

**Middleware** verifies:
1. Token exists in `Authorization` header
2. Token signature valid
3. Token not expired
4. User has required role

---

## 🗄️ Database Tables

### users table
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

### user_roles table
```sql
CREATE TABLE user_roles (
    user_id INT,
    role_name ENUM('RESEARCHER', 'FACULTY_REVIEWER', 'UNIVERSITY_REVIEWER', 'SUPERADMIN'),
    assigned_at TIMESTAMP,
    assigned_by INT,
    PRIMARY KEY (user_id, role_name)
);
```

### audit_logs (login tracking)
```sql
INSERT INTO audit_logs (
    user_id, action, ip_address, timestamp
) VALUES (
    123, 'LOGIN', '192.168.1.100', NOW()
);
```

---

## 🚨 Error Scenarios

### 401 Unauthorized - Invalid Credentials
```json
{
  "error": "Unauthorized",
  "message": "Invalid username or password"
}
```

### 403 Forbidden - Account Disabled
```json
{
  "error": "Forbidden",
  "message": "Your account has been disabled. Contact admin."
}
```

### 500 Internal Error - LDAP Unavailable
```json
{
  "error": "Internal Server Error",
  "message": "Authentication service temporarily unavailable"
}
```

---

## 🔧 Configuration

### LDAP Connection
```properties
ldap.url=ldap://ldap.university.edu.vn:389
ldap.base.dn=dc=university,dc=edu,dc=vn
ldap.user.dn=ou= users
ldap.bind.username=cn=admin,dc=university,dc=edu,dc=vn
ldap.bind.password=${LDAP_PASSWORD}
```

### JWT Settings
```properties
jwt.secret=${JWT_SECRET_KEY}
jwt.expiration=86400000  # 24 hours in milliseconds
jwt.issuer=UFPMS
```

---

## 🔄 Token Refresh (P1)

**Problem**: Token expires after 24h  
**Solution**: Refresh token endpoint

```
POST /api/auth/refresh
Authorization: Bearer {expired_token}

Response: {new_token}
```

---

## 🔐 Security Best Practices

1. **HTTPS only** in production
2. **Secure secret key**: Strong, rotated periodically
3. **Token expiration**: 24h (configurable)
4. **Rate limiting**: Max 5 login attempts per minute
5. **Audit logging**: All login attempts logged
6. **LDAP password**: Never stored in DB

---

**Related**: FR-ADM-004 (LDAP integration), NFR-Security  
**Created**: 10/02/2026
