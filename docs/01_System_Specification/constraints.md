# Ràng Buộc và Giả Định - Module Quản Lý Bài Báo Khoa Học

> ⚠️ **Phạm vi**: Đây là ràng buộc cho **module bài báo khoa học** trong môi trường trường Đại học, không phải toàn bộ hệ thống quốc gia. Xem [folder 00](../00_Problem_Context/legal_framework.md) để biết ràng buộc pháp lý toàn diện.

---

## 1. Ràng Buộc (Constraints)

### 1.1. Ràng Buộc Pháp Lý (Có Thể Bỏ Qua Một Phần)

#### A. Tuân Thủ Cơ Bản

**Không bắt buộc tuân thủ toàn bộ khung pháp lý quốc gia** vì:
- Module này phục vụ nội bộ trường ĐH
- Không trực tiếp báo cáo lên Bộ KH&CN
- Không quản lý đề tài sử dụng ngân sách nhà nước

**Chỉ cần tuân thủ:**
- ✅ Luật Sở hữu trí tuệ (2019) - Ghi nhận quyền tác giả đúng
- ✅ Luật An toàn thông tin mạng (2015) - Bảo vệ dữ liệu cá nhân
- ✅ Quy định nội bộ của trường về công bố khoa học

---

#### B. Bảo Vệ Dữ Liệu Cá Nhân

**Nghị định 13/2023/NĐ-CP về bảo vệ dữ liệu cá nhân:**
- Thu thập, xử lý dữ liệu giảng viên phải có sự đồng ý
- Phân cấp công khai: Công khai / Nội bộ / Bảo mật
- Giảng viên có quyền xem, sửa, xóa dữ liệu của mình
- Có chính sách bảo mật rõ ràng (Privacy Policy)

**Dữ liệu cần bảo vệ:**
- Email cá nhân, số điện thoại (nếu có)
- Thông tin nghiên cứu chưa công bố
- File PDF bài báo (nếu giảng viên không muốn công khai)

---

### 1.2. Ràng Buộc Kỹ Thuật

#### A. Hạ Tầng Hiện Có

**Phải tương thích với:**
- Windows Server 2016+ (hạ tầng phổ biến ở các trường ĐH VN)
- Active Directory / LDAP (cho xác thực SSO)
- SQL Server hoặc PostgreSQL (database đã có sẵn)
- Mạng nội bộ có firewall

**Các trường hợp đặc biệt:**
- ⚠️ Nếu trường chỉ có shared hosting → Cần thiết kế stateless app
- ⚠️ Nếu bandwidth thấp → Cần optimize file upload/download

---

#### B. Yêu Cầu Phi Chức Năng

**Hiệu năng:**
- Thời gian tải trang: < 3 giây (với kết nối 10Mbps)
- API response time: < 2 giây
- Hỗ trợ tối thiểu **100 người dùng đồng thời** (peak)
- Database: Tối ưu cho 10,000-50,000 bài báo

**Khả dụng:**
- Uptime: > 99% (cho phép bảo trì 1 giờ/tuần)
- Backup: Tự động hàng ngày
- Recovery time: < 4 giờ

---

#### C. Bảo Mật

**Bắt buộc:**
- ✅ HTTPS (SSL/TLS 1.3) cho toàn bộ giao tiếp
- ✅ Xác thực qua LDAP/AD (SSO) hoặc username/password
- ✅ RBAC (Role-Based Access Control) - 5 roles: SuperAdmin, Researcher, Faculty Reviewer, University Reviewer, Viewer
- ✅ Input validation (chống SQL Injection, XSS)
- ✅ Antivirus scan cho file upload
- ✅ Rate limiting API (100 requests/minute/IP)
- ✅ Audit log cho các thao tác quan trọng

**Khuyến nghị:**
- 🔸 2FA (Two-Factor Authentication) cho tài khoản Admin
- 🔸 Encryption cho dữ liệu nhạy cảm (AES-256)

---

### 1.3. Ràng Buộc Về Tài Nguyên

#### A. Ngân Sách

**Hạn chế:**
- Ngân sách phát triển: < 100 triệu VNĐ (ước tính)
- Chi phí vận hành hàng năm: < 30 triệu VNĐ/năm
  - Server: 10-20 triệu/năm (Cloud hoặc on-premise)
  - License: 0 (ưu tiên mã nguồn mở)
  - Bảo trì: 10 triệu/năm

**Hệ quả:**
- ✅ Ưu tiên công nghệ mã nguồn mở (React, PostgreSQL, .NET Core...)
- ✅ Tự host thay vì SaaS đắt tiền
- ✅ Không mua license thương mại cho database, server

---

#### B. Nhân Lực

**Đội phát triển:**
- 1-2 Backend developers
- 1 Frontend developer
- 1 Designer (part-time)
- Chia sẻ QA với dự án khác

**Đội vận hành:**
- Phòng IT: 2-3 người (không chuyên về hệ thống này)
- Phòng QLKH: 1 người admin hệ thống (không phải IT)

**Hệ quả:**
- ✅ Hệ thống phải **dễ vận hành**, không phức tạp
- ✅ Documentation phải rõ ràng, chi tiết
- ✅ UI phải trực quan, ít cần support

---

#### C. Thời Gian

**Timeline:**
- Phát triển MVP: 3 tháng
- Testing: 2 tuần
- Training: 1 tuần
- Go-live: Trước năm học mới (tháng 8)

**Hệ quả:**
- ✅ Tập trung vào core features
- ✅ Không làm tính năng "nice-to-have" trong giai đoạn 1
- ✅ Sử dụng framework mature, ít bug

---

### 1.4. Ràng Buộc Về Dữ Liệu

#### A. Dữ Liệu Kế Thừa

**Tình trạng:**
- Có file Excel lưu bài báo của 3-5 năm gần nhất
- Dữ liệu không chuẩn (thiếu DOI, ISSN; sai tên tác giả...)
- Một số giảng viên không lưu PDF

**Yêu cầu:**
- ✅ Phải có chức năng import Excel
- ✅ Có công cụ kiểm tra, làm sạch dữ liệu
- ✅ Chấp nhận dữ liệu không đầy đủ 100%

---

#### B. Định Dạng File

**File upload:**
- Định dạng chính: PDF
- Hỗ trợ: DOCX (chuyển sang PDF tự động nếu được)
- Giới hạn kích thước: **10MB/file**
- Antivirus scan bắt buộc

---

### 1.5. Ràng Buộc Về Tương Thích

#### A. Trình Duyệt

**Hỗ trợ:**
- Chrome 90+
- Firefox 88+
- Edge 90+
- Safari 14+

**Không hỗ trợ:**
- ❌ Internet Explorer (đã ngừng hỗ trợ)

---

#### B. Thiết Bị

**Responsive design:**
- Desktop: 1920x1080, 1366x768
- Tablet: iPad (768x1024)
- Mobile: 375x667 trở lên (view-only, không nhập liệu)

**Lưu ý:**
- Nhập liệu phức tạp → khuyến khích dùng desktop
- Mobile chỉ để xem, tìm kiếm

---

### 1.6. Ràng Buộc Kiến Trúc

**Nguyên tắc:**
- ✅ N-tier architecture (Presentation → Business Logic → Data Access)
- ✅ API-first design (RESTful API)
- ✅ Stateless backend (dễ scale)
- ✅ Separation of concerns

**Cấm:**
- ❌ Tight coupling giữa frontend và backend
- ❌ Hard-code connection string, API keys trong code
- ❌ Stored procedures phức tạp (khó maintain)

---

## 2. Giả Định (Assumptions)

### 2.1. Giả Định Về Người Dùng

#### A. Kỹ Năng Công Nghệ

**Giả định:**
- ✅ Giảng viên biết sử dụng Word, Excel cơ bản
- ✅ Quen với email, trình duyệt web
- ✅ Biết tải file, mở PDF
- ❌ **KHÔNG** giả định biết về database, lập trình, API

**Hệ quả:**
- Cần training video, hướng dẫn chi tiết
- Giao diện phải trực quan, ít text
- Tooltip, placeholder rõ ràng

---

#### B. Động Lực Sử Dụng

**Giả định:**
- ✅ Giảng viên muốn có profile đẹp để tăng uy tín
- ✅ Muốn giảm công sức báo cáo định kỳ
- ⚠️ **Không** giả định họ tự nguyện nhập đầy đủ ngay từ đầu

**Biện pháp:**
- Chính sách khuyến khích (điểm KPI nếu profile đầy đủ)
- Phòng QLKH nhắc nhở định kỳ
- Gamification (badge, ranking)

---

### 2.2. Giả Định Về Dữ Liệu

#### A. Chất Lượng Đầu Vào

**Giả định:**
- ✅ 80% giảng viên nhập liệu trung thực
- ✅ Phòng QLKH sẽ kiểm tra định kỳ
- ⚠️ **Không** giả định 100% chính xác ngay từ đầu

**Biện pháp:**
- Workflow phê duyệt
- Validation rules nghiêm ngặt
- Tự động kiểm tra DOI, ISSN qua API (nếu có)

---

#### B. Độ Phủ

**Giả định:**
- ✅ Năm đầu: 60% giảng viên đăng ký ít nhất 1 bài báo
- ✅ Năm thứ 2: 80%
- ✅ Năm thứ 3: 95%

---

### 2.3. Giả Định Về Môi Trường

#### A. Kết Nối Internet

**Giả định:**
- ✅ Có Internet ổn định (tốc độ tối thiểu 5Mbps)
- ✅ Truy cập từ văn phòng giảng viên, phòng IT
- ⚠️ Truy cập từ nhà qua VPN (tùy chọn)

**Rủi ro:**
- ⚠️ Internet không ổn định → Cần chế độ lưu nháp tự động
- ⚠️ Không có VPN → Chỉ truy cập trong mạng nội bộ

---

#### B. Hạ Tầng Kỹ Thuật

**Giả định:**
- ✅ Có server (hoặc cloud) với cấu hình tối thiểu (4 core CPU, 8GB RAM)
- ✅ Có backup tự động hàng ngày
- ✅ Phòng IT hỗ trợ xử lý sự cố trong giờ hành chính

---

### 2.4. Giả Định Về Tổ Chức

#### A. Cam Kết Lãnh Đạo

**Giả định:**
- ✅ Lãnh đạo trường ủng hộ dự án
- ✅ Có ngân sách đảm bảo (dù hạn chế)
- ✅ Sẵn sàng ban hành quy định yêu cầu giảng viên sử dụng

**Rủi ro nếu sai:**
- ⚠️ Không có chính sách bắt buộc → Tỷ lệ sử dụng thấp
- **Giảm thiểu**: Demo thường xuyên, báo cáo ROI cho lãnh đạo

---

#### B. Hợp Tác Giữa Các Phòng Ban

**Giả định:**
- ✅ Phòng Tổ chức - HC cung cấp danh sách giảng viên
- ✅ Phòng IT hỗ trợ về hạ tầng
- ✅ Các Khoa/Viện hợp tác thu thập dữ liệu ban đầu

---

### 2.5. Giả Định Về Tích Hợp

#### A. LDAP/Active Directory

**Giả định:**
- ✅ Trường đã có AD/LDAP hoạt động tốt
- ✅ Phòng IT hỗ trợ cấu hình SSO
- ✅ Tất cả giảng viên đều có tài khoản AD

**Nếu sai:**
- Plan B: Xác thực bằng username/password riêng

---

#### B. Hệ Thống HR (Tùy Chọn)

**Giả định (không bắt buộc):**
- 🔸 Có API để lấy thông tin giảng viên (tên, email, đơn vị)
- 🔸 Nếu không có API → Import Excel định kỳ

---

## 3. Ma Trận Rủi Ro vs Giả Định

| Giả Định | Mức độ rủi ro | Tác động nếu sai | Biện pháp giảm thiểu |
|----------|---------------|------------------|---------------------|
| **Internet ổn định** | Trung bình | Không thể sử dụng | Lưu nháp tự động, retry logic |
| **Giảng viên có kỹ năng cơ bản** | Thấp | Tỷ lệ sử dụng thấp | Training kỹ, UI đơn giản |
| **Lãnh đạo cam kết** | Cao | Dự án bị dừng | Demo sớm, báo cáo giá trị |
| **Dữ liệu đầu vào chính xác** | Trung bình | Báo cáo sai | Validation, workflow phê duyệt |
| **Phòng IT hỗ trợ** | Cao | Không deploy được | Tham vấn sớm, hệ thống đơn giản |
| **Có AD/LDAP** | Thấp | Phải xây dựng auth riêng | Thiết kế modular, plan B sẵn sàng |

---

## 4. Điều Kiện Thành Công

**Để dự án thành công, cần:**

✅ 80% giảng viên sử dụng trong vòng 6 tháng  
✅ Thời gian tạo báo cáo giảm từ 3 ngày → 30 phút  
✅ 90% người dùng hài lòng (khảo sát)  
✅ Không có sự cố bảo mật nghiêm trọng  
✅ Uptime > 99% trong năm đầu  

---

## 5. Ghi Chú Quan Trọng

> ⚠️ **Lưu ý**: Tất cả các giả định trên cần được xác nhận lại với stakeholders trong giai đoạn Requirements Gathering. Nếu bất kỳ giả định nào không đúng, cần điều chỉnh phạm vi hoặc phương án triển khai.

> ✅ **Khuyến nghị**: Review lại tài liệu này mỗi 3 tháng hoặc khi có thay đổi lớn về tổ chức, công nghệ, chính sách.

---

*So với hệ thống quốc gia, module này có ràng buộc **GIẢMnhiều** về pháp lý, nhưng **TĂNG** ràng buộc về tài nguyên (ngân sách, nhân lực hạn chế).*
