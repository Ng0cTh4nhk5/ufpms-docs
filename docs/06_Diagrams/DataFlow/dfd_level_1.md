# DFD Cấp 1 - Các Mô-đun UFPMS

> 📊 **Cấp**: 1  
> 🎯 **Phạm vi**: Phân rã thành 6 mô-đun

---

## 📊 Biểu đồ Luồng Dữ Liệu Cấp 1

```mermaid
flowchart TD
    subgraph Actors["Thực Thể Bên Ngoài"]
        RES[Nhà Nghiên Cứu]
        REV[Người Đánh Giá]
        ADM[Quản Trị Viên]
        PUB[Công Chúng]
    end
    
    subgraph Processes["Quy Trình UFPMS"]
        P1[1.0<br/>Quản Lý<br/>Ấn Phẩm]
        P2[2.0<br/>Quy Trình<br/>Phê Duyệt]
        P3[3.0<br/>Tìm Kiếm &<br/>Duyệt]
        P4[4.0<br/>Hồ Sơ<br/>Nhà Nghiên Cứu]
        P5[5.0<br/>Báo Cáo &<br/>Phân Tích]
        P6[6.0<br/>Quản Trị &<br/>QL Người Dùng]
    end
    
    subgraph DataStores["Kho Dữ Liệu"]
        D1[(D1: Ấn Phẩm)]
        D2[(D2: Người Dùng)]
        D3[(D3: Lịch Sử Đánh Giá)]
        D4[(D4: Nhật Ký Kiểm Toán)]
    end
    
    %% Luồng Nhà nghiên cứu
    RES -->|Dữ liệu ấn phẩm| P1
    P1 -->|Ấn phẩm đã tạo| RES
    RES -->|Gửi| P2
    P2 -->|Cập nhật trạng thái| RES
    RES -->|Cập nhật hồ sơ| P4
    P4 -->|Dữ liệu hồ sơ| RES
    
    %% Luồng Người đánh giá
    REV -->|Quyết định đánh giá| P2
    P2 -->|Phân công đánh giá| REV
    REV -->|Yêu cầu báo cáo| P5
    P5 -->|Báo cáo| REV
    
    %% Luồng Quản trị viên
    ADM -->|Quản lý người dùng| P6
    P6 -->|Trạng thái hệ thống| ADM
    ADM -->|Cấu hình hệ thống| P6
    
    %% Luồng Công chúng
    PUB -->|Truy vấn tìm kiếm| P3
    P3 -->|Kết quả tìm kiếm| PUB
    PUB -->|Yêu cầu xem hồ sơ| P4
    P4 -->|Hồ sơ công khai| PUB
    
    %% Luồng từ Quy trình đến Kho Dữ liệu
    P1 <-->|CRUD ấn phẩm| D1
    P2 <-->|Đọc ấn phẩm| D1
    P2 -->|Ghi lịch sử| D3
    P3 -->|Đọc đã xuất bản| D1
    P4 <-->|Đọc người dùng, ấn phẩm| D2
    P4 <-->|Đọc ấn phẩm| D1
    P5 -->|Đọc tất cả dữ liệu| D1
    P5 -->|Đọc người dùng| D2
    P5 -->|Đọc lịch sử| D3
    P6 <-->|CRUD người dùng| D2
    P6 <-->|Ghi kiểm toán| D4
    
    %% Luồng giữa các Quy trình
    P1 -.->|Kích hoạt đánh giá| P2
    P2 -.->|Cập nhật trạng thái ấn phẩm| P1
    
    style P1 fill:#6bcf7f
    style P2 fill:#ff6b9d
    style P3 fill:#4d96ff,color:#fff
    style P4 fill:#ffd93d
    style P5 fill:#c8b6ff
    style P6 fill:#ff9f43
```

---

## 📋 Các Quy Trình

### 1.0 Quản Lý Ấn Phẩm
**Đầu vào**: Dữ liệu ấn phẩm (từ Nhà nghiên cứu)  
**Đầu ra**: Ấn phẩm đã tạo/cập nhật  
**Kho Dữ Liệu**: D1 (Ấn Phẩm)

### 2.0 Quy Trình Phê Duyệt
**Đầu vào**: Yêu cầu gửi, Quyết định đánh giá  
**Đầu ra**: Cập nhật trạng thái, Thông báo  
**Kho Dữ Liệu**: D1 (Ấn Phẩm), D3 (Lịch Sử Đánh Giá)

### 3.0 Tìm Kiếm & Duyệt
**Đầu vào**: Truy vấn tìm kiếm (từ Công chúng)  
**Đầu ra**: Kết quả tìm kiếm  
**Kho Dữ Liệu**: D1 (Ấn Phẩm - CHỈ ĐỌC, CHỈ ĐÃ XUẤT BẢN)

### 4.0 Hồ Sơ Nhà Nghiên Cứu
**Đầu vào**: Cập nhật hồ sơ, Yêu cầu xem  
**Đầu ra**: Dữ liệu hồ sơ  
**Kho Dữ Liệu**: D1 (Ấn Phẩm), D2 (Người Dùng)

### 5.0 Báo Cáo & Phân Tích
**Đầu vào**: Yêu cầu báo cáo  
**Đầu ra**: Báo cáo  
**Kho Dữ Liệu**: D1, D2, D3 (CHỈ ĐỌC)

### 6.0 Quản Trị & Quản Lý Người Dùng
**Đầu vào**: CRUD Người dùng, Cấu hình hệ thống  
**Đầu ra**: Trạng thái hệ thống  
**Kho Dữ Liệu**: D2 (Người Dùng), D4 (Nhật Ký Kiểm Toán)

---

## 💾 Kho Dữ Liệu

### D1: Ấn Phẩm
- bảng publications
- bảng publication_authors
- tra cứu publication_types

### D2: Người Dùng
- bảng users
- bảng user_roles
- bảng departments, faculties

### D3: Lịch Sử Đánh Giá
- bảng review_history
- bảng review_comments

### D4: Nhật Ký Kiểm Toán
- bảng audit_logs

---

**Liên quan**: dfd_level_0.md, dfd_level_2_approval.md  
**Ngày tạo**: 10/02/2026
