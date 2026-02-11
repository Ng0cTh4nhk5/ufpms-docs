# Biểu đồ Tuần tự: Phê duyệt Cuối cùng của Trường

> 📊 **ID Biểu đồ**: SEQ-04  
> 🎯 **Ca Sử Dụng**: UC-D2-11 - Phê duyệt Cuối cùng của Trường  
> 👤 **Tác nhân**: Người đánh giá Trường  
> ⚙️ **Kết quả**: ĐÃ XUẤT BẢN hoặc gửi trả về Khoa

---

## 📊 Biểu đồ Tuần tự

```mermaid
sequenceDiagram
    actor Reviewer as 👨‍💼 Người đánh giá Trường
    participant UI as 🖥️ Giao diện
    participant API as 🔌 API
    participant Service as ⚙️ WorkflowService
    participant Repo as 💾 Repository
    participant DB as 🗄️ CSDL
    participant Notif as 📧 Thông báo
    
    %% Lấy danh sách chờ
    Reviewer->>UI: Xem đánh giá cấp trường
    UI->>API: GET /api/reviews/university
    API->>Service: getUniversityPendingReviews()
    Service->>Repo: findByStatus("UNIVERSITY_REVIEWING")
    Repo->>DB: SELECT * WHERE status = 'UNIVERSITY_REVIEWING'
    DB-->>Repo: Danh sách
    Repo-->>Service: Ấn phẩm[]
    Service-->>API: Dữ liệu
    API-->>UI: Đánh giá đang chờ
    UI-->>Reviewer: Hiển thị danh sách
    
    %% Xem chi tiết
    Reviewer->>UI: Nhấn vào ấn phẩm
    UI->>API: GET /api/publications/{id}
    API->>Repo: findWithHistory(id)
    Repo->>DB: SELECT với review_history
    DB-->>Repo: Dữ liệu đầy đủ + bình luận của khoa
    Repo-->>API: Ấn phẩm
    API-->>UI: Chi tiết
    UI-->>Reviewer: Hiển thị ấn phẩm +<br/>bình luận đánh giá của khoa
    
    alt Phê duyệt Cuối cùng → XUẤT BẢN
        Reviewer->>UI: Nhấn "Xuất bản"
        UI->>API: POST /api/reviews/{id}/publish
        activate API
        API->>Service: publishPublication(pubId, reviewerId)
        activate Service
        
        Note over Service,DB: BẮT ĐẦU GIAO DỊCH
        
        %% Cập nhật trạng thái
        Service->>Repo: updateStatus(pubId, "PUBLISHED")
        activate Repo
        Repo->>DB: UPDATE publications<br/>SET status = 'PUBLISHED',<br/>published_at = NOW()
        deactivate Repo
        
        %% Ghi lịch sử
        Service->>Repo: createReviewHistory(entry)
        Repo->>DB: INSERT INTO review_history<br/>(từ: UNIVERSITY_REVIEWING,<br/>đến: PUBLISHED,<br/>tác nhân: reviewerId)
        
        %% Nhật ký kiểm toán
        Service->>Repo: logAudit(...)
        Repo->>DB: INSERT INTO audit_logs
        
        Note over Service,DB: CAM KẾT
        
        %% Thông báo
        Service->>Notif: notifyPublished(publication)
        activate Notif
        
        Note over Notif: Thông báo:<br/>- Nhà nghiên cứu (chủ sở hữu)<br/>- Tất cả đồng tác giả<br/>- Người đánh giá khoa
        
        loop Cho mỗi người nhận
            Notif->>Notif: Gửi email
        end
        
        deactivate Notif
        
        Service-->>API: Thành công
        deactivate Service
        API-->>UI: 200 OK + Ấn phẩm đã xuất bản
        deactivate API
        UI-->>Reviewer: "Xuất bản thành công!"<br/>+ Liên kết đến chế độ xem công khai
        
    else Gửi Trả về Khoa
        Reviewer->>UI: Nhấn "Gửi Trả về Khoa"
        UI->>UI: Yêu cầu lý do
        Reviewer->>UI: Nhập lý do
        
        UI->>API: POST /api/reviews/{id}/send-back
        activate API
        API->>Service: sendBackToFaculty(pubId, reviewerId, reason)
        activate Service
        
        Note over Service,DB: BẮT ĐẦU GIAO DỊCH
        
        Service->>Repo: updateStatus(pubId, "FACULTY_REVIEWING")
        Repo->>DB: UPDATE publications<br/>SET status = 'FACULTY_REVIEWING'
        
        Service->>Repo: saveComments(pubId, reviewerId, reason)
        Repo->>DB: INSERT INTO review_comments
        
        Service->>Repo: createReviewHistory(entry)
        Repo->>DB: INSERT INTO review_history
        
        Note over Service,DB: CAM KẾT
        
        Service->>Notif: notifySentBack(publication, reason)
        activate Notif
        Notif->>Notif: Thông báo cho người đánh giá khoa
        deactivate Notif
        
        Service-->>API: Thành công
        deactivate Service
        API-->>UI: 200 OK
        deactivate API
        UI-->>Reviewer: "Đã gửi trả về khoa"
    end
```

---

## 📋 Hai Hành Động

### 1. Phê duyệt Cuối cùng → Xuất bản ✅
**Tác dụng**:
- Trạng thái: `UNIVERSITY_REVIEWING` → `PUBLISHED`
- Dấu thời gian `published_at` được thiết lập
- Ấn phẩm trở nên **hiển thị công khai**

**Thông báo**:
1. Nhà nghiên cứu (chủ sở hữu)
2. Tất cả đồng tác giả
3. Người đánh giá khoa (để biết thông tin)

**Nội dung Email**:
```
Chủ đề: Ấn phẩm của bạn đã được xuất bản!

Thân gửi {researcher_name},

Chúc mừng! Ấn phẩm của bạn đã được phê duyệt và xuất bản:

Tiêu đề: {title}
Ngày xuất bản: {timestamp}

Xem trang công khai: {public_url}

Trân trọng,
UFPMS
```

---

### 2. Gửi Trả về Khoa 🔄
**Tác dụng**:
- Trạng thái: `UNIVERSITY_REVIEWING` → `FACULTY_REVIEWING`
- Người đánh giá khoa cần đánh giá lại

**Ca Sử Dụng**:
- Người đánh giá trường không đồng ý với quyết định của khoa
- Phát hiện vấn đề mà khoa không bắt được
- Cần thêm thông tin

**Yêu cầu lý do**: Tại sao gửi trả lại

---

## 🗄️ Thay Đổi Cơ Sở Dữ Liệu

### Xuất bản
```sql
UPDATE publications 
SET status = 'PUBLISHED',
    published_at = NOW(),
    updated_at = NOW()
WHERE id = ? AND status = 'UNIVERSITY_REVIEWING';

INSERT INTO review_history (
    publication_id, from_status, to_status,
    actor_id, action, timestamp
) VALUES (
    ?, 'UNIVERSITY_REVIEWING', 'PUBLISHED',
    ?, 'FINAL_APPROVE', NOW()
);
```

### Gửi Trả lại
```sql
UPDATE publications 
SET status = 'FACULTY_REVIEWING',
    updated_at = NOW()
WHERE id = ?;

INSERT INTO review_comments (
    publication_id, reviewer_id, 
    comment_type, comment_text, timestamp
) VALUES (
    ?, ?, 'SENT_BACK_REASON', ?, NOW()
);
```

---

## 🔒 Quy Tắc Nghiệp Vụ

1. **Chỉ Người đánh giá Trường** mới có thể xuất bản
2. Sau khi XUẤT BẢN:
   - Nhà nghiên cứu **không thể chỉnh sửa** (chỉ SuperAdmin)
   - Nhà nghiên cứu **không thể xóa** (chỉ SuperAdmin)
   - Ấn phẩm hiển thị với **công chúng**
3. Ấn phẩm đã xuất bản được tính vào:
   - Thống kê nhà nghiên cứu
   - Báo cáo Khoa/Trường
   - Kết quả tìm kiếm công khai

---

## 📈 Tác Động Sau Xuất Bản

### Hiển thị
- Xuất hiện trong tìm kiếm công khai
- Hiển thị trên hồ sơ nhà nghiên cứu
- Bao gồm trong báo cáo khoa/trường

### Cập nhật Thống kê
- Số lượng ấn phẩm của nhà nghiên cứu +1
- Số lượng ấn phẩm của khoa +1
- Số lượng ấn phẩm của trường +1

### Phân tích (P2)
- Kích hoạt theo dõi trích dẫn
- Kích hoạt theo dõi lượt tải xuống

---

**Liên quan**: FR-APR-013, FR-APR-014, US-UNR-004, US-UNR-005  
**Ngày tạo**: 10/02/2026
