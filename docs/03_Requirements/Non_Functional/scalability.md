# Yêu Cầu Khả Năng Mở Rộng - Scalability Requirements

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Danh mục**: Yêu cầu Phi Chức Năng

---

## 1. Khả năng Mở rộng Dữ liệu (Data Scalability)

### NFR-SCA-001: Khối lượng Bài báo
**Dung lượng**:
- MVP: 10,000 bài báo
- 3 năm: 20,000 bài báo
- 5 năm: 50,000 bài báo

**Tốc độ tăng trưởng**: ~2,000-3,000/năm

---

### NFR-SCA-002: Lượng Người dùng
**Dung lượng**:
- MVP: 500 người dùng
- 3 năm: 1,000 người dùng
- 5 năm: 2,000 người dùng

---

### NFR-SCA-003: Lưu trữ Tệp tin
**Dung lượng**:
- MVP: 50GB tệp PDF
- 3 năm: 150GB
- 5 năm: 300GB

**Chiến lược**: Bắt đầu với File System cục bộ, chuyển sang object storage (S3) nếu cần

---

## 2. Mở rộng theo Chiều dọc (Vertical Scalability)

### NFR-SCA-010: Mở rộng Cấu hình Máy chủ
**Tối thiểu** (MVP):
- CPU: 4 cores
- RAM: 8GB
- Ổ cứng: 100GB

**Khuyến nghị** (Production):
- CPU: 8 cores
- RAM: 16GB
- Ổ cứng: 500GB SSD

**Mở rộng tối đa**:
- CPU: 16 cores
- RAM: 32GB

---

## 3. Mở rộng theo Chiều ngang (Horizontal Scalability)

### NFR-SCA-020: Ứng dụng Phi trạng thái (Stateless Application)
**Yêu cầu**: Backend PHẢI stateless

**Triển khai**:
- Session lưu trong Redis (không lưu trong bộ nhớ ứng dụng)
- JWT tokens (không phụ thuộc session server)
- Sẵn sàng cho Load balancer

---

### NFR-SCA-021: Sao chép Cơ sở dữ liệu (Database Replication)
**Chiến lược** (Giai đoạn 2):
- Sao chép Master-Slave
- Đọc từ slaves
- Ghi vào master

**Mở rộng tối đa**: 1 master + 2-3 read replicas

---

### NFR-SCA-022: Cân bằng tải (Load Balancing)
**Hỗ trợ** (Giai đoạn 2):
- Nginx hoặc HAProxy
- Round-robin hoặc least-connections
- Kiểm tra sức khỏe (Health checks)

---

## 4. Kiến trúc Mô-đun (Modular Architecture)

### NFR-SCA-030: Sẵn sàng cho Microservices
**Thiết kế**: Monolith hiện tại, nhưng sẵn sàng tách ra

**Các mô-đun tiềm năng**:
- Dịch vụ Bài báo (Publication Service)
- Dịch vụ Quy trình Phê duyệt (Approval Workflow Service)
- Dịch vụ Tìm kiếm (Search Service)
- Dịch vụ Báo cáo (Reporting Service)
- Dịch vụ Quản lý Người dùng (User Management Service)

---

## 5. Khả năng Mở rộng Cơ sở Dữ liệu

### NFR-SCA-040: Chiến lược Đánh chỉ mục (Indexing Strategy)
**Các chỉ mục**:
- Khóa chính (id)
- Khóa ngoại
- DOI, ISSN (duy nhất)
- Năm xuất bản (publicationYear), trạng thái (status)
- Chỉ mục toàn văn (tiêu đề, tóm tắt)

---

### NFR-SCA-041: Phân vùng (Partitioning - Tương lai)
**Chiến lược nếu > 100,000 bài báo**:
- Phân vùng theo năm
- Lưu trữ dữ liệu cũ (> 10 năm) ra archive

---

## 6. Chiến lược Lưu trữ đệm (Caching Strategy)

### NFR-SCA-050: Caching Đa cấp (Multi-Level Caching)
**Các lớp**:
1. Cache trình duyệt (tài nguyên tĩnh)
2. CDN/Reverse proxy (trang công khai)
3. Cache ứng dụng (Redis)
4. Cache truy vấn CSDL

**Mục tiêu tỷ lệ hit**: > 70%

---

## 7. Lộ trình Di chuyển (Migration Path)

### NFR-SCA-060: Sẵn sàng Di chuyển lên Cloud
**Từ**: Máy chủ tại chỗ (On-premise)  
**Sang**: Đám mây (AWS, Azure, GCP)

**Các thành phần di chuyển**:
- CSDL: MySQL → RDS/Cloud SQL
- Tệp tin: Local FS → S3/Blob Storage
- Ứng dụng: VMs → Containers (Docker)

---

## 8. Khả năng Mở rộng API

### NFR-SCA-070: Phiên bản API
**Hỗ trợ**: API v1, v2... (tương thích ngược)

**URL**: `/api/v1/publications`

---

### NFR-SCA-071: Giới hạn Tốc độ (Rate Limiting)
**Ngăn chặn lạm dụng**:
- Public API: 100 req/giờ
- Authenticated: 1000 req/giờ

---

## 9. Giám sát & Tự động Mở rộng

### NFR-SCA-080: Thu thập Chỉ số (Metrics Collection)
**Theo dõi**:
- Số lượng yêu cầu
- Thời gian phản hồi
- Tỷ lệ lỗi
- Sử dụng tài nguyên

**Công cụ**: Prometheus + Grafana

---

### NFR-SCA-081: Tự động Mở rộng (Giai đoạn 3)
**Kích hoạt**:
- CPU > 80% trong 5 phút: Tăng quy mô (Scale up)
- CPU < 30% trong 10 phút: Giảm quy mô (Scale down)

**Nền tảng**: Kubernetes, Docker Swarm

---

**Tài liệu liên quan**:
- [Yêu Cầu Hiệu Năng](./performance.md)
- [Technology Stack](../../01_System_Specification/technology_stack.md)
