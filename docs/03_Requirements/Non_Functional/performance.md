# Yêu Cầu Hiệu Năng - Performance Requirements

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Danh mục**: Yêu cầu Phi Chức Năng

---

## 1. Yêu cầu Thời gian Phản hồi (Response Time Requirements)

### NFR-PERF-001: Thời gian Tải trang (Page Load Time)
**Chỉ số**: Thời gian tương tác (Time to interactive - TTI)

| Loại Trang | Mục tiêu | Tối đa |
|-----------|--------|---------|
| Trang chủ | < 1.5s | < 3s |
| Kết quả tìm kiếm | < 1s | < 2s |
| Chi tiết bài báo | < 2s | < 3s |
| Bảng điều khiển (Dashboard) | < 2s | < 4s |
| Trang quản trị | < 2.5s | < 5s |

**Điều kiện**: 10,000 bài báo, 500 người dùng

---

### NFR-PERF-002: Thời gian Phản hồi API
**Chỉ số**: Thời gian từ khi gửi yêu cầu đến khi nhận phản hồi (p95)

| Loại Endpoint | Mục tiêu | Tối đa |
|---------------|--------|---------|
| GET (đơn giản) | < 200ms | < 500ms |
| GET (truy vấn phức tạp) | < 500ms | < 1s |
| POST/PUT | < 300ms | < 1s |
| API Tìm kiếm | < 500ms | < 1.5s |
| Tạo báo cáo | < 5s | < 30s |

---

### NFR-PERF-003: Hiệu suất Truy vấn CSDL
**Chỉ số**: Thời gian thực thi truy vấn (p95)

| Loại Truy vấn | Mục tiêu |
|-----------|--------|
| SELECT đơn giản | < 50ms |
| JOIN (2-3 bảng) | < 200ms |
| Tổng hợp phức tạp | < 500ms |
| Tìm kiếm toàn văn | < 300ms |

**Tối ưu hóa**:
- Đánh chỉ mục hợp lý (DOI, ISSN, năm xuất bản, trạng thái)
- Tối ưu hóa truy vấn
- Connection pooling (Gộp kết nối)

---

## 2. Yêu cầu Thông lượng (Throughput Requirements)

### NFR-PERF-010: Người dùng Đồng thời
**Chỉ số**: Số lượng người dùng hoạt động cùng lúc

| Loại Người dùng | Mục tiêu | Đỉnh điểm |
|-----------|--------|------|
| Tổng số đồng thời | 100 | 200 |
| Nội bộ (Nhà nghiên cứu + Admin) | 50 | 100 |
| Bên ngoài (Người xem) | 50 | 150 |

**Hồ sơ Tải**:
- Bình thường: 30-50 người dùng
- Giờ cao điểm (9-11 AM, 2-4 PM): 80-100 người dùng

---

### NFR-PERF-011: Giao dịch Mỗi Giây (TPS)
**Chỉ số**: Số yêu cầu HTTP/giây

- Tải bình thường: 50 TPS  
- Tải cao điểm: 100 TPS
- Sức chứa tối đa: 200 TPS

---

## 3. Yêu cầu Khả năng Mở rộng (Scalability Requirements)

### NFR-PERF-020: Khối lượng Dữ liệu
**Hỗ trợ lên đến**:
- 20,000 bài báo
- 1,000 người dùng
- 10,000 tệp PDF (tổng cộng 50GB)

**Tốc độ tăng trưởng**: ~2,000 bài báo/năm

---

### NFR-PERF-021: Mở rộng theo Chiều dọc (Vertical Scaling)
**Cấu hình máy chủ** (khuyến nghị):
- CPU: tối thiểu 4 cores
- RAM: tối thiểu 8GB, khuyến nghị 16GB
- Ổ cứng: tối thiểu 100GB
- Mạng: 100 Mbps

---

## 4. Sử dụng Tài nguyên (Resource Utilization)

### NFR-PERF-030: Sử dụng CPU
- Bình thường: < 50%
- Cao điểm: < 80%
- Ngưỡng cảnh báo: > 90% trong > 5 phút

---

### NFR-PERF-031: Sử dụng Bộ nhớ (RAM)
- Bình thường: < 60% tổng RAM
- Cao điểm: < 80%
- Cảnh báo: > 85% trong > 3 phút

---

### NFR-PERF-032: Disk I/O
- Đọc/Ghi: < 50 MB/s (bình thường)
- Cảnh báo: Ổ cứng đầy > 85%

---

## 5. Hiệu năng Tải lên/Tải xuống Tệp

### NFR-PERF-040: Tải lên PDF
- Kích thước tệp tối đa: 10MB
- Thời gian tải lên: < 10s cho tệp 10MB
- Tải lên đồng thời: Hỗ trợ 10 luồng cùng lúc

---

### NFR-PERF-041: Tải xuống PDF
- Thời gian tải xuống: ~1-2s cho tệp 5MB
- Tải xuống đồng thời: Hỗ trợ 20 luồng cùng lúc

---

## 6. Chiến lược Lưu trữ đệm (Caching Strategy)

### NFR-PERF-050: Tỷ lệ Cache Hit
**Mục tiêu**: > 70% cho các yêu cầu lặp lại

**Các lớp Cache**:
1. **Cache trình duyệt**: Tài nguyên tĩnh (JS, CSS, hình ảnh)
2. **CDN/Reverse proxy**: Trang công khai
3. **Cache ứng dụng**: Bài báo đã xuất bản, hồ sơ người dùng
4. **Cache truy vấn CSDL**: Các truy vấn thường xuyên truy cập

**TTL (Thời gian tồn tại)**:
- Tài nguyên tĩnh: 1 năm
- Trang công khai: 1 giờ
- Chi tiết bài báo: 24 giờ
- Kết quả tìm kiếm: 10 phút

---

## 7. Kịch bản Đo điểm chuẩn (Benchmark Scenarios)

### Kịch bản 1: Tải Giờ Cao Điểm
**Điều kiện**:
- 100 người dùng đồng thời
- 30% duyệt, 40% tìm kiếm, 20% xét duyệt, 10% quản trị

**Kỳ vọng**:
- Tải trang < 3s (phân vị thứ 95)
- CPU máy chủ < 70%
- Không có lỗi

---

### Kịch bản 2: Tạo Báo Cáo
**Điều kiện**:
- Báo cáo toàn trường (10,000 bài báo)
- Xuất Excel

**Kỳ vọng**:
- Thời gian tạo < 30s
- Tải xuống ngay lập tức
- Máy chủ vẫn phản hồi tốt

---

## 8. Yêu cầu Kiểm thử Hiệu năng

### NFR-PERF-080: Kiểm thử Tải (Load Testing)
**Công cụ**: JMeter, Apache Bench, k6

**Kịch bản kiểm thử**:
1. Cơ sở (10 người dùng)
2. Tải bình thường (50 người dùng)
3. Tải cao điểm (100 người dùng)
4. Stress test (200 người dùng)
5. Spike test (0 → 150 người dùng trong 1 phút)

---

### NFR-PERF-081: Giám sát Hiệu năng
**Chỉ số cần theo dõi**:
- Thời gian phản hồi (trung bình, p50, p95, p99)
- Thông lượng (yêu cầu/giây)
- Tỷ lệ lỗi (%)
- Sử dụng tài nguyên (CPU, RAM, Disk)

**Công cụ**:
- APM: Prometheus + Grafana
- Logs: ELK Stack (tùy chọn)
- Giám sát người dùng thực (Real User Monitoring - RUM)

---

## 9. Kỹ thuật Tối ưu hóa

**Frontend**:
- Code splitting (Chia nhỏ mã)
- Lazy loading (Tải chậm)
- Tối ưu hóa hình ảnh
- Minification (Nén mã nguồn)

**Backend**:
- Đánh chỉ mục CSDL (Indexing)
- Tối ưu hóa truy vấn
- Connection pooling
- Xử lý bất đồng bộ cho thông báo

**Hạ tầng**:
- Cân bằng tải (nếu mở rộng theo chiều ngang)
- Reverse proxy (Nginx)
- Sao chép CSDL (Read replicas)

---

**Tài liệu liên quan**:
- [Yêu Cầu Khả Năng Mở Rộng](./scalability.md)
- [Technology Stack](../../01_System_Specification/technology_stack.md)
