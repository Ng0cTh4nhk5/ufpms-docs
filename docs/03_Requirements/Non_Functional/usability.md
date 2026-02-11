# Yêu Cầu Khả Dụng - Usability Requirements

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Danh mục**: Yêu cầu Phi Chức Năng

---

## 1. Khả năng Dễ học (Learnability)

### NFR-USA-001: Nhập Bài Báo trong < 5 Phút
**Mục tiêu**: Giảng viên mới có thể nhập bài báo đầu tiên trong < 5 phút

**Biện pháp**:
- Form đơn giản, rõ ràng
- Các trường bắt buộc có đánh dấu *
- Chú thích (Tooltips) cho các trường phức tạp
- Tự động lưu mỗi 30s

---

### NFR-USA-002: Hướng dẫn Nhập môn (Onboarding Tutorial)
**Yêu cầu**: Người dùng lần đầu nhìn thấy hướng dẫn

**Nội dung**:
- Video 2-3 phút (tùy chọn)
- Hướng dẫn từng bước
- Tùy chọn "Bỏ qua lúc này"

---

## 2. Hiệu Quả (Efficiency)

### NFR-USA-010: Số Click Tối Thiểu
**Mục tiêu**:
- Tạo bài báo mới: < 3 clicks
- Nộp xét duyệt: 1 click (từ chi tiết bài báo)
- Duyệt công trình: 2-3 clicks
- Tạo báo cáo: 3-4 clicks

---

### NFR-USA-011: Phím Tắt Bàn Phím
**Hỗ trợ phím tắt** (tùy chọn):
- Ctrl+S: Lưu
- Ctrl+Enter: Nộp form
- Esc: Đóng hộp thoại

---

## 3. Phòng ngừa & Khắc phục Lỗi (Error Prevention & Recovery)

### NFR-USA-020: Kiểm tra Hợp lệ Thời gian thực
**Yêu cầu**: Kiểm tra ngay khi rời khỏi trường nhập (blur)

**Ví dụ**:
- Định dạng Email
- Định dạng DOI
- Các trường bắt buộc

---

### NFR-USA-021: Hộp thoại Xác nhận
**Hiển thị xác nhận cho**:
- Xóa bài báo
- Từ chối bài báo
- Nộp xét duyệt

**Định dạng**: "Bạn có chắc chắn không? Hành động [Tên hành động] không thể hoàn tác."

---

### NFR-USA-022: Tự động Lưu Nháp
**Yêu cầu**: Tự động lưu bản nháp mỗi 30 giây

**Chỉ báo**: "Đang lưu..." / "Đã lưu lúc HH:MM"

---

## 4. Thiết kế Trực quan (Visual Design)

### NFR-USA-030: Thiết kế Đáp ứng (Responsive Design)
**Hỗ trợ**:
- Máy tính: 1920x1080, 1366x768
- Máy tính bảng: 768x1024 (iPad)
- Di động: 375x667 (iPhone), 360x640 (Android)

**Điểm ngắt (Breakpoints)**:
- Di động: < 768px
- Máy tính bảng: 768px - 1024px
- Máy tính: > 1024px

---

### NFR-USA-031: Giao diện Nhất quán
**Hệ thống thiết kế**:
- Thành phần Material-UI
- Nhất quán về màu sắc, phông chữ, khoảng cách
- Thành phần tái sử dụng

---

### NFR-USA-032: Phản hồi Trực quan
**Yêu cầu**:
- Biểu tượng tải (Loading spinners) cho các tác vụ bất đồng bộ
- Thông báo Thành công/Lỗi (Toasts)
- Thanh tiến trình cho tải lên
- Màn hình khung xương (Skeleton screens) khi đang tải

---

## 5. Khả năng Truy cập (Accessibility - A11Y)

### NFR-USA-040: Chuẩn WCAG 2.1 Mức AA
**Yêu cầu**:
- Tỷ lệ tương phản màu: >= 4.5:1 (văn bản)
- Điều hướng bàn phím: Tất cả chức năng có thể truy cập
- Trình đọc màn hình: Nhãn ARIA
- Chỉ báo tiêu điểm (Focus indicators): Nhìn thấy được

---

### NFR-USA-041: Văn bản Thay thế cho Hình ảnh
**Yêu cầu**: Mọi hình ảnh đều có văn bản thay thế (alt text)

---

## 6. Quốc tế hóa (Internationalization - i18n)

### NFR-USA-050: Ngôn Ngữ Tiếng Việt
**Yêu cầu**: Giao diện, thông báo lỗi, email đều bằng tiếng Việt

**Mã hóa**: UTF-8

**Tương lai**: Hỗ trợ tiếng Anh (Giai đoạn 2)

---

## 7. Trợ giúp & Tài liệu (Help & Documentation)

### NFR-USA-060: Trợ giúp Tại chỗ (Inline Help)
**Yêu cầu**:
- Tooltips cho các trường
- Biểu tượng trợ giúp (?) bên cạnh các tính năng phức tạp
- Liên kết đến tài liệu hướng dẫn

---

### NFR-USA-061: Mục Câu hỏi Thường gặp (FAQ)
**Chủ đề**:
- Làm sao để thêm bài báo?
- Làm sao kiểm tra trạng thái xét duyệt?
- Làm sao tạo báo cáo?
- Làm sao tải lên PDF?

---

## 8. Tìm kiếm & Điều hướng

### NFR-USA-070: Tự động Hoàn thành Tìm kiếm
**Yêu cầu**: Gợi ý khi gõ >= 3 ký tự

**Gợi ý**:
- Tiêu đề bài báo
- Tên tác giả
- Từ khóa

---

### NFR-USA-071: Đường dẫn (Breadcrumbs)
**Hiển thị đường dẫn điều hướng**:
Ví dụ: Trang chủ > Bài báo > Chi tiết bài báo

---

## 9. Cơ chế Phản hồi

### NFR-USA-080: Form Phản hồi Người dùng
**Vị trí**: Chân trang hoặc menu Trợ giúp

**Các trường**:
- Loại vấn đề (Lỗi, Yêu cầu tính năng, Câu hỏi)
- Mô tả
- Tải lên ảnh chụp màn hình (tùy chọn)

---

## 10. Cảm nhận Hiệu năng

### NFR-USA-090: Chỉ báo Tiến trình
**Cho các tác vụ dài**:
- Tải lên PDF: Thanh tiến trình
- Tạo báo cáo: "Đang xử lý... 50%"
- Tìm kiếm: Biểu tượng đang tải

---

## 11. Kiểm thử Khả dụng (Usability Testing)

### NFR-USA-100: Kiểm thử Người dùng
**Tần suất**: Trước các bản phát hành lớn

**Kịch bản**:
1. Nhà nghiên cứu: Thêm bài báo mới
2. Người duyệt Khoa: Xét duyệt công trình
3. Người xem: Tìm kiếm giảng viên theo lĩnh vực

**Chỉ số**:
- Tỷ lệ hoàn thành tác vụ: > 90%
- Thời gian hoàn thành tác vụ
- Sự hài lòng của người dùng: > 4/5

---

**Tài liệu liên quan**:
- [Nhu cầu Người dùng](../../02_System_Clarification/User_Analysis/user_needs.md)
- [Nhóm Người dùng](../../02_System_Clarification/User_Analysis/user_groups.md)
