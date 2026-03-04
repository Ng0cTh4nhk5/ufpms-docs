# Error Response Conventions

Tài liệu này định nghĩa chuẩn payload trả về khi hệ thống UFPMS gặp lỗi (HTTP Status Codes 400, 401, 403, 404, 500). Việc đồng nhất format giúp Frontend dễ dàng bắt và hiển thị lỗi cho người dùng.

## 1. Cấu trúc chuẩn của một Error Response (Standard Error Payload)

Mọi HTTP Error (status >= 400) **BẮT BUỘC** trả về theo định dạng JSON sau:

```json
{
  "timestamp": "2026-02-26T12:00:00.000Z",
  "status": 400,
  "error": "Bad Request",
  "message": "Thông báo lỗi ngắn gọn (hiển thị cho user nếu cần)",
  "path": "/api/resource",
  "details": [] 
}
```

### Giải thích các trường:
- `timestamp`: (String) Thời gian xảy ra lỗi, định dạng ISO-8601.
- `status`: (Integer) Mã HTTP Status Code tương ứng (400, 401, 403, 404, etc.).
- `error`: (String) Mô tả ngắn gọn về HTTP Status Code (vd: "Bad Request", "Unauthorized").
- `message`: (String) Chi tiết lỗi do exception ném ra (thường là tiếng Việt theo SOP).
- `path`: (String) API endpoint đã được request.
- `details`: (Array of Objects) *Optional*, danh sách lỗi chi tiết (thường dùng cho validation form: 400 Bad Request).

---

## 2. Chi tiết theo từng HTTP Status Code

### 2.1. 400 Bad Request (Lỗi dữ liệu đầu vào)
Sử dụng khi: 
- Client gửi request không đúng định dạng JSON.
- Validation form thất bại (thiếu title, year sai khoảng, DOI không đúng định dạng,... theo BRD).

**Payload ví dụ (Validation Error):**
```json
{
  "timestamp": "2026-02-26T12:01:00.000Z",
  "status": 400,
  "error": "Bad Request",
  "message": "Dữ liệu đầu vào không hợp lệ",
  "path": "/api/publications",
  "details": [
    {
      "field": "title",
      "issue": "Tiêu đề là bắt buộc"
    },
    {
      "field": "year",
      "issue": "Năm phải từ 1900 đến năm hiện tại"
    }
  ]
}
```

**Payload ví dụ (Business Logic Error):** (Vd: upload file > 20MB, API không cho upload nhưng filter block quá to trả 400)
```json
{
  "timestamp": "2026-02-26T12:01:30.000Z",
  "status": 400,
  "error": "Bad Request",
  "message": "Kích thước file vượt quá giới hạn 20MB",
  "path": "/api/publications/1/upload-pdf"
}
```

### 2.2. 401 Unauthorized (Chưa đăng nhập / Token hết hạn)
Sử dụng khi: Request thiếu Authorization header, Token không hợp lệ, hoặc Token đã hết hạn.

**Payload ví dụ:**
```json
{
  "timestamp": "2026-02-26T12:02:00.000Z",
  "status": 401,
  "error": "Unauthorized",
  "message": "Token đã hết hạn hoặc không hợp lệ. Vui lòng đăng nhập lại.",
  "path": "/api/auth/me"
}
```

### 2.3. 403 Forbidden (Không có quyền truy cập)
Sử dụng khi: User đã đăng nhập nhưng cố tình truy cập resource không thuộc quyền của mình (Ví dụ: Edit/Delete bài báo của người khác hoặc khi bài báo đã SUBMITTED không được phép sửa nữa).

**Payload ví dụ:**
```json
{
  "timestamp": "2026-02-26T12:03:00.000Z",
  "status": 403,
  "error": "Forbidden",
  "message": "Bạn không có quyền thực hiện hành động này. Chỉ người tạo mới được phép chỉnh sửa bài báo nháp.",
  "path": "/api/publications/5"
}
```

### 2.4. 404 Not Found (Không tìm thấy dữ liệu)
Sử dụng khi: Resource ID truy vấn không tồn tại trong DB, hoặc đã bị soft-delete (`deleted_at` is not null).

**Payload ví dụ:**
```json
{
  "timestamp": "2026-02-26T12:04:00.000Z",
  "status": 404,
  "error": "Not Found",
  "message": "Không tìm thấy bài báo với ID 999",
  "path": "/api/publications/999"
}
```

---

## 3. Cách triển khai ở Backend (Spring Boot)
Tham khảo: Dev sẽ implement một lớp `@RestControllerAdvice` (vd: `GlobalExceptionHandler`) với các hàm `@ExceptionHandler` để bắt:
- `MethodArgumentNotValidException`: Trả về 400 + list `details`.
- `AccessDeniedException`: Trả về 403.
- `ResourceNotFoundException` (custom): Trả về 404.
- `BusinessRuleException` (custom): Trả về 400 (hoặc 409 Conflict tuỳ logic).
