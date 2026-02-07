# Vấn Đề Cần Giải Quyết (Problem Statement)

## 1. Bối Cảnh Thực Tế

Trong hoạt động khoa học và công nghệ tại các trường đại học, viện nghiên cứu và trung tâm R&D, **công trình nghiên cứu khoa học (NCKH)** là sản phẩm cốt lõi thể hiện năng lực và chất lượng nghiên cứu.

Công trình NCKH được hình thành từ việc thực hiện các đề tài nghiên cứu và tồn tại dưới **7 nhóm dạng thức** khác nhau:
1. Công bố và ấn phẩm (sách, bài báo, báo cáo)
2. Tài sản trí tuệ (bằng sáng chế, bảo hộ)
3. Sản phẩm kỹ thuật & công nghệ (thiết bị, vật liệu, chế phẩm)
4. Tiêu chuẩn & quy phạm (TCVN, QCVN)
5. Thiết kế & quy hoạch (bản vẽ, đồ án)
6. Dữ liệu & số hóa (phần mềm, database, bản đồ)
7. Văn hóa - nghệ thuật (tác phẩm nghệ thuật, chương trình biểu diễn)

---

## 2. Vấn Đề Chính

### 2.1. Thiếu Hệ Thống Quản Lý Tập Trung

**Hiện trạng:**
- Thông tin công trình được lưu trữ phân tán nhiều nơi: file Excel, Word, email, tủ hồ sơ giấy
- Mỗi đơn vị tự quản lý theo cách riêng, không có chuẩn chung
- Không có cơ sở dữ liệu tập trung để tra cứu toàn bộ công trình

**Hậu quả:**
- Mất thời gian tìm kiếm thông tin (có thể mất hàng giờ đến hàng ngày)
- Dữ liệu dễ bị mất mát khi nhân sự thay đổi
- Khó khăn trong việc thống kê tổng hợp

---

### 2.2. Đa Dạng Loại Hình, Khó Phân Loại

**Hiện trạng:**
- Hơn 25 dạng thức khác nhau của công trình NCKH
- Mỗi loại có tiêu chuẩn, thông tin riêng biệt:
  - Bài báo: tên tạp chí, ISSN, impact factor, số trích dẫn
  - Sáng chế: số bằng, ngày cấp, thời hạn bảo hộ
  - Phần mềm: phiên bản, ngôn ngữ lập trình, license
  - Thiết bị: thông số kỹ thuật, năng lực sản xuất
- Không có template chung để quản lý tất cả các loại

**Hậu quả:**
- Khó chuẩn hóa dữ liệu
- Thiếu thông tin quan trọng khi nhập liệu
- Không so sánh được giữa các loại công trình

---

### 2.3. Quy Trình Thủ Công, Tốn Thời Gian

**Hiện trạng:**
- Nhà nghiên cứu phải điền form giấy hoặc gửi email báo cáo công trình
- Cán bộ QLKH phải nhập tay vào Excel từng công trình
- Khi cần báo cáo, phải tổng hợp thủ công từ nhiều file
- Mỗi lần lãnh đạo yêu cầu thống kê, phải làm lại từ đầu

**Hậu quả:**
- Tốn hàng ngày đến hàng tuần cho mỗi đợt báo cáo
- Dễ sai sót do nhập liệu thủ công
- Nhân viên phòng QLKH quá tải công việc lặp lại

---

### 2.4. Khó Khăn Trong Tra Cứu và Thống Kê

**Hiện trạng:**
- Muốn tìm "các bài báo về AI năm 2023" → phải mở nhiều file Excel, Ctrl+F
- Muốn biết "giảng viên nào có nhiều sáng chế nhất" → phải đếm tay
- Muốn so sánh "số công trình năm 2022 vs 2023" → phải tổng hợp 2 file riêng
- Lãnh đạo hỏi "khoa nào nghiên cứu mạnh nhất" → mất ngày để trả lời

**Hậu quả:**
- Không khai thác được giá trị từ dữ liệu
- Quyết định quản lý thiếu cơ sở khoa học
- Bỏ lỡ cơ hội hợp tác, chuyển giao công nghệ

---

### 2.5. Trùng Lặp và Thiếu Đồng Bộ Dữ Liệu

**Hiện trạng:**
- Một công trình có thể được nhập nhiều lần bởi nhiều người
- Thông tin giữa các đơn vị không nhất quán
  - Phòng QLKH có 1 phiên bản
  - Phòng TCCB có phiên bản khác (để đánh giá)
  - Khoa lưu thêm phiên bản riêng
- Không có cơ chế xác minh duy nhất (unique identifier)

**Hậu quả:**
- Số liệu báo cáo không chính xác
- Mất uy tín khi có sự sai lệch
- Tốn công sức đối chiếu, làm sạch dữ liệu

---

### 2.6. Khó Tuân Thủ Quy Định Quản Lý Nhà Nước

**Hiện trạng:**
- Bộ KH&CN, Bộ GD&ĐT yêu cầu báo cáo định kỳ theo mẫu chuẩn
- Mẫu báo cáo thay đổi hàng năm
- Việc tổng hợp dữ liệu từ Excel thủ công rất khó đáp ứng đúng hạn

**Hậu quả:**
- Nộp báo cáo trễ hạn
- Dữ liệu không đầy đủ theo yêu cầu
- Bị đánh giá thấp trong các bảng xếp hạng

---

### 2.7. Thiếu Tính Minh Bạch

**Hiện trạng:**
- Nhà nghiên cứu không biết công trình của mình đã được duyệt chưa
- Không rõ tiêu chí để công trình được công nhận
- Khó tra cứu công trình của đồng nghiệp để học hỏi, hợp tác

**Hậu quả:**
- Giảm động lực nghiên cứu
- Thiếu sự hợp tác liên ngành
- Không tận dụng được nguồn lực hiện có

---

## 3. Căn Nguyên Của Vấn Đề

### 3.1. Nguyên Nhân Trực Tiếp
- Thiếu đầu tư vào công nghệ thông tin cho quản lý NCKH
- Quy trình làm việc truyền thống chưa được số hóa
- Nhận thức chưa đầy đủ về giá trị của dữ liệu

### 3.2. Nguyên Nhân Gốc Rễ
- Chưa có hệ thống phù hợp với đặc thù NCKH Việt Nam
- Ngân sách hạn chế cho phát triển hệ thống nội bộ
- Thiếu chuyên gia am hiểu cả NCKH và CNTT

---

## 4. Đối Tượng Bị Ảnh Hưởng

| Đối tượng | Tác động tiêu cực |
|-----------|-------------------|
| **Nhà nghiên cứu** | Thủ tục rườm rà, mất thời gian; Khó chứng minh năng lực |
| **Cán bộ QLKH** | Quá tải công việc thủ công; Dễ sai sót |
| **Lãnh đạo** | Thiếu thông tin để ra quyết định; Báo cáo không kịp thời |
| **Tổ chức** | Năng suất NCKH thấp; Mất uy tín học thuật |
| **Xã hội** | Công trình NCKH không được khai thác tối đa; Lãng phí nguồn lực |

---

## 5. Yêu Cầu Giải Pháp

Để giải quyết các vấn đề trên, cần có một **hệ thống quản lý công trình NCKH** đáp ứng:

### 5.1. Chức Năng Cốt Lõi
✅ Quản lý toàn diện 7 nhóm công trình với thông tin chi tiết riêng  
✅ Hỗ trợ đăng ký, cập nhật công trình dễ dàng  
✅ Tra cứu nhanh, chính xác theo nhiều tiêu chí  
✅ Thống kê, báo cáo linh hoạt, tự động  
✅ Xuất dữ liệu theo chuẩn của cơ quan quản lý  

### 5.2. Phi Chức Năng
✅ Giao diện thân thiện, dễ sử dụng  
✅ Hiệu năng cao, xử lý nhanh  
✅ Bảo mật thông tin  
✅ Khả năng mở rộng  
✅ Tích hợp với hệ thống hiện có (nếu có)  

### 5.3. Lợi Ích Mong Đợi

**Đối với Nhà nghiên cứu:**
- Giảm 80% thời gian báo cáo (từ 30 phút → 5 phút)
- Quản lý hồ sơ cá nhân tập trung
- Tra cứu công trình đồng nghiệp để hợp tác

**Đối với Cán bộ QLKH:**
- Giảm 70% công việc thủ công
- Báo cáo tự động trong vài phút (thay vì vài ngày)
- Dữ liệu luôn chính xác, đồng bộ

**Đối với Lãnh đạo:**
- Nắm bắt real-time tình hình NCKH
- Ra quyết định dựa trên dữ liệu khoa học
- Nâng cao uy tín, xếp hạng của tổ chức

**Đối với Tổ chức:**
- Tăng năng suất nghiên cứu 20-30%
- Thúc đẩy chuyển giao công nghệ
- Tối ưu hóa đầu tư vào NCKH

---

## 6. Tiêu Chí Thành Công

Giải pháp được coi là thành công khi:

1. ✅ **Tỷ lệ sử dụng**: ≥ 80% nhà nghiên cứu đăng ký công trình qua hệ thống
2. ✅ **Tiết kiệm thời gian**: Giảm 70% thời gian cho công tác báo cáo
3. ✅ **Chính xác dữ liệu**: Sai sót < 5% so với thủ công
4. ✅ **Hài lòng người dùng**: Điểm đánh giá ≥ 4/5 sao
5. ✅ **Tuân thủ quy định**: 100% báo cáo đúng mẫu cơ quan quản lý

---

*Tài liệu này là cơ sở để xác định yêu cầu chức năng và phi chức năng của hệ thống.*
