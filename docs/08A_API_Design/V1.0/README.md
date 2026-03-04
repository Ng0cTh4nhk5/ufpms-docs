# Hướng Dẫn Tích Hợp API (UFPMS Phase 1)

> 👤 **Người tạo**: API Designer / Backend Developer  
> 🎯 **Mục đích**: Hướng dẫn team Frontend, Mobile và Tester hiểu rõ cách giao tiếp với các API thuộc Phase 1 của UFPMS mà không cần đọc code Backend.

Tài liệu trong thư mục `08_API_Design` này là **"Bản hợp đồng giao tiếp" (API Contract)** giữa Frontend và Backend. Để mọi công việc diễn ra trơn tru và không ai phải sửa code vì hiểu lầm nhau, toàn bộ team cần đọc và tuân thủ các tài liệu này.

---

## 📂 Danh sách tài liệu

1. **`01_error_conventions.md` (QUAN TRỌNG NHẤT CHO FRONTEND)**
   - **Nội dung**: Định nghĩa cấu trúc JSON thống nhất mà Backend sẽ trả về mỗi khi có lỗi (status 400, 401, 403, 404, 500).
   - **Tác dụng**: Frontend chỉ cần viết 1 bộ Error Interceptor duy nhất để đọc field `message` và hiển thị ra UI. Không bao giờ phải viết if-else loằng ngoằng cho từng API nữa.

2. **`02_openapi.yaml` (DÀNH CHO FRONTEND VÀ BACKEND)**
   - **Nội dung**: Đặc tả toàn bộ Endpoints, Request Body, Response Schema, Query parameters của Phase 1.
   - **Tác dụng**: 
     - *Frontend/Mobile*: Dùng file này để generate các TypeScript Interfaces/Models tự động, hoặc paste vào `editor.swagger.io` để xem UI trực quan.
     - *Backend*: Phải code Controller và DTO đúng y xì như định nghĩa trong file này. Mọi thay đổi (thêm field, đổi type) phải báo cáo và update vào đây trước tiên.

3. **`03_postman_collection.json` (DÀNH CHO QA VÀ FRONTEND)**
   - **Nội dung**: File export chuẩn v2.1.0 của Postman, chứa các request mẫu với dữ liệu thật.
   - **Tác dụng**: Import thẳng vào Postman. Điền biến `{{token}}` một lần là test được mọi API. Rất tiện để QA viết automation test hoặc Dev gọi thử API xem nó chạy thế nào.

---

## ⚠️ Những Lưu Ý Quan Trọng Khi Làm Chung (Quy Tắc Sống Còn)

### 1. "Single Source of Truth" - Nguồn sự thật duy nhất
File `02_openapi.yaml` là chân lý. 
- Nếu Frontend gọi API mà thấy Backend trả về khác với file yaml → Lỗi của Backend.
- Nếu Backend nhận Request Body khác cấu trúc file yaml → Lỗi của Frontend.
- Không ai được phép tự ý thêm/sửa field trong JSON mà không đồng bộ cập nhật vào file YAML này.

### 2. Xử lý Lỗi (Error Handling)
Frontend **LUÔN LUÔN** mong đợi Frontend nhận về JSON có field `"message"` khi HTTP Status >= 400. *Trừ lỗi mạng (Network Error / CORS).* 
- Xem kĩ `01_error_conventions.md` để lấy message hiển thị cho User. Đối với form (400 Bad Request), sẽ có thêm mảng `"details"` để tô đỏ từng field cụ thể trên màn hình.

### 3. Phân Phối Trách Nhiệm Soft-Delete và Status
- **Backend gánh Logic**: Khi Frontend gọi `DELETE /api/publications/{id}`, Backend sẽ tự động check status bài báo. Nếu là SUBMITTED, Backend sẽ quăng `403 Forbidden`. Frontend chỉ làm nhiệm vụ bấm nút và hiện lỗi nếu bị chặn, không cần phức tạp hóa logic Frontend.
- Tuyệt đối không hard-delete bài báo. Cột `deleted_at` được Backend tự xử lý.

### 4. Về File Upload (PDF)
- File API (`POST /upload-pdf` và `GET /download-pdf`) tách biệt hoàn toàn với API tạo bài báo.
- Luồng chuẩn: Tạo bài báo trước (`POST /publications` -> nhận được id) ➡️ Dùng id đó gọi API upload PDF. Lượng tối đa là 20MB.

### 5. Xác thực (Authentication)
Trừ API Login, **tất cả các API còn lại** đều yêu cầu kèm header xác thực:
`Authorization: Bearer <your_jwt_token>`
Nếu quên, nhận ngay lỗi `401 Unauthorized` có định dạng chuẩn theo `01_error_conventions.md`.

---
Nếu có bất kỳ thắc mắc hay đề xuất thay đổi REST Endpoint nào, xin vui lòng comment trực tiếp trên Pull Request chứa các file này HOẶC ping trực tiếp người tạo API Specification trước khi bắt tay vào code!
