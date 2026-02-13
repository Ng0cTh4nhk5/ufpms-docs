# Các Bên Liên Quan - Module Quản Lý Bài Báo Khoa Học

> ⚠️ **Lưu ý**: Đây là stakeholders cho **module bài báo khoa học** (phạm vi hẹp), không phải hệ thống quản lý toàn bộ công trình NCKH. Xem [folder 00](../00_Problem_Context/README.md) để biết stakeholders toàn hệ thống.

---

## 1. Phân Loại Stakeholders

```
┌─────────────────────────────────────────────┐
│  PRIMARY (Sử dụng trực tiếp hệ thống)     │
│  - Giảng viên                              │
│  - Cán bộ Phòng QLKH                       │
│  - Lãnh đạo Trường/Khoa                    │
└─────────────────────────────────────────────┘

┌─────────────────────────────────────────────┐
│  SECONDARY (Sử dụng gián tiếp)            │
│  - Sinh viên/Nghiên cứu sinh               │
│  - Phòng Tổ chức - Hành chính              │
│  - Phòng IT                                 │
└─────────────────────────────────────────────┘

┌─────────────────────────────────────────────┐
│  EXTERNAL (Bên ngoài tổ chức)             │
│  - Cộng đồng nghiên cứu                    │
│  - Cơ quan kiểm định (AUN-QA...)           │
│  - Bộ GD&ĐT (nhận báo cáo)                │
└─────────────────────────────────────────────┘
```

---

## 2. Primary Stakeholders (Quan Trọng Nhất)

### 2.1. Giảng viên (Lecturers/Researchers)

**Vai trò:**  
Người tạo ra và quản lý bài báo khoa học

**Số lượng:**  
300-500 người (tùy quy mô trường)

**Đặc điểm:**
- Tuổi: 30-65
- Trình độ: Thạc sĩ, Tiến sĩ
- Kỹ năng IT: Trung bình (biết dùng Word, Excel)
- Áp lực: KPI xuất bản nghiên cứu cao

**Nhu cầu:**
| Nhu cầu | Mức độ | Lý do |
|---------|--------|-------|
| Nhập liệu nhanh, đơn giản | CAO | Không muốn mất nhiều thời gian |
| Profile đẹp, chuyên nghiệp | CAO | Tăng uy tín cá nhân |
| Tự động import từ ORCID | TRUNG BÌNH | Tiết kiệm công sức |
| Thống kê cá nhân | CAO | Theo dõi tiến độ KPI |

**Mối quan tâm chính:**
- ✅ "Tôi có thể nhập bài báo trong < 5 phút không?"
- ✅ "Profile của tôi có hiển thị đẹp không?"
- ✅ "Hệ thống có tính chính xác Impact Factor không?"
- ⚠️ "Thông tin của tôi có bị lộ ra ngoài không?"

**Mức độ ảnh hưởng:** ⭐⭐⭐⭐⭐ (Rất cao - nếu không dùng thì hệ thống thất bại)

**Chiến lược tiếp cận:**
- Đào tạo kỹ họ đầu tiên
- Lắng nghe feedback thường xuyên
- Khuyến khích early adopters

---

### 2.2. Trưởng Đơn Vị / Người Phê Duyệt (Unit Leaders / Approvers)

**Vai trò:**  
Sử dụng tài khoản phê duyệt của đơn vị để xét duyệt bài báo

**Cơ chế hoạt động:**  
- **CHẾ ĐỘ MỚI**: Mỗi đơn vị (Khoa/Phòng ban) có **một tài khoản phê duyệt chung**
- Trưởng đơn vị (hoặc người được ủy quyền) đăng nhập vào tài khoản này để duyệt bài
- Khi có thay đổi nhân sự: Người cũ chuyển giao tài khoản → Người mới đổi mật khẩu
- **KHÔNG CẦN** SysAdmin can thiệp khi thay đổi người phê duyệt

**Số lượng tài khoản:**  
- Cấp Khoa: 10-15 tài khoản (tương ứng số lượng Khoa/Viện)
- Cấp Trường: 1 tài khoản duy nhất

**Số lượng người sử dụng:**  
- Khoảng 20-30 người (Trưởng khoa, Phó khoa, Trưởng/Phó Phòng QLKH)

**Đặc điểm:**
- Tuổi: 35-60
- Chuyên môn: Quản lý, lãnh đạo đơn vị
- Kỹ năng IT: Trung bình đến khá
- Đặc thủ: **Có thể thay đổi người phê duyệt** theo chu kỳ bổ nhiệm

**Nhu cầu:**
| Nhu cầu | Mức độ | Lý do |
|---------|--------|-------|
| Đăng nhập tài khoản đơn vị dễ dàng | RẤT CAO | Phải truy cập nhanh để duyệt bài |
| Dashboard rõ ràng, danh sách chờ duyệt | RẤT CAO | Xem nhanh công trình cần xử lý |
| Duyệt/Từ chối/Yêu cầu sửa đơn giản | RẤT CAO | Quy trình phê duyệt phải nhanh gọn |
| Chuyển giao tài khoản an toàn | CAO | Khi hết nhiệm kỳ hoặc thay đổi nhân sự |
| Audit trail minh bạch | CAO | Trách nhiệm giải trình các quyết định |

**Mối quan tâm chính:**
- ✅ "Tôi có thể đăng nhập tài khoản đơn vị để duyệt bài không?"
- ✅ "Khi tôi chuyển công tác, làm sao chuyển giao tài khoản cho người kế nhiệm?"
- ✅ "Hệ thống có ghi lại tôi đã duyệt những bài nào không?" (Trách nhiệm cá nhân)
- ⚠️ "Mật khẩu tài khoản có an toàn không?"

**Mức độ ảnh hưởng:** ⭐⭐⭐⭐⭐ (Rất cao - quyết định công trình được công bố)

**Chiến lược tiếp cận:**
- Đào tạo kỹ về quy trình đăng nhập và phê duyệt
- Cung cấp hướng dẫn rõ ràng về chuyển giao tài khoản
- Đảm bảo audit trail ghi đầy đủ (ai, khi nào, làm gì)
- Hỗ trợ reset mật khẩu nhanh chóng khi cần

---

### 2.3. Cán bộ Phòng Quản lý Khoa học (Research Admin)

**Vai trò:**  
Quản trị hệ thống, tổng hợp báo cáo, quản lý tài khoản phê duyệt

**Số lượng:**  
2-5 người

**Đặc điểm:**
- Tuổi: 25-45
- Chuyên môn: Quản lý hành chính
- Kỹ năng IT: Khá tốt (quen với Excel, phần mềm quản lý)

**Nhu cầu:**
| Nhu cầu | Mức độ | Lý do |
|---------|--------|-------|
| Báo cáo nhanh, chính xác | RẤT CAO | Thường xuyên bị yêu cầu báo cáo đột xuất |
| Kiểm soát chất lượng dữ liệu | CAO | Chịu trách nhiệm về độ chính xác |
| Export Excel/PDF | RẤT CAO | Để gửi lãnh đạo, Bộ |
| Dashboard tổng quan | CAO | Nắm tình hình toàn trường |
| **Quản lý tài khoản phê duyệt** | **RẤT CAO** | **Tạo, reset mật khẩu tài khoản đơn vị** |
| **Theo dõi lịch sử truy cập** | **CAO** | **Xem ai đã đăng nhập tài khoản phê duyệt** |

**Mối quan tâm chính:**
- ✅ "Tôi có thể xuất báo cáo trong 5 phút không?"
- ✅ "Làm sao kiểm tra giảng viên khai báo trùng lặp?"
- ✅ "Có cảnh báo khi dữ liệu bị thiếu không?"
- ✅ **"Làm sao tạo tài khoản phê duyệt cho một Khoa mới?"**
- ✅ **"Khi Trưởng khoa thay đổi, làm sao reset mật khẩu tài khoản?"**

**Mức độ ảnh hưởng:** ⭐⭐⭐⭐⭐ (Rất cao - người dùng hệ thống nhiều nhất, quản lý tài khoản)

**Chiến lược tiếp cận:**
- Họ là power users → cần đào tạo sâu
- Lấy ý kiến trong giai đoạn thiết kế
- Ưu tiên giải quyết pain points của họ
- **Đào tạo kỹ về quản lý tài khoản phê duyệt**

---

### 2.4. Lãnh đạo Trường (University Leadership)

**Vai trò:**  
Ra quyết định chiến lược, đánh giá hiệu quả (KHÔNG trực tiếp phê duyệt bài báo)

**Số lượng:**  
10-20 người (Hiệu trưởng, PHT, Trưởng khoa, Phó khoa...)

**Đặc điểm:**
- Tuổi: 45-65
- Kỹ năng IT: Cơ bản (thích xem báo cáo hơn là sử dụng hệ thống)

**Nhu cầu:**
| Nhu cầu | Mức độ | Lý do |
|---------|--------|-------|
| Dashboard trực quan | RẤT CAO | Nắm tình hình nhanh |
| Báo cáo so sánh | CAO | So với các trường khác |
| Xu hướng theo năm | CAO | Hoạch định chiến lược |
| Dữ liệu để ra chính sách | CAO | Khuyến khích nghiên cứu |

**Mối quan tâm chính:**
- ✅ "Năng suất nghiên cứu của trường tăng hay giảm?"
- ✅ "Khoa nào xuất bản nhiều nhất?"
- ✅ "Chính sách khuyến khích hiện tại có hiệu quả không?"

**Mức độ ảnh hưởng:** ⭐⭐⭐⭐⭐ (Rất cao - quyết định ngân sách, chính sách)

**Chiến lược tiếp cận:**
- Demo dashboard đẹp mắt
- Báo cáo thường xuyên về ROI
- Không yêu cầu họ sử dụng trực tiếp hệ thống

---

## 3. Secondary Stakeholders

### 3.1. Sinh viên / Nghiên cứu sinh (Students)

**Vai trò:**  
Tìm kiếm thông tin, chọn người hướng dẫn

**Số lượng:**  
5,000-20,000 (tùy quy mô trường)

**Nhu cầu:**
- Tìm giảng viên theo lĩnh vực nghiên cứu
- Xem danh sách bài báo để hiểu hướng nghiên cứu
- Liên hệ với giảng viên

**Mối quan tâm:**
- "Thầy/Cô nào chuyên về AI?"
- "Bài báo gần nhất của thầy về chủ đề gì?"

**Mức độ ảnh hưởng:** ⭐⭐⭐ (Trung bình - không trực tiếp quyết định)

---

### 3.2. Phòng Tổ chức - Hành chính (HR Department)

**Vai trò:**  
Cung cấp dữ liệu giảng viên (tên, email, đơn vị)

**Số lượng:**  
5-10 người

**Nhu cầu:**
- Đồng bộ danh sách giảng viên
- Cập nhật khi có thay đổi nhân sự

**Mối quan tâm:**
- "Hệ thống có lấy dữ liệu từ hệ thống HR không?"
- "Có tự động cập nhật khi giảng viên chuyển khoa không?"

**Mức độ ảnh hưởng:** ⭐⭐⭐ (Trung bình - cung cấp master data)

---

### 3.3. Phòng Công nghệ Thông tin (IT Department)

**Vai trò:**  
Hỗ trợ hạ tầng, bảo mật, vận hành

**Số lượng:**  
3-8 người

**Nhu cầu:**
- Hệ thống dễ deploy, dễ bảo trì
- Không tốn nhiều tài nguyên server
- Security tốt

**Mối quan tâm:**
- "Hệ thống có tương thích với hạ tầng hiện tại không?"
- "Có backup tự động không?"
- "Làm sao khôi phục khi có sự cố?"

**Mức độ ảnh hưởng:** ⭐⭐⭐⭐ (Cao - quyết định khả năng triển khai)

**Chiến lược tiếp cận:**
- Tham vấn họ từ giai đoạn chọn công nghệ
- Cung cấp tài liệu kỹ thuật đầy đủ
- Training về vận hành

---

## 4. External Stakeholders

### 4.1. Cộng Đồng Nghiên Cứu (Research Community)

**Vai trò:**  
Tìm kiếm tri thức, tìm đối tác hợp tác

**Số lượng:**  
Không giới hạn (public access)

**Nhu cầu:**
- Tìm bài báo theo chủ đề
- Tìm nhà nghiên cứu để hợp tác

**Mức độ ảnh hưởng:** ⭐⭐ (Thấp - nhưng tăng impact của trường)

---

### 4.2. Cơ Quan Kiểm Định (Accreditation Bodies)

**Ví dụ:** AUN-QA, ABET, Kiểm định MOET

**Vai trò:**  
Đánh giá chất lượng đào tạo và nghiên cứu

**Nhu cầu:**
- Số liệu về năng suất nghiên cứu
- Bằng chứng về chất lượng đội ngũ

**Mối quan tâm:**
- "Số lượng bài báo ISI/Scopus?"
- "Tỉ lệ giảng viên có bài báo quốc tế?"

**Mức độ ảnh hưởng:** ⭐⭐⭐⭐ (Cao - ảnh hưởng đến uy tín trường)

---

### 4.3. Bộ Giáo Dục & Đào Tạo

**Vai trò:**  
Quản lý nhà nước, yêu cầu báo cáo định kỳ

**Nhu cầu:**
- Báo cáo thống kê quốc gia
- Dữ liệu để phân bổ ngân sách

**Mối quan tâm:**
- "Trường có bao nhiêu bài báo ISI/Scopus trong năm?"

**Mức độ ảnh hưởng:** ⭐⭐⭐ (Trung bình - yêu cầu báo cáo định kỳ)

---

## 5. Ma Trận Stakeholder Analysis

| Stakeholder | Mức độ quan tâm | Mức độ ảnh hưởng | Chiến lược |
|-------------|-----------------|------------------|--------------|
| **Giảng viên** | CAO | CAO | **Manage Closely** - Tham gia sâu |
| **Trưởng Đơn Vị (Người duyệt)** | RẤT CAO | RẤT CAO | **Manage Closely** - Key decision makers |
| **Phòng QLKH** | RẤT CAO | RẤT CAO | **Manage Closely** - Key partners, quản lý tài khoản |
| **Lãnh đạo** | TRUNG BÌNH | RẤT CAO | **Keep Satisfied** - Báo cáo định kỳ |
| **Sinh viên** | CAO | THẤP | **Keep Informed** - Public access |
| **Phòng HR** | THẤP | TRUNG BÌNH | **Monitor** - Sync định kỳ |
| **Phòng IT** | TRUNG BÌNH | CAO | **Keep Satisfied** - Hỗ trợ kỹ thuật |
| **Cơ quan kiểm định** | THẤP | CAO | **Keep Satisfied** - Cung cấp báo cáo |
| **Bộ GD&ĐT** | THẤP | TRUNG BÌNH | **Monitor** - Báo cáo định kỳ |

---

## 6. Kế Hoạch Giao Tiếp (Communication Plan)

| Stakeholder Group | Tần suất | Phương thức | Nội dung |
|-------------------|----------|-------------|----------|
| **Giảng viên** | Hàng tuần (giai đoạn đầu) | Email, Workshop | Hướng dẫn sử dụng, FAQ |
| **Trưởng Đơn Vị** | **Theo yêu cầu + Khi thay đổi nhân sự** | **Training, Hướng dẫn chuyển giao** | **Quy trình phê duyệt, quản lý tài khoản** |
| **Phòng QLKH** | Hàng ngày | Trực tiếp, Chat | Support, Bug fixes, Quản lý tài khoản |
| **Lãnh đạo** | Hàng tháng | Báo cáo Dashboard | Tổng quan số liệu |
| **Phòng IT** | Khi cần | Email, Ticket | Technical issues |
| **Sinh viên** | Theo yêu cầu | Public docs, Video | Hướng dẫn tìm kiếm |

---

## 7. Quản Lý Rủi Ro Stakeholder

| Stakeholder | Rủi ro tiềm ẩn | Mức độ | Biện pháp giảm thiểu |
|-------------|----------------|--------|----------------------|
| **Giảng viên** | Kháng cự thay đổi, không sử dụng | CAO | - Training kỹ<br>- Khuyến khích early adopters<br>- Làm rõ lợi ích cá nhân |
| **Trưởng Đơn Vị** | **Mất mật khẩu tài khoản chung, truy cập trái phép** | **CAO** | **- Chính sách mật khẩu mạnh<br>- Audit trail chi tiết<br>- Hướng dẫn bảo mật rõ ràng<br>- Reset mật khẩu định kỳ** |
| **Lãnh đạo** | Mất quan tâm, cắt ngân sách | TRUNG BÌNH | - Demo thường xuyên<br>- Báo cáo ROI |
| **Phòng QLKH** | Quá tải công việc, burnout | TRUNG BÌNH | - Hỗ trợ nhanh<br>- Tự động hóa tối đa |
| **Phòng IT** | Từ chối hỗ trợ do quá bận | CAO | - Tham vấn từ đầu<br>- Hệ thống dễ vận hành |

---

## 8. Kết Luận

**4 Stakeholder quan trọng nhất:**
1. **Giảng viên** - Nếu họ không dùng → hệ thống thất bại
2. **Trưởng Đơn Vị / Người Phê Duyệt** - Sử dụng tài khoản phê duyệt, quyết định công bố
3. **Phòng QLKH** - Người dùng chính, quản lý tài khoản phê duyệt, chất lượng dữ liệu
4. **Lãnh đạo** - Quyết định ngân sách, chính sách

**Nguyên tắc vàng:**
- ✅ Luôn lắng nghe Giảng viên và Phòng QLKH
- ✅ Đào tạo kỹ Trưởng Đơn Vị về quy trình phê duyệt và chuyển giao tài khoản
- ✅ Đảm bảo audit trail minh bạch (ai đăng nhập, ai duyệt, khi nào)
- ✅ Báo cáo định kỳ cho Lãnh đạo
- ✅ Phối hợp chặt chẽ với Phòng IT

**Điểm mới quan trọng:**
- 🔐 **Tài khoản phê duyệt theo đơn vị** - Không gắn role vào cá nhân
- 🔄 **Chuyển giao linh hoạt** - Khi thay đổi nhân sự, chỉ cần đổi mật khẩu
- 📊 **Audit trail chi tiết** - Ghi lại mọi truy cập và hành động

---

*Xem thêm: [Stakeholders toàn hệ thống](../00_Problem_Context/README.md#stakeholders)*
